# GEMINI.md: Thesis Project Context

## Project Overview

This thesis aims to investigate the effectiveness of event-based cameras for action recognition in comparison with conventional RGB cameras. The study will evaluate how different action recognition models—such as convolutional neural networks, recurrent architectures, and spiking-inspired models—perform when trained and tested on event-based datasets versus RGB video datasets. Performance will be measured in terms of accuracy, computational efficiency, and robustness under challenging conditions (e.g., motion blur or low lighting). The findings are expected to contribute to the growing body of research on neuromorphic vision and highlight practical trade-offs between event-based and RGB-based perception in robotics.

## Project Status & Next Steps

The project has progressed from initial experimentation to a more robust and structured implementation.

1.  **Clone repos**: Assumed complete.
2.  **Download one dataset**: **Done.** The DVS128 Gesture dataset was downloaded and used.
3.  **Write a small script**: **Done.** A script was created to load event data using `tonic`, convert it to event-frames, and prepare it for training using a PyTorch `DataLoader`.
4.  **Implement and Refine Baseline Model**: **Done.**
    *   A 3D-CNN (`Gesture3DCNN`) has been implemented and significantly refined with Batch Normalization and Dropout.
    *   A sophisticated training loop with learning rate scheduling, weight decay, and early stopping was used.
    *   The model was successfully trained on event-frames from the DVS128 Gesture dataset, achieving a **peak test accuracy of 90.9%**.
5.  **Refactor and Export Model**: **Done.**
    *   The code has been refactored, separating the model definition (`model_def.py`) from the training and inference logic.
    *   The best-performing model has been saved and exported to standard deployment formats: **ONNX** and **TorchScript**. This prepares the model for use in non-Python environments and real-world applications.
6.  **Establish RGB Baseline**: **In Progress.**
    *   The next step is to train the *same* 3D-CNN architecture on a corresponding RGB dataset to establish a fair comparison baseline.
7.  **Add one robustness test**: **Pending.** This will be done after the baseline comparison is complete. The plan is to blur or darken an RGB test set and re-evaluate the RGB model.

## Key Files

*   **`thesis.md`**: The main document containing the thesis abstract, literature review, and a detailed chapter-by-chapter structure.
*   **`Code that I ran.md`**: Contains the final Python code used for training the model and the commands for exporting it.
*   **`model_def.py`**: Contains the Python class definition for the `Gesture3DCNN` model.
*   **`export_and_infer.py`**: An end-to-end script that handles loading the trained model, exporting it to ONNX and TorchScript formats, and running a test inference.
*   **`models/dvsgesture_3dcnn_best.pth`**: The saved PyTorch checkpoint for the best performing model.
*   **`models/dvsgesture_3dcnn.onnx`**: The trained model exported to the standard ONNX format for interoperability and deployment.
*   **`paper_summary.md`**: Summaries of key research papers relevant to the project.

## Key Concepts & Literature

*   **Core Concepts:** Event-Based Vision, Neuromorphic Sensors, Action Recognition, Convolutional Neural Networks (CNNs), Spiking Neural Networks (SNNs), Model Deployment, ONNX.
*   **Key Papers:**
    *   "Event-based Vision: A Survey"
    *   "A Low Power, Fully Event-Based Gesture Recognition System"
    *   "v2e: From Video Frames to Realistic DVS Events"
*   **Key Libraries/Tutorials:**
    *   **SpikingJelly:** A library for SNNs.
    *   **Tonic:** A library for handling event-based data and datasets in PyTorch.
    *   **ONNX (Open Neural Network Exchange):** A standard format for representing machine learning models.
