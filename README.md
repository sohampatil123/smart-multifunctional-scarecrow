# Smart Multifunctional Solar-Powered Scarecrow — Arduino Software

Arduino Nano starter software for a crop-protection scarecrow using motion detection, a motor driver, a relay-controlled pump, a water-level sensor, ultrasonic distance sensing, a buzzer and an LED.

## Components covered

- Arduino Nano
- PIR motion sensor
- L298N motor driver and two DC geared motors
- Ultrasonic distance sensor (for example, HC-SR04)
- Relay module and 12 V DC pump
- Water-level sensor
- Buzzer/speaker module
- LED
- Solar panel, battery and DC-DC buck converter (power hardware; no direct software control in this version)

## Suggested pin assignments

| Component signal | Arduino Nano pin |
|---|---|
| PIR OUT | D2 |
| Ultrasonic TRIG | D3 |
| Ultrasonic ECHO | D4 |
| L298N ENA | D5 |
| L298N IN1 | D6 |
| L298N IN2 | D7 |
| L298N IN3 | D8 |
| L298N IN4 | D9 |
| L298N ENB | D10 |
| Relay input | D11 |
| Buzzer signal | D12 |
| LED control | A0 |
| Water-level sensor analog output | A1 |

**These are suggested pins, not confirmed pins for your actual build.** Make the code and wiring match.

## Uploading

1. Install the Arduino IDE.
2. Open `SmartScarecrow/SmartScarecrow.ino`.
3. Connect the Nano by USB.
4. Choose **Arduino Nano** under Tools → Board.
5. Select the correct port and processor setting for your board.
6. Click Verify, then Upload.
7. Open Serial Monitor at 9600 baud.

No third-party libraries are needed.

## How the sketch works

1. Starts with outputs OFF and waits 30 seconds for PIR stabilization.
2. Watches the PIR sensor for motion.
3. On motion, activates LED and buzzer briefly.
4. Reads the water-level sensor and runs the pump briefly only if the reading meets the configured threshold.
5. Reads the ultrasonic sensor.
6. Commands both motors forward briefly only if the distance reading is valid and at least the configured obstacle distance.
7. Stops the motors and waits for the event cooldown before handling another event.

## Values you must verify

- `RELAY_ACTIVE_LOW`: some relay boards turn on for LOW; others for HIGH.
- `WATER_LEVEL_THRESHOLD`: calibrate for your water sensor and tank.
- `MOTOR_SPEED`: begin with a low value and test with wheels raised.
- `OBSTACLE_LIMIT_CM`: tune for your installation.
- Motor direction: verify safely; reverse motor wiring or code logic if needed.

## Electrical safety

- Never drive motors or the pump directly from an Arduino I/O pin.
- Use an appropriately rated motor driver and relay, considering startup current.
- Never connect 12 V to the Nano's 5 V pin.
- Use a suitable solar charge controller between the panel and battery.
- Use regulated power appropriate to each module and connect grounds as required by module documentation.
- Verify sensor voltage compatibility. In particular, check whether the ultrasonic module's ECHO output is safe for the Nano and any connected 3.3 V logic.
- Test inputs before enabling motor/pump power. Use clean water only for pump testing.
- This prototype does not identify whether motion came from a bird, person or other animal and is not a safety-certified autonomous vehicle.

## Repository layout

```text
smart-scarecrow-arduino-code/
├── README.md
├── LICENSE
├── .gitignore
├── SmartScarecrow/
│   └── SmartScarecrow.ino
└── docs/
    └── TESTING.md
```

## Project status

Starter software for hardware integration. Confirm pin assignments and calibrate the sensors before relying on the system.
