# Bestätigte Modbus-Register

**Deutsch** | [English](REGISTERS_EN.md)

Getestet an einer **POOLSANA InverPOWER ULTRA 18** mit Steuerplatine **SP.KYZ1.5-4.1**.

Kommunikation: Modbus RTU, 9600 Baud, 8N1, Slave-ID 1, Basisadresse 0. Lesen über FC03, Schreiben der bestätigten schreibbaren Register über FC06.

| Register | Adresse | Zugriff | Bedeutung | Bestätigte Werte |
|---|---:|---|---|---|
| R20 | 0x0014 | Lesen | Statuswort, Bit 1: Durchfluss/E17 | Bit 1 = 0: Flow vorhanden; Bit 1 = 1: kein Flow/E17 |
| R47 | 0x002F | Lesen | Temperaturwert | Rohwert × 0,1 °C; folgt der angezeigten Wassertemperatur eng |
| R92 | 0x005C | Lesen/Schreiben | EIN/AUS | 0 = AUS, 1 = EIN |
| R93 | 0x005D | Lesen/Schreiben | Betriebsart | 0 = Auto, 1 = Kühlen, 2 = Heizen |
| R105 | 0x0069 | Lesen/Schreiben | Solltemperatur Heizen | direkte Ganzzahl in °C |
| R106 | 0x006A | Lesen/Schreiben | Solltemperatur Kühlen | direkte Ganzzahl in °C |
| R108 | 0x006C | Lesen/Schreiben | Solltemperatur Auto | direkte Ganzzahl in °C |
| R132 | 0x0084 | Lesen/Schreiben | Leistungsstufe | 0 = Stufe 1, 1 = Stufe 2, 2 = Stufe 3 |

## Nicht als bestätigt verwenden

- R27 wurde als mögliche Flow-/E17-Adresse untersucht, bestand die Gegenproben aber nicht.
- R39 verhält sich wie ein interner Prozess-/Sequenzstatus und ist kein einfacher EIN/AUS-Wert.
- R50 ist temperaturähnlich, die genaue Sensorzuordnung ist ungeklärt.
- R107 ist ungeklärt.
- Die Registerkarte ist bewusst unvollständig: weitere Adressen wurden nicht weiter untersucht, weil sie für das Projekt nicht benötigt wurden.

## RS485-Anschluss

Für die externe Integration wurde **RS485-1 / CN837** verwendet. **RS485-2 / CN835** gehört zum Controller-/WLAN-Pfad und wurde nicht als externe Schnittstelle verwendet.

Bei USB-RS485-Adapter bzw. Gateway wurden A/B/GND entsprechend verwendet. Die 12-V-Leitung der Wärmepumpe wird nicht mit einem normalen USB-RS485-Adapter verbunden.

## Sicherheit

Unbekannte Register nicht beschreiben. Änderungen an der Verdrahtung nur im spannungsfreien Zustand durchführen. In der Wärmepumpe befinden sich Netz- und Inverterspannungen.

[English project overview](README_EN.md)
