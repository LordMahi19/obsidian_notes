Below is a complete script for your 20-minute midterm presentation on my bachelor thesis: "Improving Robustness of Event-Based Models." I've structured it to fit approximately 20 minutes, assuming a moderate speaking pace (about 120-150 words per minute) and time for slide transitions, pauses, and visuals. The total word count is around 2,500, which should clock in at 18-20 minutes when delivered naturally.

The script is divided into sections with timing estimates, suggested slide content (e.g., titles, bullet points, or visuals), and speaker notes for delivery. Use simple slides (e.g., via PowerPoint or Google Slides) with minimal text—focus on visuals like diagrams, code snippets, dataset images, and results charts to keep the audience engaged. Practice timing to adjust as needed.

---

**Presentation Script: Midterm Update on Bachelor Thesis - Improving Robustness of Event-Based Models**

**[[Slide 1 (title slide)]]**

*Title: Improving Robustness of Event-Based Models: Midterm Presentation*  
*Subtitle: Investigating Event-Based Action Recognition*  
*Your Name, Date (November 15, 2025), Supervisor/Department*  
*Visual: Background image of a DVS camera or event stream visualization*

Good [morning/afternoon], everyone. Thank you for joining my midterm presentation on my bachelor thesis titled "Improving Robustness of Event-Based Models." My name is [Your Name], and today I'll cover the background, research problem and objectives, scope and limitations, methods and data sources, my progress so far, and my plan for completing the thesis. This should take about 20 minutes, and I'll be happy to take questions at the end.

*(Timing: 30 seconds. Transition to next slide.)*

---

**[[Slide 2 (Background Information and Context)]]**  

*Title: Background on Event-Based Vision*  
*Bullets:*  
- Traditional cameras: Frame-based, capture full images at fixed rates  
- Event-based cameras (DVS): Asynchronous, event-driven, only detect changes  
- Advantages: Low power, high dynamic range, low latency  
- Applications: Robotics, autonomous driving, gesture recognition  
*Visuals: Side-by-side comparison of RGB frame vs. event stream; timeline of event-based tech evolution*

Let's start with the background. Traditional cameras, like those in our smartphones, are frame-based—they capture complete images at fixed intervals, say 30 frames per second. This works well in controlled settings but generates a lot of redundant data, especially in static scenes, leading to high power use and latency.

In contrast, event-based cameras, or Dynamic Vision Sensors (DVS), operate asynchronously. They don't capture full frames; instead, each pixel independently detects brightness changes and outputs "events" only when something moves or light shifts. Each event includes the pixel location, timestamp, and polarity (increase or decrease in brightness). This makes them ideal for real-world applications where efficiency matters.

Event-based vision draws from neuromorphic engineering, mimicking how biological eyes work. Key advantages include ultra-low power consumption—often under 10 mW—high dynamic range (up to 140 dB vs. 60 dB for RGB cameras), and microsecond latency. This is crucial for fields like robotics, autonomous vehicles, and wearable devices.

To ground this in research, I've reviewed several key papers. For instance, the 2017 paper "A Low Power, Fully Event-Based Gesture Recognition System" by Amir et al. introduced the DVS128 Gesture dataset and demonstrated a hardware system achieving 96.5% accuracy with under 200 mW power—foundational for gesture recognition. Other works, like the DailyDVS-200 benchmark, push for larger datasets using transformers, while DHP19 explores 3D pose estimation with multi-view DVS data. Tools like ESIM and v2e simulators address data scarcity by generating synthetic events from videos.

This context sets the stage: event-based models promise efficiency, but their robustness in messy real-world scenarios needs improvement.

*(Timing: 4 minutes. Speak conversationally, point to visuals. Transition: "With this foundation, let's define the problem.")*

----

**[[Slide 3 (Research Problem and Objectives)]]**  

*Title: Research Problem and Objectives*  
*Bullets:*  
- Problem: Models trained on clean lab data underperform in real-world variations (e.g., lighting, angles)  
- Hypothesis: Augmenting with custom real-world data mitigates performance drop  
- Objectives:  
  - Evaluate baseline on clean data  
  - Test degradation on augmented data  
  - Retrain and measure improvement  
*Visual: Flowchart of hypothesis; icons for variations (light bulb for lighting, etc.)*

Now, the research problem. Event-based models, like those for action recognition, are often trained on clean, lab-recorded datasets. For example, the DVS128 Gesture dataset was captured in controlled indoor settings with consistent lighting and backgrounds. But in real life, gestures happen in varied conditions—different angles, distances, lighting, cluttered backgrounds, and speeds. My core hypothesis is that a model trained on this clean data will experience a significant performance drop when tested on real-world data with these variations.

The key research question is: To what extent can this drop be mitigated by augmenting the training dataset with custom-recorded, real-world data?

My objectives are focused: First, establish a baseline performance on the original DVS128 dataset. Second, collect and integrate custom data to create an augmented test set, then quantify the degradation. Third, retrain the model on an augmented training set and evaluate improvements in generalization.

This is a pivot from my initial broader idea of comparing RGB and event-based cameras, which was too ambitious for a bachelor thesis. The current focus is narrower, more feasible, and directly addresses robustness—a key challenge in deploying event-based systems.

*(Timing: 3 minutes. Emphasize the pivot for honesty. Transition: "Of course, this focus comes with boundaries.")*

----

**[[Slide 4 (Scope and Limitations)]]**  

*Title: Scope and Limitations*  
*Bullets:*  
- Scope: Focus on DVS128 Gesture dataset; 3D-CNN model; Data augmentation via v2e simulation  
- Limitations:  
  - No real DVS hardware (simulation only)  
  - Limited custom data scale (time/resource constraints)  
  - Single model architecture (no extensive comparisons)  
  - Ethical: No sensitive data involved  
*Visual: Boundary diagram (in-scope vs. out-of-scope circles)*

In terms of scope, this thesis is limited to the DVS128 Gesture dataset, which has 11 gesture classes from 29 subjects. I'll use a 3D Convolutional Neural Network (3D-CNN) for classification, as it's effective for spatio-temporal event data. Data augmentation will involve recording RGB videos with real-world variations and converting them to events using the v2e tool, which simulates DVS output.

Limitations include not having access to actual DVS hardware—I'm relying on simulation, which might not capture all sensor nuances like noise. Custom data collection will be modest, perhaps 50-100 samples per gesture, due to time and resources as a solo student project. I won't compare multiple architectures extensively or explore advanced models like spiking neural networks in depth, though I've reviewed SpikingJelly for potential extensions. Ethically, there's no sensitive data—just gestures—so privacy isn't an issue, but I'll ensure diverse subjects if possible to avoid bias.

Overall, this keeps the project achievable within the thesis timeline.

*(Timing: 2 minutes. Be upfront about limitations to show realism. Transition: "Now, how am I approaching this?")*


----

**[[Slide 5 (Methods and Data Sources)]]**  

*Title: Methods and Data Sources*  
*Bullets:*  
- Data: DVS128 Gesture (1,342 samples, 11 classes); Custom RGB videos converted via v2e  
- Model: Gesture3DCNN (3D conv layers, PyTorch)  
- Pipeline: Tonic for data loading; Training with Adam optimizer; Metrics: Accuracy, F1, confusion matrix  
- Tools: v2e for simulation; Matplotlib/Seaborn for visualization  
*Visuals: Code snippet from your baseline; Diagram of video -> events -> model pipeline*

For methods, I'm using a structured pipeline. The primary data source is the DVS128 Gesture dataset, with 1,078 training and 264 test samples across 11 classes like hand clapping and arm rolls. I'll augment it with custom data: recording RGB videos of these gestures with variations in angles, distances, lighting, backgrounds, and speeds. These videos will be converted to event streams (.aedat4 format) using v2e, simulating a 128x128 DVS sensor with thresholds around 0.2 for event generation.

The model is a custom 3D-CNN called Gesture3DCNN, implemented in PyTorch. It processes event frames (60 time bins) through convolutional layers, max pooling, and a fully connected output for 11 classes. Training uses cross-entropy loss, Adam optimizer at 1e-3 learning rate, and mixed precision for efficiency. Evaluation includes accuracy, per-class F1 scores, and confusion matrices to pinpoint weaknesses.

Libraries like Tonic handle event data loading and framing, while v2e enables simulation. This draws from papers like the SpikingJelly tutorial for event handling and ESIM for simulation rationale.

*(Timing: 4 minutes. Show a quick code demo if time allows, but keep it high-level. Transition: "So, what have I accomplished?")*

----

**[[Slide 6 (Progress So Far)]]**  

*Title: Methods and Data Sources*  
*Bullets:*  
- Data: DVS128 Gesture (1,342 samples, 11 classes); Custom RGB videos converted via v2e  
- Model: Gesture3DCNN (3D conv layers, PyTorch)  
- Pipeline: Tonic for data loading; Training with Adam optimizer; Metrics: Accuracy, F1, confusion matrix  
- Tools: v2e for simulation; Matplotlib/Seaborn for visualization  
*Visuals: Code snippet from your baseline; Diagram of video -> events -> model pipeline*

For methods, I'm using a structured pipeline. The primary data source is the DVS128 Gesture dataset, with 1,078 training and 264 test samples across 11 classes like hand clapping and arm rolls. I'll augment it with custom data: recording RGB videos of these gestures with variations in angles, distances, lighting, backgrounds, and speeds. These videos will be converted to event streams (.aedat4 format) using v2e, simulating a 128x128 DVS sensor with thresholds around 0.2 for event generation.

The model is a custom 3D-CNN called Gesture3DCNN, implemented in PyTorch. It processes event frames (60 time bins) through convolutional layers, max pooling, and a fully connected output for 11 classes. Training uses cross-entropy loss, Adam optimizer at 1e-3 learning rate, and mixed precision for efficiency. Evaluation includes accuracy, per-class F1 scores, and confusion matrices to pinpoint weaknesses.

Libraries like Tonic handle event data loading and framing, while v2e enables simulation. This draws from papers like the SpikingJelly tutorial for event handling and ESIM for simulation rationale.

*(Timing: 4 minutes. Show a quick code demo if time allows, but keep it high-level. Transition: "So, what have I accomplished?")*

---

**[[Slide 7 (Plan for Completing the Thesis in Part 2)]]**  

*Title: Completion Plan*  
*Bullets:*  
- Phase 2: Collect/convert custom data (1-2 weeks)  
- Phase 3: Test degradation (1 week)  
- Phase 4: Retrain model (1-2 weeks)  
- Phase 5: Evaluate improvement (1 week)  
- Phase 6: Analyze/write-up (2-3 weeks)  
- Milestones: Draft by [date], Final submission by [thesis deadline]  
*Visual: Gantt chart or timeline*

For the remaining work, I'll follow the six-phase plan. Phase 2: Finish recording 50+ videos per gesture with variations and convert them via v2e—aiming for completion in 1-2 weeks. Phase 3: Create an augmented test set and quantify performance drop with the baseline model (1 week).

Phase 4: Augment the training set and retrain (1-2 weeks, monitoring for overfitting). Phase 5: Evaluate the retrained model on the augmented test (1 week). Finally, Phase 6: Analyze metrics, discuss hypothesis, and write the thesis (2-3 weeks).

I'll incorporate potential extensions like basic augmentations or SNN trials if time allows. Milestones include a full draft by mid-December and final submission by the thesis deadline. This timeline accounts for holidays and buffers for debugging.

*(Timing: 2 minutes. End positively. Transition to conclusion.)*

---

**[[Slide 8 (Conclusion and Q&A)]]**  

*Title: Conclusion*  
*Bullets:*  
- Summary: Focused on robustness via augmentation  
- Next: Complete data collection and experiments  
- Thank you!  
*Visual: Key takeaway quote or overall flowchart*

In summary, this thesis addresses a practical gap in event-based model robustness through targeted data augmentation. I've built a strong foundation with baseline results and literature, and I'm excited to test the hypothesis in the coming weeks.

Thank you for your attention. I'd love to hear your questions or feedback.

*(Timing: 1 minute. Open floor for Q&A.)*

---
