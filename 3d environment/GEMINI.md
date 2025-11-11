# Gemini Project Context: Real-time 2.5D Mapping for Robotics

## Directory Overview

This directory serves as the planning and documentation hub for a bachelor thesis focused on **real-time robotic perception**. The project's goal is to build a prototype system that uses a single camera to create a simplified, live "2.5D" map of its environment. This map is not a photorealistic 3D model, but a geometric representation of the robot's path and the location of key objects, suitable for real-time navigation. The system will be built by combining two core computer vision techniques: **Visual Odometry** (to track motion) and **Object Detection** (to identify objects).

## Key Files

*   `thesis.md`: The formal thesis proposal, which details the plan to build the real-time 2.5D mapping system.
*   `research_ideas.md`: A document that captures the evolution of the project idea to its final, clarified goal.
*   `plan.md`: A step-by-step action plan for the software implementation of the system in Python.

## Implementation Progress

The implementation of the prototype has begun, following the plan outlined in `plan.md`.

*   **Visual Odometry (VO):** The first module, responsible for tracking camera motion, is in development.
    *   **Technology:** Implemented in Python using the OpenCV library.
    *   **Functionality:** It detects and matches features between consecutive video frames to estimate the camera's rotation and translation.
    *   **Location:** The code is being developed in a new `2_5D_Reconstruction` directory, specifically in `src/vo.py`.
    *   **Status:** A basic implementation is complete and provides real-time trajectory visualization. The next step is to integrate object detection.

## Usage

This directory is for managing the research and documentation aspects of the thesis.

*   Refer to `thesis.md` for the formal structure and research questions.
*   Use `plan.md` as a coding and implementation guide.
