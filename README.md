# Smart Multifunctional Solar-Powered Scarecrow

An Arduino Nano software starter project for a mobile scarecrow prototype that detects motion and can activate lights, a buzzer, and a relay-controlled DC pump. It also includes an ultrasonic obstacle check and a water-level input.

> **Hardware note:** This is a configurable starter implementation, not a verified wiring diagram for your exact build. Confirm every pin and module voltage against your actual hardware before powering it. Test the pump with clean water only.

## Features

- PIR motion detection
- Ultrasonic distance check to help avoid driving into nearby obstacles
- Two DC geared motors controlled through an L298N driver
- LED and buzzer alert
- Relay-controlled 12 V pump with a timed run
- Water-level input to prevent a pump run when the tank reads low
- Serial Monitor messages for basic debugging

## Hardware

- Arduino Nano
- L298N dual H-bridge motor driver
- 2 × 12 V geared DC motors
- PIR motion sensor
- HC-SR04-style ultrasonic sensor (check your module's voltage requirements)
- Water-level sensor
- Relay module suitable for the pump's voltage and current
- 12 V DC pump
- Buzzer/speaker module
- LED (use a suitable series resistor if it is a bare LED)
- 12 V battery, solar panel, and a suitable solar charge controller
- DC-DC buck converter for a regulated supply suitable for the Nano and sensors

## Suggested pin map

These are **suggested defaults only**. Change the constants in `src/SmartScarecrow.ino` to match your wiring.

| Function | Arduino Nano pin |
|---|---|
| PIR output | D2 |
| Ultrasonic TRIG | D3 |
| Ultrasonic ECHO | D4 |
| L298N ENA | D5 (PWM) |
| L298N IN1 | D6 |
| L298N IN2 | D7 |
| L298N IN3 | D8 |
| L298N IN4 | D9 |
| L298N ENB | D10 (PWM) |
| Relay module input | D11 |
| Buzzer input | D12 |
| LED output | A0 |
| Water-level sensor analog output | A1 |

## Important electrical safety

- **Do not power motors or the pump from an Arduino I/O pin.**
- The motor driver and relay contacts must be rated for the motors/pump and their startup current.
- Connect the Arduino, sensor, and motor-driver logic grounds together where required by the module design.
- Use a suitable regulated supply for the Nano. Do not connect 12 V directly to the Nano's 5 V pin.
- Use a suitable solar charge controller between the solar panel and battery. Do not connect a panel directly to a battery unless the battery system explicitly supports that arrangement.
- Relay boards may be active-low or active-high. Set `RELAY_ACTIVE_LOW` correctly before use.
- Keep wiring insulated and dry. Secure wheels and raised parts before testing.
- For first tests, disconnect the pump and motors, verify sensor readings, then test one output at a time. Use clean water for pump testing; do not use pesticides as a test liquid.

## Upload the sketch

1. Install the Arduino IDE.
2. Open `src/SmartScarecrow.ino`.
3. Connect the Arduino Nano by USB.
4. In the IDE, select **Tools → Board → Arduino AVR Boards → Arduino Nano** (menu wording may vary).
5. Select the correct processor option for your Nano clone if upload fails.
6. Select the correct serial port.
7. Click **Verify**, then **Upload**.
8. Open **Tools → Serial Monitor** and set the baud rate to **9600**.

No third-party Arduino libraries are required.

## Initial setup and tuning

1. Confirm the pin map matches your wiring.
2. Set `RELAY_ACTIVE_LOW` to match your relay module.
3. With motors and pump disconnected, confirm PIR, ultrasonic, and water-level readings in Serial Monitor.
4. Set `WATER_LEVEL_THRESHOLD` based on the readings from your specific sensor. Some sensors produce higher readings when wet; others may differ.
5. Verify motor direction with the wheels raised safely. If a motor turns the wrong way, swap that motor's two output wires or invert its direction in code.
6. Start with low motor speed and short run times.

## Behaviour

When the PIR sensor detects motion, the sketch activates the LED and buzzer, checks the water-level input, runs the pump for a short configurable period if the level reads as sufficient, and commands the motors to move only if the ultrasonic sensor reports the path is clear. It then stops the motors and returns to monitoring.

This is a simple demonstration logic. It does not identify whether a moving object is a bird, person, or animal, and the ultrasonic sensor is not a safety-certified obstacle detector.

## Repository structure

```text
smart-scarecrow-github/
├── README.md
├── LICENSE
├── .gitignore
├── src/
│   └── SmartScarecrow.ino
└── docs/
    ├── wiring.md
    └── software-flow.md
```

## Future improvements

- Add a calibrated water-level sensor routine
- Add low-battery monitoring
- Add adjustable alert and motor timings
- Add a manual override / emergency stop
- Log detection counts over serial
- Add a verified circuit diagram after the final wiring is confirmed

## Project status

Prototype software starter. Validate pin assignments, relay polarity, sensor calibration, and motor directions on the actual hardware before deployment.
