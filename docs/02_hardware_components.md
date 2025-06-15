# 2. Robot Hardware and Components

This section provides a detailed enumeration and description of all hardware components integrated into the robot.

## Main Control and Processing Unit

### **Component:**  **MEGA 2560 Pro Embed**

* **Quantity:** 1
* **Voltage:** 5V (operating), 7-12V (Vin)
* **Description:** Serves as the main controller board, based on the ATmega2560 microcontroller. It processes all sensor data, executes control algorithms, and manages actuation.
* **Features:** 54 digital I/O pins, 16 analog inputs, 256 KB flash memory, and 16 MHz clock speed.

![Mega 2560 Pro Embed](../assets/hardware_photos/mega2560pro.jpg)

## Motion System Components

### **Component:** **Hobby Gearmotor with 48:1 gearbox**

* **Quantity:** 1
* **Voltage Range:** 3-12V (operating at 3.7V)
* **Current Consumption** ~200 mA (no load)
* **Stall Torque:** ~0.8 kg·cm @ 6V
* **Description:** A brushed DC motor with an integrated gearbox for increased torque. Utilized for rear-wheel propulsion.

![Hobby Gearmotor](../assets/hardware_photos/hobbymotor.jpg)

### **Component:** **Servo Motor MG90S**

* **Quantity:** 1
* **Voltage Range:** 4.8-6V
* **Current Consumption:** ~250 mA (max)
* **Torque:** 1.5 kg·cm @ 5V
* **Description:** A micro servo motor employed for front-wheel steering. Operates via PWM signal.

![Servo Motor MG90S](../assets/hardware_photos/servo.jpg)

### **Component:** **Mini L298N Motor Driver**

* **Quantity:** 1
* **Logic Voltage:** 5V
* **Motor Voltage Range:** Up to 12V
* **Current Output:** Up to 2A per channel
* **Description:** A dual H-bridge motor driver responsible for interfacing the low-current control signals from the Arduino Mega to the higher-current requirements of the DC motors.

![Mini Motor Driver L298N](../assets/hardware_photos/motordriver.jpg)

## Sensor Suite

### **Component:** **PixyCam 2**

* **Quantity:** 1
* **Voltage:** 5V
* **Current Consumption:** ~140 mA
* **Interface:** ICSP
* **Description:** Smart vision sensor for real-time color and object recognition. Used for obstacle detection.

![PixyCam2](../assets/hardware_photos/pixycam.jpg)

### **Component:** **TCS3472 Color Sensor**

* **Quantity:** 1
* **Voltage:** 3.3-5V
* **Current Consumption** ~235 µA (active)
* **Interface:** I2C
* **Description:** High-resolution color sensor with IR filtering. Mounted underneath the robot to detect blue and orange floor lines that indicate turns.

![TCS3472 Color Sensor](../assets/hardware_photos/tcs3472color.jpg)

### **Component:** **TCS3200 Color Sensor**

* **Quantity:** 2
* **Voltage:** 2.7-5.5V
* **Power Consumption:** ~10-50 mA
* **Output:** Frequency proportional to color intensity
* **Description:** Side-mounted color recognition sensors used for detecting the magenta signal for parking. Converts color input to frequency output.

![TCS3200 Color Sensor](../assets/hardware_photos/tcs3200color.jpg)

### **Component:** **HC-SR04 Ultrasonic Sensors**

* **Quantity:** 4
**Voltage:** 5V
**Current Consumption:** ~15 mA
**Range of Detection:** 2 cm to 4 m
* **Description:** Distance sensors placed at the front and rear utilized for measuring real-time distances to walls, used for collision avoidance and maintaining orientation.

![Ultrasonic Sensor HC-SR04](../assets/hardware_photos/ultrasonicsensor.jpg)

### **Component:** **MPU6050 Accelerometer + Gyroscope**

* **Quantity:** 1
* **Voltage:** 3.3-5V
* **Current Consumption:** ~3.8 mA
* **Interface:** I2C
* **Description:** A 3-axis MPU providing acceleration and angular velocity data, used for angle correction and maintaining trajectory stability through PID control.

![MPU6050 Gyroscope](../assets/hardware_photos/MPU6050.jpg)

### **Component:** **Infrared Optocoupler Encoder**

* **Quantity:** 1
* **Voltage:** 3.3-5V
* **Current Consumption:** <20 mA
* **Description:** A laser interruption-based encoder used for detecting rotational position, enabling accurate measurement of distance and speed (odometry).

![IR Encoder](../assets/hardware_photos/encoder.jpg)

## Power Supply and Regulation

### **Component:** **3.7V batteries**

* **Quantity:** 2
* **Voltage:** 3.7V nominal
* **Capacity:** 5000 mAh
* **Discharge Current:** Up to 2A (depending on model)
* **Description:** Power supply for the robot's DC motors. Specifically, **Li-ion 18650 Battery 3.7V 5000 mAh** is used.

![Li-ion 18650 3.7V Battery](../assets/hardware_photos/3.7Vbattery.jpg)

### **Component:** **Rechargable 9V Battery**

* **Quantity:** 1
* **Voltage:** 9V nominal
* **Capacity:** ~500 mAh
* **Description:** A standard 9V battery used for the sensors and Arduino MEGA unit.

![Standard 9V Battery](../assets/hardware_photos/9Vbattery.jpg)

## Miscellaneous Components

### **Component:** **Custom Chassis (RWD)**

* **Quantity:** 1
* **Material:** 3D printed (PLA)
* **Description:** A 3D designed rear-wheel drive chassis designed to house motors, mounts, sensors, battery holders, and the controller.

[Interactive 3D Model of Custom Chassis](../embeds/interactive_chassis.html)

### **Component:** **Pushbutton**

* **Quantity:** 1
* **Voltage Handling:** Signal-level (logic input)
* **Current:** <10 mA
* **Description:** A momentary switch used to initiate the main program.

### **Component:** **Toggle Switch**

* **Quantity:** 1
* **Voltage Handling:** 5-12V
* **Current:** Up to 3A
* **Description:** A switch for toggling between two states, serving as the main power switch for the robot.

### **Component:** **LED**

* **Quantity:** 1
* **Forward Voltage:** ~2V
* **Current:** ~10-20 mA
* **Description:** A standard red LED used as a visual indicator, signaling program readiness.

### **Component:** **Resistor**

* **Quantity:** 1
* **Power Rating:** 1/4 W
* **Description:** Current-limiting resistor for the LED.

## Circuit Design

We developed a custom shield circuit using a Printed Circuit Board (PCB) to streamline the electrical connections, in order to reduce cable clutter, and minimize the overall weight, size, and complexity of the system. All components and routes were manually soldered onto the PCB to ensure a compact and custom integration of all components.

![PCB VS Prototype Circuit](../assets/hardware_photos/imagen%20(6).jpg)

* **Detailed Electromechanical Diagram:** For a more in-depth view of how all electronic and mechanical components are interconnected, please refer to the [Electromechanical Diagram](./../schemes/electromechanical_diagram.png) in the `schemes/` folder.

* **Cirkit Circuit Design:** A detailed interactive visual representation of our circuit, can be found in `embeds/`: [Interactive Cirkit Circuit Design](../embeds/interactive_circuit.html).

---

[Back to Main README.md Index](../README.md)
