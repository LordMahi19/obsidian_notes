# Bachelor Thesis Research Idea: The Journey to a Real-time Robotic Perception System

## The High-Level Vision
The starting point was a powerful, high-level concept: in order to effectively train robots, we often use detailed 3D simulators or "digital twins." A robot trained in such a world could navigate the real world more effectively if it could create its own, simplified version of a digital twin in real-time.

## The Core Problem
This reframed the thesis goal. The objective was not to create a high-fidelity, offline 3D model for viewing. Instead, the core problem is: **How can a robot with a single camera perceive the world and build a simple, geometric map in real-time for the purpose of navigation?**

## Exploring and Discarding Alternatives
*   **Path 1: High-Fidelity Reconstruction (NeRFs/Offline SfM):** Initial thoughts centered on creating detailed 3D models. However, these methods are computationally expensive and slow (offline), making them unsuitable for a robot that needs to react instantly. They also provide a level of photorealistic detail that is unnecessary for simple path planning.
*   **Path 2: Building a Basic System from Scratch (Classical SfM):** This was closer, as it focused on fundamentals. However, a classical SfM pipeline is still designed for offline use and produces a point cloud, not the simplified, object-oriented map needed for the "digital twin" navigation concept.

## The Final Decision: A Real-time, Semantic, 2.5D Map
The final, clarified project combines the most important constraints: **real-time performance** and **semantic understanding** (knowing what an object is).

**Project Title:** "Real-time 2.5D Scene Representation using Visual Odometry and Object Detection for Robotic Navigation"

**Rationale:** This project directly tackles the core problem by building a prototype that does two things simultaneously:
1.  **Tracks its own motion** using a lightweight **Visual Odometry** algorithm.
2.  **Identifies important objects** using a pre-trained, real-time **Object Detector** (like YOLO).

By fusing the robot's path with the locations of detected objects into a simple top-down 2D map (a "2.5D" representation), this project represents the most direct and feasible path to achieving the user's original vision in the scope of a bachelor thesis.
