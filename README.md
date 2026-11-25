# 🚐 Dethleffs Grand Alpa Plus – Ultimate 3D Smart Camper OS (Home Assistant)

## 🎥 Live Demo: Interactive 3D Digital Twin



https://github.com/user-attachments/assets/b92a4228-7a75-47c1-a851-0639eeaaa7ff






*(Deutsche Version weiter unten / German version below)*

Welcome to my Smart Camper ecosystem! Living 9 months a year in my motorhome (**Dethleffs Grand Alpa Plus on Iveco Daily**), I built a fully local, autonomous Home Assistant control center – from reverse-engineered hardware protocols to an interactive 3D Digital Twin.




## 📁 Repository Structure & Highlights

* **`/esphome/` & Protocols:** Reverse-engineered hardware protocols including M5Stack Atom Lite for the Alde 3020 LIN-Bus, Simarine STR1 sensor decoding, and MPU-6050 gyro sensor for tank and leveling data.
* **Dashboards & 3D Digital Twin:** Features an interactive 3D model of the vehicle with live solar output, dynamic lighting, and integrated Blink exterior camera feeds.
* **Automations & Energy:** Priority-based MaxxFan climate control (Prio 1–9) with weather/storm protection, solar-surplus fridge switching via Victron and Shelly, and an automated GPS logbook with custom POI integration.
* 
I designed, developed, and implemented the entire system in just 8 weeks.

---

# 🇩🇪 Deutsche Version

Willkommen in meinem vollautomatischen Smart-Camper-Projekt für meinen **Dethleffs Grand Alpa Plus auf Iveco Daily** – entwickelt über 9 Monate Reisezeit mit KI-Unterstützung.

## ✨ Highlights & Module

* **Interaktives 3D-Dashboard:** Frei drehbares 3D-Modell mit Live-Solarwerten und Blink-Kameras in den Spiegeln.
* **Alde 3020 LIN-Bus Komplettsteuerung:** Vollständige Protokollentschlüsselung (Landstromautomatik, lautlose Nachtheizung, Alexa-Warmwasser-Boost, Gasverbrauchs-Tracking).
* **Simarine STR1 & Energie-Logik:** Solarüberschuss-Kühlschranksteuerung (Victron/Shelly), temperaturkompensierter Gas-Algorithmus und 7-Tage-Wasserprognose via MPU-6050 Neigungssensor.
* **MaxxFan Prioritäten-Automatik (Prio 1–9):** Klimasteuerung nach CO₂, gefühlter Temperatur und automatischem Sturm-/Regenschutz.
* **Automatisches Fahrtenbuch & Camper-Radar:** GPS-basierte Streckenerfassung, Schlafplatz-Logger und POI-Integration (*Park4Night*, *LPG*, *Ver-/Entsorgung*).
Ich habe das gesamte System in nur 8 Wochen konzipiert, entwickelt und umgesetzt.


## 🔌 Hardware & Verkabelung (M5Stack Atom Lite -> Alde 3020 HE)

Der **M5Stack Atom Lite** agiert als **Master** an der **gelben 6-poligen CI-Bus-Buchse** auf der Rückseite des Alde-3020-Bedienteils (nicht am internen roten Heizungs-Bus).

| Alde Panel (Gelbe CI-Bus Buchse) | LIN-Transceiver (z. B. TJA1020 / MCP2003) | M5Stack Atom Lite | Hinweis |
| :--- | :--- | :--- | :--- |
| **Pin 3** (LIN / CI-Bus) | `LIN` | – | 12 V Pegel |
| **Pin 5** (GND) | `GND` | `GND` | Gemeinsame Masse |
| 12 V Bordspannung | `VBAT` / `12V` | – | Versorgung Transceiver-Busseite |
| – | `TXD` (Transceiver sendet) | **GPIO19** (RX) | 19200 Baud, 8N1 |
| – | `RXD` (Transceiver empfängt) | **GPIO22** (TX) | 19200 Baud, 8N1 |
| – | `VCC` (3,3 V / 5 V) | `3V3` / `5V` | Logikversorgung |

---

## 🧬 Entschlüsseltes Alde 3020 CI-Bus Protokoll

* **Baudrate & Framing:** `19200 Baud, 8N1`, Enhanced Checksum (inkl. PID).
* **Master-Polling:** Der Atom Lite sendet jede Sekunde `Break + 0x55 + 0x5B`, das Alde-Panel antwortet mit **8 Datenbytes + Prüfsumme**.
* **Schreiblogik (Read-Modify-Write):** Befehle werden über PID `0x1A` gesendet. Basis sind immer die aktuell gelesenen Bytes `st[3]`, `st[4]` und `st[5]` aus Frame `0x5B` (max. 5 s alt), wobei jeweils nur ein Parameter gezielt überschrieben wird. Vorab erfolgt bei Bedarf die Kennungsanmeldung über `0x3C` (`10 06 B2 00 DE 41 01 00` = Compact 3020).

### Status-Frame (`PID 0x5B` – Lesen) & Steuer-Frame (`PID 0x1A` – Schreiben)

| Byte | Bits | Funktion | Kodierung / Wertebereich |
| :--- | :--- | :--- | :--- |
| **Byte 0** | `0..7` | Raumtemperatur (Lesen) | `raw * 0,5 - 42,0` °C (`>= 0xFB` = ungültig) |
| **Byte 1** | `0..7` | Reserviert / System | – |
| **Byte 2** | `0..7` | Außentemperatur (Lesen) | `raw * 0,5 - 42,0` °C (`>= 0xFB` = ungültig) |
| **Byte 3** | `0..5` | **Solltemperatur** (Lesen & Schreiben) | `(raw * 0,5) + 5,0` °C (`0..50` = `5,0..30,0 °C`) |
| **Byte 3** | `6` | **Gasbetrieb erlauben** (Lesen & Schreiben) | `0` = Aus, `1` = Ein |
| **Byte 3** | `7` | Gasventil-Status (Lesen) | `0` = Geschlossen, `1` = Offen |
| **Byte 4** | `6..7` | **Elektro-Heizstufe** (Lesen & Schreiben) | `0` = Aus, `1` = 1 kW, `2` = 2 kW, `3` = 3 kW |
| **Byte 5** | `0` | **Alde Panel Ein/Aus** (Lesen & Schreiben) | `0` = Aus, `1` = Ein |
| **Byte 5** | `2` | Fehlerstatus (Lesen) | `0` = OK, `1` = Störung |
| **Byte 5** | `3..4` | **Warmwasser / Boiler** (Lesen & Schreiben) | `0` = Aus, `1` = An (Normal), `2` = Boost |
| **Byte 5** | `5` | 230 V Landstrom (Lesen) | `0` = Kein 230 V, `1` = 230 V vorhanden |
| **Byte 5** | `7` | Umwälzpumpe (Lesen) | `0` = Aus, `1` = Läuft |
| **Byte 6–7** | `0..7` | Padding beim Schreiben (`0x1A`) | `0xFF, 0xFF` |

---

## ⚠️ Safety & Legal Disclaimers / Hinweise

* **Safety Warning:** Work on 12V/230V systems, gas, and heating buses is at your own risk. / *Arbeiten an Elektrik, Gas und Heizung erfolgen auf eigene Gefahr.*
* **Trademark Disclaimer:** Independent hobby project. Trademarks ("Dethleffs", "Grand Alpa", "Iveco", "Truma Alde", "Simariney") belong to their respective owners.
