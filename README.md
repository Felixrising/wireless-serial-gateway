MrDIY Wireless Serial Web Server
================================

Fork Notice:
------------
This project is a fork of the MrDIY Wireless Serial Gateway by MrDIYca
(https://gitlab.com/MrDIYca/wireless-serial-gateway/). Modifications have
been made to add features such as interface selection between hardware
and software serial and mDNS advertisement.

Features:
---------
- Serial Communication Interface Selection:
  * Choose between the default Hardware Serial (UART0) and SoftwareSerial. [NEW]
  * For SoftwareSerial, select RX/TX pins from available GPIOs. [NEW]
  * Prevents setting the same GPIO for both RX and TX. [BORING!]

- Web-based Console Interface:
  * Type commands and view serial output directly in your web browser.
  * Real-time updates via WebSocket communication.

- mDNS Advertisement:
  * Advertises the device as "MrDIY-Wireless-Serial.local" on the local network.
  * Simplifies access without needing to know the device's IP address.

- Dual-Platform Support:
  * Works on both ESP8266 (D1 Mini class) **and** ESP32-S3 (Seeed Xiao) using conditional compilation.
  * USB-CDC, hardware UARTs, and SoftwareSerial handled automatically per platform.

Requirements:
-------------
Hardware:
  - ESP8266-based board (e.g., Wemos D1 Mini).
  - ESP32-S3 board (tested with Seeed Studio Xiao ESP32-S3).
  - Standard wiring for serial communication if needed.

Software:
  - Arduino IDE or PlatformIO for compiling and uploading code.
  - Required libraries:
      • ESP8266WiFi
      • ESP8266WebServer
      • WebSocketsServer
      • ArduinoJson
      • EEPROM
      • ArduinoOTA
      • SoftwareSerial
      • ESP8266mDNS
      • (ESP32) WiFi / WebServer / ESPmDNS (comes with ESP32 Arduino core)

Setup and Installation:
-----------------------
1. Clone the repository:
   git clone https://github.com/Felixrising/wireless-serial-gateway.git

2. Open the Project:
   - Open "wifi_serial.ino" in the Arduino IDE or PlatformIO.

3. Configure Board Settings:
   - Select the appropriate board (e.g., "Wemos D1 Mini") and port in the IDE.

4. Compile and Upload:
   - This project is now a **PlatformIO** workspace with multiple environments:

     ```bash
     # ESP32-S3 Xiao over USB-CDC
     pio run -e esp32s3_serial -t upload

     # ESP32-S3 Xiao OTA (after first flash & Wi-Fi configured)
     pio run -e esp32s3_ota -t upload

     # ESP8266 D1 Mini over UART
     pio run -e esp8266_d1mini -t upload
     ```

     OTA for ESP8266 (`esp8266_d1mini_ota`) is provided but **not yet fully tested**.

5. Network Setup:
   - Upon startup, the firmware attempts to connect to a configured Wi-Fi network.
   - If Wi-Fi credentials are not set, it will start in AP mode for initial configuration.

6. RX/TX Pin selection:
    - Safe TX and RX Pins for Wemos D1 Mini Boards/Clones

   When using the Wemos D1 Mini boards or their clones, not all pins are equally suitable for TX and RX due to specific hardware constraints during boot. Below is a detailed list of which pins are safe to use for TX and RX, along with important notes.

   ![Wemos-D1-Mini-Safe-GPIO-Pins](/Media/WeMos-D1-Mini-Safe-GPIO-Pins.png?raw=true)
   
   Pin Safety Table
   | Label | GPIO   | Safe for TX?       | Safe for RX?                  |
   |-------|--------|--------------------|-------------------------------|
   | D1    | GPIO5  | Yes                | Yes                           |
   | D2    | GPIO4  | Yes                | Yes                           |
   | D5    | GPIO14 | Yes                | Yes                           |
   | D6    | GPIO12 | Yes                | Yes                           |
   | D7    | GPIO13 | Yes                | Yes                           |
   | RX    | GPIO3  | Yes                | Yes                           |
   | TX    | GPIO1  | Yes                | Yes                           |
   | D3    | GPIO0  | Yes (pulled up)    | No (boot fails if pulled LOW) |
   | D4    | GPIO2  | Yes (pulled up)    | No (boot fails if pulled LOW) |
   | D8    | GPIO15 | Yes (pulled down)  | No (boot fails if pulled HIGH)|
   | D0    | GPIO16 | No (special use)   | No (special use)              |
   
   NB: The Rx/Tx pin selection restricted to safe to use pins only, TX and RX pins (GPIO1 and GPIO3) are reserved for Hardware Serial.

Using the Web Interface:
------------------------
1. Access the Web Interface:
   - Open a web browser and navigate to: 
     http://MrDIY-Wireless-Serial.local 
     (or use the device's IP address if mDNS is not resolving).

2. Select Serial Interface Settings:
   - At the top of the page, you'll see dropdowns labeled:
       • Serial Type: Choose between Hardware Serial and SoftwareSerial.
       • Baud Rate: Select the desired baud rate (default is 115200).
       • RX Pin: Select the RX pin (default is D6/GPIO12 for SoftwareSerial).
       • TX Pin: Select the TX pin (default is D5/GPIO14 for SoftwareSerial).
   - The RX/TX dropdowns will be disabled (greyed out) when "Hardware Serial" is selected.
   - On ESP32-S3 you will also see a **USB Serial** option which uses the native USB-CDC port.
   - Changing any dropdown values will automatically update the device settings.

3. Interact with the Serial Device:
   - Use the Console Output area to view serial data.
   - Type commands in the Console Input field and click SEND or press Enter to send commands.
   - The serial output will appear in the console output area.

mDNS Advertisement:
-------------------
- The device advertises itself via mDNS as "MrDIY-Wireless-Serial.local".
- Use "ping MrDIY-Wireless-Serial.local" or navigate to 
  http://MrDIY-Wireless-Serial.local in a browser from a device on the same network.
- Ensure your network supports mDNS (most modern operating systems do).

Customization:
--------------
Changing Default Pin Selections:
  - Modify the option elements in the HTML snippet for #rxPin and #txPin in the html_template
    if you need different default choices.

License:
--------
This project is licensed under the MIT License. See the LICENSE file for details.

Acknowledgements:
-----------------
- This project is a fork and extension of the original MrDIY Wireless Serial Gateway
  by MrDIYca.
- Thanks to the contributors of the ESP8266 libraries and jQuery used in the project.
- Inspired by the MrDIY Wireless Serial project for easy serial communication over Wi-Fi.

For questions or issues, please open an issue in this repository.
