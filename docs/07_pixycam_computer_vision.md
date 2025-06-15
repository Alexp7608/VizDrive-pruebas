# 7. Vision and Color Detection

VizDrive's ability to perceive its environment is crucial for both obstacle evasion and circuit navigation. This section details the implementation of artificial vision with PixyCam 2 and the various color sensors utilized for environmental perception.

## PixyCam 2 for Vision-Based Obstacle Evasion

The **PixyCam 2** is a compact, intelligent vision sensor that provides rapid object recognition based on color signatures. Its on-board processing capability offloads significant computational burden from the main microcontroller.

* **Detection Mechanism:** PixyCam 2 is configured to detect specific colored objects placed on the circuit.
* **Evasion Logic:**
  * If a **Red object** is detected, the robot initiates an evasion maneuver to the **right**.
  * If a **Green object** is detected, the robot initiates an evasion maneuver to the **left**.
* **Region of Interest (ROI):** A predefined Region of Interest is established to focus PixyCam's detection.
  * `FRAME_WIDTH = 316` (Camera dimension)
  * `FRAME_HEIGHT = 208` (Camera dimension)
  * `ROI_TOP = 60`
  * `ROI_BOTTOM = 208` 
  * `LEFT_BOUND = FRAME_WIDTH / 3` 
  * `RIGHT_BOUND = 2 * FRAME_WIDTH / 3`
* **Evasion Maneuver:** The robot actively turns until the detected obstacle is no longer within the PixyCam's ROI.

## 06.2. Ultrasonic Sensors for Distance Detection

While PixyCam handles vision-based object recognition, **Ultrasonic Sensors** provide critical real-time distance measurements to nearby walls or obstacles, complementing the vision system.

* **Role in Obstacle Avoidance:** These sensors detect short distances to walls, which can trigger an evasion maneuver in conjunction with PixyCam detection.
* **Role in Orientation:** Ultrasonic sensors are also utilized to detect distances to both walls, contributing to the robot's orientation control and helping it re-center after evasion.

---

[Back to Main README.md Index](../README.md)
