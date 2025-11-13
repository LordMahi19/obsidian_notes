# Bachelor Thesis Action Plan: Lightweight, Primitive-based 3D Scene Reconstruction

This document outlines the practical coding steps for building the primitive-based 3D reconstruction system, as detailed in the current `thesis.md`.

## Phase 1: Foundational Modules (Pose and Depth Estimation)

The goal of this phase is to establish the core components for tracking camera motion and understanding scene geometry.

### 1.1. Environment Setup
*   **Objective:** Prepare the Python environment for SLAM and depth estimation.
*   **Action:**
    *   Install a robust SLAM library (e.g., ORB-SLAM3 or a Python wrapper for it).
    *   Install a monocular depth estimation library: `pip install timm opencv-python torch torchvision`.
    *   Clone the MiDaS repository: `git clone https://github.com/isl-org/MiDaS.git`.

### 1.2. Pose Estimation
*   **Objective:** Generate accurate camera poses from a video feed.
*   **Action:**
    1.  Integrate and run a SLAM system on a sample indoor video.
    2.  Write a script to process the output to get a per-frame camera pose matrix (rotation and translation).
    3.  Save the poses for use in later phases.

### 1.3. Depth Estimation
*   **Objective:** Generate a depth map for each video frame.
*   **Action:**
    1.  Write a `DepthEstimator` class using the MiDaS library.
    2.  The class should take a video frame and return a dense depth map.
    3.  Test the output qualitatively to ensure reasonable depth results.

## Phase 2: Primitive Extraction (Planes and Objects)

The goal of this phase is to detect and extract geometric primitives (planes and cuboids) from each frame.

### 2.1. Environment Setup
*   **Objective:** Prepare the environment for plane and object detection.
*   **Action:**
    *   Set up the environment for PlaneRCNN by following its repository instructions.
    *   Ensure YOLOv8 is installed: `pip install ultralytics`.

### 2.2. Plane Detection
*   **Objective:** Detect large planar surfaces like walls and floors.
*   **Action:**
    1.  Write a `PlaneDetector` class that uses PlaneRCNN.
    2.  The class should take a video frame and return a set of plane equations and their corresponding masks.

### 2.3. 3D Object Detection
*   **Objective:** Detect objects and estimate their 3D bounding boxes (cuboids).
*   **Action:**
    1.  Use a `YOLOv8` model to get 2D bounding boxes for objects of interest.
    2.  Implement a `CuboidFitter` class that takes the 2D box, the depth map from Phase 1, and camera intrinsics to estimate a 3D oriented bounding box for the object. This can be based on principles from CubeSLAM.

## Phase 3: Fusion, Visualization, and Evaluation

The goal is to combine all the extracted information into a single, coherent 3D scene and visualize it.

### 3.1. Environment Setup
*   **Objective:** Add a 3D visualization library.
*   **Action:** Install Open3D: `pip install open3d`.

### 3.2. Multi-View Fusion
*   **Objective:** Create a consistent global 3D scene graph.
*   **Action:**
    1.  Develop a `Scene` class that maintains a list of all primitives (planes and cuboids).
    2.  In the main loop, for each new frame:
        *   Use the camera pose (from Phase 1) to transform the newly detected primitives (from Phase 2) into the global world coordinate frame.
        *   Implement logic to merge new primitives with existing ones (e.g., merging co-planar surfaces or updating the pose of a tracked object).

### 3.3. Visualization
*   **Objective:** Render the reconstructed 3D scene in real-time.
*   **Action:**
    1.  Use Open3D to create a visualization window.
    2.  In the main loop, clear the renderer and draw the current set of primitives from the `Scene` class.
    3.  Also, draw the camera's current position and trajectory.

### 3.4. Performance Profiling
*   **Objective:** Measure the computational cost of the pipeline.
*   **Action:**
    1.  Implement a `Profiler` class to measure latency, memory usage (CPU/GPU), and FPS.
    2.  Log these metrics during runtime for later analysis.

## Phase 4: Baseline Comparison and Navigation Task

The goal of this phase is to evaluate the system's output against a high-fidelity baseline and test its utility for navigation.

### 4.1. High-Fidelity Baseline
*   **Objective:** Generate a dense, high-quality reconstruction for comparison.
*   **Action:**
    1.  Set up and run Instant-NGP on the same video dataset.
    2.  Extract a mesh from the trained NeRF to serve as a "ground truth" for geometric comparison.
    3.  Measure the resource usage and time required for the Instant-NGP pipeline.

### 4.2. Navigation Task
*   **Objective:** Evaluate the navigational utility of the primitive-based map.
*   **Action:**
    1.  Create a 2D top-down projection of the reconstructed 3D scene.
    2.  Implement a simple pathfinding algorithm (e.g., A*) on this 2D map.
    3.  Run tests to see if the planner can successfully find collision-free paths between points in the environment.
    4.  Compare the results with paths planned on the baseline reconstruction.