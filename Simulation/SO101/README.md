# SO101 Robot - URDF and MuJoCo Description

This repository contains the URDF and MuJoCo (MJCF) files for the SO101 robot.

## Overview

- The robot model files were generated using the [onshape-to-robot](https://github.com/Rhoban/onshape-to-robot) plugin from a CAD model designed in Onshape.
- The generated URDFs were modified to allow meshes with relative paths instead of `package://...`.
- Base collision meshes were removed due to problematic collision behavior during simulation and planning.

## Calibration Methods

The MuJoCo file `scene.xml` supports two differenly calibrated SO101 robot files:

- **New Calibration (Default)**: Each joint's virtual zero is set to the **middle** of its joint range. Use -> `so101_new_calib.xml`. 
- **Old Calibration**: Each joint's virtual zero is set to the configuration where the robot is **fully extended horizontally**. Use -> `so101_old_calib.xml`.

To switch between calibration methods, modify the included robot file in `scene.xml`.

## Wrist Camera Variant

- `so101_new_calib_camera.urdf` / `so101_new_calib_camera.xml` extend the new-calibration model with a **wrist camera mount and camera** (Hex-Nut, 32×32 UVC module form factor), matching the Wrist-Mount Camera hardware option in the main README's [Optional Hardware](../../README.md#optional-hardware) section.
- Two fixed links are added off the gripper: `wrist_camera_mount_link` (mount, `assets/wrist_camera_mount_so101_v1.stl`) and `wrist_camera_link` (camera body, `assets/wrist_camera_so101_v1.stl`).
- Use these files instead of the base `so101_new_calib` files when simulating a robot built with the wrist camera mount installed.

## Motor Parameters

Motor properties for the STS3215 motors used in the robot are adapted from the [Open Duck Mini project](https://github.com/apirrone/Open_Duck_Mini).

## Gripper Note

In LeRobot, the gripper is represented as a **linear joint**, where:

* `0` = fully closed
* `100` = fully open

This mapping is **not yet reflected** in the current URDF and MuJoCo files. 

---

Feel free to open an issue or contribute improvements!
