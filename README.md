# BeagleBone GPS Tracker: Distance & Bearing Calculator 📍🛰️

A Python-based application designed for **BeagleBone Black/Green** that interfaces with a GPS module via **UART**. The script parses NMEA sentences to provide real-time location tracking, local time synchronization, and navigation logic to calculate the distance and compass bearing to a specific target coordinate.

## ✨ Features
- **Real-time GPS Parsing:** Extracts data from `$GPRMC`, `$GPGSV`, and `$GPGGA` sentences.
- **Geodesic Calculations:** Uses the **Haversine formula** to calculate the great-circle distance between the current location and a target.
- **Navigation Logic:** Calculates the precise **bearing (azimuth)** and converts it into human-readable cardinal directions (N, NE, E, etc.).
- **Hardware Integration:** Automatically configures BeagleBone pins (`p9_24`, `p9_26`) for UART communication.
- **Local Time Sync:** Converts UTC time from satellites to local time based on a configurable offset.
- **Satellite Monitoring:** Tracks both "Satellites in View" and "Satellites Used" for fix quality assurance.

## 🛠️ Hardware Requirements
- **Board:** BeagleBone Black, BeagleBone Green, or similar.
- **GPS Module:** Any module supporting NMEA over Serial (e.g., NEO-6M, SIM808, etc.).
- **Connections:**
  - TX (GPS) -> P9_26 (UART1_RXD)
  - RX (GPS) -> P9_24 (UART1_TXD)

## 🚀 Getting Started

### 1. Prerequisites
Ensure you have Python installed on your BeagleBone. You will also need the `pyserial` library:
```bash
pip install pyserial
2. ConfigurationThe script uses UART1 by default (/dev/ttyO1). If you are using a different UART port, update the following line in main.py:Pythonser = serial.Serial(port="/dev/ttyO1", baudrate=9600, timeout=1)
3. Running the ScriptRun the script:Bashpython main.py
Enter the Target Latitude and Longitude when prompted.Wait for the GPS to get a "Valid fix" (this may take a few minutes if you are indoors).📊 Gesture & Logic BreakdownDistance: Calculated in meters using the Earth's radius ($6371.0$ km).Bearing: Calculated using spherical trigonometry to determine the degree ($0-360^\circ$) relative to North.Pin Config: Uses config-pin utility to ensure UART multiplexing is active on the P9 header.⚠️ Important NotesAntenna: Ensure your GPS antenna has a clear view of the sky.Permissions: You might need to run the script with sudo to access hardware pins and serial ports:Bashsudo python main.py
📜 LicenseThis project is open-source. Feel free to use and modify it for your robotics or navigation projects.
