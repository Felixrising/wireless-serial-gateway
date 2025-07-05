1) Serial
When working with Arduino IDE, Serial communication is an essential part of many projects. To use Serial in Arduino IDE, you need to start by opening the Serial Monitor window. This can be done by clicking on the Serial Monitor icon in the toolbar or by pressing the Ctrl+Shift+M shortcut key.

General Usage
Some of the commonly used Serial functions include:

Serial.begin() -- which initializes the communication at a specified baud rate;
Serial.print() -- which sends data to the Serial port in a readable format;
Serial.write() -- which sends binary data to the Serial port;
Serial.available() -- which checks if there is any data available to be read from the Serial port;
Serial.read() -- which reads a single byte of data from the Serial port;
Serial.flush() -- which waits for the transmission of outgoing serial data to complete.
By using these Serial functions, you can send and receive data between the Arduino board and your computer, which opens up many possibilities for creating interactive projects.

Here is an example program:

void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
}

void loop() {
  // send data to the serial port
  Serial.println("Hello World!");

  // read data from the serial port
  if (Serial.available() > 0) {
    // read the incoming byte:
    char incomingByte = Serial.read();
    // print the incoming byte to the serial monitor:
    Serial.print("I received: ");
    Serial.println(incomingByte);
  }
  
  // wait for a second before repeating the loop
  delay(1000);
}

In this code, we first initialize the Serial communication at a baud rate of 9600 using the Serial.begin() function in the setup() function. Then, in the loop() function, we use the Serial.print() function to send "Hello World!" to the Serial port.

We also use the Serial.available() function to check if there is any data available to be read from the Serial port. If there is, we read the incoming byte using the Serial.read() function and store it in a variable called incomingByte. We then use the Serial.print() and Serial.println() functions to print "I received: " followed by the value of incomingByte to the Serial monitor.

Finally, we add a delay() function to wait for one second before repeating the loop. This code demonstrates how to use some of the commonly used Serial functions in Arduino IDE for sending and receiving data through the Serial port.

After uploading the program, open the Serial Monitor in Arduino IDE and set the baud rate to 9600. You will see the following message on the serial monitor, which outputs 'Hello World!' every second. Also, you can send content to the XIAO ESP32S3 through the serial monitor, and XIAO will print out each byte of the content you send.


Serial1 Usage
According to the above XIAO ESP32S3 Pin diagrams for specific parameters, we can observe that there are TX pin and RX pin. This is different from serial communication, but the usage is also very similar, except that a few parameters need to be added. So next, we will use the pins led out by the chip for serial communication.

Core Function that need to be include:

Serial1.begin(BAUD,SERIAL_8N1,RX_PIN,TX_PIN); -- enalbe Serial1,the function prototype : <Serial.Type>.begin(unsigned long baud, uint32_t config, int8_t rxPin, int8_t txPin);
baud :baud rate
config:Configuration bit
rxPin :Receive Pin
txPin :Send Pin
It is worth nothing that if we use digital pin port to define,this place should be#define RX_PIN D7、#define TX_PIN D6,if we use GPIO pin port to define,this place should be #define RX_PIN 44、#define TX_PIN 43,please refer to the pin diagrams of different XIAO Series for specific parameters

Here is an example program:

#define RX_PIN D7
#define TX_PIN D6
#define BAUD 115200

void setup() {
    Serial1.begin(BAUD,SERIAL_8N1,RX_PIN,TX_PIN);
}
 
void loop() {
  if(Serial1.available() > 0)
  {
    char incominByte = Serial1.read();
    Serial1.print("I received : ");
    Serial1.println(incominByte);
  }
  delay(1000);
}

After uploading the program, open the Serial Monitor in Arduino IDE and set the baud rate to 115200.then,you can send content you want in the XIAO ESP32S3 through the serial monitor Serial ,and XIAO will print out each byte of the content you send.,In here,the content i entered is "Hello Everyone",my result chart is as follows



2) Other Hardware Serial
The ESP32S3 has a total of three UART communication interfaces, numbered from 0 to 2, which are UART0, UART1, and UART2. The pins of these three serial ports are not fixed and can be remapped to any IO port.

By default, we don't use UART0 as it is used for USB serial communication. You can use other hardware serial ports by customizing the hardware serial mapping.

// Need this for the lower level access to set them up.
#include <HardwareSerial.h>

//Define two Serial devices mapped to the two internal UARTs
HardwareSerial MySerial0(0);
HardwareSerial MySerial1(1);

void setup()
{
    // For the USB, just use Serial as normal:
    Serial.begin(115200);

    // Configure MySerial0 on pins TX=D6 and RX=D7 (-1, -1 means use the default)
    MySerial0.begin(9600, SERIAL_8N1, -1, -1);
    MySerial0.print("MySerial0");

    // And configure MySerial1 on pins RX=D9, TX=D10
    MySerial1.begin(115200, SERIAL_8N1, 9, 10);
    MySerial1.print("MySerial1");
}

void loop()
{

}



