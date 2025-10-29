---
date: "2025-10-29"
draft: true
title: 'Understanding Pointpillars | EUFS'
author: 'King Jin'
tags: ["Pointcloud","EUFS"]
showtoc: true
---
Why we need to know PointPillar? Well since most autonumous vehicle companies use or reference this algorithm in their perception system, e.g. Waymo, Baidu Apollo.

## What is PointPillars
PointPillar is a deep learning architecture specifically designed for 3D object detection from point clouds.

The name "PointPillars" comes from how it processes data: instead of treating the point cloud as random 3D points or complex 3D voxels, it organizes into vertical columns called "pillars".

## How PointPillar works?
#### Step 1: From point clouds to Pillars
- We start with input point clouds data that detected by our LiDAR
- We then divide the ground plane into a grid of small cells
- Each cell is like a vertical column or pillar extending upward
- We assign each 3D point to the pillar it falls into

#### Step 2: Pillar Feature Encoding
For each pillar, we need to extract meaningful features from all the points inside it:
- The average location of points in the pillar
- How spread out the points are
- The shape formed by the points
- How the poins relate to the pillar's center
This step converts irregular, variable-length point sets into fixed-size feature vectors that a neural network can process.

#### Step 3: Bird’s Eye View Representation
The pillar features are “scattered” back to their original 2D grid positions, creating a Bird’s Eye View (BEV) representation.

Imagine looking down at the track from a drone above the car. This BEV image represents:
- Where pillars contain points (occupied space)
- What features those points have (learned by the network)
- The spatial relationship between different areas

Why this is clever: By converting 3D point clouds into a 2D BEV image, we can now use standard 2D CNNs


#### Step 4: 2D Backbone Network
Now we have a 2D image, we can process it with CNNs:

What happens:
- Multiple layers of convolutions extract increasingly abstract features
- Early layers might detect edges and basic shapes
- Deeper layers combine information to understand “this pattern looks like a cone”
- Multiple resolution levels are processed and combined


## Series Perception
1. [Introduction to point cloud](../pointcloud)
2. [Introduction to PointPillars](../pointpillars)
