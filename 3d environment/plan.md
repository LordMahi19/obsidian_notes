# Bachelor Thesis Action Plan: Real-time 2.5D Mapping System

This document outlines the practical coding steps for building the real-time perception system, as detailed in the thesis proposal.

## Phase 1: Visual Odometry (Tracking Camera Motion)

The goal of this phase is to create a Python class that can estimate the camera's trajectory from a live video feed.

### 1.1. Environment Setup
*   **Objective:** Prepare your Python environment.
*   **Action:** Install necessary libraries: `pip install opencv-python numpy`.

### 1.2. Visual Odometry Implementation
*   **Objective:** Write a `VisualOdometry` class.
*   **Action:**
    1.  **Initialization:** The constructor (`__init__`) will take camera intrinsic parameters and initialize internal state variables (e.g., current pose, reference keypoints).
    2.  **Processing Frames:** A main method (`process_frame`) will take a new image as input and perform these steps:
        *   Track previously detected keypoints into the new frame using `cv2.calcOpticalFlowPyrLK` (this is the KLT tracker).
        *   Estimate the Essential Matrix from the tracked points using `cv2.findEssentialMat`.
        *   Recover the relative rotation and translation using `cv2.recoverPose`.
        *   Update the absolute camera pose by accumulating the rotation and translation.
        *   Decide if the current frame should become a new keyframe for tracking.
    3.  **Visualization:** Draw the camera's trajectory on the output video frames.

## Phase 2: Object Detection (Identifying Objects)

The goal of this phase is to create a Python class that finds objects in a video feed.

### 2.1. Environment Setup
*   **Objective:** Add deep learning libraries to your environment.
*   **Action:** Install PyTorch and a YOLO implementation: `pip install torch torchvision ultralytics`.

### 2.2. Object Detector Implementation
*   **Objective:** Write an `ObjectDetector` class.
*   **Action:**
    1.  **Initialization:** The constructor will load a pre-trained YOLO model (e.g., `yolo = torch.hub.load('ultralytics/yolov5', 'yolov5s')`).
    2.  **Processing Frames:** A method (`detect_objects`) will take an image, run the YOLO model on it, and return a list of bounding boxes for the detected objects.
    3.  **Visualization:** Draw the bounding boxes and class labels on the output video frames.

## Phase 3: Fusion and 2.5D Map Visualization

The goal is to combine the two components into a single application that generates the final map.

### 3.1. Map Environment Setup
*   **Objective:** Add a simple graphics library for the map.
*   **Action:** Install Pygame: `pip install pygame`.

### 3.2. Main Application
*   **Objective:** Write the main script that runs the system.
*   **Action:**
    1.  **Initialization:**
        *   Create instances of your `VisualOdometry` and `ObjectDetector` classes.
        *   Initialize a Pygame window for the 2.5D map.
    2.  **Main Loop:** Loop over each frame of the input video.
        *   Call `vo.process_frame()` to get the updated camera pose.
        *   Call `detector.detect_objects()` to get the bounding boxes.
    3.  **Map Fusion and Drawing:**
        *   Clear the Pygame window.
        *   Draw the camera's trajectory on the Pygame grid based on the poses from the VO.
        *   For each detected object, use a simple heuristic (e.g., based on the bounding box's `y` position and size) to estimate its position in the 2D map and draw a shape (e.g., a circle or square) at that location.
    4.  **Display:** Show the main video feed (with annotations) and the Pygame map window side-by-side.
