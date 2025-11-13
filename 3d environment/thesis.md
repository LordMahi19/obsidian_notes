# Bachelor Thesis Proposal: Lightweight, Primitive-based 3D Scene Reconstruction from Monocular Video for Robotic Navigation

## Abstract

A critical capability for autonomous robots, particularly those trained in simulation, is the ability to perceive their environment and create a simplified, geometrically-aware internal model in real-time. This thesis proposes the design, implementation, and evaluation of a system that generates a lightweight, primitive-based 3D reconstruction of its surroundings using only a single camera (monocular vision). The system will not aim for photorealistic detail, but for a computationally efficient scene representation composed of simple geometric primitives, such as planes for walls and floors, and cuboids for objects like beds and chairs. This will be achieved by integrating several modern computer vision techniques, including monocular depth estimation, plane detection, and 3D object detection. The primary research contribution will be the analysis of the trade-offs between reconstruction quality, computational resource usage (latency, CPU/GPU, memory), and navigational utility of this low-detail approach compared to a high-fidelity, dense reconstruction baseline (e.g., Instant-NGP).


## 🧠 Refined Thesis Idea (in my own words)

> Build a pipeline that takes **a live or recorded monocular camera feed** and reconstructs a **lightweight, low-detail 3D representation** of the environment using **simple geometric primitives** (planes, cuboids, etc.).
> 
> The 3D reconstruction doesn’t aim for photorealism, but for **functional geometry** — enough detail for an autonomous agent or robot to **understand its surroundings** for path planning or navigation.
> 
> The research focus is on **analyzing the tradeoff** between **level of detail** and **system performance metrics** — compute time, memory, latency, and navigation usefulness.

---

## 🎯 Research Goal

To quantify **how much 3D detail is “enough”** for a robot to navigate effectively in a reconstructed environment, and how decreasing visual/geometry detail affects:

- Reconstruction latency (ms/frame)
    
- Memory & compute cost (RAM/VRAM usage)
    
- Navigation performance (collision-free path success, planning accuracy)
    

---

## 🧩 Why This Is a Good Thesis

✅ **Novel yet feasible** — You’re exploring a simplified, measurable version of real-world systems like Tesla’s FSD or Apple’s RoomPlan, but with open methods (MiDaS, PlaneRCNN, CubeSLAM).  
✅ **Quantitative research** — You’ll gather real performance data (fps, memory, latency, accuracy).  
✅ **Integration-focused** — Combines multiple CV & geometry modules (depth → primitives → fusion → navigation).  
✅ **Aligns with robotics, CV, and 3D vision** — all key areas for higher research or ML/AI lab work.

---

## 🧱 How to Frame It as a Thesis Proposal

### Title (draft ideas)

- “Primitive-Based 3D Scene Reconstruction from Monocular Video for Efficient Robotic Navigation”
    
- “Evaluating Geometry Simplification in Real-Time 3D Scene Reconstruction”
    
- “Low-Detail 3D Environment Modeling from Video Feed for Lightweight Navigation Systems”
    

### Problem Statement

Dense 3D reconstruction methods (e.g., NeRF, instant-ngp) produce highly detailed models but are computationally expensive and unsuitable for real-time robotic navigation on resource-limited hardware.  
This work investigates whether **simplified, primitive-based 3D reconstructions** can provide sufficient environmental understanding for navigation, while dramatically reducing computational cost.

### Objectives

1. Develop a pipeline to generate **low-detail 3D reconstructions** from a monocular camera feed.
    
2. Represent objects and surfaces with **simple geometric primitives** (planes, cuboids).
    
3. **Quantify** the impact of detail reduction on:
    
    - Reconstruction accuracy
        
    - Computational cost (time, memory)
        
    - Navigation performance
        
4. Compare the approach with **high-detail baselines** (instant-ngp, NeRF).
    

### Research Questions

1. How much geometric simplification can a 3D reconstruction undergo before it becomes unusable for navigation?
    
2. What is the relationship between level of detail and system latency/memory usage?
    
3. How do primitive-based reconstructions compare to dense methods like instant-ngp in accuracy vs efficiency?
    

### Hypothesis

> A primitive-based reconstruction pipeline can provide sufficient geometric understanding for navigation while requiring significantly less computational resources compared to dense 3D methods.

---

## 🧪 Methodology Summary (what you’ll actually do)

| Step | Task | Tools / Libraries |
|---|---|---|
| 1 | Capture video feed | Any webcam or phone camera |
| 2 | Estimate depth | MiDaS (monocular depth) |
| 3 | Detect planes | PlaneRCNN |
| 4 | Detect objects | YOLOv8 |
| 5 | Fit cuboids / primitives | CubeSLAM / custom fitting |
| 6 | Fuse multi-view data | Using VO/SLAM poses (ORB-SLAM3) |
| 7 | Render low-detail 3D scene | Open3D / glTF |
| 8 | Measure performance | Python timing, psutil, pynvml |
| 9 | Run navigation test | Simple path planner (A* or RRT) |
| 10 | Compare with dense method | instant-ngp baseline |

---

## 📊 Evaluation Metrics

| Category | Metric | Description |
|---|---|---|
| Reconstruction | Plane error (angle, offset), cuboid size error | Compare primitive scene vs GT or LiDAR |
| Performance | FPS, latency (ms/frame), CPU/GPU/RAM usage | Efficiency comparison |
| Navigation | Success rate, path length ratio, collision rate | Usability of reconstruction for movement |
| Tradeoff | Detail level vs performance | Key thesis insight |

---

## 📅 Suggested Timeline (Bachelor Thesis Scale)

|Phase|Duration|Deliverable|
|---|---|---|
|Literature Review|2 weeks|Related work (NeRF, PlaneRCNN, CubeSLAM, primitive modeling)|
|Prototype 1|2 weeks|MiDaS + PlaneRCNN per-frame depth/planes|
|Prototype 2|2 weeks|YOLO + Cuboid fitting + fusion|
|Data Collection|2 weeks|Scene tests, runtime data logs|
|Evaluation & Comparison|2 weeks|Metrics + instant-ngp baseline|
|Thesis Writing|2–3 weeks|Final document + demo video|

---

## 💡 Experimental Detail-Level Variation Plan

To test your main idea (“how low can you go”), you can run your system at **multiple simplification levels**:

|Level|What You Keep|Expected Result|
|---|---|---|
|L0|Full depth map (dense mesh)|Baseline, accurate but slow|
|L1|Planes only (walls/floor)|Faster, usable for navigation|
|L2|Planes + large cuboids|Moderate accuracy, good tradeoff|
|L3|Only bounding boxes (no planes)|Very lightweight, possibly too coarse|

You’ll measure at which level navigation starts to fail.

---

## 🧾 Your Expected Deliverables

- **Thesis report** (with literature, pipeline design, experiments, evaluation)
    
- **Working prototype** (Python scripts for depth, plane, cuboid, fusion, renderer)
    
- **Demo video** (live video feed → low-poly 3D render)
    
- **Graphs/tables** comparing:
    
    - Detail vs. latency
        
    - Memory vs. accuracy
        
    - Navigation success vs. simplification level
        

---

## 🚀 Next Step

If you’d like, I can:

1. **Write your formal thesis proposal (1–2 pages)** suitable to submit to your supervisor or school’s approval system — including background, motivation, objectives, methodology, and expected outcome.
    
2. Or **generate a ready-to-run repo skeleton** with modular folders like:

    ```
    ├── src/
    │   ├── depth_midas.py
    │   ├── plane_rcnn.py
    │   ├── yolo_cuboids.py
    │   ├── fusion.py
    │   ├── renderer.py
    │   └── profiler.py
    └── data/
    └── results/
    ```
