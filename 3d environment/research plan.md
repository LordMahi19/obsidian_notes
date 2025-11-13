## Detailed Research Plan

### Chapter 1: Introduction
*   **1.1. Motivation:** The "Sim-to-Real" gap in robotics. Robots trained in clean, 3D simulated worlds require a method to parse the complex real world into a similarly structured, low-polygon representation to effectively leverage their training.
*   **1.2. Problem Statement:** The challenge of creating a geometrically accurate yet lightweight 3D map of an unknown environment in real-time from a single video stream. This project tackles the problem by representing the world as a collection of simple geometric primitives.
*   **1.3. Research Questions:**
    *   How can monocular depth estimation, 2D object detection, and planar surface detection be combined to generate a consistent, primitive-based 3D scene?
    *   What are the computational costs (latency, memory, CPU/GPU utilization) of such a primitive-based pipeline?
    *   How does the quality and performance of a lightweight primitive-based reconstruction compare to a state-of-the-art, high-fidelity reconstruction method like Instant-NGP?
    *   How can the "usefulness" of the generated low-detail map be evaluated for a robotic navigation task?
*   **1.4. Thesis Outline:** Briefly describe the structure of the thesis, chapter by chapter.

### Chapter 2: Literature Review
*   **2.1. Camera Pose Estimation:** A review of monocular SLAM / Visual Odometry for robust pose tracking (e.g., ORB-SLAM3), which is essential for fusing information over time.
*   **2.2. Monocular Depth Estimation:** An overview of deep learning models for estimating depth from a single image, with a focus on robust architectures like MiDaS and DPT.
*   **2.3. Semantic 3D Reconstruction:**
    *   **Planar Reconstruction:** A review of methods for detecting and reconstructing large planar surfaces from images, such as PlaneRCNN.
    *   **3D Object Detection:** An overview of techniques for estimating 3D oriented bounding boxes (cuboids) for objects from a single image, with references to seminal works like Deep3DBox and CubeSLAM.
*   **2.4. High-Fidelity Scene Representation (Baselines):** A brief survey of Neural Radiance Fields (NeRFs) and their variants, specifically focusing on fast implementations like Instant-NGP, which will serve as a high-quality baseline for comparison.
*   **2.5. Key Foundational Papers:**
    *   **Pose Estimation:** Mur-Artal, R., & Tardós, J. D. (2017). "ORB-SLAM2: an Open-Source SLAM System for Monocular, Stereo and RGB-D Cameras".
    *   **Depth Estimation:** Ranftl, R., et al. (2021). "Vision Transformers for Dense Prediction".
    *   **Plane Detection:** Liu, C., et al. (2019). "PlaneRCNN: 3D Plane Detection and Reconstruction From a Single Image".
    *   **3D Object Detection:** Mousavian, A., et al. (2017). "3D Bounding Box Estimation Using Deep Learning and Geometry".
    *   **Primitive-based SLAM:** Yang, S., & Scherer, S. (2019). "CubeSLAM: Monocular 3D Object SLAM".
    *   **High-Fidelity Baseline:** Müller, T., et al. (2022). "Instant Neural Graphics Primitives with a Multiresolution Hash Encoding".

### Chapter 3: Methodology and System Design
*   **3.1. System Architecture:** Present a diagram of the proposed pipeline:
    1.  Input video frame is processed by a SLAM/VO system to get the camera pose.
    2.  The same frame is fed into three parallel modules:
        *   A Monocular Depth Estimator (e.g., MiDaS).
        *   A Plane Detector (e.g., PlaneRCNN).
        *   A 2D Object Detector (e.g., YOLO) followed by a 3D Cuboid Proposal module.
    3.  The outputs (pose, depth map, plane equations, 3D cuboids) are sent to a "Multi-View Fusion" component.
    4.  The fusion component optimizes and merges these primitives into a single, consistent 3D scene graph.
    5.  A lightweight renderer visualizes the final primitive-based scene.
*   **3.2. Implementation Details:**
    *   **Pose Estimation:** Utilize an off-the-shelf SLAM system like ORB-SLAM3 for robust camera tracking.
    *   **Primitive Extraction:** Implement scripts to run pre-trained MiDaS, PlaneRCNN, and YOLO models on each frame. For 3D cuboid generation, implement a method based on the principles from CubeSLAM (e.g., generating proposals from 2D boxes and vanishing points).
    *   **Data Fusion:** Develop algorithms to transform all per-frame primitives into a global coordinate frame using the camera poses. Implement a strategy for merging co-planar surfaces and associating object detections across multiple views.
    *   **Visualization:** Use a lightweight library like Open3D or PyOpenGL to render the final set of planes and cuboids.

### Chapter 4: Experimental Setup and Evaluation
*   **4.1. Dataset and Ground Truth:** Describe the data collection process (e.g., recording a video of a room). If possible, detail a method for obtaining ground truth geometry, even if coarse (e.g., manual measurements of the room and furniture).
*   **4.2. Performance Metrics:** Define the metrics for evaluation:
    *   **Resource Usage:** Per-frame latency (ms), average FPS, CPU/GPU utilization (%), and RAM/VRAM usage (MB).
    *   **Reconstruction Quality:** Plane normal and offset errors; object cuboid position, orientation, and scale errors compared to ground truth.
    *   **Navigational Utility:** Define a simple planning task (e.g., A* on a top-down projection) and measure success rate and path sub-optimality.
*   **4.3. Baseline Comparison:** Detail the procedure for running the baseline, Instant-NGP, on the same dataset. The comparison will focus on the trade-off between the high geometric detail of the NeRF and its higher computational cost versus the lower detail and higher efficiency of the proposed primitive-based method.

### Chapter 5: Results and Discussion
*   **5.1. System Performance:** Present the quantitative results for the proposed system and the Instant-NGP baseline across all defined metrics. Use tables and plots to illustrate the trade-offs.
*   **5.2. Qualitative Analysis:** Show side-by-side visualizations of the input video, the generated primitive-based 3D scene, and the high-fidelity baseline reconstruction.
*   **5.3. Limitations and Failure Modes:** Discuss the primary sources of error, such as scale ambiguity in monocular reconstruction, inaccuracies in primitive fitting, and challenges in data association during fusion.

### Chapter 6: Conclusion and Future Work
*   **6.1. Conclusion:** Summarize the findings regarding the feasibility and performance of lightweight, primitive-based 3D reconstruction for robotic applications.
*   **6.2. Future Work:** Propose avenues for improvement, such as incorporating cheap stereo cameras, using learned data fusion techniques, or integrating the primitive representation directly into a robot's planning and control loop.
