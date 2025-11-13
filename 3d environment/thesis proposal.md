Perfect — let’s start by drafting a **formal thesis proposal** for your bachelor thesis project. Based on our past discussions, your topic is:

> **“2.5D Reconstruction of Indoor Environments from Monocular Videos”**

This version below follows the **formal academic structure** expected for a Bachelor’s thesis proposal — suitable for submission to your supervisor or department.

---

# **Bachelor’s Thesis Proposal**

## **Title**

**2.5D Reconstruction of Indoor Environments from Monocular Videos**

## **Student**

**MD Mahi Al Jubair Talukder (lordmahi)**  
Bachelor’s Degree Programme in Smart Systems / Software Engineering

## **Supervisor**

_(To be added once confirmed)_

---

## **1. Introduction**

Three-dimensional reconstruction of real-world environments plays a crucial role in robotics, virtual reality (VR), augmented reality (AR), and digital twin systems. However, full 3D reconstruction using LiDAR or multi-view cameras can be costly and computationally heavy. An alternative is **2.5D reconstruction**, which captures surface geometry (depth maps) and approximate object layouts from a **single RGB video**.

This project aims to develop a **lightweight and fast proof-of-concept pipeline** for **reconstructing simplified 3D geometry of an indoor scene** (such as a meeting room) using only a monocular video input. The output will be a low-detail but spatially meaningful 3D model — a “2.5D” representation — suitable for applications such as environment understanding, scene visualization, or digital twin prototyping.

---

## **2. Background and Motivation**

Traditional 3D reconstruction methods (e.g., multi-view stereo or SLAM) require multiple synchronized views or specialized sensors, making them impractical for quick scanning or low-budget setups. With advances in **deep learning-based monocular depth estimation** (e.g., MiDaS) and **object detection models** (e.g., YOLO), it is now possible to infer scene geometry and structure from regular video footage.

The motivation behind this work is to:

- Explore **lightweight scene understanding** methods combining computer vision and geometry.
    
- Develop a **pipeline suitable for creating digital twins** with minimal hardware.
    
- Build foundational skills for future research in **AI-driven 3D perception and robotics**, especially for tasks like robot navigation in simulated environments.
    

---

## **3. Research Objectives**

The primary goal is to **develop and evaluate a proof-of-concept 2.5D reconstruction system** from monocular videos.

### **Specific Objectives:**

1. Implement a pipeline that:
    
    - Extracts depth information using **MiDaS** (monocular depth estimation).
        
    - Detects objects using **YOLOv8**.
        
    - Reconstructs a minimal 3D scene with **axis-aligned boxes** approximating detected objects using estimated depths.
        
2. Produce a **lightweight 3D visualization** (e.g., using Open3D or Blender visualization).
    
3. Evaluate the reconstruction qualitatively and quantitatively (e.g., comparing relative geometry or depth consistency).
    

---

## **4. Research Questions**

1. How effectively can depth maps and object detections from a single RGB video approximate the 3D layout of an indoor scene?
    
2. What are the main limitations of using monocular depth estimation for lightweight 3D reconstruction?
    
3. Can such a system generate geometrically consistent low-detail 3D environments suitable for digital twin applications?
    

---

## **5. Methodology**

### **5.1 Dataset**

- Short indoor video sequences recorded with a handheld or stationary RGB camera (e.g., a smartphone).
    
- Alternatively, use open datasets such as NYUv2 or ScanNet for benchmarking.
    

### **5.2 System Pipeline**

1. **Frame Extraction:**  
    Extract key frames from video.
    
2. **Depth Estimation (MiDaS):**  
    Generate per-frame depth maps.
    
3. **Object Detection (YOLOv8):**  
    Detect and classify key objects (e.g., table, chair, wall, monitor).
    
4. **3D Point Projection:**  
    Use depth + camera intrinsics to project pixels into 3D space.
    
5. **Box Fitting:**  
    Fit simple **axis-aligned bounding boxes** under each detection using median depth and mask area.
    
6. **Visualization:**  
    Combine object boxes and point cloud into a scene using Open3D or Blender.
    

### **5.3 Evaluation**

- **Qualitative:** Visual comparison between reconstructed and real-world scenes.
    
- **Quantitative:** Relative depth error and layout accuracy (if ground truth available).
    

---

## **6. Expected Results**

The expected output is a **simplified 3D model** of an indoor environment, reconstructed from monocular video.  
The model will not capture fine geometry but should preserve:

- Approximate object positions.
    
- Relative depth and scale relationships.
    
- Visual coherence for virtual scene approximation.
    

This would serve as an efficient basis for **digital twin prototypes**, **robotic simulation environments**, or **VR/AR pre-visualizations**.

---

## **7. Tools and Technologies**

- **Python 3**
    
- **PyTorch** (for MiDaS, YOLOv8)
    
- **OpenCV** (for frame extraction and preprocessing)
    
- **Open3D / Blender Python API** (for visualization)
    
- **Ubuntu (WSL)** for development environment
    

---

## **8. Timeline**

|**Task**|**Duration**|**Period**|
|---|---|---|
|Literature Review & Data Collection|2 weeks|Nov 2025|
|Pipeline Implementation|4 weeks|Dec 2025 – Jan 2026|
|Testing & Evaluation|3 weeks|Feb 2026|
|Thesis Writing|4 weeks|Mar – Apr 2026|
|Final Submission|1 week|Apr 2026|

---

## **9. References**

(Initial list)

1. Ranftl, R., Bochkovskiy, A., Koltun, V. (2022). _MiDaS: Monocular Depth Estimation Using Multi-Scale Vision Transformers._
    
2. Bochkovskiy, A., Wang, C.-Y., Liao, H.-Y. (2020). _YOLOv4: Optimal Speed and Accuracy of Object Detection._
    
3. Fischler, M. A., & Bolles, R. C. (1981). _Random Sample Consensus: A Paradigm for Model Fitting._
    
4. Mur-Artal, R., Montiel, J. M., & Tardós, J. D. (2015). _ORB-SLAM: A Versatile and Accurate Monocular SLAM System._
    

---

## **10. Expected Contribution**

This project contributes a minimal and accessible method for **lightweight 2.5D reconstruction**, combining computer vision and deep learning. The result will demonstrate how existing AI models can quickly generate **approximate spatial representations** of real-world environments, opening pathways to digital twin integration and autonomous agent training.

---

Would you like me to make this more **academic (for submission)** — e.g., with formal referencing, abstract, and research justification — or keep it **compact (for supervisor approval and internal documentation)**?

Once you decide, we’ll move to **Part 2: Implementation & Experimentation Plan**, where I’ll write the actual MiDaS + YOLO + 3D projection prototype roadmap and Python skeleton.