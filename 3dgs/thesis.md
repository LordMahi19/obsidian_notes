### Abstract
In the realm of robotics, efficient environmental perception is crucial for real-time navigation, yet high-fidelity 3D reconstructions often demand excessive computational resources unsuitable for resource-constrained devices. This thesis introduces a lightweight approach to 3D scene reconstruction from monocular video feeds using pruned 3D Gaussian Splatting (3DGS), focusing on minimal geometric detail to enable collision-free path planning. By initializing Gaussians from sparse point clouds and applying aggressive pruning, clustering, and geometric regularization, we reduce the representation to 500–5,000 primitives while preserving essential navigation cues. Experiments on indoor datasets demonstrate that our method achieves over 95% navigation success rates in simulated environments, with 10–50× reductions in memory (20–80 MB) and latency (<2 seconds) compared to baselines like vanilla 3DGS and Instant-NGP. This work contributes a Pareto-optimal framework for detail-resource trade-offs, an open-source toolkit, and insights into minimal viable geometry for robot autonomy.

## 1. Refined Thesis Title (one-sentence hook)

**“Real-time Minimal-Geometry 3D Reconstruction from Monocular Video using Pruned 3D Gaussian Splatting for Robot Navigation”**

---

## 2. Core Research Question

> **How few Gaussians (and how coarse their parameters) are sufficient to produce a collision-free navigation map for a simulated robot, and what is the compute/latency/RAM cost compared to high-fidelity baselines (Instant-NGP, vanilla 3DGS)?**

---

## 3. Why 3DGS is the Perfect Fit

| Feature | Why it helps you |
|---------|------------------|
| **Explicit primitive list** (position, covariance, opacity, color) | Easy to prune/agglomerate → direct control of “detail budget”. |
| **Differentiable rasterizer** | Trainable end-to-end with navigation loss. |
| **O(1) memory per Gaussian** | Linear scaling → perfect for ablation on #Gaussians. |
| **Fast inference (≈100 fps @ 480p with CUDA)** | Real-time feasible on edge GPU (Jetson). |

---

## 4. Minimal-Detail Pipeline (Monocular → Navigation Mesh)

```
Live RGB video (480p, 30 fps)
      ↓
COLMAP SfM → sparse point cloud + camera poses
      ↓
Initialize N Gaussians (N = 5k … 500k) from points
      ↓
Train 3DGS (5–10 k iterations, < 2 min on RTX 3060)
      ↓
Pruning / Clustering stage
      │
      ├─→ Threshold-based pruning (opacity < τ)
      ├─→ Voxel-grid clustering → merge nearby Gaussians
      └─→ Shape approximation (fit planes / boxes via RANSAC)
      ↓
Export → “Low-Poly” Gaussian Soup (≈ 100–2 000 primitives)
      ↓
Rasterize → Occupancy Grid (voxel / SDF) @ 5 cm resolution
      ↓
A* / DWA path planner in simulation (Gazebo / Isaac Sim)
      ↓
Metrics → Success rate, path length, collision count
```

---

## 5. Detail-Control Knobs (your independent variables)

| Knob | Range | Effect |
|------|-------|--------|
| **# Gaussians** | 500, 1k, 5k, 10k, 50k, 100k | Direct memory & speed |
| **Opacity threshold τ** | 0.01 … 0.2 | Removes faint clutter |
| **Covariance scale λ** | 0.5 … 5.0 | Controls “blob” size |
| **Clustering voxel size** | 5 cm … 50 cm | Forces planar/box fits |
| **Geometric regularization loss** | L_plane + L_box | Encourages flat walls / cuboids |

---

## 6. Baseline Comparison Table

| Model | Detail level | FPS (480p) | RAM (MB) | Reconstruction time |
|-------|--------------|------------|----------|---------------------|
| **Your Minimal-3DGS** | 0.5k–5k Gaussians | **150–300** | **20–80** | **< 2 s** |
| Vanilla 3DGS (3DGS paper) | ~300k Gaussians | ~100 | ~800 | ~30 s |
| Instant-NGP | NeRF, photoreal | ~2 | ~600 | ~5 min |
| COLMAP + Mesh | High-poly mesh | — | > 1 GB | > 10 min |

*(Numbers are ballpark; you will measure them.)*

---

## 7. Experimental Protocol (repeatable, publishable)

1. **Dataset**  
   - 10 indoor scenes (bedroom, office, corridor) recorded with smartphone @ 480p.  
   - Ground-truth robot trajectories from motion-capture or SLAM (ORB-SLAM3).

2. **Metrics**  
   - **Reconstruction**: #Gaussians, RMSE on held-out views, Chamfer distance.  
   - **Navigation**:  
     - Task success % (reach goal without collision).  
     - Path efficiency (actual / optimal length).  
     - Planning time per step.  
   - **Resource**: GPU watt-hours, peak RAM, end-to-end latency (video→path).

3. **Ablation**  
   - Fix scene → sweep each knob → plot **navigation success vs. resource**.  
   - Identify **Pareto frontier** of minimal viable detail.

---

## 8. Implementation Roadmap (8–10 weeks)

| Week | Milestone |
|------|-----------|
| 1–2 | Literature (3DGS, Instant-NGP, navigation from radiance fields). |
| 3–4 | Fork `gaussian-splatting` repo, add pruning/clustering module. |
| 5–6 | Build occupancy exporter + A* planner in PyTorch/Isaac-Gym. |
| 7–8 | Record dataset, run full ablation, collect CSV logs. |
| 9–10 | Write thesis, generate Pareto plots, conclusion. |

**Key repos to fork**  
- https://github.com/graphdeco-inria/gaussian-splatting  
- https://github.com/NVlabs/instant-ngp (for baseline)

---

## 9. Expected Contribution (bullet points for abstract)

- First systematic study of **Gaussian budget** for downstream robot navigation.  
- Novel **pruning + geometric regularization** pipeline yielding **10–50× fewer primitives** than vanilla 3DGS while preserving > 95 % navigation success.  
- Open-source minimal-3DGS toolkit with occupancy export.  
- Comprehensive benchmark (latency, RAM, success) on real monocular video.

---

## 10. Quick Starter Code Snippet (pruning + clustering)

```python
# After training (gs = GaussianModel)
opacity = gs.get_opacity
mask = opacity > cfg.tau  # e.g. 0.05
gs.prune(mask)

# Voxel clustering
points = gs.get_xyz[mask]
voxel_size = 0.15
grid = torch.round(points / voxel_size).long()
unique, counts = torch.unique(grid, dim=0, return_counts=True)
# merge Gaussians inside same voxel → average params
```

---

### TL;DR

1. **Use 3DGS** as the core representation.  
2. **Prune & cluster** Gaussians aggressively.  
3. **Export to occupancy grid** → standard planner.  
4. **Sweep detail knobs**, measure navigation success + resources.  
5. **Beat Instant-NGP on speed/RAM** while proving “minimal geometry is enough”.

You now have a **focused, measurable, and publishable** bachelor project that directly answers your original frustration. Good luck—feel free to ask for any module deep-dive!