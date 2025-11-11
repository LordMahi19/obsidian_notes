# Bachelor Thesis Proposal: Real-time 2.5D Scene Representation using Visual Odometry and Object Detection for Robotic Navigation

## Abstract

A critical capability for autonomous robots is the ability to perceive their environment and create a simplified internal model, or "digital twin," for real-time navigation. This thesis proposes the design and implementation of a prototype system that generates a "2.5D" map of its surroundings using only a single camera (monocular vision). The system will not aim for photorealistic reconstruction, but for a functionally simple map that represents the robot's position and the locations of key environmental objects. This will be achieved by integrating two core computer vision techniques: a classical, feature-based **Visual Odometry (VO)** pipeline to track the camera's movement, and a modern, deep-learning-based **Object Detection** model (YOLO) to identify objects. The outputs of these two components will be fused to generate a live, top-down 2D map, demonstrating a feasible, lightweight approach to the problem of real-time perception and path planning for robotics.

---

## Detailed Research Plan

### Chapter 1: Introduction
*   **1.1. Motivation:** The "Sim-to-Real" problem in robotics: robots trained in clean, simulated 3D worlds need a way to perceive the messy real world and convert it into a similarly simple, navigable representation.
*   **1.2. Problem Statement:** The challenge of creating a simplified, geometric map of an unknown environment in real-time using only a single camera. This project tackles the problem by breaking it down into two parts: "Where am I?" (localization) and "What is around me?" (perception).
*   **1.3. Research Questions:**
    *   How can a feature-based visual odometry algorithm be implemented to robustly track a camera's trajectory from a video stream?
    *   How can a pre-trained, real-time object detector like YOLO be integrated into the system?
    *   What is an effective method for fusing the camera's path and the 2D object detections into a coherent 2.5D top-down map for navigational planning?
*   **1.4. Thesis Outline:** Briefly describe the structure of the thesis, chapter by chapter.

### Chapter 2: Literature Review
*   **2.1. Visual Odometry (VO):** A review of feature-based monocular VO. This includes feature detection and tracking (e.g., KLT tracker), and motion estimation from essential matrix decomposition between keyframes. The problem of scale drift in monocular VO will be discussed.
*   **2.2. Real-time Object Detection:** An overview of convolutional neural networks for object detection, with a focus on the architecture and performance of the YOLO (You Only Look Once) family of models.
*   **2.3. Sensor Fusion and Map Representations:** A discussion of how different sensor inputs are commonly fused in robotics. An overview of different map representations, such as occupancy grids, and their use in path planning.
*   **2.4. Semantic SLAM:** A brief survey of the state-of-the-art in Semantic SLAM, which combines classical SLAM with object recognition to build maps rich with meaning, providing context for the proposed project.
*   **2.5. Key Foundational Papers:** The following papers form the theoretical basis for the components that will be built in this thesis.
    *   **Visual Odometry:**
        *   Nistér, D. (2004). "An Efficient Solution to the Five-Point Relative Pose Problem". *IEEE Transactions on Pattern Analysis and Machine Intelligence*. ([Link](https://ieeexplore.ieee.org/document/1288525))
        *   Shi, J., & Tomasi, C. (1994). "Good Features to Track". *1994 Proceedings of IEEE Conference on Computer Vision and Pattern Recognition*. ([Link](https://www.ai.mit.edu/courses/6.891/handouts/shi94good.pdf))
        *   Baker, S., & Matthews, I. (2004). "Lucas-Kanade 20 Years On: A Unifying Framework". *International Journal of Computer Vision*. ([Link](https://www.ri.cmu.edu/pub_files/pub3/baker_simon_2002_3/baker_simon_2002_3.pdf))
    *   **Object Detection:**
        *   Redmon, J., Divvala, S., Girshick, R., & Farhadi, A. (2016). "You Only Look Once: Unified, Real-Time Object Detection". *2016 IEEE Conference on Computer Vision and Pattern Recognition (CVPR)*. ([Link](https://arxiv.org/abs/1506.02640))
    *   **Semantic SLAM Context:**
        *   Chen, K., Xiao, J., et al. (2022). "Semantic Visual Simultaneous Localization and Mapping: A Survey". *IEEE Transactions on Intelligent Transportation Systems*. ([Link](https://arxiv.org/abs/2209.06428))

### Chapter 3: Methodology and System Design
*   **3.1. System Architecture:** Present a diagram illustrating the proposed system. It will show the input video stream being processed by two parallel components: the Visual Odometry pipeline and the Object Detection pipeline. Their outputs (camera pose and object bounding boxes) are then fed to a "Map Fusion" component that generates the final 2.5D map.
*   **3.2. Visual Odometry Implementation:** Detail the plan to implement a VO pipeline in Python using OpenCV. This will involve:
    *   Detecting initial features (e.g., FAST).
    *   Tracking features across frames using the Kanade-Lucas-Tomasi (KLT) algorithm.
    *   Deciding when to select a new keyframe.
    *   Estimating the camera's pose between keyframes using the 5-point RANSAC algorithm to find the Essential Matrix.
*   **3.3. Object Detection Implementation:** Detail the plan to use a pre-trained YOLO model (e.g., from Ultralytics) for efficient, real-time object detection.
*   **3.4. 2.5D Map Generation:** Describe the algorithm for creating and updating the top-down map. This will involve creating a 2D grid, drawing the camera's estimated trajectory on it, and developing a heuristic to estimate the position of detected objects on the grid based on their bounding box size and position.

### Chapter 4: The Real-time Mapping Software
*   **4.1. System Setup:** Document the development environment, including Python, OpenCV, and PyTorch.
*   **4.2. Code Implementation:** Present the core Python code for each major component: the Visual Odometry class, the Object Detector class, and the main loop that handles the data fusion and map visualization.

### Chapter 5: Results and Discussion
*   **5.1. System Output:** Showcase the final running system, displaying the input video annotated with the VO path and object bounding boxes, alongside the live-updating 2.5D map.
*   **5.2. Performance Analysis:** Evaluate the real-time performance of the system (frames per second). Discuss the computational trade-offs.
*   **5.3. Limitations:** Analyze the primary sources of error and limitations, such as the scale drift inherent in monocular VO and the inaccuracy of placing objects on the 2D map without true depth information.

### Chapter 6: Conclusion and Future Work
*   **6.1. Conclusion:** Summarize the success and challenges of building a real-time 2.5D mapping system from a single camera.
*   **6.2. Future Work:** Propose avenues for improvement, such as incorporating a simple depth estimation network, using stereo cameras to solve the scale problem, or implementing more sophisticated data fusion techniques.
