### A Low Power, Fully Event-Based Gesture Recognition System

*   **Contribution:** This paper presents the first end-to-end gesture recognition system built entirely on event-based hardware. It uses a Dynamic Vision Sensor (DVS) for capturing event streams and an IBM TrueNorth neurosynaptic processor for real-time classification.
*   **Hardware:** The system pairs a DVS camera, which only transmits data when a pixel's brightness changes, with a TrueNorth chip, a natively event-based processor with one million spiking neurons. This combination is designed for extreme power efficiency.
*   **Methodology:** The authors configured the TrueNorth chip to run a Convolutional Neural Network (CNN). They also created and introduced the DVS128 Gesture dataset, which is the one you are currently using, featuring 11 gestures from 29 subjects under various lighting conditions.
*   **Performance:** The system demonstrates impressive performance with high accuracy (96.5%), low latency (105 ms), and extremely low power consumption (<200 mW).
*   **Key Takeaway:** The main point of this paper is that pairing an event-based sensor with an event-based processor allows for the creation of highly efficient and responsive recognition systems, which are ideal for power-constrained environments like robotics and mobile devices. This is a foundational paper for your project.

### Classify DVS Gesture — spikingjelly alpha 文档

*   **Contribution:** This is a tutorial from the SpikingJelly documentation, providing a practical guide on how to build and train a Spiking Neural Network (SNN) to classify the DVS128 Gesture dataset.
*   **Library:** It uses `spikingjelly`, a PyTorch-based library specifically designed for SNNs.
*   **Methodology:** The tutorial defines a network (`DVSGestureNet`) using convolutional layers and Leaky Integrate-and-Fire (LIF) spiking neurons. It explains how to load the DVS128 Gesture dataset, prepare it for an SNN, and train it in a multi-step mode, averaging the output spikes over time for classification.
*   **Performance:** The tutorial achieves a final test accuracy of 93.75% on the DVS128 Gesture dataset.
*   **Key Takeaway:** This document is a step-by-step guide for implementing a "spiking-inspired model" as mentioned in your thesis abstract. It provides the exact code and structure needed to build an SNN for your specific dataset, which is a crucial part of your proposed research plan.

### DailyDVS-200 A Comprehensive Benchmark

*   **Contribution:** This paper introduces a new, large-scale event-based dataset for object recognition called **DailyDVS-200**. It aims to address the lack of large, diverse datasets in the event-based vision field, which has hindered progress compared to the RGB domain.
*   **Dataset:** The benchmark contains over 300,000 samples across 200 daily object categories, making it significantly larger and more diverse than previous datasets like N-Caltech101.
*   **Methodology:** The authors propose a new baseline model, the **Event-based Vision Transformer (EViT)**, which adapts the popular Vision Transformer (ViT) architecture for event data. They also introduce a new data representation method called Event-to-Static-Image (E2SI).
*   **Performance:** The proposed EViT model achieves state-of-the-art results on the new DailyDVS-200 benchmark.
*   **Key Takeaway:** This paper highlights the trend towards larger datasets and more sophisticated models (like Transformers) in the event-based vision community. While your focus is on action recognition, this paper is a good reference for advanced model architectures and shows the direction the field is heading.

### DHP19 Dynamic Vision Sensor 3D Human Pose Dataset

*   **Contribution:** This paper introduces **DHP19**, the first benchmark dataset for **3D human pose estimation** using event-based cameras. It aims to facilitate research into low-latency and power-efficient 3D pose estimation.
*   **Dataset:** DHP19 contains recordings of 17 subjects performing 33 different movements. The data was captured by 4 synchronized DVS cameras and, crucially, includes accurate 3D ground truth joint positions from a professional Vicon motion capture system.
*   **Methodology:** The authors provide a baseline proof-of-concept model. They convert the DVS event streams into frames, train a CNN to predict 2D joint heatmaps, and then use geometric triangulation from the multi-camera 2D predictions to reconstruct the final 3D pose.
*   **Performance:** The baseline model achieves an average 3D joint error of ~8 cm, demonstrating the viability of using DVS for this complex task. Their proposed CNN is also noted to be significantly smaller and faster than comparable RGB-based models.
*   **Key Takeaway:** While your thesis is on action recognition, this paper is highly relevant as it provides a multi-view DVS dataset with precise 3D annotations. It tackles a more complex task (3D pose vs. gesture classification) and could be a valuable resource if you choose to explore more advanced problems or require precise 3D joint data for your analysis.

### ESIM: an Open Event Camera Simulator

*   **Contribution:** This paper presents **ESIM**, an open-source event camera simulator designed to address the scarcity and high cost of real event cameras. It allows researchers to generate large quantities of high-quality, labeled synthetic event data.
*   **Problem:** The paper notes that progress in event-based vision is slowed by the lack of data. Simulators are needed for algorithm prototyping, benchmarking, and especially for training deep learning models that require vast datasets.
*   **Methodology:** ESIM's key innovation is its **adaptive sampling scheme**. Instead of rendering frames at a fixed high rate (which is inefficient), it tightly couples with a 3D graphics engine to predict how the scene will change and only renders new frames when necessary to accurately simulate the event generation process. This is both more accurate and more efficient.
*   **Features:** The simulator can generate events, standard camera images, depth maps, and camera trajectories, along with realistic noise models.
*   **Key Takeaway:** This paper is directly relevant to your question about creating synthetic data. A tool like ESIM (or `v2e`, which is similar) gives you the power to create custom datasets for specific, challenging scenarios (e.g., very fast motion, difficult lighting) that may not be available in public datasets. This provides a clear path to adding novelty to your thesis by allowing you to design targeted experiments.
