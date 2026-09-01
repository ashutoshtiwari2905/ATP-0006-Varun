# VARUN — Versatile Adaptive Reconnaissance Underwater Navigator

> **A low-cost underwater ROV for seabed exploration, metal-rich deposit detection, and spatial heat mapping.**

## Overview

**VARUN** is an underwater **Remotely Operated Vehicle (ROV)** designed to descend through the water column and perform systematic surveys close to the seabed.

The primary objective of VARUN is to detect and spatially map **metal-rich seabed deposits** over a defined survey area. Instead of manually navigating the vehicle across the seafloor, VARUN is designed to follow a structured **lawnmower (boustrophedon) survey pattern**, allowing it to cover the target area systematically while maintaining a controlled altitude above the seabed.

VARUN is connected to a **surface station through a strong, waterproof Ethernet tether**, providing a reliable power supply and communication link between the underwater vehicle and the operator while also supporting the transmission of live camera footage and collected survey data.

During the survey, onboard sensing systems collect information related to the presence and relative intensity of detectable metallic deposits. An **underwater pressure sensor** measures the surrounding water pressure, which is used to estimate the vehicle's **depth** using the hydrostatic pressure relationship. **Ultrasonic sensors** continuously measure the distance between VARUN and the seabed, enabling it to maintain a specific **altitude** while accounting for variations in seabed elevation. An **IMU (Inertial Measurement Unit)** monitors the vehicle's motion and orientation by providing acceleration and angular-motion data, which can be used to estimate parameters such as **orientation, velocity, and relative position** for improved navigation and motion stability. A **temperature sensor** records the water temperature at the vehicle's operating depth, while a waterproof **camera and two underwater lights** provide real-time visual observation of the surrounding environment and seabed.

The collected sensor data can then be processed and represented as a **spatial heat map**, providing a visual representation of areas with higher or lower detected metallic activity. The vehicle is designed with a focus on **low-cost construction, modularity, stability, and practical underwater operation**, making it suitable as a prototype platform for underwater surveying and exploration.

![Mapping_Geometry](medias/Mapping_Geometry.png)

## What is VARUN?

VARUN is a compact underwater ROV consisting of:

* A waterproof electronics enclosure
* A dedicated waterproof camera chamber
* Underwater lighting
* Four thrusters for vehicle movement and orientation
* Ballast tanks positioned toward the lower section
* Buoyancy tanks positioned toward the upper section
* A seabed-facing metal detection system for identifying metal-rich regions
* An underwater pressure sensor for depth measurement
* Underwater ultrasonic sensors for measuring the distance from the seabed
* An IMU sensor for measuring acceleration and angular motion and supporting orientation, velocity, and relative-position estimation
* A temperature sensor for measuring the surrounding water temperature
* A control and communication system for operating the vehicle and collecting survey data

The vehicle is intended to operate **a few inches above the seabed**, rather than continuously touching or travelling directly on the seafloor. This allows the sensing system to scan the seabed while the vehicle maintains a controlled and relatively consistent surveying altitude.

---

## Survey Method

VARUN is designed around a **Boustrophedon (lawnmower) pattern survey strategy**.

![Lawnmover_Pattern](medias/Lawnmower_Horizontal.jpeg)
![Lawnmover_Pattern_2](medias/Lawnmower_Vertical.jpeg)

The vehicle moves along parallel passes across the selected survey area, periodically changing its heading at the end of each pass. This approach provides structured coverage of the seabed and reduces the possibility of unintentionally leaving large gaps between surveyed regions.

While moving through the survey area, the detection system continuously records measurements along with the vehicle's estimated **position, motion and orientation, depth, seabed distance, and surrounding water temperature**.

These measurements can subsequently be converted into a spatial representation such as a **heat map**, where different regions of the surveyed area represent different levels of detected metallic activity.

![Heat_Map_Sample](medias/Heat_Map_Sample.jpeg)
![Heat_Map_Sample_2](medias/Heat_Map_Sample%20(2).jpeg)

### Simplified Survey Flow

![Flowchart_1](medias/Flowchart_1.png)

---

## Thruster Configuration

VARUN uses **four thrusters** arranged to provide controlled underwater movement and orientation.

![Thruster](medias/Thruster.png)

### Horizontal Thrusters

Two horizontally mounted thrusters are positioned on the left and right sides of the vehicle.

Their primary purpose is to provide **yaw control**, allowing VARUN to rotate and change its heading during navigation and while following the survey pattern.

![Horizontal_Thrusters](medias/Horizontal_Thrusters.png)

### Vertical Thrusters

Two vertically mounted thrusters are positioned approximately along the central region of the vehicle, with one toward the front and one toward the rear.

![Vertical_Thrusters](medias/Vertical_Thrusters.png)

These thrusters provide **vertical control**, allowing the vehicle to adjust its depth and pitch while maintaining its desired operating altitude above the seabed.

The combination of horizontal and vertical thrust is intended to provide stable and controllable movement while surveying underwater terrain.

The **IMU provides motion and orientation feedback** during these movements, allowing the control system to monitor changes in the vehicle's orientation and motion and improve the stability of the vehicle during operation.

---

## Depth & Seabed Distance Measurement

Maintaining a consistent position relative to the seabed is an important part of VARUN's surveying operation. To achieve this, the vehicle uses an **underwater pressure sensor**, **ultrasonic sensors**, and an **IMU** for complementary measurements.

### Pressure Sensor

The underwater pressure sensor measures the **water pressure at the current depth** of VARUN.

The measured pressure can be used to estimate the vehicle's depth using the hydrostatic pressure relationship:

```text
P = ρgh
svg
```

![Pressure_Formula](medias/Pressure_Formula.jpeg)

where:

* `P` = hydrostatic pressure
* `ρ` = density of water
* `g` = acceleration due to gravity
* `h` = depth below the water surface

Rearranging the relationship allows the depth to be estimated from the measured water pressure:

```text
h = P / (ρg)
svg
```

This provides VARUN with an estimate of its **depth below the water surface** during operation.

### Ultrasonic Seabed Distance Measurement

The underwater ultrasonic sensors are used to measure the **distance between VARUN and the seabed**.

![Ultrasonic_Sensor](medias/Underwater_Ultrasonic_Sensor.jpg)

Unlike the pressure sensor, which provides an estimate of the vehicle's depth in the water column, the ultrasonic sensors provide a direct measurement of the distance to the seabed beneath the vehicle.

This measurement is used to help VARUN maintain a **specific operating distance above the seabed** while conducting its survey.

By continuously monitoring the seabed distance, the vehicle can account for changes in seabed elevation and adjust its vertical position accordingly, helping maintain a more consistent surveying altitude.

### IMU-Based Motion & Orientation Measurement

VARUN also incorporates an **Inertial Measurement Unit (IMU)** to monitor the vehicle's motion and orientation.

![IMU_Sensor](medias/IMU_Sensor_Geometry.jpg)

The IMU provides measurements such as:

* Linear acceleration
* Angular velocity
* Vehicle orientation
* Changes in motion

These measurements can be processed to estimate the vehicle's **velocity and relative position**, particularly when combined with other navigation and sensor data. The IMU also provides important motion feedback for maintaining stable pitch, roll, and yaw during underwater operation.

Since position and velocity estimates derived solely from an IMU can accumulate error over time, the IMU is intended to work together with other available measurements and navigation information rather than acting as the vehicle's sole positioning system.

### Combined Depth, Altitude & Motion Awareness

The combination of pressure-based depth estimation, ultrasonic seabed-distance measurement, and IMU-based motion monitoring gives VARUN several important pieces of underwater positional information:

**Water Depth + Seabed Distance + Motion + Orientation**

![Depth_and_Altitude](medias/Depth_and_Altitude.png)

This allows the system to distinguish between its overall depth in the water column, its relative height above the seabed, and its current motion and orientation while navigating through the survey area.

---

## Water Temperature Measurement

VARUN also incorporates an **underwater temperature sensor** to measure the temperature of the surrounding water at the vehicle's current operating level.

![Temperature_Sensor](medias/Temperature_Sensor.jpeg)

During a survey, the temperature sensor can continuously record the water temperature along with other collected measurements.

This provides a temperature reading associated with the vehicle's **current depth and surveying location**, allowing temperature variations within the surveyed water column and area to be recorded as part of the collected survey data.

---

## Buoyancy & Stability

A major design consideration for VARUN is maintaining stability underwater.

The vehicle incorporates separate **ballast and buoyancy chambers**:

* **Ballast tanks** are positioned toward the lower portion of the vehicle.
* **Buoyancy tanks** are positioned toward the upper portion.

![COM_and_Buoyancy](medias/MC_COM_Buoyancy.gif)

This arrangement is intended to naturally distribute the vehicle's mass and buoyancy around its vertical axis, helping VARUN maintain a more stable orientation in water.

![COM_and_Buoyancy_2](medias/MC_COM_Buoyancy_2.gif)

The design aims to reduce unnecessary corrective thrust and make it easier for the vehicle to maintain a consistent surveying position above the seabed.

The **IMU further supports stability monitoring** by continuously providing information about the vehicle's orientation and motion, allowing the control system to detect unwanted changes in pitch or yaw and apply appropriate corrective action.

---

## Vision System

VARUN incorporates a dedicated **waterproof camera chamber** containing:

* An underwater camera
* Two onboard lights

![Camera](medias/Camera.webp)
![Lights](medias/Lights.jpeg)

The camera provides a live visual view of the underwater environment, allowing the operator to observe the seabed, verify the vehicle's position, and monitor the survey area.

The onboard lighting system is intended to improve visibility in low-light underwater conditions where natural illumination may be insufficient.

---

## Waterproof Electronics

The vehicle's primary electronics are housed inside a separate **waterproof enclosure** designed to isolate sensitive electronic components from the surrounding water.

The enclosure is intended to accommodate components such as:

* Microcontroller / onboard computing hardware
* Motor control electronics
* Power management circuitry
* Communication hardware
* Sensor interfaces
* IMU and other navigation sensors
* Other supporting electronics

The modular enclosure approach also makes it easier to modify or upgrade the electronics as the project develops.

---

## Key Features

* 🌊 **Underwater seabed surveying**
* 🤖 **Structured lawnmower-pattern navigation**
* 🧭 **Controlled yaw, pitch, and vertical movement**
* 📐 **IMU-based motion and orientation monitoring**
* 📍 **Relative position and velocity estimation**
* 📏 **Pressure-based depth estimation**
* 📡 **Ultrasonic seabed-distance measurement**
* 🎯 **Controlled operating altitude above the seabed**
* 🌡️ **Underwater temperature measurement**
* ⚓ **Ballast and buoyancy-based stability**
* 🔍 **Metal-rich seabed deposit detection**
* 🗺️ **Spatial heat-map generation**
* 📷 **Waterproof onboard camera**
* 💡 **Integrated underwater lighting**
* 🔒 **Waterproof electronics enclosure**
* 💰 **Low-cost prototype-oriented design**

---

## What VARUN Aims to Provide

VARUN is intended to transform underwater surveying from a purely visual inspection task into a **data-driven exploration process**.

Instead of simply showing an operator what the seabed looks like, the system aims to combine:

**Navigation + Sensing + Depth + Seabed Distance + Temperature + Motion + Orientation + Positioning + Data Processing**

to produce a more useful representation of the surveyed region.

The pressure sensor provides an estimate of the vehicle's **depth**, while the ultrasonic sensors monitor its **distance from the seabed**. Together, these measurements help maintain a controlled surveying altitude while the vehicle moves across the survey area.

The IMU continuously monitors the vehicle's **acceleration, angular motion, and orientation**, providing motion information that can support estimates of velocity and relative position and help maintain stable vehicle movement.

At the same time, the temperature sensor records the **water temperature at the vehicle's operating level**, while the metal detection system collects measurements associated with potentially metal-rich regions of the seabed.

The final output is envisioned as a map showing **where detectable metal-rich deposits are more likely to be concentrated**, allowing areas of interest to be identified for further investigation.

---

## System Architecture

At a high level, VARUN can be divided into the following subsystems:

![Flowchart_2](medias/Flowchart_2.png)

This architecture brings together the vehicle's **propulsion, sensing, depth measurement, seabed-distance measurement, motion and orientation monitoring, temperature monitoring, vision, control, and data processing** into a single underwater surveying platform.

---

## Project Goals

The long-term goal of VARUN is to develop a **practical, affordable, and modular underwater surveying platform** capable of systematically exploring seabed regions and converting sensor observations into useful spatial information.

Rather than building a vehicle that simply moves underwater, VARUN is being developed as a complete **underwater reconnaissance and surveying system** where the vehicle, sensors, navigation, depth measurement, seabed-distance monitoring, motion and orientation sensing, temperature sensing, and data processing work together.
