# Title: Improving Robustness of Event-Based Models

---

### **Front Matter**

*   **Title Page**
    *   Title: Improving the Robustness of Event-Based Gesture Recognition Models through Real-World Data Augmentation
    *   Author: [Your Name]
    *   Institution, Degree, Date
*   **Abstract (1 page)**
    *   *Use the content from `abstract.md`.*
*   **Acknowledgements (1 page)**
    *   Acknowledge supervisors, colleagues, family, and any funding sources.
*   **Table of Contents (1-2 pages)**
*   **List of Figures (1 page)**
*   **List of Tables (1 page)**

---

### **Chapter 1: Introduction (3-4 pages)**

*   **1.1. The Promise of Neuromorphic Vision**
    *   Introduction to event-based cameras (Dynamic Vision Sensors - DVS).
    *   Core principles: asynchronous, sparse, high temporal resolution, high dynamic range.
    *   Advantages over traditional frame-based cameras, especially for low-power, high-speed applications.
*   **1.2. The "Lab-to-Real" Domain Gap**
    *   Discuss the common machine learning problem where models trained on clean, curated datasets fail in uncontrolled, real-world environments.
    *   Introduce the concept of model brittleness and lack of generalization.
*   **1.3. Problem Statement**
    *   State the central problem: A high-performing 3D-CNN model, trained on the clean DVS128 Gesture dataset, is expected to be non-robust against real-world variations in lighting, viewpoint, and background.
*   **1.4. Research Question and Hypothesis**
    *   **Primary Research Question:** To what extent can this performance degradation be mitigated by augmenting the training dataset with new, custom-recorded real-world data?
    *   **Hypothesis:** Augmenting the training set with varied, realistic data will significantly improve the model's generalization and performance on a test set containing similar real-world challenges.
*   **1.5. Scope and Delimitations**
    *   Define the boundaries of the research:
        *   Focus on a single model architecture (`Gesture3DCNN`).
        *   Focus on a single primary dataset (DVS128 Gesture).
        *   The augmentation technique is limited to the addition of custom-recorded data converted via `v2e`.
        *   Other architectures (e.g., SNNs) or augmentation methods are not explored.
*   **1.6. Thesis Outline**
    *   Briefly describe the structure of the remaining chapters.

---

### **Chapter 2: Background and Literature Review (6-7 pages)**

*   **2.1. Fundamentals of Event-Based Vision**
    *   **2.1.1. Dynamic Vision Sensor (DVS) Technology:** A deeper explanation of the hardware and how it generates events based on brightness changes.
    *   **2.1.2. Event Data Representation and Processing:** Discuss the `(x, y, t, p)` structure of event streams and common representations for deep learning (e.g., event volumes, voxel grids).
*   **2.2. Deep Learning for Event-Based Action Recognition**
    *   Survey of modern approaches, contrasting Spiking Neural Networks (SNNs) with conventional Artificial Neural Networks (ANNs).
    *   Justify the use of 3D-CNNs for their ability to naturally process spatio-temporal data.
*   **2.3. Benchmark Datasets for Gesture Recognition**
    *   **2.3.1. The DVS128 Gesture Dataset:** A detailed description of the dataset, its collection methodology, classes, and its limitations (i.e., its "clean" nature).
    *   **2.3.2. Other Neuromorphic Datasets:** Briefly mention other relevant datasets (e.g., DailyDVS, DHP19) to contextualize the field.
*   **2.4. Domain Adaptation and Data Augmentation**
    *   Review the role of data augmentation in improving model robustness in traditional computer vision.
    *   Discuss the specific challenge of the "lab-to-real" gap in event-based vision.
*   **2.5. Synthetic Event Generation from Video**
    *   Introduce the concept of generating event data from conventional video.
    *   **2.5.1. The `v2e` Tool:** Explain its purpose, underlying model, and why it is a suitable tool for this project's goal of creating realistic, varied data without requiring a physical DVS camera for every scenario.
*   **2.6. Research Gap and Contribution**
    *   Summarize the literature to highlight the specific gap this thesis addresses: a systematic, quantitative study on improving a pre-trained event-based model's robustness via a practical, accessible data augmentation workflow.

---

### **Chapter 3: Methodology (7-8 pages)**

*   **3.1. Overall Research Framework**
    *   Present a high-level flowchart of the six-phase project plan (from `README.md`).
    *   This diagram will visually guide the reader through the entire experimental process.
*   **3.2. Baseline Model and Environment**
    *   **3.2.1. The `Gesture3DCNN` Architecture:** Provide a detailed description of the model's layers, including filter sizes, strides, and activation functions. Include an architectural diagram.
    *   **3.2.2. Baseline Performance Evaluation (Phase 1):** Describe the initial experiment to confirm the model's performance (~84% accuracy) on the original DVS128 Gesture test set. This result serves as the primary benchmark.
*   **3.3. Custom Real-World Dataset Generation (Phase 2)**
    *   **3.3.1. Data Recording Protocol:** Detail the procedure for recording new data with a standard RGB camera.
        *   **Target Gestures:** List the 11 gestures from the DVS128 dataset.
        *   **Recording Conditions:** Provide a table summarizing the variations introduced (Angles, Distances, Lighting, Backgrounds, Speed).
    *   **3.3.2. Video-to-Event Conversion (Phase 2, cont.)**
        *   Detail the `v2e` conversion process.
        *   Specify and justify the key parameters used (`dvs_resolution=128x128`, contrast thresholds, etc.).
*   **3.4. Experimental Design**
    *   **3.4.1. Experiment 1: Quantifying Performance Degradation (Phase 3)**
        *   Describe the creation of the "Augmented Test Set" (original test data + all new custom data).
        *   Explain the process of evaluating the *original baseline model* on this set.
    *   **3.4.2. Experiment 2: Model Re-training with Augmentation (Phase 4)**
        *   Describe the creation of the "Augmented Training Set" (original training data + new custom data).
        *   Detail the re-training parameters (optimizer, learning rate, number of epochs).
    *   **3.4.3. Experiment 3: Evaluating Performance Improvement (Phase 5)**
        *   Explain the process of evaluating the *newly re-trained model* on the same "Augmented Test Set".
*   **3.5. Evaluation Metrics**
    *   Define the metrics that will be used for all evaluations: Overall Accuracy, Per-Class Precision, Recall, F1-Score, and Confusion Matrices.

---

### **Chapter 4: Results and Analysis (5-6 pages)**

*   **4.1. Result Set 1: Baseline Performance**
    *   Re-state the performance of the original model on the original DVS128 test set.
    *   Include a table of metrics and a confusion matrix.
*   **4.2. Result Set 2: Degraded Performance on Real-World Data**
    *   Present the results from Experiment 1 (original model on augmented test set).
    *   Use tables and a confusion matrix to show the significant drop in performance.
    *   Analyze which gestures were most misclassified and correlate this with the introduced variations.
*   **4.3. Result Set 3: Improved Performance after Re-training**
    *   Present the results from Experiment 3 (re-trained model on augmented test set).
    *   Use tables and a confusion matrix to show the improved performance.
*   **4.4. Comparative Analysis**
    *   Directly compare the three result sets.
    *   Use bar charts to provide a clear visual comparison of overall accuracy and F1-scores across the three stages (Baseline, Degraded, Improved).
    *   Analyze the change in per-class accuracy to identify which gestures benefited most from augmentation.

---

### **Chapter 5: Discussion (3-4 pages)**

*   **5.1. Interpretation of Findings**
    *   **5.1.1. The Impact of the Lab-to-Real Gap:** Discuss the significance of the performance drop observed in Result Set 2. Why did the model fail?
    *   **5.1.2. The Efficacy of the Augmentation Strategy:** Analyze the performance lift in Result Set 3. How effective was the re-training? Did it fully recover the initial loss?
*   **5.2. Answering the Research Question**
    *   Provide a direct, quantitative answer to the primary research question based on the results from Chapter 4. (e.g., "The augmentation strategy mitigated the performance drop by X%...").
*   **5.3. Implications for Real-World Neuromorphic Systems**
    *   Discuss the practical implications of the findings. This workflow provides a cost-effective method to make event-based models more robust and deployable.
*   **5.4. Limitations of the Study**
    *   Acknowledge the study's limitations:
        *   The use of synthetic (`v2e`) vs. native event data.
        *   The scope being limited to one model and dataset.
        *   The scale of the custom-recorded data.

---

### **Chapter 6: Conclusion and Future Work (2-3 pages)**

*   **6.1. Summary of the Research**
    *   Provide a concise summary of the entire project: the problem, the method, and the key results.
*   **6.2. Conclusion**
    *   State the final conclusion clearly: Real-world data augmentation via video conversion is a viable and effective strategy for improving the robustness of event-based recognition models.
*   **6.3. Recommendations for Future Work**
    *   Suggest potential future research directions:
        *   Testing the methodology on different models (especially SNNs) and tasks.
        *   Validating the results with a real DVS camera.
        *   Exploring more advanced video-to-event synthesis techniques.
        *   Investigating online or continual learning systems that adapt to new data automatically.

---

### **Back Matter**

*   **References (2-3 pages)**
    *   A complete list of all cited academic papers, books, and online resources.
*   **Appendices (Optional)**
    *   **Appendix A:** Python code for the `Gesture3DCNN` model definition.
    *   **Appendix B:** Example `v2e` command-line usage.
    *   **Appendix C:** Full-page versions of key figures or tables (e.g., confusion matrices).
