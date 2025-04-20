# Air Drums Prototype

## Repository

Full source code, including real-time visualization tools, network data access, and a serial port bridge, is available here:  
[Virtual-Drums](https://github.com/deithh/Virtual-Drums)

## Team Members

- [**Hubert Błaszczyk** ](https://github.com/hub-bla)

- [**Jan Cieśla** ](https://github.com/deithh) 
 
- **Me [(Bartosz Operacz)](https://github.com/Bordomir)**

## Project Overview

The goal of this project was to build a virtual air drum set consisting of two drumsticks and a foot pedal. 
By equipping these components with motion sensors and integrating a Bluetooth speaker, we aimed to replicate the experience of playing a real drum set while significantly reducing the physical space required.

## Hardware Platform

- **Processing Unit**: Raspberry Pi 4B
- **Sensors**: 6-axis IMU (initially), later upgraded to 9-axis IMU for improved orientation accuracy
- **Trigger**: Foot pedal
- **Output Device**: Bluetooth speaker

## Objective and Scope

The objective was to develop a virtual drum system that detects the motion of the sticks and the pressing of a foot pedal, analyzes the sensor data, and plays corresponding drum sounds. 
The system leverages motion data to classify hits and generate appropriate audio responses.

### Project Scope Included:

- Utilizing Raspberry Pi 4B as the processing and control unit
- Connecting motion sensors (IMUs) to the Pi via I2C
- Interpreting IMU data for detecting stick orientation and hit gestures
- Interfacing with a foot pedal for kick drum triggering
- Playing audio through an external Bluetooth speaker
- Allowing overlapping sound playback (multiple simultaneous hits)

## Project Implementation

### Achieved Goals:

- Connected 6-axis IMUs to the Raspberry Pi using I2C communication
- Calibrated IMUs to increase motion tracking precision
- Implemented data processing algorithms to calculate stick orientation
- Detected hits and classified them based on stick orientation
- Triggered audio playback based on detected events (hits and pedal)
- Integrated Bluetooth speaker to play drum sounds
- Supported simultaneous sound playback
- Assembled all hardware components into a working prototype

### Unachieved Goals and Challenges:

- **IMU Limitation**: The initial 6-axis IMUs failed to maintain orientation accuracy over time, making them unsuitable for reliable hit detection. We replaced them with 9-axis IMUs, which provided a stable reference point.
- **Position-Based Sound Selection**: The system was unable to reliably calculate the stick's position in space due to accumulating errors, making it impractical to dynamically position virtual drums around the player for extended sessions.

## System Architecture

1. **Sensor Input**: Two IMUs, one per drumstick, detect orientation and motion.
2. **Foot Pedal**: Pressing the foot pedal triggers a kick sound.
3. **Processing**: Raspberry Pi receives and processes IMU and pedal input.
4. **Audio Output**: Selected drum sound is played via Bluetooth speaker.

## Software Design

- A `Sensor` class aggregates and processes data from each drumstick.
- Calibration functions are applied to ensure reliable orientation data.
- The main script:
  - Loads audio files on startup
  - Spawns threads to handle each drumstick and foot pedal input
  - Continuously listens for sensor events and classifies them

### Code Features:

- Sensor data smoothing and calibration
- Orientation-based hit classification
- Multi-threaded architecture for real-time input handling
- Overlapping sound playback support

## System Photos

![image](https://github.com/user-attachments/assets/b631c1d0-d714-40c1-9962-f43718c6d665)  

## Potential Improvements

- Implement more advanced IMU filtering and sensor fusion algorithms to enhance positional accuracy
- Add velocity-based volume scaling for dynamic sound effects
- Introduce external tracking (e.g. a camera) to provide positional input and better spatial drum mapping
- Allow users to configure custom drum layouts and assign sounds
- Add functionality to record and playback drumming sessions
- Include a rhythm game mode with timed drum hits for training or entertainment

## Result

[Video](https://drive.google.com/file/d/1z3zXan86EZ6XceUL_VHCWaNOBvNVzolA/view?usp=drive_link)

## Conclusion

This prototype demonstrated that it's possible to simulate drumming using motion sensors and a Raspberry Pi. 
While some features like accurate spatial tracking were limited by sensor drift and computational performance, the core functionality of detecting stick hits and playing corresponding drum sounds was successfully implemented.

The project highlighted both the strengths and limitations of the Raspberry Pi as a real-time processing unit. 
Effective IMU calibration was essential to system performance. 
To address performance bottlenecks and visualization demands, we offloaded real-time visualization to a separate computer via network communication.

The development process offered valuable hands-on experience in sensor integration, real-time data processing, and responsive audio output—all within a compact, embedded Linux environment.
