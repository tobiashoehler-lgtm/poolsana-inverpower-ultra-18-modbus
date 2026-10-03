# POOLSANA InverPOWER ULTRA 18 – RS485 / Modbus RTU

[Deutsch](README.md) | **English**

Experimentally determined and practically tested Modbus registers for the **POOLSANA InverPOWER ULTRA 18** pool heat pump using the **SP.KYZ1.5-4.1** controller board.

The original goal of this project was simply to switch the heat pump **ON and OFF from a home automation system** without cutting mains power. Inspection of the controller electronics revealed RS485 connections, which suggested that a Modbus interface might be available. Using a USB-to-RS485 adapter and QModMaster, working **Modbus RTU communication** was established and verified by controlled read/write tests.

The interface turned out to provide more than ON/OFF control. Operating mode, mode-specific temperature setpoints, performance level, a temperature value closely following the displayed water temperature, and the flow/E17 status could also be accessed.

The register map is intentionally incomplete. Many additional readable or changing addresses were observed but were not investigated further because they were not required for this project.

## Tested hardware

- **POOLSANA InverPOWER ULTRA 18**
- Controller board: **SP.KYZ1.5-4.1**
- RS485-1 connector: **CN837**
- RS485-2 connector: **CN835**
- Modbus gateway used in the practical integration: **MDT SCN-MBGRTU.01**
- Modbus RTU: **9600 baud, 8 data bits, no parity, 1 stop bit (8N1)**
- Slave ID: **1**
- Register base: **0**
- Reading: **FC03 – Read Holding Registers**
- Writing confirmed writable registers: **FC06 – Write Single Register**

## Confirmed Modbus registers

| Register | Hex address | Function | Confirmed values / scaling |
|---|---:|---|---|
| R20 | 0x0014 | Status word, bit 1: no-flow / E17 | bit 1 = 0: water flow present; bit 1 = 1: no flow / E17 |
| R47 | 0x002F | Temperature value | raw × 0.1 °C; closely follows the displayed water temperature |
| R92 | 0x005C | Power ON/OFF | 0 = OFF, 1 = ON |
| R93 | 0x005D | Operating mode | 0 = Auto, 1 = Cooling, 2 = Heating |
| R105 | 0x0069 | Heating setpoint | direct integer value in °C |
| R106 | 0x006A | Cooling setpoint | direct integer value in °C |
| R108 | 0x006C | Auto-mode setpoint | direct integer value in °C |
| R132 | 0x0084 | Performance level | 0 = level 1, 1 = level 2, 2 = level 3 |

For the detailed register notes, including addresses that were investigated but **not** confirmed, see:

- [Confirmed Modbus register reference – English](REGISTERS_EN.md)
- [Bestätigte Modbus-Register – Deutsch](REGISTERS.md)

## RS485 connection

For the external integration, **RS485-1 / CN837** was used.

**RS485-2 / CN835** belongs to the controller/Wi-Fi path and was not used as the external automation interface in this project.

The connectors are marked **GND / B / A / 12V**. For a normal USB-to-RS485 adapter or the tested Modbus gateway, use the required RS485 lines such as A/B and GND as applicable. **Do not connect the heat pump's 12 V line to a normal USB-RS485 adapter.**

## Project documentation and photos

The complete project documentation is currently available in German. It contains the test procedure, register findings, PCB photographs, E17/E22 observations, rejected hypotheses, safety notes, and the practical Modbus/KNX implementation example.

- [Full project documentation – PDF, German](Pool-Waermepumpe-Modbus-Projektdokumentation.pdf)
- [Editable project documentation – DOCX, German](Pool-Waermepumpe-Modbus-Projektdokumentation.docx)
- [Full controller board photograph](Steuerplatine_gesamt.jpg)
- [RS485 connector photograph](RS485_Anschluesse.jpg)
- [License information](LICENSE.md)

## Search terms / related hardware

POOLSANA InverPOWER ULTRA 18 Modbus, POOLSANA InverPOWER ULTRA 18 RS485, SP.KYZ1.5-4.1 Modbus, SP.KYZ1.5-4.1 RS485, CN837 Modbus, CN837 RS485, CN835, pool heat pump Modbus registers, pool heat pump RS485, heat pump home automation, QModMaster, MDT SCN-MBGRTU.01, E17 water flow error, E22 temperature difference protection, Modbus RTU pool heat pump.

## Important note

This is an **independent, experimentally determined project documentation** based on practical tests performed on one POOLSANA InverPOWER ULTRA 18 unit.

It is **not manufacturer documentation**, has not been officially confirmed by POOLSANA, and is not affiliated with or endorsed by the manufacturer. Firmware or hardware revisions may behave differently.

Do not write to unknown registers. Wiring changes should only be made with the unit safely de-energized. Pool heat pumps contain mains-voltage and inverter electronics.

## Acknowledgements

The project was practically tested by Tobias, with ChatGPT used as support for analysis, controlled test planning, cross-checking, and documentation.

Special thanks go to Heiko and Jan for making their pool system available as a real-world test environment. Their heat pump is now integrated into their home automation system as a useful side effect of the project.

## License

The project documentation and other original project content are published under **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)**.

- Sharing and adaptation are permitted.
- Attribution is required.
- Commercial use of the licensed content is not permitted.
- Adaptations must be shared under the same terms.

License information: [LICENSE.md](LICENSE.md)

Technical facts or information that are not protected by copyright may fall outside the scope of the Creative Commons license.
