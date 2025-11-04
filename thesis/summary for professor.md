# Thesis Project Update & Discussion Points

This document summarizes my thesis project progress and outlines discussion points for our meeting.

## 1. Project Progress

*   [ ] Set up event-based data processing pipeline using Tonic.
*   [ ] Implemented and refined a 3D CNN model for event-based action recognition.
*   [ ] Achieved a peak test accuracy of 90.9% on the DVS128 Gesture dataset.
*   [ ] Incorporated advanced training techniques (Batch Norm, Dropout, LR scheduling, early stopping) to improve model robustness.
*   [ ] Refactored code and exported the trained model to ONNX and TorchScript for deployment readiness.

## 2. Next Steps & Research Plan

My immediate next steps for the thesis are:

1.  **Establish RGB Baseline:** I will train the same 3D CNN architecture on a comparable RGB video dataset to create a direct performance baseline.
2.  **Conduct Robustness Tests:** I will evaluate both RGB and event-based models under challenging conditions (e.g., motion blur, low light) relevant to robotics.
3.  **Explore Advanced Architectures (Optional):** I plan to investigate Spiking Neural Networks (SNNs) for event data and Recurrent Neural Networks (RNNs) for RGB data.
4.  **Synthesize Results:** I will analyze all experimental results to draw conclusions about trade-offs for event-based sensors in robotics.

## 3. Questions for Discussion

I have a few questions regarding the direction and novelty of the research that I would appreciate your guidance on:

1.  **Novelty and Data Strategy:** I have successfully trained a model on the DVS128 Gesture dataset, which is a standard benchmark. To ensure the novelty of my thesis, what would be a valuable direction? Should I focus on creating a custom synthetic dataset using a simulator like `v2e` to test specific, challenging scenarios, or is there more value in applying more advanced or novel model architectures to existing datasets?

2.  **Comparative Methodology:** I want to ensure the comparison between the RGB and DVS models is as fair and insightful as possible. Beyond using the same model architecture, what are the key factors I should control for or be mindful of? For example, how can I best account for intrinsic differences in the data (e.g., frame rate vs. temporal resolution) to make a scientifically valid claim about which sensor is "better" for certain tasks?

3.  **Connecting to Robotics:** My goal is to frame this research within the context of robotics. How can I best design my experiments to highlight the practical advantages of event-based cameras for robotic perception? Should I focus the robustness tests on scenarios commonly encountered by robots (e.g., fast manipulator movements, sudden lighting changes)? And how can I quantify the benefits beyond accuracy, for instance, in terms of latency or computational load, which are critical for real-time robotic systems?

## 4. Literature Review Progress

I am actively reviewing relevant research papers to build my foundational knowledge. I have summarized key papers including:

*   **A Low Power, Fully Event-Based Gesture Recognition System:** Introduces DVS128 Gesture dataset and a low-power event-based gesture recognition system.
*   **Classify DVS Gesture (SpikingJelly tutorial):** A guide for building and training an SNN on the DVS128 Gesture dataset.
*   **DailyDVS-200 A Comprehensive Benchmark:** Presents a large-scale event-based dataset for object recognition.
*   **DHP19 Dynamic Vision Sensor 3D Human Pose Dataset:** Introduces an event-based dataset for 3D human pose estimation with ground truth.
*   **ESIM: an Open Event Camera Simulator:** Describes an open-source event camera simulator for generating synthetic data.
I am focusing on understanding the high-level contributions and relevance of each paper to my thesis.