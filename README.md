# codtech-task-1

To design a system that controls an LED light using a microcontroller (such as Arduino) and a mobile app, we can break the project into two main components:

Hardware (Microcontroller & LED)
Software (Mobile App & Arduino Code)
Here’s an outline of how you can build this working prototype.

1. Hardware:
Components Needed:

Microcontroller: Arduino (e.g., Arduino Uno, Arduino Nano, or any similar model)
LED: A simple LED
Resistor: A 220 ohm resistor to limit current to the LED
Bluetooth Module: HC-05 or HC-06 Bluetooth module (for communication between the mobile app and Arduino)
Wires & Breadboard: For connections
Wiring Diagram:

Arduino → Bluetooth Module (HC-05)
VCC of HC-05 to 5V on Arduino
GND of HC-05 to GND on Arduino
TX of HC-05 to RX on Arduino
RX of HC-05 to TX on Arduino (cross connection)
Arduino → LED
One end of the LED to pin 13 on Arduino (or any available digital pin)
Other end of the LED to one end of a 220-ohm resistor
The other end of the resistor to GND on the Arduino
2. Software:
Arduino Code:
This code will allow the Arduino to communicate with the mobile app via Bluetooth and turn the LED on or off based on the commands received.

cpp
Copy
#include <SoftwareSerial.h>

// Define Bluetooth RX and TX pins
SoftwareSerial BTSerial(10, 11); // RX, TX

// Define LED pin
int ledPin = 13;

void setup() {
  // Start communication
  Serial.begin(9600);
  BTSerial.begin(9600); // HC-05 Bluetooth module baud rate

  // Set the LED pin as output
  pinMode(ledPin, OUTPUT);
}

void loop() {
  if (BTSerial.available()) {
    char command = BTSerial.read();  // Read the command from the Bluetooth module

    if (command == '1') {  // If '1' is received, turn the LED on
      digitalWrite(ledPin, HIGH);
      Serial.println("LED ON");
    } else if (command == '0') {  // If '0' is received, turn the LED off
      digitalWrite(ledPin, LOW);
      Serial.println("LED OFF");
    }
  }
}
Explanation of Arduino Code:

The code uses the SoftwareSerial library to communicate with the HC-05 Bluetooth module.
The BTSerial object is initialized to listen for commands sent via Bluetooth.
The LED pin is set to pin 13 and configured as an output.
The loop constantly listens for data from the Bluetooth module. When it receives '1', it turns the LED on; when it receives '0', it turns the LED off.
Mobile App (Android Example)
For the mobile app, you can use MIT App Inventor (a simple drag-and-drop tool for Android app development) or Arduino Bluetooth Controller apps for testing. Below is an outline for creating a custom app using MIT App Inventor.

MIT App Inventor Steps:
Go to MIT App Inventor and create a new project.
Design a simple interface with two buttons: one to turn the LED on and one to turn it off.
Add the BluetoothClient component to the app, which allows communication with the Bluetooth module (HC-05).
Set up the blocks to connect to the HC-05 Bluetooth device and send data (either '1' for LED on or '0' for LED off).
Sample Blocks for App:

When the ON button is clicked, send the value '1' to the Bluetooth module.
When the OFF button is clicked, send the value '0' to the Bluetooth module.
Steps for Assembly and Testing:
Wiring the Hardware:

Connect the LED and Bluetooth module to the Arduino according to the wiring diagram above.
Upload the Arduino Code:

Open the Arduino IDE, select the appropriate board and port, and upload the code to the Arduino.
Install the App:

If using MIT App Inventor, build the APK and install it on your phone. If you're using an existing Bluetooth controller app, pair the HC-05 Bluetooth module with your phone (using the default pairing code 1234 or 0000).
Test the System:

Open the app on your phone and connect it to the HC-05 Bluetooth module.
Press the “ON” button to turn the LED on and the “OFF” button to turn it off.
Optional Enhancements:
Add status feedback: Have the Arduino send a response back to the app indicating whether the LED is on or off.
Use Wi-Fi instead of Bluetooth: If you prefer to use Wi-Fi for communication, you can use an ESP8266 or ESP32 microcontroller and control the LED via a web interface or an app that sends HTTP requests.
Conclusion:
This system, using Arduino and a mobile app, provides basic control over an LED light through Bluetooth communication. The app sends simple commands, and the Arduino receives these commands to control the LED. This prototype can be expanded further by adding more features like multiple LEDs, a web interface, or controlling other devices via Bluetooth or Wi-Fi.


