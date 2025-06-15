# 6. Orientation Control

This section provides an in-depth explanation of our Proportional-Integral-Derivative (PID) control implementation, specifically tailored to stabilize the robot's orientation using the MPU-6050 gyroscope data. Maintaining a stable and precise trajectory is crucial for VizDrive's performance in the WRO circuit.

## MPU6050 Gyroscope Integration

The **MPU6050** is a 3-axis gyroscope and accelerometer that continuously monitors the robot's real-time angular velocity and acceleration. The Z axis (Yaw) is used to determine the robot's orientation.

* **Data Acquisition:** The `measureGyroscope(float deltaTime)` function is responsible for retrieving sensor data from the MPU6050. It subtracts a pre-calibrated offset and converts the raw angular velocity from radians per second to degrees per second. A small threshold (0.1 degrees/sec) is applied to filter out measurement noise.
* **Yaw Angle Accumulation:** The `yaw` variable accumulates the angular displacement based on the integrated gyroscope readings over time (`yaw += gyroZ_deg_per_sec * deltaTime`). This provides the robot's current relative orientation.

## Fundamentals of PID Control

PID is a widely used feedback control loop mechanism. It continuously calculates an "error" value as the difference between a desired setpoint and a measured process variable. The controller then attempts to minimize this error by adjusting the process control inputs.

* **P (Proportional) Term:** Reacts to the *current* error. A larger error results in a proportionally larger corrective action. It provides the main driving force for correction.
* **I (Integral) Term:** Accounts for *past* errors. It sums up the instantaneous errors over time. This helps to eliminate any steady-state error that the proportional term might leave.
* **D (Derivative) Term:** Predicts *future* errors based on the *rate of change* of the current error. It helps to dampen oscillations and improve the system's response speed by applying a larger correction when the error is changing rapidly, and a smaller one when it's stabilizing.

## Application to the Gyroscope (Yaw Axis)

A **Proportional-Derivative (PD) control** scheme is implemented to determine the appropriate steering angle for the servo motor, thereby correcting errors in orientation and maintaining the robot's central trajectory.

* **Setpoint:** For straight-line travel, the desired yaw angular velocity is effectively zero. When executing a turn, the `straight_direction` variable is adjusted (e.g., by 90 degrees for a left or right turn) to define the new target orientation.
* **Error Calculation:** The `error` is calculated as the difference between the `straight_direction` (setpoint) and the current `yaw` angle (`error = straight_direction - yaw`).
* **Derivative Term:** The `derivative` is computed as the difference between the current `error` and the `previous_error` (`derivative = error - previous_error`). This term helps to dampen oscillations and improve the system's response to changes in orientation.
* **PD Adjustment:** The PD control output (`PD_adjustment`) is calculated using the proportional (`Kp`) and derivative (`Kd`) gains multiplied by their respective error terms (`PD_adjustment = Kp * error + Kd * derivative`). This adjustment value is then used to modulate the steering servo angle, guiding the robot back to its intended path.
* **Exclusion of Integral Term** Why no integral term correction? The control loop operates in short, real-time intervals where persistent, cumulative errors are negligible. Therefore, introducing an integral term (which addresses long-term steady-state error) is unnecessary and counterproductive, and could lead to instability. As a result, the integral gain is set to zero (`Ki = 0`)

### PID Constants

The tuning of the `Kp` and `Kd` parameters is crucial for optimal performance:

* `Kp = 1.3`
* `Kd = 0.5`
* `Ki = 0`

These values have been **empirically** determined to provide a stable and responsive control loop:

* **Kp** was adjusted by gradually increasing it until the robot started oscillating around the desired path (overcorrection), then slightly reducing it.
* **Kd** was used to smooth the response and reduce overshoot, adjusted after Kp.

## MPU Calibration Process

Accurate MPU readings are fundamental for effective PID control. A dedicated calibration procedure is performed to account for manufacturing biases and environmental factors.

* **Calibration Code:** The [MPU Calibration Code](./../src/main_control/mpu_orientation_control/mpu_calibration.ino) is designed to collect data regarding accumulated error from the MPU.
* **Data Collection:** This code collects gyroscope data over a 10-second measurement period, utilizing various sample sizes to determine the optimal average correction.
* **Offset Determination:** The `gyroZ_offset` is calculated by averaging gyroscope readings over a set number of samples (e.g., 1000 samples) while the sensor is stationary. This offset is then subtracted from subsequent raw gyroscope readings to ensure accurate, bias-corrected measurements.
* **Optimal Sample Size:** The collected data is visualized to identify the appropriate number of samples required to reduce the error to approximately ±0.01°, which is sufficient for operational accuracy. The graph indicates that around **200-250 samples** are optimal, as the error reduction becomes insignificant beyond this point.

* **Data Visualization:**
    [Accumulated error vs Number of samples](./assets/data_graphs/mpu_calibration_graph.png)
  * *Graph illustrating the accumulated error reduction as a function of the number of samples during MPU calibration.*

---

[Back to Main README.md Index](../README.md)
