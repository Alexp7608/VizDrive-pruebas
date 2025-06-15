# 8. Color Sensors for Circuit Perception

VizDrive employs multiple color sensors to perceive crucial cues on the competition circuit:

## **TCS3200 Color Sensor (Side-mounted):**

* **Placement:** Positioned at the bottom of the robot.
* **Function:** Primarily used for correcting obstacle color-based evasion maneuvers and, crucially, for detecting the **magenta signal** that indicates the parking lot for the completion phase.
* **Magenta:** High red and blue values, low green value.
* **Thresholds:** Specific thresholds are defined for color detection, according to light-based sensor calibration:
  * `MAGENTA_RED_THRESHOLD = 100` (greater than)
  * `MAGENTA_BLUE_THRESHOLD = 100` (greater than)
  * `MAGENTA_GREEN_THRESHOLD = 50` (less than)

## **TCS3472 Color Sensors (Bottom-mounted):**

* **Placement:** Two sensors located at the bottom of the robot.
* **Function:** Specifically used for detecting **blue** and **orange** lines on the circuit mat. These lines act as indicators for strategic turning points.
* **Color Normalization:** Raw color sensors detections are normalized and inverted to a value between 0 and 255 in the `int normalize(int value, int maxVal)` function. This converts the raw lectures into similar values to RGB.
  * **Orange:** High red and green values, low blue value.
  * **Blue:** High blue value, low red and green values.
* **Thresholds:** Specific thresholds are defined for color detection, according to light-based sensor calibration:
  * `ORANGE_RED_THRESHOLD = 100`
  * `ORANGE_GREEN_THRESHOLD = 100`
  * `ORANGE_BLUE_THRESHOLD = 50`
  * `BLUE_BLUE_THRESHOLD = 100`
  * `BLUE_RED_THRESHOLD = 50`
  * `BLUE_GREEN_THRESHOLD = 50`

---

[Back to Main README.md Index](../README.md)
