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