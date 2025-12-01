## 🤖 Alve-Web-Interface: Alve Dashboard

**The Official Web Interface for the Alve Humanoid Robot**

<p align="center">
  <img src="https://img.shields.io/badge/ROS%202-Jazzy-blue.svg" alt="ROS 2 Jazzy Badge">
  <img src="https://img.shields.io/badge/OS-Ubuntu%2024.04-orange.svg" alt="Ubuntu 24.04 Badge">
  <img src="https://img.shields.io/badge/Tech-HTML%20|%20CSS%20|%20JS-red.svg" alt="Web Technologies Badge">
  <img src="https://img.shields.io/badge/Interface-macOS%20Aesthetic-lightgrey.svg" alt="macOS Aesthetic Badge">
</p>

-----

### ⭐ Project Overview

An **effective human-robot interface** is the cornerstone of any robotics deployment. This repository hosts the official, feature-rich web interface for the **Alve Humanoid Robot**, designed to provide an intuitive, platform-agnostic solution for **real-time visualization and remote control**.

Leveraging the **universal accessibility of the web browser**, this interface transforms any internet-connected device into a powerful control station. It offers a **generic, powerful, and highly customizable** platform built on the enduring core technologies of HTML, CSS, and JavaScript.

<img src="https://i.ibb.co/rGzVLNvP/image.png" alt="Alve Web Interface Dashboard Screenshot">


-----

### ✨ Key Features of the Dashboard

The Alve Web Interface is a central control hub, featuring a visually clean (**macOS-inspired aesthetic**) and functional design. All application windows feature the familiar traffic-light buttons (close, restore, maximize/minimize).

  * **Mecanum Drive Controller:** Provides responsive **teleoperation** for the robot's omnidirectional movement via a **dual-joystick interface**.
      * One joystick for **linear velocity** (XY-plane).
      * One joystick for **angular velocity** (Yaw).
      * Configurable **speed limits** via dedicated slider bars.
  * **Real-time Sensor Feeds:** Dedicated windows for live video streaming.
      * **RGB Camera Feed:** Live stream from the Intel RealSense D435i camera.
      * **Depth Camera Feed:** Processed depth image for spatial perception.
      * Both include a **full-screen toggle** for detailed inspection.
  * **Odometry Data Display:** Real-time visualization of the robot’s estimated position $(X, Y, 0)$, derived from wheel encoder data, relative to the starting origin $(0, 0, 0)$.
  * **Quad View Toggle:** An instant-access button to arrange the primary views (Drive Controller, RGB Feed, Odometry, and Depth Feed) into a unified, **max-efficiency quad-view layout**.

-----

### 🚀 Getting Started

This guide assumes you are running **ROS 2 Jazzy** on **Ubuntu 24.04**.

---

#### 1. Prerequisites and Installation

**A. Core Robot Repository**

First, clone the main robot repository and complete its setup. **Follow all installation and setup instructions within that repository's README** before proceeding.

[![View the Alve-robot Repository](https://img.shields.io/badge/-View%20Repository-007EC6?style=for-the-badge&logo=github)](https://github.com/MohamedAliZouariEng/Alve-robot.git)

**B. Essential ROS Packages**

Install the necessary web communication packages for ROS 2 Jazzy:

```bash
sudo apt update
sudo apt install ros-jazzy-rosbridge-suite
sudo apt install ros-jazzy-web-video-server
````

> For more information, see the official repositories:
>
>   * **rosbridge\_suite:** [https://github.com/RobotWebTools/rosbridge\_suite/tree/jazzy](https://github.com/RobotWebTools/rosbridge_suite/tree/jazzy)
>   * **web\_video\_server:** [https://github.com/RobotWebTools/web\_video\_server](https://github.com/RobotWebTools/web_video_server)

-----

#### 2\. Launching Services

To enable full web-based functionality, you must launch three core services in separate terminal sessions.

| Step | Command | Description |
| :--- | :--- | :--- |
| **1. Start HTTP Server** | `python3 -m http.server 7010` | Initiates a lightweight Python HTTP server to host the static HTML/CSS/JS files for the web interface. Binds to `0.0.0.0:7010`. |
| **2. Start ROSBridge** | `ros2 launch rosbridge_server rosbridge_websocket_launch.xml` | Starts the **rosbridge\_websocket** (WebSocket server on port 9090) and **rosapi\_node**, enabling JSON-based communication between the web client and the ROS 2 network. |
| **3. Start Video Server** | `ros2 run web_video_server web_video_server` | Subscribes to ROS image topics (e.g., `/camera/image_raw`) and republishes them as **MJPEG streams** accessible via HTTP on port 8080. |

```
```
-----

### 🌐 Accessing the Interface

1.  Open your web browser and navigate to the server address:
    ```
    http://<host_machine_ip>:7010/
    ```
    *(If running locally, use `http://0.0.0.0:7010/`)*
2.  In the dashboard's **"Connection Status"** field, enter the WebSocket URI for ROSBridge (e.g., `ws://localhost:9090`).
3.  Click the **Connect** button. A successful connection (to the robot or simulation) will trigger an **audible confirmation tone** and transition the interface to the `control.html` page, ready for operation\!

-----

**Pro-Tip:** Remember to click the **"Power Off"** button in the interface when done to safely disconnect, which will also be confirmed by an audible tone.

---
### 🎥 Demonstration and Usage

See the **Alve Web Interface** in action, showcasing real-time teleoperation, sensor visualization, and the quad-view layout.

[![Watch the Live Demo on Vimeo](https://img.shields.io/badge/Watch%20Demo-Vimeo-1AB7EA?style=for-the-badge&logo=vimeo)](https://vimeo.com/user/242059085/folder/27481654?fl=tl&fe=cc)

---
