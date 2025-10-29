---
date: "2025-10-22"
draft: false
title: 'Introduction to Point Cloud | EUFS'
author: 'King Jin'
tags: ["EUFS","Pointcloud"]
showtoc: true
---
Earlier this month, I joined the perception team at EUFS(Edinburgh University Formula Student). I learned many interesting topics in autonomous vehicle perception and teamwork tools. Today, I would like to share what I've learned about point cloud technology.

> This is a new series of for my blog, stay tuned 😎！ 

## What is Point Cloud?
A point cloud is a collection of millions of 3D points that represent everything around you. Usually we use a sensor called LiDAR(Light Detection and Ranging) to create these point clouds.

## How Point Cloud work:
1. The system emits a laser pulse (usually a single-wavelength infrared light)
2. measures the time it takes for the laser to reflect back. This calculates the distance and generates a 3D point cloud. 
3. Each point contains only the spatial coordinates (x, y, z) and the reflection intensity, without RGB color information.
![pointcloud](/TechStuff/pointcloud.png)

## Point Cloud property:
1. unorder
2. sparsity
3. unstructured
4. geometric transformability

## How can we process point clouds
### 1.PCL
We use a popular library called PCL that provides tools for:
- Filtering: Removing noise and irrelevant points
- Segmentation: Grouping points that belong to the same object
- Clustering : Finding groups of point that might be cones
- Feature extraction: Calculating geometric properties like shapes and sizes.

### 2. Grid-Based Approaches
- Divide the space around the car into a 2D grid
- Count how many points fell into each grid cell
- Look for patern that match cone shapes
- Extract potential cone locations

### 3. PointPillars
See details in this blog: [Understanding PointPillars](../../pointpillars)


## Common Point Cloud tasks:
1. 3d shape classification: categorizing entire point clouds into object classes(car, pedestrain)
2. 3d object detection and tracking: Locating objects with 3D bounding boxes and following them across frames
3. 3d point cloud segmentation: Assigning a class label to every single point.

## Common Library used in Point Cloud:
The point cloud ecosystem offers several powerful libraries:
1. PCL: C++ library for classical algorithms
2. VCGLib: Specialized for mesh processing and geometry
3. CGAL: Computational geometry algorithms library
4. Open3d: Python library with excellent visualization

## High quality point cloud datasets:
1. KITTI
2. waymo
3. nuScenes

## Other Methods for 3D object detection:
while LiDAR is powerful, various other approaches exists for 3D perception.
1. monocular camera
   1. D4LCN
   2. Mono3D-PLiDAR
2. binocular camera
   1. Stereo R-CNN
   2. PSMNet
3. RGB-D
   1. F-PointNets
4. LiDAR
   1. PV-RCNN
   2. PointPillar
   3. PointRCNN
5. RGB+Li-dar
   1. EPNet
   2. CLOCs
   3. 3D-CVF
Each approach has trade-offs in term of accuracy, speed, cost and robustness.

## Series Perception
1. [Introduction to Point Cloud](../pointcloud)

