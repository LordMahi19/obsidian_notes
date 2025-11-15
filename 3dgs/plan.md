### Step-by-Step Plan to Complete the Bachelor Thesis

1. **Preparation Phase (Weeks 1–2)**
    - Conduct a thorough literature review on 3DGS, Instant-NGP, monocular reconstruction, and robot navigation (e.g., read 10–15 key papers).
    - Set up development environment: Install Python 3.10+, PyTorch 2.0+, CUDA, and fork relevant GitHub repos (gaussian-splatting, instant-ngp).
    - Record or source initial datasets: Capture 5–10 short monocular videos of indoor scenes (e.g., rooms with furniture) using a smartphone; annotate ground-truth poses if possible via ORB-SLAM3.
    - Define exact metrics and ablation parameters in a Jupyter notebook for tracking.
2. **Core Implementation Phase (Weeks 3–4)**
    - Implement the base pipeline: Integrate COLMAP for SfM, initialize 3DGS from point clouds, and train a vanilla model.
    - Add pruning module: Code opacity thresholding and voxel-based clustering (use the starter snippet from earlier as a base).
    - Incorporate geometric regularization: Implement RANSAC for fitting planes/cuboids to clustered Gaussians.
    - Test on a single scene: Verify low-detail output (e.g., <5k Gaussians) renders correctly and exports to an occupancy grid.
3. **Integration and Simulation Phase (Weeks 5–6)**
    - Build the navigation component: Use PyTorch for occupancy grid generation, then integrate with a planner (A* in NetworkX or DWA in ROS/Gazebo).
    - Set up simulation: Install Gazebo or Isaac Sim; create a simple robot model and test paths in reconstructed scenes.
    - Run preliminary experiments: On 2–3 scenes, sweep detail knobs (#Gaussians, voxel size) and log basic metrics (success rate, latency).
    - Debug and optimize: Profile with NVIDIA nsight or torch.utils.bottleneck to identify bottlenecks.
4. **Experimentation and Data Collection Phase (Weeks 7–8)**
    - Expand dataset to 10 scenes, ensuring variety (e.g., cluttered vs. sparse rooms).
    - Perform full ablations: For each knob, run 5–10 trials per scene, collecting CSV data on reconstruction quality, navigation metrics, and resources (RAM via psutil, latency via timeit).
    - Benchmark baselines: Train/run Instant-NGP and vanilla 3DGS on the same datasets; compare in tables/plots.
    - Analyze interim results: Generate Pareto plots (e.g., success vs. RAM) using Matplotlib; note any surprises for thesis discussion.
5. **Writing and Finalization Phase (Weeks 9–10)**
    - Draft thesis structure: Introduction, Related Work, Methodology, Experiments, Results, Discussion, Conclusion.
    - Write sections incrementally: Start with methodology/experiments (easiest), then abstract/intro; incorporate plots and tables.
    - Polish and revise: Ensure 40–60 pages, cite sources properly (20+ references); get peer feedback.
    - Prepare defense: Create slides summarizing pipeline, results, and contributions; rehearse.
    - Submit: Package code/dataset on GitHub; deliver final thesis and proposal updates to professor.