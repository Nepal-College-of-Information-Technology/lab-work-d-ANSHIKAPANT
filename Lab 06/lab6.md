# Lab 06: Getting Started with ESP32 - Blinking the Built-in LED

## Title
Getting Started with ESP32: Blinking the Built-in LED

## Objective
The main objectives of this experiment are to:
- Install and configure the ESP32 board in the Arduino IDE.
- Write and upload a basic LED blink program.
- Understand the structure of an Arduino program using `setup()` and `loop()`.
- Verify communication between the computer and the ESP32 board using the Serial Monitor.

## Requirements
### Hardware
- ESP32 development board
- USB cable
- Computer or laptop

### Software
- Arduino IDE
- ESP32 board package
- USB driver (if required)

## Theory
The ESP32 is a powerful microcontroller with built-in Wi-Fi and Bluetooth capabilities. It is widely used in Internet of Things (IoT) projects because of its flexibility and performance.

Most ESP32 development boards have a built-in LED connected to GPIO 2. By setting this pin to HIGH and LOW alternately with a delay, the LED can be made to blink continuously.

An Arduino program generally consists of two main functions:
- `setup()`: runs once when the board starts or resets and is used for initialization.
- `loop()`: runs continuously after `setup()` and contains the main program logic.

## Program
```cpp
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
```

## Code Explanation
- `const int LED_PIN = 2;` defines GPIO 2 as the pin connected to the built-in LED.
- `pinMode(LED_PIN, OUTPUT);` configures the selected pin as an output.
- `Serial.begin(115200);` starts serial communication at a baud rate of 115200 bits per second.
- `digitalWrite(LED_PIN, HIGH);` turns the LED on.
- `digitalWrite(LED_PIN, LOW);` turns the LED off.
- `delay(500);` pauses the program for 500 milliseconds.

## Procedure
1. Open the Arduino IDE.
2. Install the ESP32 board package.
3. Connect the ESP32 board using a USB cable.
4. Select the correct board and COM port:
   - Board: ESP32 Dev Module
   - Port: appropriate COM port
5. Copy the blink program into the Arduino IDE.
6. Click Verify to compile the code.
7. Click Upload to flash the program to the board.
8. Open the Serial Monitor.
9. Set the baud rate to 115200.
10. Observe the blinking of the LED and the serial messages.

## Expected Output
### LED Behavior
- The LED turns ON for 500 ms.
- The LED turns OFF for 500 ms.
- This pattern repeats continuously.

### Serial Monitor Output
```text
ESP32 BLINK Program Started
LED ON
LED OFF
LED ON
LED OFF
...
```

### Upload Status
The program should compile and upload successfully. The upload console typically shows messages such as:
```text
Writing firmware to ESP32
Verifying flash
Hash verified
Hard resetting via RTS pin
```

## Screenshot
If you want to include a screenshot in the report, place the image in an images folder and embed it as follows:

```html
<p align="center">
  <img src="images/esp32_blink_output.png" width="900">
</p>
```

## Result
The ESP32 blink program was successfully compiled and uploaded using the Arduino IDE. The built-in LED connected to GPIO 2 blinked continuously at a 500 ms interval, and the Serial Monitor displayed the expected ON/OFF status, confirming that the board was programmed correctly and communication was successful.

## Conclusion
This experiment demonstrated the basic programming workflow for the ESP32 using the Arduino IDE. It verified that the development environment was configured correctly, the board could be programmed successfully, and GPIO pins could be controlled to blink the onboard LED. This foundational exercise provides a strong starting point for more advanced IoT applications involving sensors, actuators, Wi-Fi communication, and cloud connectivity.
