## 1. Summary of Work Completed

I have significantly advanced the initial phase of my project, focusing on building a robust and well-optimized pipeline for event-based action recognition.

*   **Objective:** My primary goal remains to compare the effectiveness of event-based cameras against traditional RGB cameras for action recognition, focusing on accuracy, efficiency, and robustness.
*   **Dataset:** I am using the DVS128 Gesture dataset for my experiments.
*   **Methodology:**
    1.  I have refined my data processing pipeline. I now use a fixed number of time bins (`n_time_bins`) to convert the event stream into fixed-length "videos" of event-frames. This provides a more stable input for the model.
    2.  I have substantially improved my 3D Convolutional Neural Network (`Gesture3DCNN`). The new architecture now includes **Batch Normalization** after each convolution to stabilize training and **Dropout** as a regularization technique to prevent overfitting.
    3.  I have implemented a more sophisticated training procedure which includes **weight decay** in the optimizer, a **learning rate scheduler** (`ReduceLROnPlateau`) that adapts based on performance, and **early stopping** to prevent overfitting and save the best-performing model.
*   **Results:** I have successfully trained and evaluated the improved model, achieving a new peak test accuracy of **90.9%**. The inclusion of regularization and early stopping has resulted in a more generalized model. Furthermore, I have generated a detailed **classification report**, which shows that while the overall accuracy is high, the model's performance varies across different gestures. For example, it achieves perfect recall on some classes but struggles with others, providing specific targets for future model tuning and error analysis.

## 2. Proposed Research Plan

The following plan outlines my next steps to complete the comparative study.

1.  **Establish RGB Baseline (Immediate Next Step):**
    *   **Task:** I will train the exact same `Gesture3DCNN` architecture on a comparable RGB video dataset.
    *   **Action:** I will identify a suitable public RGB gesture dataset. I will modify the model's input layer to accept 3 channels (for RGB) instead of 2 (for DVS events).
    *   **Goal:** My goal is to create a direct performance baseline (accuracy, inference time) for a conventional camera under ideal conditions.

2.  **Conduct Robustness Tests:**
    *   **Task:** I will evaluate the performance of both the RGB and event-based models under challenging conditions that are relevant to robotics.
    *   **Action (RGB):** I will artificially degrade the RGB test dataset by adding motion blur and reducing brightness to simulate fast movements and low-light environments.
    *   **Action (DVS):** I will evaluate the DVS model on corresponding data to quantify its inherent advantages in these scenarios.
    *   **Goal:** My goal is to scientifically measure the robustness trade-offs between the two sensor modalities.

3.  **Explore Advanced Architectures (Optional Extension):**
    *   **Task:** I will investigate models that are more naturally suited to the data type, as mentioned in my thesis proposal.
    *   **Action:**
        *   I will implement a Spiking Neural Network (SNN) using a library like `SpikingJelly` or `snnTorch` for the event-based data.
        *   I will implement a Recurrent Neural Network (RNN/LSTM) for the RGB data, potentially using pose estimation (e.g., MediaPipe) as an intermediate representation.
    *   **Goal:** My goal is to compare the initial CNN-based approach with more specialized architectures.

4.  **Synthesize Results and Write Thesis:**
    *   **Task:** I will analyze all experimental results, focusing on the key metrics: accuracy, computational efficiency (inference time, FLOPs), and robustness.
    *   **Action:** I will structure the findings into the thesis, drawing conclusions about the practical trade-offs for using event-based sensors in robotics.

## 3. Questions for Discussion

I have a few questions regarding the direction and novelty of the research that I would appreciate your guidance on:

1.  **Novelty and Data Strategy:** I have successfully trained a model on the DVS128 Gesture dataset, which is a standard benchmark. To ensure the novelty of my thesis, what would be a valuable direction? Should I focus on creating a custom synthetic dataset using a simulator like `v2e` to test specific, challenging scenarios, or is there more value in applying more advanced or novel model architectures to existing datasets?

2.  **Comparative Methodology:** I want to ensure the comparison between the RGB and DVS models is as fair and insightful as possible. Beyond using the same model architecture, what are the key factors I should control for or be mindful of? For example, how can I best account for intrinsic differences in the data (e.g., frame rate vs. temporal resolution) to make a scientifically valid claim about which sensor is "better" for certain tasks?

3.  **Connecting to Robotics:** My goal is to frame this research within the context of robotics. How can I best design my experiments to highlight the practical advantages of event-based cameras for robotic perception? Should I focus the robustness tests on scenarios commonly encountered by robots (e.g., fast manipulator movements, sudden lighting changes)? And how can I quantify the benefits beyond accuracy, for instance, in terms of latency or computational load, which are critical for real-time robotic systems?

## 4. Literature Review Progress

I have been actively engaging with the research literature to build a strong foundation for my thesis. I am taking detailed notes on each paper to understand the key concepts and methodologies. While the technical language can be challenging, I am focusing on gaining a high-level overview of each paper's contribution. So far, I have reviewed the following:

*   **A Low Power, Fully Event-Based Gesture Recognition System:** The paper that introduces the DVS128 Gesture dataset and demonstrates a highly efficient gesture recognition system on a neuromorphic chip.
*   **Classify DVS Gesture (SpikingJelly tutorial):** A practical guide showing how to build and train a Spiking Neural Network (SNN) for the DVS128 Gesture dataset.
*   **DailyDVS-200 A Comprehensive Benchmark:** This paper introduces a very large and diverse event-based dataset for object recognition to push the boundaries of model performance.
*   **DHP19 Dynamic Vision Sensor 3D Human Pose Dataset:** This work provides a new event-based dataset for 3D human pose estimation, complete with synchronized 3D ground truth from a motion capture system.
*   **ESIM: an Open Event Camera Simulator:** A paper presenting a simulator that can generate realistic synthetic event data, which is highly relevant for my interest in creating custom datasets.
