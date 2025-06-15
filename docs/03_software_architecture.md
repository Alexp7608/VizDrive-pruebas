# 3. Software Architecture

This section details the software architecture of VizDrive, covering the essential libraries, the core functionalities implemented, and the overall structure of the firmware. The code is primarily written in C++ for the Arduino Mega 2560 Pro.

## Required Libraries

The following libraries are used for the various functionalities of the robot:

* `Servo.h`: Standard Arduino library for controlling servo motors, utilized for steering.
* `Wire.h`: Essential for I2C (Inter-Integrated Circuit) communication, used by the MPU6050 and the I2C color sensor.
* `NewPing.h`: Specifically designed for managing ultrasonic sensors, providing efficient distance measurements.
* `Adafruit_MPU6050.h`: Library for interfacing with the MPU6050 gyroscope and accelerometer.
* `Adafruit_Sensor.h`: Core library supporting various Adafruit sensors, including the MPU6050.
* `Adafruit_TCS34725.h`: Library for integrating the TCS34725 I2C color sensor.
* `Pixy2.h`: Library for communication and data retrieval from the PixyCam 2.

## Core Functionalities

The robot's firmware is structured around several core functions:

### Motion System

* `driveForward(int speed)`: Controls the rear DC motors to move the robot forward.
* `driveBackwards(int speed)`: Controls the rear DC motors to move the robot backward.
* `stopMotors()`: Deactivates all motors, allowing for a natural deceleration.
* `stopBrake()`: Implements a forced stop by applying reverse current to the motors, ensuring rapid deceleration.
* `setSteeringAngle(int angle)`: Adjusts the angle of the front steering servo motor.
* `performTurn(direction)`: Manages the execution of pre-defined turns (left/right) by modifying the `straight_direction` variable for PID control.

### Vision-Based Obstacle Evasion

* Utilizes **PixyCam 2** to detect colored objects in the robot's path.
* Implements a decision-making process based on object color (Red for right evasion, Green for left evasion) and object size/coordinates for determining its position in a region of interest.
* The `Pixy2` library handles the interface with the camera, allowing the robot to receive block information (color signature, x/y position, width, height).

### Distance Detection

* **Ultrasonic sensors** measure real-time distance to nearby walls.
* The `NewPing` library facilitates accurate and efficient distance readings from multiple ultrasonic sensors.

### Color Detection

* **TCS230 Color Sensor (Bottom):** Detects *blue* and *orange* lines on the circuit mat to signal turn requirements. Color normalization and thresholding are applied to raw sensor data to identify specific colors.
* **TCS34725 Color Sensors (Sides):** Used for detecting the *magenta* parking signal.

### Orientation Control

* The **MPU6050 gyroscope** continuously monitors the robot's real-time angle.
* A **PD control loop** (`keepOrientation()`) utilizes the gyroscope data to correct any unwanted rotational drift and maintain a stable, straight trajectory.
* `measureGyroscope(float deltaTime)` function processes raw gyroscope data, subtracts offsets, and calculates the cumulative yaw angle.

## Program Flow and State Management

The main program (`loop()`) manages the robot's state and transitions between operational phases:

* **Initialization:** The `setup()` function handles sensor and motor initialization, including MPU calibration.
* **Program Start:** The robot waits for a button press to begin operations (`programStarted` flag).
* **Main Loop:** Once started, the `loop()` continuously executes core functionalities:
  * `driveForward(motorSpeed)`: Maintains forward motion.
  * `measureGyroscope(deltaTime)`: Updates orientation data.
  * `keepOrientation()`: Applies PID control for trajectory correction.
  * `detectColor()`: Performs continuous color detection.
* **State Variables:**
  * `direction`: Configures turning direction ("left" or "right") for each lap.
  * `lapTurnCount`: Tracks the number of turns completed within a lap (3 turns for a full lap).
  * `lapCompletedCount`: Counts completed laps.
  * `parkingMode`: Boolean flag to trigger the parking maneuver.
  * `SystemShutdown`: Flag to halt program execution.

## Code Organization in Documentation

The [source code](../src/) (`src/`) is logically organized into subdirectories based on functionality (e.g., `main_control`, `computer_vision`, `test_code`) for readability. In the main code, it is all integrated together.

---
[Back to Main README.md Index](../README.md)
