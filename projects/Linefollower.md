# LineFollower Robot 

## Repository  

[Linefollower](https://github.com/Bordomir/Linefollower)

## Team Members

- [**Hubert Błaszczyk** ](https://github.com/hub-bla)
  - PCB etching  
  - Software development  
  - Video production  
  - System testing and calibration  

- [**Jan Cieśla** ](https://github.com/deithh) 
  - PCB etching  
  - Robot design  
  - Component assembly  
  - System testing and calibration
 
- **Me [(Bartosz Operacz)](https://github.com/Bordomir)**
  - PCB etching  
  - Software development  
  - Documentation preparation  
  - System testing and calibration
  
## Introduction

The goal of our team was to build a **LineFollower robot** from scratch, capable of following a black line on the ground.

### The robot was expected to:
- Detect the line underneath it
- Move on flat surfaces and turn as needed
- Have its own power supply
- Generate control signals to follow the line
- Provide feedback on its status
- Be easy to program externally

## Technical Solutions

The robot uses the following components:

- **5 TCRT5000 reflective opto-transistors** – for detecting the black line. Chosen for their long detection range.
- **2 N20-BT16 motors** – directly connected to wheels for propulsion and turning. With 2000 RPM, they allow for speeds of ~2m/s using 24mm diameter wheels, providing satisfying acceleration.
- **TB6612FNG dual motor driver** – to control the motors.
- **Li-Pol 2S 7.4V 20C Dualsky 800mAh battery** – selected for its good weight-to-capacity ratio and high current delivery.
- **LM7805 voltage regulator** – with reverse current protection circuit.
- **ATMEGA328P-PN microcontroller**, clocked with a 16MHz oscillator.
- **Voltage divider** – for monitoring battery voltage and detecting low charge.
- **2 LEDs and a button** – for user interaction and feedback.
- **SPI interface** – exposed for programming.
- **Reverse polarity protection** – using an asymmetric power connector.
- **Power filtering for ICs** – carefully designed to minimize interference.

## Robot Construction

The robot consists of two custom-made etched PCBs, forming a T-shape. 
The front PCB houses the optical sensors, arranged for early and efficient line detection. 
The rest of the robot is mounted toward the rear, positioning the center of gravity near the drive system to improve steering stability.

## Schematics and PCB Description

### Main Board:

![image](https://github.com/user-attachments/assets/7d722abe-8b8d-4574-a72f-9f4de2b580a8)  

### Sensor Board:

![image](https://github.com/user-attachments/assets/e1439ff4-5d7e-4be8-81c2-3caab87816e7)

### PCB Etching Process:

1. **Film preparation** – Printed the layout on transparent film. Two films were used for better opacity, aligned using registration marks.
2. **Darkroom setup** – Prepared solutions of universal developing fluid (5.5g/100ml) and sodium persulfate etchant (20g/100ml). Laminates were trimmed ~5mm over final size and deburred.
3. **UV exposure** – Removed protective foil from laminate. Placed the film (non-mirrored, toner side down), and exposed for ~180s with a UV lamp. For additional pressure we used a glass sheet and vacuum bag.
4. **Developing** – ~150–180s in developer at room temperature with agitation. Rinsed afterward.
5. **Etching** – ~10–20min depending on board size and solution freshness. Heated solution to ~50°C. Etching was complete when all copper between traces disappeared. Rinsed afterward.
6. **Cleaning and finishing** – Residual resist removed with acetone. Edges trimmed with a saw. Boards were coated with lacquer or solder mask.

## Software

Custom software was developed to:
- Read signals from optical sensors
- Calculate control signals for the motors based on line position
- Ensure smooth line tracking

### Libraries Used

- **SparkFun TB6612** motor driver library

#### Key Classes & Methods:
- `Motor` class
  - `drive()` – move specific motor
  - `brake()` – stop both motors

### Defined Macros

Used for:
- Pin identifiers
- Register bit manipulation

### Custom Functions

- `sbi`, `cbi` – set/clear bits in SFRs
- `start()` – robot activation
- `shutdown()` – robot deactivation
- `calculate_error()` – determine deviation from the line
- `calculate_motors_speed()` – compute speed corrections
- `drive_motors()` – set motor speeds
- `calibrate()` – calibrate sensors

### Microcontroller Setup

Includes:
- Configure reference voltage on analog inputs
- Configure ADC clock
- Pin mode configuration
- Sensor weight calculation
- Ensuring that LEDs are turned off

## Main Program Loop

### Battery Monitoring

Voltage is measured using a divider:
- If below threshold: warning LED is activated
- If critically low: robot halts and flashes LED to indicate shutdown

### Button Logic

- Button state is tracked to detect presses
- Short vs. long press determines calibration or power toggle
- Current state is indicated by rear LED
- Calibration is disabled while robot is running

### Line Following Logic

- If robot is active, it reads sensor data
- Line position is computed
- Error is calculated (how far off the line)
- PID control algorithm determines correction
- Motor speeds are adjusted accordingly

**Failsafe:**  
If no line is detected:
- Robot repeats last movement
- "Off-track" timer increases
- If too much time off-track: robot shuts down automatically

## Final Result

Linefollower:  
![image](https://github.com/user-attachments/assets/ea5b5476-1c89-461b-8c08-f09a8cb69a10)  
  
Video presenting entire process of robot creation and final result is available below  
[Video](https://www.youtube.com/watch?v=wPkWPQ8s4SI)
