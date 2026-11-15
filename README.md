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

<img width="1008" height="2244" alt="Screenshot_20261115-170219" src="https://github.com/user-attachments/assets/70c043d4-869f-4f83-bc4c-832c285da112" />
<img width="1008" height="2244" alt="Screenshot_20261115-170211" src="https://github.com/user-attachments/assets/dce474c7-0f07-4f59-b720-e81452463023" />
<img width="1008" height="2244" alt="Screenshot_20261115-170238" src="https://github.com/user-attachments/assets/7eadddc0-a7f7-43d9-be2d-6a4a72084475" />
<img width="1008" height="2244" alt="Screenshot_20261115-170228" src="https://github.com/user-attachments/assets/5b0481c5-7f76-44b9-baea-70d684a4667a" />
<img width="1008" height="2244" alt="Screenshot_20261115-170244" src="https://github.com/user-attachments/assets/3976999f-db88-40f3-8f40-9fb52104735a" />
<img width="1008" height="2244" alt="Screenshot_20261115-170307" src="https://github.com/user-attachments/assets/30622d02-8529-4b39-bb3b-b824df131ffa" />
<img width="1008" height="2244" alt="Screenshot_20261115-170254" src="https://github.com/user-attachments/assets/20e5b8a4-0778-43cc-928c-0c9be2d21f8f" />
<img width="1008" height="2244" alt="Screenshot_20261115-170326" src="https://github.com/user-attachments/assets/9509574d-fa2c-4ad7-9bb8-f6e1a61a5de4" />
<img width="1008" height="2244" alt="Screenshot_20261115-170333" src="https://github.com/user-attachments/assets/54266881-c81a-48bf-986f-aa742f7f13cd" />
<img width="1008" height="2244" alt="Screenshot_20261115-170342" src="https://github.com/user-attachments/assets/4b507649-a1b0-4520-8e00-f9a65adf6740" />
<img width="1008" height="2244" alt="Screenshot_20261115-170340" src="https://github.com/user-attachments/assets/00babf29-4ba2-4bc5-a718-0f418b6aa585" />
<img width="1008" height="2244" alt="Screenshot_20261115-170347" src="https://github.com/user-attachments/assets/23d966c0-c5d2-45e6-b134-e433e136081d" />
<img width="1008" height="2244" alt="Screenshot_20261115-170731" src="https://github.com/user-attachments/assets/c9d54df2-f3da-42b2-8b92-e2a0efff6ec4" />
<img width="1008" height="2244" alt="Screenshot_20261115-170724" src="https://github.com/user-attachments/assets/b9ddf97d-981f-4ae6-b863-5c82150ecd95" />
<img width="1008" height="2244" alt="Screenshot_20261115-170736" src="https://github.com/user-attachments/assets/7b16afc7-452f-418e-b180-3c4d1be0839a" />
<img width="1008" height="2244" alt="Screenshot_20261115-170741" src="https://github.com/user-attachments/assets/ba4a0583-b21e-4e9b-8314-81fbc47be8ed" />
<img width="1008" height="2244" alt="Screenshot_20261115-170759" src="https://github.com/user-attachments/assets/3bac3849-2af4-4d1c-b2b4-c240f0badac7" />
<img width="1008" height="2244" alt="Screenshot_20261115-170753" src="https://github.com/user-attachments/assets/16c15a47-be67-4bef-8d80-6465270c572d" />
<img width="1008" height="2244" alt="Screenshot_20261115-170804" src="https://github.com/user-attachments/assets/89190b9e-7786-486a-9044-c7bc61e1ed6b" />
<img width="1008" height="2244" alt="Screenshot_20261115-170802" src="https://github.com/user-attachments/assets/c91b079f-ca5b-4d0b-8270-9199d9b768c4" />
<img width="1008" height="2244" alt="Screenshot_20261115-170812" src="https://github.com/user-attachments/assets/62647d6d-df40-426a-96d1-634e553b660a" />
<img width="1008" height="2244" alt="Screenshot_20261115-170807" src="https://github.com/user-attachments/assets/e0ad2809-d542-4c40-84c0-cd02ffd577fc" />
<img width="1008" height="2244" alt="Screenshot_20261115-170820" src="https://github.com/user-attachments/assets/6ee5e121-ab00-4a0e-b9b1-2109d2e63ce9" />
<img width="1008" height="2244" alt="Screenshot_20261115-170354" src="https://github.com/user-attachments/assets/c8004187-e104-4ff5-8565-cf4f238bab71" />
<img width="1008" height="2244" alt="Screenshot_20261115-170250" src="https://github.com/user-attachments/assets/1096c85f-fc8e-4a13-b793-d48e938cb63d" />

<!-- Failed to upload "Alpa.mp4" -->

<!-- Failed to upload "Alpa innen.mp4" -->
