# 3D Scene Reconstruction Pipeline Documentation

This document provides an overview of the 3D scene reconstruction pipeline, explaining the project structure, the purpose of each file and function, and the steps taken to build and debug the pipeline.

## Project Overview

The goal of this project is to create a pipeline that takes a monocular video (from a single camera) and generates a lightweight, primitive-based 3D reconstruction of the scene. This is useful for applications like robotic navigation, where a full, photorealistic 3D model is not necessary, and computational efficiency is important.

The pipeline performs the following steps for each frame of the video:
1.  **Depth Estimation:** Estimates the depth of each pixel in the image.
2.  **Object Detection:** Identifies objects in the scene using a pre-trained model.
3.  **Point Cloud Generation:** Converts the 2D image and its depth map into a 3D point cloud.
4.  **Bounding Box Fitting:** Fits 3D bounding boxes around the detected objects.
5.  **Scene Rendering:** Creates a 3D visualization of the point cloud and bounding boxes.

## Project Structure

The project is organized into the following directories:

-   `data/`: Contains input and intermediate data.
    -   `input_videos/`:  Input video files are placed here.
    -   `frames/`:  Frames extracted from the video are saved here.
-   `results/`: Stores the output of the pipeline.
    -   `depth/`:  Per-frame depth maps are saved here as `.npy` and `.png` files.
    -   `detections/`: Per-frame object detections are saved as `.json` files.
    -   `exports/`:  Final 3D outputs, such as point clouds (`.ply`), bounding boxes (`.json`), and rendered images (`.png`) are saved here.
-   `src/`: Contains the source code for the different modules of the pipeline.
-   `scripts/`: Contains the main script for running the pipeline.
-   `notebooks/`: For Jupyter notebooks, for demos or experiments.

## Source Code (`src/`)

Each file in the `src` directory corresponds to a specific step in the pipeline.

### `utils.py`

This file contains common helper functions used across the project.

-   `read_json(file_path)`: Reads a JSON file and returns its contents.
-   `ensure_dir(dir_path)`: Creates a directory if it doesn't already exist.

### `frame_extract.py`

-   `extract_frames(video_path, output_dir)`: Takes a path to a video file and extracts each frame, saving it as a PNG image in the specified output directory. It uses OpenCV to read the video.

### `depth_midas.py`

-   `run_midas(image_path, output_dir)`:  This function uses the MiDaS model (a state-of-the-art monocular depth estimation model) to predict the depth for a single input image. It downloads the pre-trained model from PyTorch Hub, runs the inference, and saves the resulting depth map as both a NumPy array (`.npy`) for further processing and a visual PNG image for inspection.

### `yolo_detect.py`

-   `run_yolo(image_path, output_dir)`: This function performs object detection on an input image using the YOLOv8 model. It loads a pre-trained YOLO model, runs it on the image, and saves the detected objects (including their labels, confidence scores, and 2D bounding boxes) to a JSON file.

### `depth_to_3d.py`

-   `depth_to_point_cloud(depth_map_path, color_image_path, output_dir, intrinsic_params)`: This function converts a depth map and its corresponding color image into a 3D point cloud. It uses the Open3D library to create a point cloud from an RGBD image. The function requires camera intrinsic parameters (focal length, principal point) to correctly project the 2D pixels into 3D space. The resulting point cloud is saved as a `.ply` file.

### `fit_boxes.py`

-   `fit_boxes_to_detections(pcd_path, detections_path, output_dir)`: This function takes a point cloud and a set of 2D object detections and fits 3D bounding boxes around the objects. The current implementation is a simplified placeholder that creates an axis-aligned bounding box based on the 2D detection's coordinates, with an arbitrary depth.

### `renderer.py`

-   `render_scene(pcd_path, bbox_path, output_dir)`: This function creates a 3D visualization of the reconstructed scene. It loads the point cloud and the 3D bounding boxes and uses Open3D's visualization tools to render a 2D image of the 3D scene, which is then saved as a PNG file.

### `profiler.py`

-   `Profiler`: A simple class for measuring the execution time of different parts of the pipeline.
    -   `start()`: Starts the timer.
    -   `record(step_name)`: Records the time elapsed since the last call to `start()` or `record()`.
    -   `report()`: Prints a summary of the recorded execution times.

## Pipeline Script (`scripts/run_pipeline.py`)

This is the main entry point for running the entire 3D reconstruction pipeline. It orchestrates the execution of the different modules in the correct order.

-   It uses `argparse` to accept the path to the input video as a command-line argument.
-   It initializes the `Profiler` to measure performance.
-   It calls the functions from the `src` directory in sequence for each frame:
    1.  `extract_frames()`
    2.  `run_midas()`
    3.  `run_yolo()`
    4.  `depth_to_point_cloud()`
    5.  `fit_boxes_to_detections()`
    6.  `render_scene()`
-   Finally, it prints the profiler's report, showing the time taken for each step.

## How the Pipeline Was Built and Debugged

The pipeline was built incrementally, one module at a time. This approach allowed for easier debugging and verification at each step.

1.  **Project Scaffolding**: Initially, the project structure was created with empty files and directories as specified.
2.  **Argument Parsing**: The `run_pipeline.py` script was populated with basic argument parsing to handle the video input.
3.  **Frame Extraction**: The `frame_extract.py` module was implemented. A key bug was that the initial test video file was empty, causing an OpenCV error. This was resolved by creating a dummy image to allow the rest of the pipeline to be tested.
4.  **Depth Estimation**: The `depth_midas.py` module was added. This required adding `torch` and `timm` to `requirements.txt`. The initial run failed because the dummy frame was an empty file, which OpenCV could not read. This was fixed by creating a valid, black image using NumPy and OpenCV.
5.  **Object Detection**: The `yolo_detect.py` module was implemented, adding `ultralytics` to the dependencies. This step worked smoothly.
6.  **Point Cloud Generation**: The `depth_to_3d.py` module was created, adding `open3d` to the dependencies. A file naming bug was identified and fixed here to ensure the output `.ply` file had the correct name.
7.  **Bounding Box Fitting**: The `fit_boxes.py` module was added. The logic was kept simple as a placeholder for a more advanced implementation.
8.  **Rendering**: The `renderer.py` module was implemented to provide a visual output of the 3D scene.
9.  **Profiling**: The `profiler.py` module was created and integrated into the main pipeline to measure the performance of each step.
10. **Refactoring**: Finally, the code was refactored to use utility functions from `utils.py` for creating directories. This led to an `ImportError` due to incorrect relative imports, which was resolved by using absolute imports from the `src` directory.
