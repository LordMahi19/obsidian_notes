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
