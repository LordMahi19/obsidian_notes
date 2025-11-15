### Relevant Key Papers, Tutorials, and GitHub Repos

**Note:** Some papers could not be downloaded due to restricted access. They are marked with `[ ]`.

Based on a thorough search, I've curated a list of 10–15 essential papers (focusing on foundational and recent works from 2022–2025), tutorials (step-by-step guides for beginners), and GitHub repositories. These cover 3D Gaussian Splatting (3DGS), Instant-NGP, monocular reconstruction/SLAM, and robot navigation from 3D reconstructions. I've prioritized open-access or arXiv links where possible, and selected items that are directly actionable for your thesis (e.g., implementations, reviews, and navigation-specific applications). For papers, aim to read the abstracts first, then skim methods/results, and finally dive deep into 3–5 core ones per topic.

#### Key Papers
Here's a prioritized list (start with the top 3–4 per category):

**3D Gaussian Splatting (3DGS):**
- [x] "3D Gaussian Splatting for Real-Time Radiance Field Rendering" by Bernhard Kerbl et al. (2023). This is the foundational paper introducing 3DGS for fast rendering and reconstruction. Available on arXiv: https://arxiv.org/abs/2308.04079.
- [x] "3DGS2: Near Second-order Converging 3D Gaussian Splatting" by Lei Lan et al. (2025). Focuses on optimization for faster convergence, ideal for your pruning experiments. Available on ACM: https://dl.acm.org/doi/10.1145/3721238.3730687.
- [x] "Efficient Decoupled Feature 3D Gaussian Splatting" (CVPR 2025 poster). Emphasizes faster training and rendering with fewer resources. Available on CVPR: https://cvpr.thecvf.com/virtual/2025/poster/34457.
- [x] "3D Gaussian Splatting Methods for Real-World Scenarios" (2025). A review of 3DGS extensions for practical applications like yours. PDF: https://isprs-annals.copernicus.org/articles/X-G-2025/641/2025/isprs-annals-X-G-2025-641-2025.pdf.

**Instant-NGP:**
- [x] "Instant Neural Graphics Primitives with a Multiresolution Hash Encoding" by Thomas Müller et al. (2022). The original paper on Instant-NGP for near-instant neural reconstructions—your key baseline. Available on Towards Data Science: https://towardsdatascience.com/paper-explained-instant-neural-graphics-primitives-with-a-multiresolution-hash-encoding-8e5a05865378 (includes explanations).
- [x] "Compact Neural Graphics Primitives with Learned Hash Probing" (2023). An extension for more efficient representations. PDF: https://research.nvidia.com/labs/toronto-ai/compact-ngp/assets/compact-ngp.pdf.

**Monocular Reconstruction and SLAM:**
- [x] "Real-Time Dense Scene Reconstruction from Monocular RGB Videos" (SLAM3R, 2024). Focuses on monocular dense reconstruction for real-time use. Available on arXiv: https://arxiv.org/html/2412.09401v2.
- [ ] "A Monocular SLAM System for Large-Scale 3D Reconstruction" (2025). Integrates 3DGS with monocular SLAM, directly relevant to your pipeline. Available on ACM: https://dl.acm.org/doi/10.1145/3726010.3726086.
- "ORB-SLAM3: An Accurate Open-Source Library for Visual, Visual-Inertial, and Multi-Map SLAM" by Campos et al. (2020, but foundational for your pose annotation). The core paper for ORB-SLAM3. Available via GitHub repo (linked below).
- [ ] "MASt3R-SLAM: Real-Time Dense SLAM with 3D Reconstruction Priors" (2025). Combines dense SLAM with priors for navigation. Explained on LearnOpenCV: https://learnopencv.com/mast3r-slam-realtime-dense-slam-explained/.

**Robot Navigation from 3D Reconstructions:**
- [ ] "3D Reconstruction in Robotics: A Comprehensive Review" (2025). A broad overview to contextualize your work. Available on ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0097849325000974.
- [ ] "Vision-Guided Autonomous Robot Navigation in Realistic 3D Environments" (2025). Focuses on RGB-D/monocular navigation from reconstructions. Available on MDPI: https://www.mdpi.com/2076-3417/15/5/2323.
- [x] "3D Lidar Reconstruction with Probabilistic Depth Completion for Robotic Navigation" (2022). Useful for navigation metrics inspiration. Available on arXiv: https://arxiv.org/abs/2207.12520.
- [x] "Real-time Semantic 3D Reconstruction for High-Touch Surface Recognition in Robotic Disinfection" (2022). Applies reconstructions to robot tasks. PDF: https://motion.cs.illinois.edu/papers/IROS2022-Qiu-RealTimeSemanticReconstruction.pdf.

For more, check awesome lists like "Awesome-3D-Gaussian-Splatting-Paper-List" for ongoing updates.

#### Tutorials and Guides
These are beginner-friendly, with code examples and videos:

**3DGS Tutorials:**
- "3D Gaussian Splatting Tutorial" (official, with slides on foundations, practice, and dynamics). Available: https://3dgstutorial.github.io/.
- "3D Gaussian Splatting - Paper Explained, Training with NeRFStudio" (2024, includes custom data training). On LearnOpenCV: https://learnopencv.com/3d-gaussian-splatting/.
- "3D Gaussian Splatting Tutorial from Scratch in 100 lines of PyTorch Code" (2025, pure Python for beginners). On Medium: https://papers-100-lines.medium.com/3d-gaussian-splatting-tutorial-from-scratch-in-100-lines-of-pytorch-code-no-cuda-no-c-6ef104dc6419.
- "Getting Started With 3D Gaussian Splatting for Windows (Beginner Tutorial)" (2023 video, step-by-step install and use). On YouTube: https://www.youtube.com/watch?v=UXtuigy_wYc.

**Instant-NGP Tutorials:**
- "Instant 3D Reconstruction with Python and Instant-NGP" (2024, pure Python implementation). On Medium: https://papers-100-lines.medium.com/instant-3d-reconstruction-with-python-and-instant-ngp-68973cd6f706.
- "Instant NGP in 100 lines of PyTorch code" (2024 video tutorial). On YouTube: https://www.youtube.com/watch?v=PXbPeG5PJd0.
- Official docs on Nerfstudio: https://docs.nerf.studio/nerfology/methods/instant_ngp.html.

**Monocular Reconstruction/SLAM and ORB-SLAM3 Tutorials:**
- "ORB-SLAM 3: A Tool for 3D Mapping and Localization" (2023, beginner intro). On Sigmoidal: https://sigmoidal.ai/en/orb-slam-3-a-tool-for-3d-mapping-and-localization/.
- "Full Setup Guide and Implementation for ORB-SLAM3" (GitHub tutorial with dependencies). On GitHub: https://github.com/kevin-robb/orb_slam_implementation.
- "How to Implement Visual SLAM" (tutorial on ORB-SLAM3). On Institute for Future Technologies: https://ift.devinci.fr/how-implement-visual-slam.

**Robot Navigation Tutorials:**
- Many papers above include code; for basics, pair with ROS/Gazebo tutorials (e.g., official ROS docs for A* planning: https://wiki.ros.org/navigation).

#### GitHub Repos
Fork these for your project (go to the repo page, click "Fork" in the top-right):

- **3DGS Core:** graphdeco-inria/gaussian-splatting (official implementation). https://github.com/graphdeco-inria/gaussian-splatting.
- **Awesome 3DGS List:** MrNeRF/awesome-3D-gaussian-splatting (curated papers, resources, and extensions). https://github.com/MrNeRF/awesome-3D-gaussian-splatting.
- **Instant-NGP Core:** NVlabs/instant-ngp (official NVIDIA repo with binaries). https://github.com/NVlabs/instant-ngp.
- **PyTorch Instant-NGP:** kwea123/ngp_pl (lightweight PyTorch version for easy integration). https://github.com/kwea123/ngp_pl.
- **ORB-SLAM3 Core:** UZ-SLAMLab/ORB_SLAM3 (official for pose annotation). https://github.com/UZ-SLAMLab/ORB_SLAM3.
- **ORB-SLAM3 Setup Guide Repo:** kevin-robb/orb_slam_implementation (beginner-friendly install scripts). https://github.com/kevin-robb/orb_slam_implementation.

Spend Week 1 reading 2–3 papers/tutorials per day, taking notes on methods (e.g., pruning in 3DGS) and how they relate to your minimal-detail goal.

### Detailed Instructions on How to Set Up the Development Environment

As an absolute beginner, we'll go step-by-step. Assume you're on Ubuntu 22.04+ (recommended for compatibility; if on Windows, use WSL2—search "install WSL2 Ubuntu" on Google). You'll need admin access (sudo) and an NVIDIA GPU with CUDA support (check with `nvidia-smi` in terminal; if no GPU, use CPU but expect slower training).

#### Step 1: Install Python 3.10+
1. Open a terminal (Ctrl+Alt+T on Ubuntu).
2. Update your system: `sudo apt update && sudo apt upgrade -y`.
3. Install Python 3.10: `sudo apt install python3.10 python3.10-venv python3.10-dev -y`.
4. Verify: `python3.10 --version` (should show 3.10.x).
5. Create a virtual environment (isolates packages): `python3.10 -m venv thesis_env`.
6. Activate it: `source thesis_env/bin/activate` (do this every new terminal session; you'll see `(thesis_env)` prompt).

#### Step 2: Install PyTorch 2.0+ with CUDA
PyTorch handles neural networks; CUDA enables GPU acceleration.
1. In activated env: Install pip tools: `pip install --upgrade pip setuptools wheel`.
2. Install PyTorch (for CUDA 12.x; check your CUDA version with `nvcc --version`): `pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121` (use 2.0+; latest is fine as of 2025).
3. Verify: `python -c "import torch; print(torch.__version__); print(torch.cuda.is_available())"` (should print version >2.0 and True if GPU ready).

#### Step 3: Install CUDA (if not already)
If `nvidia-smi` works but CUDA not installed:
1. Download from NVIDIA: Go to https://developer.nvidia.com/cuda-downloads, select Ubuntu, follow instructions (e.g., `wget` commands for installer).
2. Run: `sudo apt install cuda` (or specific version like cuda-12-1).
3. Add to PATH: `echo 'export PATH=/usr/local/cuda-12.1/bin${PATH:+:${PATH}}' >> ~/.bashrc` and `source ~/.bashrc`.
4. Verify: `nvcc --version`.

#### Step 4: Install Additional Dependencies
These are common for the repos:
1. `sudo apt install git build-essential libopencv-dev libpangolin-dev libeigen3-dev libglew-dev cmake -y`.
2. In env: `pip install numpy scipy matplotlib pandas opencv-python plyfile tqdm`.
3. For 3DGS/NGP specifics, check repo READMEs later.

#### Step 5: Fork and Clone Relevant GitHub Repos
1. Create a GitHub account if none (github.com).
2. For each repo (e.g., https://github.com/graphdeco-inria/gaussian-splatting):
   - Click "Fork" (creates your copy).
   - Clone to local: `git clone https://github.com/YOUR_USERNAME/gaussian-splatting.git` (replace YOUR_USERNAME).
3. Do this for: gaussian-splatting, instant-ngp, ORB_SLAM3.
4. Navigate: `cd gaussian-splatting` and follow README for build (e.g., `cmake . && make` for C++ parts).

Test: Run a sample from each repo's examples to ensure setup works (e.g., Instant-NGP has testbed).

If errors: Search "error message + repo name" on Google/StackOverflow.

### Guide on How to Annotate Ground-Truth Poses via ORB-SLAM3

ORB-SLAM3 estimates camera poses (position/orientation) from videos, serving as "ground-truth" for your datasets (though not perfect, it's accurate for indoors).

#### Step 1: Install ORB-SLAM3
1. Clone forked repo: `git clone https://github.com/YOUR_USERNAME/ORB_SLAM3.git`.
2. Install dependencies (from README): `sudo apt install libboost-all-dev libssl-dev -y`.
3. Build: `cd ORB_SLAM3 && ./build.sh` (takes 10–30 min; fixes errors by installing missing libs).
4. Download vocabulary: In repo, run `./Thirdparty/DBoW2/build.sh` if needed.

#### Step 2: Prepare Your Video Dataset
1. Capture 5–10 short videos: Use smartphone (e.g., Android/iPhone app like "Open Camera" for 480p@30fps MP4). Film indoor rooms (bed/chair as example) slowly, covering 360° if possible. Aim for 10–30 seconds each.
2. Calibrate camera: Use ORB-SLAM3's calibration tool. Print checkerboard (search "camera calibration pattern PDF"), film video waving it. Run: `./Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt Examples/Monocular/TUM1.yaml path_to_video`.
3. Output: Save calibration YAML file (e.g., camera.yaml with intrinsics like fx,fy,cx,cy).

#### Step 3: Run ORB-SLAM3 on Videos for Poses
1. Download example data to test: EuRoC dataset from https://projects.asl.ethz.ch/datasets/doku.php?id=kmavvisualinertialdatasets (MH_01_easy.zip).
2. Run monocular mode: `./Examples/Monocular/mono_euroc Vocabulary/ORBvoc.txt Examples/Monocular/EuRoC.yaml path_to_unzipped/MH_01_easy/mav0/cam0/data EuRoC_TimeStamps/MH01.txt`.
3. For your video: Convert MP4 to image sequence: Use FFmpeg (`sudo apt install ffmpeg`, then `ffmpeg -i your_video.mp4 -vf fps=30 images/frame_%04d.png`).
4. Create YAML for your camera: Copy Examples/Monocular/TUM1.yaml, edit with your calibration (fx, etc.).
5. Run: `./Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt your_camera.yaml path_to_images`.
6. Output: Poses saved as "CameraTrajectory.txt" (format: timestamp tx ty tz qx qy qz qw). This is your ground-truth poses per frame.
7. Visualize: Use repo's viewer or export to PCL for 3D map.

Tips: If loop closure fails, refilm with more overlaps. For accuracy, use inertial if phone has IMU (edit to visual-inertial mode).

### How to Define Exact Metrics and Ablation Parameters in a Jupyter Notebook for Tracking

Jupyter notebooks are interactive Python docs for experiments.

#### Step 1: Install Jupyter
In env: `pip install jupyter notebook`.

#### Step 2: Create and Run Notebook
1. Start: `jupyter notebook` (opens browser at http://localhost:8888).
2. New > Python 3: Name "thesis_metrics.ipynb".
3. Cells: Code (Python) or Markdown (text).

#### Step 3: Define Metrics (Exact Ones from Your Thesis)
In a Markdown cell: 
```
# Metrics and Ablations

## Reconstruction Metrics
- #Gaussians: Number of primitives after pruning.
- RMSE: Root Mean Squared Error on held-out views (use torch.sqrt(torch.mean((pred - gt)**2))).
- Chamfer Distance: Symmetric point-cloud distance (use from plyfile or scipy.spatial).

## Navigation Metrics
- Success Rate: % of paths reaching goal without collision (e.g., >95% target).
- Path Efficiency: Actual path length / optimal (A* straight-line).
- Collision Count: Number of hits in simulation.

## Resource Metrics
- Latency: End-to-end time (use time.time()).
- RAM: Peak memory (use psutil.virtual_memory().used).
- FPS: Frames per second during rendering.

## Ablation Parameters (Knobs to Sweep)
- num_gaussians: [500, 1000, 5000, 10000, 50000]
- opacity_tau: [0.01, 0.05, 0.1, 0.2]
- voxel_size: [0.05, 0.1, 0.15, 0.5]  # meters
- covariance_scale: [0.5, 1.0, 2.0, 5.0]
```

#### Step 4: Implement Tracking Code
In code cells:
```python
import pandas as pd
import time
import psutil
import torch

# Example: Define params as dict
ablation_params = {
    'num_gaussians': [500, 1000, 5000],
    'opacity_tau': [0.01, 0.05, 0.1]
}

# Create DataFrame for logging
results = pd.DataFrame(columns=['run_id', 'num_gaussians', 'opacity_tau', 'rmse', 'success_rate', 'latency_sec', 'peak_ram_mb'])

# Simulate a run (replace with your code)
for ng in ablation_params['num_gaussians']:
    for tau in ablation_params['opacity_tau']:
        start_time = time.time()
        # Your model code here, e.g., train_3dgs(ng, tau)
        # Fake metrics
        rmse = 0.05  # Compute actually
        success_rate = 0.95
        latency = time.time() - start_time
        ram = psutil.virtual_memory().used / (1024 ** 2)  # MB
        
        # Log
        new_row = {'run_id': len(results)+1, 'num_gaussians': ng, 'opacity_tau': tau, 'rmse': rmse, 
                   'success_rate': success_rate, 'latency_sec': latency, 'peak_ram_mb': ram}
        results = pd.concat([results, pd.DataFrame([new_row])], ignore_index=True)

# Save to CSV
results.to_csv('ablation_results.csv', index=False)

# Plot
import matplotlib.pyplot as plt
plt.plot(results['num_gaussians'], results['success_rate'], 'o-')
plt.xlabel('# Gaussians')
plt.ylabel('Success Rate')
plt.show()
```

Run cells with Shift+Enter. Export CSV for thesis plots. Track per scene/run to build Pareto curves.

This completes Week 1–2 prep—proceed to implementation next!