# GEMINI.md: Thesis Project Context (New Idea)

## Project Overview

This project investigates the robustness of a pre-trained 3D-CNN event-based action recognition model. The core hypothesis is that a model trained on clean, lab-recorded data (DVS128 Gesture) will see a performance drop when evaluated against custom-recorded, real-world data containing variations in angle, lighting, and background. The project will then measure the extent to which this performance drop can be mitigated by augmenting the training dataset with this new real-world data.

## Background

This work is a pivot from an initial thesis plan that aimed to directly compare the performance of event-based cameras versus traditional RGB cameras. In the project's first stage, a `Gesture3DCNN` model was successfully developed and trained on the DVS128 Gesture dataset, achieving a **peak test accuracy of 84.1%**. This baseline model was also exported to ONNX and TorchScript formats. The current research direction builds directly on this success, using the existing high-performing model as a foundation to investigate its robustness in more realistic scenarios, a change proposed to create a more focused and less complicated thesis.

## Project Plan & Status

The project is broken down into six distinct phases.

*   **Phase 1: Baseline Model Evaluation**: **Completed.** The baseline performance of the pre-trained `Gesture3DCNN` on the original DVS128 Gesture test set has been established.
*   **Phase 2: Custom Data Collection and Conversion**: **In Progress.** This involves recording new RGB videos of the gestures and converting them to event data using the `v2e` tool.
*   **Phase 3: Robustness Test 1 (Performance Drop)**: **Pending.** The baseline model will be tested against the new, custom-recorded event data to quantify the expected drop in accuracy.
*   **Phase 4: Data Augmentation & Re-training**: **Pending.** The custom event data will be added to the training set, and the model will be re-trained.
*   **Phase 5: Robustness Test 2 (Performance Improvement)**: **Pending.** The newly re-trained model will be evaluated on the custom test data to measure any performance improvement.
*   **Phase 6: Analysis and Conclusion**: **Pending.** The results from all tests will be compared and analyzed to draw final conclusions.

## Key Files & Directories

*   **`newidea.md`**: A high-level description of the new research plan.
*   **`project.md`**: A detailed, step-by-step plan outlining the six phases of the project.
*   **`execution.md`**: A technical guide with code and commands for executing each phase of the project.
*   **`models/`**: This directory contains the core model artifacts:
    *   `dvsgesture_3dcnn_best.pth`: The combined PyTorch checkpoint containing the model state dictionary and metadata.
    *   `dvsgesture_config.json`: A JSON file storing key model and data parameters.
    *   `dvsgesture_3dcnn.onnx`: The model exported to the ONNX format.
*   **`custom_rgb_data/`**: (To be created) Directory for storing the newly recorded RGB videos of gestures.
*   **`custom_event_data/`**: (To be created) Directory for storing the event data files (`.aedat4`) after conversion with `v2e`.

## Implementation Details

### Model Architecture (`Gesture3DCNN`)
*   **Type**: 3D Convolutional Neural Network.
*   **Input Shape**: `(Batch, 2, 60, 128, 128)` corresponding to `(B, Channels, Time, Height, Width)`.
*   **Layers**: Consists of three `Conv3d` -> `BatchNorm3d` -> `MaxPool3d` blocks, followed by a `Dropout` layer, an `AdaptiveAvgPool3d` layer, and a final `Linear` layer for classification.

### Data Preprocessing
The data pipeline is critical for reproducing results and is defined in `export_and_infer.py` and replicated in `execution.md`.

1.  **Framing**: Raw event streams are converted into a fixed-size tensor by binning events into a set number of frames.
    *   **Tool**: `tonic.transforms.ToFrame`
    *   **Parameters**: `n_time_bins=60`, `sensor_size=(128, 128, 2)`
2.  **Normalization**: The resulting frame tensor is normalized using **per-sample-max** normalization.
    *   **Formula**: `x = x / (x.amax(dim=(1, 2, 3), keepdim=True) + 1e-6)`
    *   This normalizes each sample in the batch independently.

### Configuration Management
Key parameters are managed via `models/dvsgesture_config.json` to ensure consistency between scripts. This includes:
*   `num_classes`
*   `n_frames`
*   `sensor_size`
*   `normalization` type
*   `class_names`

## Key Concepts
*   **Event-Based Vision**: Using data from neuromorphic sensors that capture changes in brightness.
*   **Action Recognition**: Classifying actions from sequential data.
*   **Model Robustness**: Testing a model's ability to maintain performance on data with real-world variations.
*   **Data Augmentation**: Artificially increasing the diversity of a training set.
*   **Domain Adaptation**: Improving a model's performance on a target domain (real-world data) by training on a source domain (lab data).
*   **v2e**: A tool for converting traditional video into synthetic event data.
