# 5. Robot Mobility

This section elaborates on the mechanical and functional aspects of VizDrive's mobility system, encompassing motor configuration, steering mechanics, and fundamental movement functions. The design prioritizes a balance of power, precision, and agile maneuverability for the WRO circuit.

## Motor and Wheel Configuration

VizDrive employs a **rear-wheel drive (RWD)** configuration, where one DC motor provides propulsion to the rear wheels in a solid axle. Front-wheel steering is achieved via a servo-controlled angle.

* **Propulsion Motor:** **Hobby Gearmotor with 48:1 gearbox** is used for the rear drive, providing sufficient torque through their integrated gearboxes.
* **Steering Mechanism:** A **Servo Motor SG90** is employed to control the angle of the front steering wheels.
* **Base Speed:** The nominal base speed for the motors is set to `200` (PWM signal).
* **Wheel Characteristics:**
  * Wheel Circumference: `22.0 cm`.
  * Pulses per Revolution (PPR) from encoder: `16.0`.
  * Calculated Pulses per Centimeter: `PULSES_PER_REVOLUTION / WHEEL_CIRCUMFERENCE`.

## Mechanical Design Considerations for Mobility

Several mechanical design principles were applied to enhance the robot's mobility and precision:

* **Light Frame:** The chassis is designed as a light beam structure, compacting components while maintaining high driving precision and durability.
* **Tolerance Management:** Varied tolerances were incorporated during part design. For instance, screws are designed for a snug fit, while wheel and steering mechanisms have higher tolerance to allow for slight movement and reduce friction. This tolerance also contributes to a degree of suspension, accommodating minor ground deformities and enhancing stability.
* **Caster Angle:** To counteract the inherent imprecision from high steering tolerances, a **caster angle of 10°** was implemented. This mechanism ensures that the wheels naturally return to a centered position, facilitating precise straight-line movement.
* **Steering Angle:** The robot's steering system is capable of a **45-degree turn in each direction**, enabling sharp turns and addressing specific challenges like parallel parking maneuvers.
* **Screw Orientation:** Screws are oriented to tighten when the robot moves forward, preventing wheels from detaching if screws loosen due to excessive friction. This detail is crucial during 3D printing, with hub designs including options for both screw orientations.

## Fundamental Motion Software Functions

The robot's movement is managed by the following core functions:

* `driveForward(int speed)`: Initiates forward movement of the robot by setting the PWM signal for the motors.
* `driveBackwards(int speed)`: Commands backward movement.
* `stopMotors()`: Halts all motor activity, allowing the robot to coast to a stop.
* `stopBrake()`: Executes an immediate and forceful stop of all motors.
* `setSteeringAngle(int angle)`: Controls the servo motor to set the precise steering angle for the front wheels.
  * `SERVO_STRAIGHT`: Represents the angle for straight-line travel (e.g., 90 degrees).
  * `SERVO_GIRO`: Defines the maximum rotational angle for turns.
  * `SERVO_LEFT`: Calculated as `SERVO_STRAIGHT - SERVO_GIRO`.
  * `SERVO_RIGHT`: Calculated as `SERVO_STRAIGHT + SERVO_GIRO`.
* `performTurn(direction)`: Executes a pre-defined turning maneuver. The `straight_direction` variable is adjusted by `±90` degrees depending on whether the turn is "left" or "right".

---
[Back to Main README.md Index](../README.md)