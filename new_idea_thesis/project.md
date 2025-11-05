# Project Plan: Investigating Model Robustness with Real-World Event Data

This document outlines the step-by-step process for implementing the new thesis idea, focusing on evaluating and improving the robustness of an event-based action recognition model against real-world data variations.

## Phase 1: Baseline Model Evaluation

1.  **Load Pre-trained Model:**
    *   Load the `Gesture3DCNN` model from `models/dvsgesture_3dcnn_best.pth`.
    *   Ensure the model architecture defined in `model_def.py` is consistent with the saved checkpoint.

2.  **Evaluate on Original Test Set:**
    *   Use the existing PyTorch `DataLoader` for the DVS128 Gesture dataset.
    *   Run inference on the original DVS128 Gesture test set.
    *   Collect and record comprehensive metrics:
        *   Overall Accuracy
        *   Precision, Recall, F1-score per class
        *   Confusion Matrix
    *   Document these results as the "Baseline Performance."

## Phase 2: Custom Data Collection and Conversion

1.  **Identify Target Gestures:**
    *   List the specific gestures from the DVS128 dataset that will be re-recorded (e.g., hand clap, wave, arm cross).

2.  **Record Custom Videos:**
    *   Using a standard RGB camera (e.g., smartphone, webcam), record multiple instances of each target gesture.
    *   **Introduce Variations:**
        *   **Angles:** Record from different viewpoints (front, side, slightly above/below).
        *   **Distances:** Vary the distance of the subject from the camera.
        *   **Lighting:** Record under different lighting conditions (bright, dim, uneven).
        *   **Backgrounds:** Use varied backgrounds (cluttered, plain).
        *   **Speed:** Vary the speed of the gesture execution.
        *   **Subject Variation:** If possible, have different individuals perform the gestures.
    *   Ensure video quality is sufficient for `v2e` conversion.

3.  **Convert Videos to Event Data using `v2e`:**
    *   Install and configure the `v2e` tool (if not already done).
    *   For each recorded RGB video, use `v2e` to generate a corresponding event stream (e.g., `.aedat4`, `.hdf5`).
    *   Experiment with `v2e` parameters (e.g., contrast threshold, event rate) to generate realistic event data.
    *   Store the generated event data in a structured directory (e.g., `custom_event_data/`).

## Phase 3: Robustness Test 1 - Performance Degradation

1.  **Integrate Custom Data into Test Set:**
    *   Modify the existing data loading script or create a new one to combine:
        *   The original DVS128 Gesture test set.
        *   The newly generated custom event data.
    *   Ensure proper labeling for the custom data.
    *   Create a new PyTorch `DataLoader` for this "Augmented Test Set."

2.  **Evaluate Baseline Model on Augmented Test Set:**
    *   Load the *original* pre-trained `Gesture3DCNN` model (from Phase 1).
    *   Run inference on the "Augmented Test Set."
    *   Collect and record comprehensive metrics (accuracy, precision, recall, F1-score, confusion matrix).
    *   Compare these results with the "Baseline Performance" to quantify the performance drop due to real-world variations.
    *   Document this as "Performance with Custom Test Data (Pre-Augmentation Training)."

## Phase 4: Data Augmentation and Re-training

1.  **Integrate Custom Data into Training Set:**
    *   Modify the existing data loading script or create a new one to combine:
        *   The original DVS128 Gesture training set.
        *   The newly generated custom event data.
    *   Ensure proper labeling for the custom data.
    *   Create a new PyTorch `DataLoader` for this "Augmented Training Set."

2.  **Re-train the Model:**
    *   Initialize a new `Gesture3DCNN` model (or load the baseline model and continue training).
    *   Train the model using the "Augmented Training Set."
    *   Utilize the sophisticated training loop (learning rate scheduling, weight decay, early stopping) established previously.
    *   Monitor training progress and validation accuracy.
    *   Save the best-performing model checkpoint (e.g., `dvsgesture_3dcnn_augmented_best.pth`).

## Phase 5: Robustness Test 2 - Performance Improvement

1.  **Evaluate Re-trained Model on Augmented Test Set:**
    *   Load the newly re-trained `Gesture3DCNN` model (from Phase 4).
    *   Run inference on the *same* "Augmented Test Set" used in Phase 3.
    *   Collect and record comprehensive metrics (accuracy, precision, recall, F1-score, confusion matrix).
    *   Compare these results with "Performance with Custom Test Data (Pre-Augmentation Training)" and the "Baseline Performance."
    *   Document this as "Performance with Custom Test Data (Post-Augmentation Training)."

## Phase 6: Analysis and Conclusion

1.  **Compare Results:**
    *   Analyze the three sets of performance metrics:
        *   Baseline Performance (original model, original test set)
        *   Performance with Custom Test Data (Pre-Augmentation Training)
        *   Performance with Custom Test Data (Post-Augmentation Training)
    *   Quantify the performance drop and subsequent recovery/improvement.

2.  **Draw Conclusions:**
    *   Discuss whether injecting more real-world-like data into the training set improved the model's accuracy and generalization to varied conditions.
    *   Address the hypothesis that the DVS128 Gesture dataset's lab environment data might not generalize well to real-world scenarios.
    *   Identify limitations and potential future work.

3.  **Thesis Write-up:**
    *   Integrate all findings, methodologies, and conclusions into the thesis document.
