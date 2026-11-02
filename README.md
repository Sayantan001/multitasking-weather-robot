# Multitasking & Weather Forecasting Robot

A multi-mode Arduino-based robot that avoids obstacles, follows lines, follows objects, and can be driven by Android app, IR remote, voice or gestures. It also shows live temperature and humidity and raises a buzzer alert when it detects flame.

![Circuit diagram](Circuit%20Diagram.png)

## Features

- **Obstacle avoidance:** a servo-mounted ultrasonic sensor scans left and right, and the robot turns toward the side with more free space.
- **Line following:** IR sensors detect the line and the Arduino drives the motors through the motor driver.
- **Object following:** IR sensors and an ultrasonic sensor let it follow a person or object and back away when too close.
- **Manual control:** Android app over Bluetooth (HC-05), IR remote, voice control via Google Assistant, and gesture control.
- **Weather display:** DHT11 temperature and humidity shown on a 16x2 LCD.
- **Flame alert:** flame sensors trigger a 12 V buzzer.

## System overview

Two microcontrollers share the work:

- **Arduino Nano:** reads the DHT11 and flame sensors, drives the LCD and the buzzer.
- **Arduino Uno:** runs the main robot logic (modes, motor control, ultrasonic scanning, Bluetooth and IR input).

Mode selection comes from the Bluetooth or IR input. Manual, line-follower and obstacle-avoidance modes each have their own logic in the main loop.

## Hardware

- Arduino Uno and Arduino Nano
- L298N 2A motor driver
- 4 x dual-shaft BO motors
- HC-SR04 ultrasonic sensor and servo motor
- IR sensor modules and IR receiver module
- 5-pin flame sensor and single-pin flame sensor
- DHT11 temperature and humidity sensor
- 16x2 LCD display
- HC-05 Bluetooth module
- 12 V buzzer

## Software

- Arduino IDE
- Libraries: `SoftwareSerial`, `IRremote`, `DHT11`, `LiquidCrystal`
- MIT App Inventor (Android control app)

## Repository structure

- `firmware/nano_sensors/` - Nano sketch (weather display and flame alert)
- `firmware/uno_main/` - Uno sketch (robot modes and motor control)
- `Circuit Diagram.png` and `Circuit Diagram.fzz` - wiring (Fritzing)
- `images/` - code screenshots

The Android app is available under [Releases](../../releases).

## Build and run

1. Wire the circuit as shown in the circuit diagram.
2. Install the required libraries in the Arduino IDE.
3. Upload `firmware/nano_sensors/nano_sensors.ino` to the Nano. The LCD should show temperature and humidity, and the buzzer should sound when flame is detected.
4. Disconnect the HC-05 RX/TX pins, upload `firmware/uno_main/uno_main.ino` to the Uno, then reconnect them.
5. Install the APK from the Releases page, pair your phone with the HC-05, and choose a mode.

## Safety and power notes

- Do not switch on the battery while the Arduino is connected to a laptop over USB (the Uno's maximum input is 12 V).
- Power the motor driver and the HC-05 from a separate 5 V supply, not from the Arduino 5 V pin.
- Powering the sensors and LCD separately avoids delays and overloading the Arduino.
- If the app crashes, check that Bluetooth is on and permissions are granted, then reinstall it.

## Limitations

- High power consumption, with about 1 hour of runtime on 2 x 3.7 V cells.
- Bluetooth adds some control latency.
- The components can be damaged by overuse.

## Future work

- PCB version to replace the breadboard wiring
- Lower-power design for longer runtime

## License

MIT
