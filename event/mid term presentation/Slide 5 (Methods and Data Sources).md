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