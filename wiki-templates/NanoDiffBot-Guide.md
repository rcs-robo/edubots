# NanoDiffBot Guide

NanoDiffBot is an Arduino Nano-based differential drive educational robot designed for learning robotics and programming.

![NanoDiffBot](https://via.placeholder.com/600x400/667eea/ffffff?text=NanoDiffBot)

## Overview

NanoDiffBot features:
- **Microcontroller:** Arduino Nano (ATmega328P)
- **Motor Driver:** L298N dual H-bridge
- **Sensors:** Ultrasonic distance, light, dual line following, IR receiver
- **Actuators:** RGB LED, buzzer
- **Power:** Rechargeable battery or USB power

## Hardware Specifications

### Motors & Drive System
- **Type:** DC geared motors with wheels
- **Configuration:** Differential drive (left and right independent control)
- **Speed Control:** PWM (0-255)
- **Direction Control:** H-bridge via L298N

### Sensors

#### Ultrasonic Distance Sensor (HC-SR04)
- **Range:** 2cm - 400cm
- **Accuracy:** ±3mm
- **Use Case:** Obstacle detection, distance measurement
- **Pins:** TRIG=4, ECHO=2

#### Light Sensor (LDR/Photoresistor)
- **Type:** Analog light sensor
- **Range:** 0-1023 (raw ADC value)
- **Use Case:** Light following, ambient light detection
- **Pin:** A0

#### Line Following Sensors
- **Type:** Infrared reflective sensors (TCRT5000 or similar)
- **Count:** 2 (left and right)
- **Detection:** Black line on white surface or vice versa
- **Pins:** LEFT=A1, RIGHT=A2

#### IR Receiver
- **Type:** 38kHz infrared receiver
- **Use Case:** Remote control
- **Pin:** 10

### Actuators

#### RGB LED
- **Type:** Common cathode or anode RGB LED
- **Colors:** Red, Green, Blue (mix for other colors)
- **Control:** PWM for Red and Green, digital for Blue
- **Pins:** RED=3, GREEN=6, BLUE=A3

#### Buzzer
- **Type:** Piezo buzzer
- **Use Case:** Sounds, tones, melodies
- **Pin:** 9

## Pin Configuration

```
Left Motor:
  - PWM (Speed):     Pin 5  (ENA on L298N)
  - Direction 1:     Pin 7  (IN1 on L298N)
  - Direction 2:     Pin 8  (IN2 on L298N)

Right Motor:
  - PWM (Speed):     Pin 11 (ENB on L298N)
  - Direction 1:     Pin 12 (IN3 on L298N)
  - Direction 2:     Pin A4 (IN4 on L298N)

Sensors:
  - Ultrasonic TRIG: Pin 4
  - Ultrasonic ECHO: Pin 2
  - Light Sensor:    Pin A0
  - Line Left:       Pin A1
  - Line Right:      Pin A2
  - IR Receiver:     Pin 10

Actuators:
  - RGB LED Red:     Pin 3  (PWM)
  - RGB LED Green:   Pin 6  (PWM)
  - RGB LED Blue:    Pin A3 (Digital only)
  - Buzzer:          Pin 9  (PWM)
```

## Wiring Diagram

### L298N Motor Driver Connections

```
Arduino Nano → L298N
Pin 5  → ENA (Left Motor Speed)
Pin 7  → IN1 (Left Motor Direction)
Pin 8  → IN2 (Left Motor Direction)
Pin 11 → ENB (Right Motor Speed)
Pin 12 → IN3 (Right Motor Direction)
Pin A4 → IN4 (Right Motor Direction)

L298N → Motors
OUT1, OUT2 → Left Motor
OUT3, OUT4 → Right Motor

Power:
12V Battery → L298N 12V Input
L298N 5V Output → Arduino 5V (if not using USB power)
GND → Common ground for all components
```

### Sensor Connections

```
Ultrasonic HC-SR04:
VCC → 5V
GND → GND
TRIG → Pin 4
ECHO → Pin 2

Light Sensor (LDR):
One leg → 5V
Other leg → A0 and 10kΩ resistor to GND

Line Sensors:
VCC → 5V
GND → GND
OUT Left → A1
OUT Right → A2

IR Receiver:
VCC → 5V
GND → GND
OUT → Pin 10
```

## Assembly Guide

### Step 1: Chassis Assembly
1. Attach motors to chassis
2. Install caster wheel at back
3. Attach wheels to motors

### Step 2: Electronics Mounting
1. Mount L298N motor driver on chassis
2. Mount Arduino Nano on chassis
3. Install battery holder

### Step 3: Wiring Motors
1. Connect left motor to L298N OUT1 and OUT2
2. Connect right motor to L298N OUT3 and OUT4
3. Wire Arduino pins to L298N as per pin configuration

### Step 4: Sensor Installation
1. Mount ultrasonic sensor at front (elevated position)
2. Install line sensors at bottom front
3. Mount light sensor on top
4. Install IR receiver (facing forward/up)

### Step 5: Actuator Installation
1. Mount RGB LED in visible location
2. Install buzzer
3. Connect to Arduino pins

### Step 6: Power Connections
1. Connect battery to L298N power input
2. Connect grounds together (common ground)
3. Optional: Connect L298N 5V output to Arduino VIN

### Step 7: Testing
1. Upload test program to Arduino
2. Verify each motor direction
3. Test all sensors
4. Test LED and buzzer

## Programming Basics

### Motor Control

#### Move Forward
```
Drive forward at speed 100 for 2000ms
Stop motors
```

#### Turn
```
Turn right at speed 80 for 1000ms
Stop motors
```

#### Precise Control
```
Steer: Left motor 100, Right motor 50
Wait 1000ms
Stop motors
```

### Sensor Reading

#### Ultrasonic Distance
```
If ultrasonic distance < 20cm
  Then: Stop motors
  Else: Drive forward
```

#### Light Sensor
```
Display light sensor value on console
If light value > 500
  Then: LED green
  Else: LED off
```

#### Line Following
```
If left sensor on line AND right sensor on line
  Then: Drive forward
Else if left sensor on line
  Then: Turn left
Else if right sensor on line
  Then: Turn right
Else
  Then: Stop
```

## Example Projects

### 1. Basic Movement Demo
- Move forward 1 second
- Turn right 90 degrees
- Move forward 1 second
- Turn left 90 degrees
- Repeat

### 2. Obstacle Avoidance
- Drive forward continuously
- Check ultrasonic distance
- If obstacle < 30cm, stop and turn
- Continue driving

### 3. Line Following Robot
- Read both line sensors
- Adjust motor speeds to follow line
- Handle intersections and endpoints

### 4. Light Seeker
- Read light sensor
- Rotate slowly while reading
- Drive toward brightest direction

### 5. Remote Control
- Receive IR remote commands
- Map commands to movements
- Add LED feedback for commands

## Troubleshooting

### Motor Issues

**Motors not spinning:**
- Check power connections
- Verify L298N enable jumpers are in place
- Check motor wiring (try swapping wires)
- Verify code is sending PWM signal

**Motors spinning wrong direction:**
- Swap motor wires at L298N output
- Or swap DIR1/DIR2 pins in code

**Motors weak or stuttering:**
- Check battery voltage (needs 7-12V)
- Ensure common ground connection
- Check PWM signal strength in code

### Sensor Issues

**Ultrasonic not reading:**
- Check wiring (TRIG and ECHO correct)
- Verify 5V power to sensor
- Keep sensor away from motors (noise)

**Line sensors not detecting:**
- Adjust sensor height (3-5mm from surface)
- Check sensor polarity (some are NC/NO)
- Calibrate threshold values in code
- Test on high contrast surface

**Light sensor readings erratic:**
- Check wiring and pull-down resistor
- Shield from direct sunlight
- Add smoothing in code (average readings)

### Power Issues

**Arduino resets when motors start:**
- Add capacitor across motor terminals (100nF)
- Use separate power for motors and Arduino
- Check battery capacity

**Robot stops after few seconds:**
- Battery discharged - recharge
- Check for short circuits
- Verify current draw is within limits

## Calibration

### Line Sensor Calibration
1. Place robot on white surface
2. Note sensor values (should be low)
3. Place robot on black line
4. Note sensor values (should be high)
5. Set threshold at midpoint

### Motor Balance
1. Drive both motors at same speed
2. If robot veers, adjust motor speeds
3. Some motors may need trim adjustment
4. Save calibration values in code

## Advanced Topics

### PID Line Following
Implement PID control for smooth line following:
- P: Proportional - error correction
- I: Integral - accumulated error
- D: Derivative - rate of change

### Encoder Addition
Add wheel encoders for:
- Accurate distance measurement
- Precise turning angles
- Speed feedback control

### Bluetooth Control
Add HC-05/HC-06 module for:
- Smartphone control
- Wireless programming
- Data logging

## Maintenance

- **Clean wheels** regularly for good traction
- **Check connections** periodically
- **Recharge batteries** before storage
- **Update firmware** when available
- **Calibrate sensors** if behavior changes

## Resources

- [Wiring Diagrams](Wiring-Diagrams)
- [Example Programs](NanoDiffBot-Examples)
- [Pin Configuration Reference](Pin-Configuration)
- [Troubleshooting Guide](Common-Issues)

---

Have questions? [Ask on GitHub](https://github.com/rcs-robo/edubots/issues)
