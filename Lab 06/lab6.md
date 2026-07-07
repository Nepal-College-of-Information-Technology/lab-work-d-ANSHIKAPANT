Lab 06
Title

Getting Started with ESP32: Blinking the Built-in LED

Objective
To install and configure the ESP32 board in Arduino IDE.
To write and upload a basic LED Blink program.
To understand the structure of an Arduino program (setup() and loop()).
To verify successful communication between the computer and ESP32 using the Serial Monitor.
Requirements
Hardware
ESP32 Development Board
USB Cable
Computer/Laptop
Software
Arduino IDE
ESP32 Board Package
USB Driver (if required)
Theory

The ESP32 is a powerful microcontroller with built-in Wi-Fi and Bluetooth. It is widely used for Internet of Things (IoT) applications.

The built-in LED on most ESP32 development boards is connected to GPIO 2. By setting this pin HIGH and LOW repeatedly with a delay, the LED blinks continuously.

An Arduino program consists of two main functions:

setup()
Runs only once after the board powers on or resets.
Used for initialization.
loop()
Runs continuously after setup().
Contains the main program logic.
Program
const int LED_PIN = 2;

void setup() {
  pinMode(LED_PIN, OUTPUT);

  Serial.begin(115200);
  delay(1000);

  Serial.println("ESP32 BLINK Program Started");
}

void loop() {
  digitalWrite(LED_PIN, HIGH);
  Serial.println("LED ON");
  delay(500);

  digitalWrite(LED_PIN, LOW);
  Serial.println("LED OFF");
  delay(500);
}
Code Explanation
const int LED_PIN = 2;

Defines GPIO 2 as the LED pin.

pinMode(LED_PIN, OUTPUT);

Configures GPIO 2 as an output pin.

Serial.begin(115200);

Starts serial communication at a baud rate of 115200 bps.

digitalWrite(LED_PIN, HIGH);

Turns the LED ON.

digitalWrite(LED_PIN, LOW);

Turns the LED OFF.

delay(500);

Waits for 500 milliseconds.

Procedure
Open Arduino IDE.
Install the ESP32 board package.
Connect the ESP32 board using a USB cable.
Select:
Board: ESP32 Dev Module
Correct COM Port
Copy the Blink program into Arduino IDE.
Click Verify to compile the code.
Click Upload to flash the program.
Open the Serial Monitor.
Set the baud rate to 115200.
Observe the LED blinking and serial messages.
Output
LED Behavior
LED turns ON for 500 ms.
LED turns OFF for 500 ms.
This process repeats continuously.
Serial Monitor
ESP32 BLINK Program Started

LED ON
LED OFF
LED ON
LED OFF
LED ON
LED OFF
...
Upload Status

The program compiled and uploaded successfully.

The upload console showed:

Writing firmware to ESP32
Verifying flash
Hash verified
Hard resetting via RTS pin

This confirms successful programming of the ESP32.

Screenshot

Create an images folder in your repository and save the uploaded screenshot as:

Lab05/
│── README.md
│── images/
│     └── esp32_blink_output.png

Add the screenshot using:

<p align="center">
  <img src="images/esp32_blink_output.png" width="900">
</p>
Result

The ESP32 Blink program was successfully compiled and uploaded using the Arduino IDE. The built-in LED connected to GPIO 2 blinked continuously with a 500 ms interval, and the Serial Monitor displayed the LED ON/OFF status, confirming proper operation of the ESP32 board and successful serial communication.

Conclusion

This experiment demonstrated the basic programming workflow of the ESP32 using the Arduino IDE. It verified that the ESP32 development environment was correctly configured, the board could be programmed successfully, and GPIO pins could be controlled to blink the onboard LED. This foundational experiment prepares the ESP32 for more advanced IoT applications involving sensors, actuators, Wi-Fi communication, and cloud connectivity.
