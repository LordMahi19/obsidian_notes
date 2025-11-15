**Abstract (Bachelor Thesis Proposal)**
Recent advances in neuromorphic vision sensors, such as event-based cameras, have opened new possibilities for perception in robotics. Unlike conventional RGB cameras that record images at fixed frame rates, event-based cameras asynchronously capture changes in pixel intensity, offering high temporal resolution, low latency, and reduced power consumption. These properties make them particularly attractive for fast and robust action recognition, a critical capability for human-robot interaction and autonomous systems. This thesis aims to investigate the effectiveness of event-based cameras for action recognition in comparison with conventional RGB cameras. Specifically, the study will evaluate how different action recognition models—such as convolutional neural networks, recurrent architectures, and spiking-inspired models—perform when trained and tested on event-based datasets versus RGB video datasets. Performance will be measured in terms of accuracy, computational efficiency, and robustness under challenging conditions (e.g., motion blur or low lighting).By systematically comparing event-based and frame-based approaches, this work will provide insights into which models and vision modalities are most suitable for robotic action recognition tasks. The findings are expected to contribute to the growing body of research on neuromorphic vision and highlight practical trade-offs between event-based and RGB-based perception in robotics.

## Literature Review

Here are some research papers to read for your thesis:

*   **Title:** Event-based Vision: A Survey
    *   **Link:** https://arxiv.org/abs/1904.08405
    *   **Relevance:** This paper provides a comprehensive overview of the field of event-based vision. It is an excellent starting point to understand the fundamentals of event cameras, the challenges in the field, and the existing methods for processing event data. It will help you to build a strong foundation for your thesis and to understand the context of your research.

*   **Title:** EV-ACT: A New Benchmark and Framework for Event-based Action Recognition
    *   **Link:** https://www.researchgate.net/publication/371061131_EV-ACT_A_New_Benchmark_and_Framework_for_Event-based_Action_Recognition
    *   **Relevance:** This paper is highly relevant to your thesis as it introduces a new framework and a large-scale benchmark dataset for event-based action recognition. The paper's approach of fusing multiple event representations and using a slow-fast network architecture is a state-of-the-art method that you should study. The new dataset could also be a valuable resource for your experiments.

*   **Title:** SpikMamba: When SNN meets Mamba in Event-based Human Action Recognition
    *   **Link:** https://arxiv.org/abs/2405.18655
    *   **Relevance:** This paper introduces a novel architecture that combines Spiking Neural Networks (SNNs) with Mamba, a new deep learning model. This is relevant to your thesis as it explores the use of SNN-inspired models, which you mentioned in your abstract. This paper can provide insights into cutting-edge model architectures for event-based action recognition.

additional reading from this webpage. it has tutorial on how to use spikingjelly: https://spikingjelly.readthedocs.io/zh-cn/latest/activation_based_en/basic_concept.html

## Thesis Structure (Approx. 25 pages)

Here is a recommended structure for your thesis. The page counts are suggestions to help you stay within the 25-page limit.

### **1. Title Page (1 page)**

#### demo tittles:
- Action Recognition with Event-Based vs. RGB Cameras: A Comparative Study
- Evaluating Action Recognition Models on Event-Based and Conventional Cameras
- Towards Efficient Action Recognition in Robotics: Event-Based vs. RGB Vision
- Action Recognition with Event-Based Vision
- Event-Based vs. RGB Cameras for Action Recognition
- Evaluating Action Recognition Models on Event Data
- Event-Based Vision for Robotic Action Recognition
- Comparing Event and Frame Cameras in Action Recognition
#### tittle page content:
*   **Content:** Thesis Title, Name, Student ID, Degree Program, University, Department, Date of Submission.
*   **To-Do:** Create a formal title page according to your university's guidelines.

### **2. Abstract (1 page)**
*   **Content:** A refined version of your current proposal abstract. It should be a concise summary of the entire thesis, including the problem, methods, key findings, and contributions.
*   **To-Do:** Revise the abstract after you have completed your research and have concrete results.

### **3. Table of Contents (1 page)**
*   **Content:** A list of all chapters, sections, and their corresponding page numbers.
*   **To-Do:** This can be prepared after entire thesis writing is complete. 

### **4. Chapter 1: Introduction (3-4 pages)**
*   **1.1. Background and Motivation:**
    *   **Content:** Introduce the field of action recognition in robotics and its importance. Discuss the limitations of traditional RGB cameras that motivate the need for alternative sensors.
    *   **To-Do:** Write a compelling narrative that sets the stage for your research.
*   **1.2. Problem Statement:**
    *   **Content:** Clearly state the problem you are addressing: the need for a systematic comparison of event-based and frame-based cameras for action recognition.
    *   **To-Do:** Be specific and concise.
*   **1.3. Research Questions:**
	* #### current questions in mind:
		  Which action recognition models are most effective for event-based camera data, and how do they compare to RGB-based models in terms of accuracy, efficiency, and robustness for robotic applications?
    *   **Content:** Formulate specific questions that your thesis will answer. For example:
        1.  How do different action recognition models perform on event-based versus RGB data?
        2.  What are the computational and power consumption trade-offs?
        3.  How does performance vary under challenging lighting and motion conditions?
    *   **To-Do:** Ensure your research questions are answerable within the scope of your thesis.
*   **1.4. Thesis Outline:**
    *   **Content:** Briefly describe the structure of the rest of the thesis, with a one-sentence summary of each chapter.
    *   **To-Do:** Write this at the end to ensure it accurately reflects the final structure.

### **5. Chapter 2: Background and Literature Review (6-7 pages)**
*   **2.1. Conventional Frame-Based Cameras:**
    *   **Content:** Explain the principles of frame-based cameras, their data format, and their use in action recognition.
    *   **To-Do:** Provide a brief technical overview.
*   **2.2. Neuromorphic Vision and Event-Based Cameras:**
    *   **Content:** Dive deep into the working principles of event-based cameras. Explain concepts like asynchronous events, temporal resolution, and high dynamic range. Discuss the advantages and disadvantages.
    *   **To-Do:** Use the "Event-based Vision: A Survey" paper as a primary source.
*   **2.3. Action Recognition Techniques:**
    *   **Content:** Provide an overview of the models mentioned in your abstract:
        *   Convolutional Neural Networks (CNNs)
        *   Recurrent Neural Networks (RNNs)
        *   Spiking Neural Networks (SNNs)
    *   **To-Do:** Explain how each of these architectures can be adapted for both event-based and frame-based data.
*   **2.4. Review of Key Papers:**
    *   **Content:** Summarize and critically analyze the papers from your literature review section, including the ones on EV-ACT and SpikMamba.
    *   **To-Do:** Connect these papers to your research questions and explain how they inform your work.

### **6. Chapter 3: Methodology (5-6 pages)**
*   **3.1. Dataset Selection:**
    *   **Content:** Describe the dataset(s) you will use for your experiments. If you use the EV-ACT benchmark, explain its structure and why it is suitable.
    *   **To-Do:** Justify your choice of a dataset.
*   **3.2. Experimental Setup:**
    *   **Content:** Detail the hardware (e.g., GPU, CPU) and software (e.g., programming languages, deep learning frameworks) you will use.
    *   **To-Do:** Be precise so that your experiments are reproducible.
*   **3.3. Models for Comparison:**
    *   **Content:** Provide detailed architectures of the specific CNN, RNN, and SNN models you will implement and compare. Include diagrams if possible.
    *   **To-Do:** Specify hyperparameters and training procedures.
*   **3.4. Evaluation Metrics:**
    *   **Content:** Define the metrics you will use to measure performance, such as:
        *   **Accuracy:** Top-1 and Top-5 accuracy.
        *   **Computational Efficiency:** FLOPs, inference time.
        *   **Robustness:** Performance under simulated or real challenging conditions.
    *   **To-Do:** Explain why these metrics are appropriate for your comparison.

### **7. Chapter 4: Results and Discussion (5-6 pages)**
*   **4.1. Performance Comparison:**
    *   **Content:** Present the results of your experiments using tables and figures. Compare the performance of the different models on both event-based and RGB datasets.
    *   **To-Do:** Visualize your results clearly.
*   **4.2. Analysis under Challenging Conditions:**
    *   **Content:** Show how the different systems perform under adverse conditions like motion blur and low light.
    *   **To-Do:** This is a key part of your thesis, so provide a thorough analysis.
*   **4.3. Discussion of Trade-offs:**
    *   **Content:** Discuss the practical implications of your findings. What are the trade-offs between accuracy, efficiency, and robustness for each approach?
    *   **To-Do:** Interpret your results in the context of real-world robotics applications.

### **8. Chapter 5: Conclusion (1-2 pages)**
*   **5.1. Summary of Findings:**
    *   **Content:** Briefly summarize the answers to your research questions.
    *   **To-Do:** Be direct and to the point.
*   **5.2. Contributions:**
    *   **Content:** Highlight the main contributions of your thesis to the field.
    *   **To-Do:** Explain what is novel about your work.
*   **5.3. Limitations and Future Work:**
    *   **Content:** Acknowledge the limitations of your study and suggest directions for future research.
    *   **To-Do:** Show that you have a critical understanding of your own work.

### **9. References (1-2 pages)**
*   **Content:** A list of all the papers, articles, and other resources you have cited in your thesis.
*   **To-Do:** Use a consistent citation style (e.g., IEEE, APA).
