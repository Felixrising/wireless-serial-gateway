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

Requirements:
-------------
Hardware:
  - ESP8266-based board (e.g., Wemos D1 Mini).
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

Setup and Installation:
-----------------------
1. Clone the repository:
   git clone https://github.com/Felixrising/wireless-serial-gateway.git

2. Open the Project:
   - Open "wifi_serial.ino" in the Arduino IDE or PlatformIO.

3. Configure Board Settings:
   - Select the appropriate board (e.g., "Wemos D1 Mini") and port in the IDE.

4. Compile and Upload:
   - Compile the code and upload it to your ESP8266 board.

5. Network Setup:
   - Upon startup, the firmware attempts to connect to a configured Wi-Fi network.
   - If Wi-Fi credentials are not set, it will start in AP mode for initial configuration.

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
