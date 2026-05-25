# Vehicle Diagnostics — Android App

Android client for the [Vehicle CAN-Bus project](../README.md). Connects to the Arduino over Bluetooth and shows live OBD-II data plus diagnostic trouble codes.

<p align="center">
  <img src="../docs/images/screenshot-main-menu.jpeg" alt="Main menu" width="240" />
  <img src="../docs/images/screenshot-dashboard.jpeg" alt="Dashboard" width="240" />
  <img src="../docs/images/screenshot-diagnostic.jpeg" alt="Diagnostic" width="240" />
</p>

## Build

| | |
|---|---|
| Min SDK | 16 (Jelly Bean) |
| Target SDK | 26 (Oreo) |
| Android Gradle Plugin | 3.0.0 |
| Package | `com.bdev.burrows.vehiclediagnostics` |
| 3rd-party libs | [speedviewlib](https://github.com/anastr/SpeedView) for the dashboard gauge |

Open this folder in Android Studio, let it sync Gradle, then **Run**.

> The Bluetooth module name is hard-coded in [`BTManager`](app/src/main/java/com/bdev/burrows/vehiclediagnostics/BTManager.java). Update it if you use a different HC-06.

## Architecture

Four activities/classes:

| Class | Purpose |
|---|---|
| [`BTManager`](app/src/main/java/com/bdev/burrows/vehiclediagnostics/BTManager.java) | Owns the Bluetooth connection thread and dispatches messages to the active activity's handler |
| [`MainMenu`](app/src/main/java/com/bdev/burrows/vehiclediagnostics/MainMenu.java) | Landing page; gates navigation on a successful Bluetooth connection |
| [`Dashboard`](app/src/main/java/com/bdev/burrows/vehiclediagnostics/Dashboard.java) | Real-time speed / RPM / fuel / throttle / voltage view |
| [`Diagnostics`](app/src/main/java/com/bdev/burrows/vehiclediagnostics/Diagnostics.java) | Reads and displays Diagnostic Trouble Codes (DTCs) |

## Permissions

- `BLUETOOTH`
- `BLUETOOTH_ADMIN`
- `ACCESS_COARSE_LOCATION` (required for device discovery on Android 6+)
