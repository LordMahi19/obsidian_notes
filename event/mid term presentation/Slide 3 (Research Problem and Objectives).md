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