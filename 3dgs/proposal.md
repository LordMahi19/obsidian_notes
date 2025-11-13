### Proposal Draft for Professor

**Bachelor Thesis Proposal**

**Student Name:** [Your Name]  
**Degree Program:** [Your Program, e.g., Computer Science]  
**Supervisor:** [Professor's Name]  
**Proposed Title:** Real-time Minimal-Geometry 3D Reconstruction from Monocular Video using Pruned 3D Gaussian Splatting for Robot Navigation  
**Date:** November 13, 2025  

#### 1. Introduction and Motivation
Modern robotics relies on accurate 3D environmental models for tasks like navigation and obstacle avoidance. However, traditional methods such as Neural Radiance Fields (NeRF) or full 3D Gaussian Splatting (3DGS) produce photorealistic reconstructions that are computationally intensive, often requiring gigabytes of memory and minutes of processing time—impractical for real-time applications on mobile robots. Inspired by simplified 3D renders in systems like Tesla's autonomous driving visualization, this thesis aims to develop a minimal-detail 3D reconstruction pipeline that captures only essential geometry (e.g., planes for walls, cuboids for furniture) from live monocular video. The goal is to enable efficient robot navigation while quantifying performance trade-offs in compute, memory, and latency against high-fidelity baselines.

#### 2. Research Objectives
- **Primary Objective:** Design and implement a pruned 3DGS-based system for real-time, low-detail 3D scene reconstruction from monocular video, optimized for downstream navigation.
- **Secondary Objectives:**
  - Develop techniques for Gaussian pruning, clustering, and geometric regularization to minimize detail while maintaining usability.
  - Evaluate the system's navigation efficacy in simulated environments, measuring success rates and path efficiency.
  - Benchmark resource usage (GPU/CPU time, RAM, latency) against proprietary models like Instant-NGP and vanilla 3DGS.
  - Collect statistical data on detail-resource Pareto frontiers to inform future edge-deployable robotics applications.

#### 3. Related Work
Key foundations include:
- 3D Gaussian Splatting (Kerbl et al., 2023): An explicit, differentiable representation for fast radiance field rendering.
- Instant-NGP (Müller et al., 2022): A high-fidelity NeRF variant for rapid training but with high detail overhead.
- Robot navigation from reconstructions (e.g., ORB-SLAM3 for SLAM, DWA for planning).
This work extends 3DGS by introducing navigation-specific optimizations, differing from prior efforts focused on visual fidelity.

#### 4. Methodology
The pipeline processes live RGB video (480p, 30 fps) as follows:
- Use COLMAP for structure-from-motion to obtain sparse points and poses.
- Initialize and train a 3DGS model, then apply pruning (opacity thresholding), clustering (voxel-grid merging), and regularization (plane/cuboid fitting via RANSAC).
- Export to an occupancy grid for path planning (A* or DWA) in simulators like Gazebo.
- Ablate parameters (#Gaussians, voxel size, etc.) across 10 indoor scenes.
- Metrics: Reconstruction accuracy (Chamfer distance), navigation success (>95% target), resources (via NVIDIA profiling tools).

Implementation will fork open-source repositories (e.g., gaussian-splatting on GitHub) in Python/PyTorch, targeting an NVIDIA GPU for development.

#### 5. Expected Outcomes and Contributions
- A functional prototype demonstrating minimal-geometry reconstruction for navigation.
- Empirical data on optimal detail levels, potentially showing 10–50× efficiency gains.
- Open-source code and dataset for reproducibility.
- Insights applicable to low-power robotics, such as drones or service robots.

#### 6. Timeline and Resources
- **Weeks 1–2:** Literature review and environment setup.
- **Weeks 3–4:** Implement core 3DGS pruning pipeline.
- **Weeks 5–6:** Integrate navigation module and dataset collection.
- **Weeks 7–8:** Conduct experiments and ablations.
- **Weeks 9–10:** Analyze results, write thesis, and prepare defense.
Resources needed: Access to a GPU-equipped machine (e.g., lab workstation); no additional funding required.

#### 7. Risks and Mitigations
- Risk: Dataset collection delays—Mitigation: Use public indoor video datasets as fallback.
- Risk: Convergence issues in 3DGS training—Mitigation: Start with pre-trained models.
- Risk: Simulator integration bugs—Mitigation: Test incrementally with unit cases.

I believe this project aligns with [Department/Professor's Research Interests, e.g., computer vision and robotics], and I am eager for your guidance. Please let me know if you'd like to discuss or refine this proposal.

**Signature:** [Your Name]

