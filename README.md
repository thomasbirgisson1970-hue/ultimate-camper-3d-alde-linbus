# 🚐 Dethleffs Grand Alpa Plus – Ultimate 3D Smart Camper OS (Home Assistant)

*(Deutsche Version weiter unten / German version below)*

Welcome to my Smart Camper ecosystem! Living 9 months a year in my motorhome (**Dethleffs Grand Alpa Plus on Iveco Daily**), I built a fully local, autonomous Home Assistant control center – from reverse-engineered hardware protocols to an interactive 3D Digital Twin.

> **My Journey:** In August, I started with **zero knowledge** of Linux servers, Home Assistant, or ESP32. With the help of AI (Claude & ChatGPT) and months of hands-on testing on the road, this system grew into what it is today.

## ✨ Key Features & Reverse Engineering

### 1. Interactive 3D Digital Twin & Camera Mirrors
* Rotatable 3D model of the Dethleffs Grand Alpa Plus (including Iveco Daily cab, interior cutaway view, external solar suitcase, and bike rack).
* Live solar wattage floating above the roof panels, dynamic lighting effects, and live **Blink exterior camera feeds** integrated into the side mirrors.

### 2. Full Alde Compact 3020 LIN-Bus Control (Reverse Engineered)
* **Hardware:** M5Stack Atom Lite + TTL-LIN Transceiver.
* **Complete Protocol Decoding:** Full read & write access to all CI raw data and control commands without expensive manufacturer clouds.
* **Smart Heating Logic:**
  * Automatic switch from Gas to 230V Electric when shore power is plugged in.
  * Silent night heating (< 19 °C) without waking up the bright original control panel.
  * Alexa voice control for hot water & 30-minute boost.
  * Dynamic gas consumption tracking & air cushion maintenance countdown.

### 3. Simarine SDA1 Sensor Decoding & Energy Management
* **Simarine SDA1:** Decoded the sensor protocol prior to the official broadcast mode release.
* **Solar Surplus Fridge Control:** Switches the fridge to 12V via Victron BMV-712 relay & Shelly based on battery SoC (`off < 97%`, `on > 99.9%`).
* **Temperature-Compensated Fridge Gas Algorithm:** Calculates real-time gas usage dynamically based on outside temperature.
* **Water & Leveling:** 7-day rolling average for fresh water autonomy + **MPU-6050 gyro sensor** for precise tank readings and hydraulic leveling checks.

### 4. Priority-Based MaxxFan Climate Automation (Prio 1–9)
* Automatically switches between intake (`In`) and exhaust (`Out`) using indoor sensors, SwitchBot CO₂ sensors, and local GPS weather stations (felt temperature).
* **Storm & Rain Protection:** Automatically closes the roof vent when wind gusts exceed 40 km/h or rain starts (via DWD, AEMET, etc.).

### 5. Automatic GPS Logbook & Camper Radar
* Automatic `D+` detection (> 13.8V) logs trip start, destination, and daily mileage.
* Nightly GPS sleep-spot logger (00:25) + one-click POI map (*Park4Night*, *LPG*, *Dump Stations*, *Supermarkets*, *Pet Supplies*).
* Dedicated dashboards for **Tractive GPS (Dog)**, **SwitchBot entrance door**, and **1. FC Saarbrücken**.

---

# 🇩🇪 Deutsche Version

Willkommen in meinem Smart-Camper-Projekt! Da ich 9 Monate im Jahr in meinem Wohnmobil (**Dethleffs Grand Alpa Plus auf Iveco Daily**) lebe, habe ich ein vollautomatisches, lokal laufendes Home-Assistant-System entwickelt – von entschlüsselten Hardware-Protokollen bis zum interaktiven 3D-Digital-Twin.

> **Die Geschichte dahinter:** Im August habe ich ohne Vorkenntnisse über Linux-Server, Home Assistant oder ESP32 gestartet. Mit Unterstützung von KI (Claude & ChatGPT) und intensiver Praxis auf Reisen ist daraus diese Steuerungszentrale entstanden.

## ✨ Highlights & Module

* **Interaktives 3D-Dashboard:** Frei drehbares 3D-Modell (inklusive Iveco-Daily-Fahrerhaus, Innenansicht, Solarkoffer & Heckträger) mit Live-Solarwerten und Blink-Kameras in den Spiegeln.
* **Alde 3020 LIN-Bus Komplettsteuerung:** Mit M5Stack Atom Lite & TTL-LIN-Modul alle Befehle und CI-Rohdaten entschlüsselt (automatische Landstrom-Umschaltung, lautlose Nachtheizung unter 19 °C ohne Panel-Licht, Alexa-Warmwasser-Boost, Höhenmodus & Gasverbrauchsschätzung).
* **Simarine SDA1 & Energie-Logik:** Simarine SDA1 Sensor noch vor Veröffentlichung des Broadcast-Modus entschlüsselt; Victron BMV-712 & Shelly Solarüberschuss-Steuerung für den Kühlschrank; temperaturkompensierter Gas-Algorithmus; 7-Tage-Wasserprognose & MPU-6050 Neigungssensor.
* **MaxxFan Prioritäten-Automatik (Prio 1–9):** Steuerung nach CO₂, gefühlter Außentemperatur (GPS-Wetterdienste wie DWD/AEMET) sowie automatischer Sturm- (> 40 km/h) und Regenschutz.
* **Automatisches Fahrtenbuch & Camper-Radar:** D+-Erkennung dokumentiert Strecken & Kilometer; nächtlicher Schlafplatz-Logger; POI-Karte (*Park4Night*, *LPG*, *Ver-/Entsorgung*) sowie Dashboards für **Tractive GPS (Hund)**, **SwitchBot Aufbautür** und **1. FC Saarbrücken**.

---

## ⚠️ Disclaimer / Sicherheitshinweis
Work on 12V/230V electrical systems, gas appliances, and heating buses (Alde LIN-Bus) is strictly at your own risk. / Arbeiten an Elektrik, Gas und Heizung (Alde LIN-Bus) erfolgen ausschließlich auf eigene Gefahr.

https://github.com/user-attachments/assets/8241c83d-7c63-4c02-9587-6388603c0c1d
