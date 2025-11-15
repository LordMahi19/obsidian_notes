# GEMINI.md: Thesis Project Context

## Project Overview

This project investigates the robustness of a pre-trained 3D-CNN event-based action recognition model. The core hypothesis is that a model trained on clean, lab-recorded data (DVS128 Gesture) will see a performance drop when evaluated against custom-recorded, real-world data. The project will then measure the extent to which this performance drop can be mitigated by augmenting the training dataset with this new real-world data.

## Background & History

This work is a pivot from an initial thesis plan that aimed to directly compare the performance of event-based cameras versus traditional RGB cameras. In the project's first stage, a `Gesture3DCNN` model was successfully developed and trained on the DVS128 Gesture dataset, achieving a peak test accuracy of over 84%. The model was also exported to ONNX and TorchScript formats.

The current research direction, proposed to create a more focused and less complicated thesis, builds directly on this success. It uses the existing high-performing model as a foundation to investigate its robustness in more realistic scenarios.

## Project Plan

The current project plan is detailed in `README.md` and involves six phases:
1.  **Baseline Model Evaluation (Completed)**
2.  **Custom Data Collection and Conversion (In Progress)**
3.  **Robustness Test 1 (Performance Drop)**
4.  **Data Augmentation & Re-training**
5.  **Robustness Test 2 (Performance Improvement)**
6.  **Analysis and Conclusion**

The technical steps for execution are documented in `execution.md`.

## Directory Structure

This `event/` directory consolidates all current and past materials for the thesis project.

*   `README.md`: The main file outlining the current research goals and the detailed 6-phase project plan.
*   `execution.md`: A technical guide with commands for executing each phase of the project.
*   `model_def.py`: The Python class definition for the `Gesture3DCNN` model.
*   `export_and_infer.py`: A script to handle model loading, exporting to ONNX/TorchScript, and running inference.
*   `baseline_test_log.md`: A log of the initial model training and performance evaluation, which established the baseline accuracy of ~84%.
*   `abstract.md`: The abstract for the thesis.
*   `thesis_structure.md`: The detailed structure and outline for the thesis.
*   `research/`: Contains literature and supporting materials.
    *   `paper_summaries.md`: Summaries of key research papers.
    *   `papers/`: PDFs of the research papers themselves.
*   `archive/`: Contains materials from the previous research direction for reference.
    *   `previous_thesis_proposal.md`: The original thesis proposal.
    *   `full_training_code.md`: The complete code and logs from the initial, more complex training runs.
    *   `thesis_mind_map.canvas`: The mind map from the original project plan.
