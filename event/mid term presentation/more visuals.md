Below is the revised script for your 20-minute midterm presentation on your bachelor thesis: "Improving Robustness of Event-Based Models." I've enhanced it with more visuals to make the slides more engaging and illustrative. This includes:

- Additional diagrams, images, and charts in each slide's visual suggestions.
- Incorporation of searched images (e.g., comparisons of event streams vs. RGB, gesture examples, 3D CNN architectures, and application scenarios) to visually demonstrate concepts.
- Generated plots for the training curve and confusion matrix (based on your baseline data) for data-driven visuals.
- Suggestions for animations (e.g., fade-ins for comparisons) and icons to keep slides dynamic without overwhelming text.

The timing remains ~20 minutes. Use a tool like PowerPoint, Google Slides, or Keynote to implement these—embed the suggested images directly (I've provided sources and example renders below for reference). Practice with transitions to ensure smooth flow.

---

**Presentation Script: Midterm Update on Bachelor Thesis - Improving Robustness of Event-Based Models**

**[Slide 1: Title Slide]**  
*Title: Improving Robustness of Event-Based Models: Midterm Presentation*  
*Subtitle: Investigating Event-Based Action Recognition*  
*Your Name, Date (November 15, 2025), Supervisor/Department*  
*Visuals: Background image of a DVS camera setup; subtle animation of event sparks (red/blue dots) fading in; your university logo in the corner. Include an example DVS event stream image in the lower right for intrigue.*

[[more visuals]]



Good [morning/afternoon], everyone. Thank you for joining my midterm presentation on my bachelor thesis titled "Improving Robustness of Event-Based Models." My name is [Your Name], and today I'll cover the background, research problem and objectives, scope and limitations, methods and data sources, my progress so far, and my plan for completing the thesis. This should take about 20 minutes, and I'll be happy to take questions at the end.

*(Timing: 30 seconds. Transition to next slide with a fade effect.)*

**[Slide 2: Background Information and Context]**  
*Title: Background on Event-Based Vision*  
*Bullets:*  
- Traditional cameras: Frame-based, capture full images at fixed rates  
- Event-based cameras (DVS): Asynchronous, event-driven, only detect changes  
- Advantages: Low power, high dynamic range, low latency  
- Applications: Robotics, autonomous driving, gesture recognition  
*Visuals: Side-by-side animated comparison of RGB frame vs. event stream (fade between them); timeline infographic of event-based tech evolution (e.g., from 2000s neuromorphic sensors to modern apps); icons for advantages (battery for low power, eye for high dynamic range); embed images of real-world applications like robots and self-driving cars. Add a small video clip thumbnail if your tool supports embeds.*












Let's start with the background. Traditional cameras, like those in our smartphones, are frame-based—they capture complete images at fixed intervals, say 30 frames per second. This works well in controlled settings but generates a lot of redundant data, especially in static scenes, leading to high power use and latency.

In contrast, event-based cameras, or Dynamic Vision Sensors (DVS), operate asynchronously. They don't capture full frames; instead, each pixel independently detects brightness changes and outputs "events" only when something moves or light shifts. Each event includes the pixel location, timestamp, and polarity (increase or decrease in brightness). This makes them ideal for real-world applications where efficiency matters.

Event-based vision draws from neuromorphic engineering, mimicking how biological eyes work. Key advantages include ultra-low power consumption—often under 10 mW—high dynamic range (up to 140 dB vs. 60 dB for RGB cameras), and microsecond latency. This is crucial for fields like robotics, autonomous vehicles, and wearable devices.

To ground this in research, I've reviewed several key papers. For instance, the 2017 paper "A Low Power, Fully Event-Based Gesture Recognition System" by Amir et al. introduced the DVS128 Gesture dataset and demonstrated a hardware system achieving 96.5% accuracy with under 200 mW power—foundational for gesture recognition. Other works, like the DailyDVS-200 benchmark, push for larger datasets using transformers, while DHP19 explores 3D pose estimation with multi-view DVS data. Tools like ESIM and v2e simulators address data scarcity by generating synthetic events from videos.

This context sets the stage: event-based models promise efficiency, but their robustness in messy real-world scenarios needs improvement.

*(Timing: 4 minutes. Point to visuals during explanations; use animations to highlight comparisons. Transition: "With this foundation, let's define the problem.")*

**[Slide 3: Research Problem and Objectives]**  
*Title: Research Problem and Objectives*  
*Bullets:*  
- Problem: Models trained on clean lab data underperform in real-world variations (e.g., lighting, angles)  
- Hypothesis: Augmenting with custom real-world data mitigates performance drop  
- Objectives:  
  - Evaluate baseline on clean data  
  - Test degradation on augmented data  
  - Retrain and measure improvement  
*Visuals: Flowchart of hypothesis with icons for variations (e.g., light bulb for lighting, camera angle icon); before-after bar chart illustrating performance drop (hypothetical); embed gesture examples from DVS128 to show "clean" vs. potential "real-world" variations (use image overlays).*








Now, the research problem. Event-based models, like those for action recognition, are often trained on clean, lab-recorded datasets. For example, the DVS128 Gesture dataset was captured in controlled indoor settings with consistent lighting and backgrounds. But in real life, gestures happen in varied conditions—different angles, distances, lighting, cluttered backgrounds, and speeds. My core hypothesis is that a model trained on this clean data will experience a significant performance drop when tested on real-world data with these variations.

The key research question is: To what extent can this drop be mitigated by augmenting the training dataset with custom-recorded, real-world data?

My objectives are focused: First, establish a baseline performance on the original DVS128 dataset. Second, collect and integrate custom data to create an augmented test set, then quantify the degradation. Third, retrain the model on an augmented training set and evaluate improvements in generalization.

This is a pivot from my initial broader idea of comparing RGB and event-based cameras, which was too ambitious for a bachelor thesis. The current focus is narrower, more feasible, and directly addresses robustness—a key challenge in deploying event-based systems.

*(Timing: 3 minutes. Emphasize the pivot for honesty. Transition: "Of course, this focus comes with boundaries.")*

**[Slide 4: Scope and Limitations]**  
*Title: Scope and Limitations*  
*Bullets:*  
- Scope: Focus on DVS128 Gesture dataset; 3D-CNN model; Data augmentation via v2e simulation  
- Limitations:  
  - No real DVS hardware (simulation only)  
  - Limited custom data scale (time/resource constraints)  
  - Single model architecture (no extensive comparisons)  
  - Ethical: No sensitive data involved  
*Visuals: Boundary diagram (in-scope vs. out-of-scope circles with icons); pie chart showing time allocation for phases; simple infographic for limitations (e.g., red warning icons).*  

In terms of scope, this thesis is limited to the DVS128 Gesture dataset, which has 11 gesture classes from 29 subjects. I'll use a 3D Convolutional Neural Network (3D-CNN) for classification, as it's effective for spatio-temporal event data. Data augmentation will involve recording RGB videos with real-world variations and converting them to events using the v2e tool, which simulates DVS output.

Limitations include not having access to actual DVS hardware—I'm relying on simulation, which might not capture all sensor nuances like noise. Custom data collection will be modest, perhaps 50-100 samples per gesture, due to time and resources as a solo student project. I won't compare multiple architectures extensively or explore advanced models like spiking neural networks in depth, though I've reviewed SpikingJelly for potential extensions. Ethically, there's no sensitive data—just gestures—so privacy isn't an issue, but I'll ensure diverse subjects if possible to avoid bias.

Overall, this keeps the project achievable within the thesis timeline.

*(Timing: 2 minutes. Be upfront about limitations to show realism. Transition: "Now, how am I approaching this?")*

**[Slide 5: Methods and Data Sources]**  
*Title: Methods and Data Sources*  
*Bullets:*  
- Data: DVS128 Gesture (1,342 samples, 11 classes); Custom RGB videos converted via v2e  
- Model: Gesture3DCNN (3D conv layers, PyTorch)  
- Pipeline: Tonic for data loading; Training with Adam optimizer; Metrics: Accuracy, F1, confusion matrix  
- Tools: v2e for simulation; Matplotlib/Seaborn for visualization  
*Visuals: Detailed pipeline diagram (video -> v2e -> events -> 3D-CNN -> output); code snippet from your baseline with syntax highlighting; embed 3D CNN architecture diagram; icons for tools (e.g., Python logo).*








For methods, I'm using a structured pipeline. The primary data source is the DVS128 Gesture dataset, with 1,078 training and 264 test samples across 11 classes like hand clapping and arm rolls. I'll augment it with custom data: recording RGB videos of these gestures with variations in angles, distances, lighting, backgrounds, and speeds. These videos will be converted to event streams (.aedat4 format) using v2e, simulating a 128x128 DVS sensor with thresholds around 0.2 for event generation.

The model is a custom 3D-CNN called Gesture3DCNN, implemented in PyTorch. It processes event frames (60 time bins) through convolutional layers, max pooling, and a fully connected output for 11 classes. Training uses cross-entropy loss, Adam optimizer at 1e-3 learning rate, and mixed precision for efficiency. Evaluation includes accuracy, per-class F1 scores, and confusion matrices to pinpoint weaknesses.

Libraries like Tonic handle event data loading and framing, while v2e enables simulation. This draws from papers like the SpikingJelly tutorial for event handling and ESIM for simulation rationale.

*(Timing: 4 minutes. Show a quick code demo if time allows, but keep it high-level. Transition: "So, what have I accomplished?")*

**[Slide 6: Progress So Far]**  
*Title: Progress Update*  
*Bullets:*  
- Phase 1 Completed: Baseline model trained/evaluated (~84% test accuracy)  
- Key Results: Strong on waves/ccw arms; Weaker on air drums/rolls  
- Papers Reviewed: 5 key works (e.g., DVS128 intro, simulators)  
- Phase 2 In Progress: Planning custom recordings  
*Visuals: Line chart of training/test accuracy over epochs; heatmap confusion matrix; classification report as a table with color-coded F1 scores; timeline bar for phases completed (green for done, yellow for in progress); embed additional gesture images for context.*  
(Include the generated training curve plot here: [describe as a blue/orange line graph showing accuracy rising to 0.859 train and 0.841 test].)  
(Include the generated confusion matrix: [describe as a heatmap with diagonal dominance, off-diagonals showing confusions like air drums vs. guitar].)








Progress-wise, I've completed Phase 1: Baseline Model Evaluation. I loaded the DVS128 dataset via Tonic, framed events into 60 bins, and trained the Gesture3DCNN for 4 epochs. Training accuracy reached 85.9%, and test accuracy is 84.1%—matching literature benchmarks.

From the classification report, precision and recall vary: "Left arm counter-clockwise" is perfect at 1.00, but "Air drums" has only 0.55 precision, likely due to confusion with similar motions. The confusion matrix highlights these overlaps, which I expect real-world variations to exacerbate.

I've also reviewed five papers, building a strong literature foundation: from the DVS128 origin to simulators like ESIM and datasets like DHP19. Phase 2 is in progress—I've planned the custom video recordings and v2e setup, including directory structures and batch scripts.

This puts me on track, with solid baseline results to build upon.

*(Timing: 4 minutes. Highlight visuals; zoom in on plots during discussion. Transition: "Looking ahead...")*

**[Slide 7: Plan for Completing the Thesis in Part 2]**  
*Title: Completion Plan*  
*Bullets:*  
- Phase 2: Collect/convert custom data (1-2 weeks)  
- Phase 3: Test degradation (1 week)  
- Phase 4: Retrain model (1-2 weeks)  
- Phase 5: Evaluate improvement (1 week)  
- Phase 6: Analyze/write-up (2-3 weeks)  
- Milestones: Draft by mid-December 2025, Final submission by [thesis deadline]  
*Visuals: Gantt chart timeline with colored bars for phases; checklist icons for milestones; simple flowchart recapping all phases with arrows.*  

For the remaining work, I'll follow the six-phase plan. Phase 2: Finish recording 50+ videos per gesture with variations and convert them via v2e—aiming for completion in 1-2 weeks. Phase 3: Create an augmented test set and quantify performance drop with the baseline model (1 week).

Phase 4: Augment the training set and retrain (1-2 weeks, monitoring for overfitting). Phase 5: Evaluate the retrained model on the augmented test (1 week). Finally, Phase 6: Analyze metrics, discuss hypothesis, and write the thesis (2-3 weeks).

I'll incorporate potential extensions like basic augmentations or SNN trials if time allows. Milestones include a full draft by mid-December 2025 and final submission by the thesis deadline. This timeline accounts for holidays and buffers for debugging.

*(Timing: 2 minutes. End positively. Transition to conclusion.)*

**[Slide 8: Conclusion and Q&A]**  
*Title: Conclusion*  
*Bullets:*  
- Summary: Focused on robustness via augmentation  
- Next: Complete data collection and experiments  
- Thank you!  
*Visuals: Overall project flowchart recap; motivational image of a robust robot in a real-world scene; contact info/Q&A prompt.*  

In summary, this thesis addresses a practical gap in event-based model robustness through targeted data augmentation. I've built a strong foundation with baseline results and literature, and I'm excited to test the hypothesis in the coming weeks.

Thank you for your attention. I'd love to hear your questions or feedback.

*(Timing: 1 minute. Open floor for Q&A.)*

---

This updated script incorporates more visuals for better engagement—aim for 1-2 key images/charts per slide to avoid clutter. The rendered images above serve as examples you can download from the provided URLs and embed in your actual slides. If you need help exporting this to a slide deck format or generating more custom plots, let me know!