# Confirmed Modbus registers

[Deutsch](REGISTERS.md) | **English**

Tested on a **POOLSANA InverPOWER ULTRA 18** with controller board **SP.KYZ1.5-4.1**.

Communication settings used successfully:

- Modbus RTU
- 9600 baud
- 8 data bits
- no parity
- 1 stop bit
- Slave ID 1
- base address 0
- read using **FC03**
- write confirmed writable registers using **FC06**

## Confirmed register map

| Register | Address | Access | Meaning | Confirmed values |
|---|---:|---|---|---|
| R20 | 0x0014 | Read | Status word; bit 1 = flow/E17 state | bit 1 = 0: water flow present; bit 1 = 1: no flow / E17 |
| R47 | 0x002F | Read | Temperature value | raw × 0.1 °C; closely follows the displayed water temperature; exact physical sensor identity not confirmed |
| R92 | 0x005C | Read/Write | Power ON/OFF | 0 = OFF, 1 = ON |
| R93 | 0x005D | Read/Write | Operating mode | 0 = Auto, 1 = Cooling, 2 = Heating |
| R105 | 0x0069 | Read/Write | Heating setpoint | direct integer value in °C |
| R106 | 0x006A | Read/Write | Cooling setpoint | direct integer value in °C |
| R108 | 0x006C | Read/Write | Auto-mode setpoint | direct integer value in °C |
| R132 | 0x0084 | Read/Write | Performance level | 0 = level 1, 1 = level 2, 2 = level 3 |

## R20 / 0x0014 – flow / E17

R20 was verified with repeated operating-state changes.

Typical complete register values observed:

- **0x01F0 (496)** with water flow present
- **0x01F2 (498)** with no flow / E17

The difference is **0x0002**, i.e. **bit 1**.

Therefore:

- bit 1 = **0** → water flow present
- bit 1 = **1** → no water flow / E17

This correlation was confirmed in a complete sequence of **E17 → FLOW → E17 → FLOW → E17**.

R20 should be treated as read-only.

## R47 / 0x002F – temperature value

R47 behaves as a temperature value with the scaling:

**temperature in °C = raw register value × 0.1**

Example:

- raw 181 → 18.1 °C

It closely tracks the water temperature shown on the controller. The exact physical sensor identity was not established, so it is intentionally described here as a temperature value rather than assigned to a specific sensor.

R47 should be treated as read-only.

## R92 / 0x005C – power ON/OFF

Confirmed by controlled read/write tests:

- 0 = OFF
- 1 = ON

Read with FC03 and write with FC06.

In the tested MDT SCN-MBGRTU.01 setup, R92 worked reliably when written as a **complete numeric 16-bit register value 0/1**. Treating it as a single bit within the register did not reliably switch the heat pump ON.

## R93 / 0x005D – operating mode

Confirmed mapping:

- 0 = Auto
- 1 = Cooling
- 2 = Heating

Read with FC03 and write with FC06. The physical controller display followed the written mode and the value could be read back correctly.

## R105 / R106 / R108 – mode-specific setpoints

Confirmed writable setpoint registers:

- R105 / 0x0069 = Heating setpoint
- R106 / 0x006A = Cooling setpoint
- R108 / 0x006C = Auto-mode setpoint

Values are direct integer temperatures in °C.

## R132 / 0x0084 – performance level

Confirmed mapping:

- 0 = level 1
- 1 = level 2
- 2 = level 3

Read with FC03 and write with FC06.

## Investigated but not confirmed for control

The following addresses should **not** be used as confirmed control registers:

- **R27 / 0x001B** – initially appeared related to flow/E17, but failed reversed and repeated tests; it is explicitly **not** the confirmed flow/E17 register.
- **R39 / 0x0027** – behaves like an internal process/sequence/status value; values such as 0, 1, 49, 51 and 59 were observed. Do not write.
- **R50 / 0x0032** – another temperature-like value using approximately raw × 0.1; exact sensor identity not established. Do not write.
- **R107 / 0x006B** – function unknown. Do not write.

The register map is intentionally incomplete. Additional addresses were readable or changed during operation, but were not investigated further because they were not required for the project.

## RS485 connection

The tested external interface is:

- **RS485-1 / CN837**

The adjacent connection:

- **RS485-2 / CN835**

belongs to the controller/Wi-Fi path and was not used as the external integration interface.

Both connectors are marked **GND / B / A / 12V**.

For a normal USB-to-RS485 adapter or Modbus gateway, use the required RS485 lines such as A/B and GND as applicable. Do **not** connect the heat pump's 12 V line to a normal USB-RS485 adapter.

## E17 and E22

According to the POOLSANA documentation used during the project:

- **E17** = water flow protection
- **E22** = temperature-difference protection between water inlet and outlet

During testing, E17 appeared after the filter pump was switched off; E22 appeared later. E22 was observed but was not mapped to a Modbus register and was not investigated further.

## Safety

Do not write to unknown registers.

Only change wiring with the unit safely de-energized. The heat pump contains mains-voltage and inverter electronics.

Firmware or hardware revisions may differ from the tested unit, so verify read values before writing even to addresses documented here.

[Back to English project overview](README_EN.md)
