# Project Summary and Next Steps

## Goal
To complete a bachelor thesis project investigating the suitability of Neural Radiance Fields (NeRFs) for robotic perception.

## Progress
1.  **Topic Selection:** Narrowed down the research topic to focus on deep learning approaches, specifically NeRF-based models.
2.  **Thesis Proposal:** Created a detailed thesis proposal including an abstract and a chapter-by-chapter research plan. This was saved to `thesis.md`.
3.  **Experimental Setup:** Began the practical setup for the project using the **Instant-NGP** framework.
    *   Confirmed prerequisites: NVIDIA GPU (RTX 3060) and Python are installed.
    *   Installed dependencies: Git, Visual Studio 2022 (with C++ workload).
    *   Cloned the Instant-NGP repository.

## Current Roadblock
The project build failed due to an outdated version of CMake. The project requires **CMake v3.21 or higher**.

## Next Steps
1.  **Uninstall Old CMake:** Remove the current, outdated version of CMake from your system.
2.  **Install Latest CMake:** Download and install the latest version from the [CMake website](https://cmake.org/download/), ensuring to add it to the system PATH during installation.
3.  **Clean Build Directory:** Delete the `build` folder inside your `instant-ngp` project directory to ensure a clean start.
4.  **Re-run Build:** Open a **new terminal** and execute the following commands from within the `instant-ngp` directory:
    ```bash
    cmake . -B build
    cmake --build build --config RelWithDebInfo -j
    ```

https://www.youtube.com/watch?v=3TWxO1PftMc
