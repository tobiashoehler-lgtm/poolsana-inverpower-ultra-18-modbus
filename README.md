# POOLSANA InverPOWER ULTRA 18 – RS485 / Modbus RTU

**Deutsch** | [English](README_EN.md)

Praktisch ermittelte und getestete Modbus-Register für die Pool-Wärmepumpe **POOLSANA InverPOWER ULTRA 18** mit Steuerplatine **SP.KYZ1.5-4.1**.

Ziel des Projekts war zunächst, die Wärmepumpe zuverlässig über eine Hausautomation **ein- und auszuschalten**, ohne die Netzversorgung hart zu trennen. Bei der Untersuchung der Steuerung zeigte sich, dass die Platine eine RS485-Schnittstelle besitzt. Nach Tests mit USB-RS485 und QModMaster ließ sich eine funktionierende **Modbus-RTU-Kommunikation** herstellen. Dadurch konnten zusätzlich Betriebsart, Solltemperaturen, Leistungsstufe, Isttemperatur und der Durchfluss-/E17-Status ermittelt werden.

## Getestete Hardware

- POOLSANA InverPOWER ULTRA 18
- Steuerplatine: **SP.KYZ1.5-4.1**
- RS485-1: **CN837**
- RS485-2: **CN835**
- Modbus-Gateway im Praxistest: **MDT SCN-MBGRTU.01**
- Modbus RTU: **9600 Baud, 8N1, Slave-ID 1**
- Lesen: **FC03**
- Schreiben: **FC06**

## Bestätigte Register

| Register | Hex | Funktion | Werte / Skalierung |
|---|---:|---|---|
| R20 | 0x0014 | Statuswort, Bit 1: kein Flow / E17 | Bit 1 = 0 Flow, 1 kein Flow/E17 |
| R47 | 0x002F | Temperaturwert | raw × 0,1 °C |
| R92 | 0x005C | EIN/AUS | 0 = AUS, 1 = EIN |
| R93 | 0x005D | Betriebsart | 0 = Auto, 1 = Kühlen, 2 = Heizen |
| R105 | 0x0069 | Solltemperatur Heizen | direkte °C |
| R106 | 0x006A | Solltemperatur Kühlen | direkte °C |
| R108 | 0x006C | Solltemperatur Auto | direkte °C |
| R132 | 0x0084 | Leistungsstufe | 0 = Stufe 1, 1 = Stufe 2, 2 = Stufe 3 |

Weitere Register sind vorhanden, wurden aber bewusst nicht vollständig untersucht, da sie für den geplanten Anwendungsfall nicht benötigt wurden.

## Dokumentation

Die vollständige Projektdokumentation enthält Testablauf, Registerübersicht, Platinenbilder, E17/E22, verworfene Hypothesen und die praktische Modbus-/KNX-Umsetzung.

- [Bestätigte Register als Kurzreferenz](REGISTERS.md)
- [English register reference](REGISTERS_EN.md)
- [Lizenzhinweise](LICENSE.md)

- [PDF-Dokumentation](Pool-Waermepumpe-Modbus-Projektdokumentation.pdf)
- [Bearbeitbare DOCX-Version](Pool-Waermepumpe-Modbus-Projektdokumentation.docx)
- [Vollständige Steuerplatine](Steuerplatine_gesamt.jpg)
- [RS485-Ausschnitt](RS485_Anschluesse.jpg)

## Suchbegriffe / Hardware

POOLSANA InverPOWER ULTRA 18, InverPOWER Ultra 18 Modbus, Pool Wärmepumpe Modbus, SP.KYZ1.5-4.1, CN837, CN835, RS485-1, RS485-2, Modbus RTU, QModMaster, MDT SCN-MBGRTU.01, E17 Wasserdurchfluss, E22 Temperaturdifferenz, Wärmepumpe Hausautomation.

## Hinweis

Diese Dokumentation entstand aus eigenen praktischen Tests an einer POOLSANA InverPOWER ULTRA 18. Sie stammt **nicht vom Hersteller**, ist nicht offiziell bestätigt und steht in keiner Verbindung zu POOLSANA. Änderungen an elektrischen Geräten erfolgen auf eigene Verantwortung.

Das Projekt wurde von Tobias praktisch getestet und mit Unterstützung von ChatGPT bei Auswertung, Kontrolltests und Dokumentation ausgearbeitet. Danke an Heiko und Jan für die Bereitstellung ihrer Poolanlage als reale Testumgebung.

## Lizenz

Die Dokumentation und die von uns erstellten Inhalte stehen unter **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)**.

- Teilen und Bearbeiten ist erlaubt.
- Namensnennung ist erforderlich.
- Kommerzielle Nutzung der lizenzierten Inhalte ist nicht erlaubt.
- Bearbeitungen müssen unter denselben Bedingungen weitergegeben werden.

Lizenz: https://creativecommons.org/licenses/by-nc-sa/4.0/

Hinweis: Technische Tatsachen oder Informationen, die nicht urheberrechtlich geschützt sind, können außerhalb des Lizenzumfangs liegen.
