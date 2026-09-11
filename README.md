# Fovea-Lidar
An adaptive, variable-resolution 2.5D LiDAR perception engine for autonomous UGVs. Engineered for edge-computing with >95% memory reduction

This organization hosts the codebase for the Fovea Lidar project, developed for the Smart India Hackathon (Team Beyonders / ID26053). The system processes raw 3D point cloud data into a compressed 2.5D map for autonomous vehicle navigation.

The primary objective is to reduce the memory and processing requirements of standard 3D mapping while retaining critical height data that standard 2D flat maps lose.

## Core Features

* **Adaptive Resolution:** Adjusts mapping detail based on the distance from the vehicle. It maintains high precision (0.5m) near the vehicle and uses lower precision (2.0m) at further distances to reduce memory consumption by over 95%.
* **Data Compression:** Converts standard 3D data into a 2.5D grid. Each grid cell stores only the maximum height, minimum height, and object category.
* **Surface Tracking:** Uses a moving average algorithm to monitor the road surface. This allows the system to detect road defects and depressions exceeding 12cm, even when operating on slopes or uneven terrain.
* **Error Correction:** Automatically verifies and corrects object classifications based on their physical height relative to the ground.

## Technology Stack

* **Core Logic:** Python 3.12 and NumPy for optimized array processing.
* **Simulation Environment:** CARLA Autonomous Driving Simulator (v0.9.16) operating in synchronous mode.
* **Data Source:** Ray-cast Semantic Lidar.
* **Visualization:** Matplotlib with customized rendering logic to maintain consistent frame rates.

## System Architecture

The workflow consists of data acquisition through the CARLA simulator, followed by an initial filtering stage to remove vehicle self-occlusion. The point cloud is then processed through a simulated perception layer before entering the NumPy mapping engine.

The mapping engine applies the distance-based resolution rules, checks for road depressions, and stores the final output in a compressed format. The visualization module reads this compressed data, mathematically removes points outside the current camera view to prevent system lag, and renders the map for operator viewing.
