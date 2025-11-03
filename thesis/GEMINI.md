# GEMINI.md: Thesis Project Context

## Project Overview

This thesis aims to investigate the effectiveness of event-based cameras for action recognition in comparison with conventional RGB cameras. The study will evaluate how different action recognition models—such as convolutional neural networks, recurrent architectures, and spiking-inspired models—perform when trained and tested on event-based datasets versus RGB video datasets. Performance will be measured in terms of accuracy, computational efficiency, and robustness under challenging conditions (e.g., motion blur or low lighting). The findings are expected to contribute to the growing body of research on neuromorphic vision and highlight practical trade-offs between event-based and RGB-based perception in robotics.

## Current Focus: Starting Checklist

This is the concrete starting checklist to act on now:

1.  **Clone repos**: v2e, ESIM/vid2e, and a template PyTorch action-recognition training repo.
2.  **Download one dataset**: e.g., DVS128 Gesture (for gesture tasks) and DHP19 (if you want paired human pose/action).
3.  **Write a small script** that: (a) loads events and converts to event-frames (and/or voxel grids); (b) saves tensors ready for training. Use the SpikingJelly loader examples if helpful.
4.  **Implement a small baseline**: train a 2D CNN on RGB frames and the *same* 2D CNN on event-frames (keeps comparison fair). Measure accuracy & inference time.
5.  **Add one robustness test**: blur or darken RGB test set and re-evaluate.

## Key Files

*   **`thesis.md`**: The main document containing the thesis abstract, literature review, and a detailed chapter-by-chapter structure.
*   **`currently working on.md`**: Contains the concrete starting checklist for the project.

## Key Concepts & Literature

*   **Core Concepts:** Event-Based Vision, Neuromorphic Sensors, Action Recognition, Convolutional Neural Networks (CNNs), Spiking Neural Networks (SNNs).
*   **Key Papers:**
    *   "Event-based Vision: A Survey"
    *   "EV-ACT: A New Benchmark and Framework for Event-based Action Recognition"
    *   "SpikMamba: When SNN meets Mamba in Event-based Human Action Recognition"
*   **Key Libraries/Tutorials:**
    *   **SpikingJelly:** A library for SNNs with tutorials for getting started.
