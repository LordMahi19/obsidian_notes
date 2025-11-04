# plan 1

1. **Clone repos**: v2e, ESIM/vid2e, and a template PyTorch action-recognition training repo. [GitHub+1](https://github.com/SensorsINI/v2e?utm_source=chatgpt.com)
    
2. **Download one dataset**: e.g., DVS128 Gesture (for gesture tasks) and DHP19 (if you want paired human pose/action). [CVF Open Access+1](https://openaccess.thecvf.com/content_cvpr_2017/papers/Amir_A_Low_Power_CVPR_2017_paper.pdf?utm_source=chatgpt.com)
    
3. **Write a small script** that: (a) loads events and converts to event-frames (and/or voxel grids); (b) saves tensors ready for training. Use the SpikingJelly loader examples if helpful. [spikingjelly.readthedocs.io](https://spikingjelly.readthedocs.io/zh_CN/latest/activation_based_en/neuromorphic_datasets.html?utm_source=chatgpt.com)
    
4. **Implement a small baseline**: train a 2D CNN on RGB frames and the _same_ 2D CNN on event-frames (keeps comparison fair). Measure accuracy & inference time.
    
5. **Add one robustness test**: blur or darken RGB test set and re-evaluate.


# plan 2

The key is to shift from **static gesture classification** (which your `signlang` project does) to **dynamic action recognition** (which your thesis requires).

- **Your `signlang` project:**
    
    - **Task:** Static classification. It captures single images (`collect_imgs.py`) and classifies them (e.g., "This _pose_ is the letter 'A'").
        
    - **Features:** Hand landmarks from a single frame (implied by `handtracking.py`) or image features.
        
    - **Model:** `RandomForestClassifier`, which is great for static classification.
        
- **Your Thesis Project:**
    
    - **Task:** Action recognition. You need to classify a _sequence_ of motion (e.g., "This _action_ is the sign for 'Hello'").
        
    - **Models:** CNNs, Recurrent Architectures (RNNs/LSTMs), and Spiking-inspired models, as you mentioned in your abstract.
        

**Here is the expansion plan:**

1. **Leverage Your "Conventional RGB" Skills:**
    
    - **Data Collection:** Modify your `collect_imgs.py` script. Instead of capturing single `.jpg` files, you will capture _sequences_ of frames (i.e., short videos) for each action.
        
    - **Feature Extraction:** Your skill with MediaPipe (`handtracking.py`) is perfect here. Instead of extracting landmarks from one frame, you will run it on every frame of your video sequence. This will give you a **time-series of landmark data** (e.g., 30 frames x 21 landmarks x 3 coordinates).
        
    - **Model Upgrade:** This time-series data is the _exact_ type of input that **Recurrent Architectures (like RNNs, LSTMs, or GRUs)** are designed for. You will replace your `train_classifier.py` script. Instead of feeding single feature vectors into a Random Forest, you will feed the _sequences_ of landmarks into an RNN (using PyTorch or TensorFlow) to classify the _action_. This directly addresses the "recurrent architectures" part of your thesis.
        
    - You can also train a **3D-CNN** or **CNN-LSTM** model on the raw video sequences themselves, which fulfills another part of your abstract.
        
2. **Add the "Event-Based Camera" Expansion:**
    
    - This is the new research part of your thesis. You will need to acquire data from an event-based sensor (also called a DVS or neuromorphic camera).
        
    - You will then apply the _same_ models (RNNs, CNNs) to this event data to create a direct comparison against your RGB models.
        
    - Crucially, you will also implement the **"spiking-inspired models" (like Spiking Neural Networks - SNNs)** mentioned in your abstract, as they are specifically designed for event-based data.
        
3. **Perform the Comparison (The Thesis Core):**
    
    - You will compare the results of Path 1 (RGB) and Path 2 (Event-Based).
        
    - **Accuracy:** Which modality/model combination is most accurate?
        
    - **Efficiency:** How computationally expensive is landmark extraction + RNN vs. a 3D-CNN vs. an SNN?
        
    - **Robustness:** This is key. You can test this by adding motion blur to your RGB videos or testing in low-light conditions, as your abstract suggests. Event-based cameras are inherently robust to motion blur, and this comparison will be a central finding of your thesis.
        

### 2. Can You Use the Same Dataset?

**No, it is highly unlikely you can use your existing `signlang` dataset.**

There are two main reasons:

1. **Static vs. Dynamic:** Your current dataset (from `collect_imgs.py`) consists of _static images_ for gesture _classification_. Your thesis is on _action recognition_, which requires _dynamic videos_ or _event-streams_ of actions being performed.
    
2. **Missing Modality:** Your thesis is a _comparison_. You need a dataset that contains the _exact same actions_ captured by _both_ an RGB camera and an event-based camera simultaneously. Your current dataset is only RGB.
    

**Recommendation:** Your best approach is to find a public, pre-existing dataset that was created for this exact purpose. Many research projects have published "paired" datasets containing both RGB video and DVS/event-stream data for action recognition.

You should search for datasets like:

- **DVS128 Gesture Dataset**
    
- **ASLDVS (American Sign Language DVS)**
    
- **SL-Animals (Sign Language Animals)**
    
- Other "neuromorphic" or "event-based" action/gesture datasets.
    

Using one of these standard datasets will save you an immense amount of time in data collection and allow you to focus on the core of your thesis: implementing and comparing the models.

# plan 3
### Step 4: Pillar 2 - Event-Based Recognition (The Novel Work)

Now, you will use the DVS128 dataset to implement the "neuromorphic" models.

**Path A: Convolutional Architecture (Direct Comparison to Pillar 1, Path B)**

1. **Data Loader:** Use `tonic` to create a PyTorch `DataLoader` for the DVS128 dataset.
    
2. **Transform:** Apply the `tonic.transforms.ToFrame` transform to convert the event streams into "event-frame videos." The resulting tensor will have a shape like `(Time, 2, 128, 128)`, where the 2 channels are for "on" (positive) and "off" (negative) events.
    
3. **Model:** Use the _exact same 3D-CNN architecture_ you built in `Pillar 1, Path B`.
    
4. **Training:** Train this model on the event-frames. You now have a perfect comparison: the _same model_ trained on _RGB data_ vs. _event-frame data_.
    

**Path B: Spiking-Inspired Model (as per your abstract)**

1. **Data Loader:** Use `snnTorch`'s built-in data loader, which is optimized for SNNs (`snntorch.spikevision.spikedata.DVSGesture`). It will handle converting events into sparse spike tensors.
    
2. **Model:** Build a **Convolutional Spiking Neural Network (CSNN)**.
    
    - Follow the `snnTorch` gesture recognition tutorial, which uses this exact dataset.
        
    - The architecture will be a stack of `Conv2d` layers followed by `snnTorch.Leaky` (spiking) neurons and `MaxPool2d` layers, ending in a classifier. A documented architecture is `12C5-MP2–32C5-MP2–800FC11`.
        
3. **Training:** Train the SNN. This is the most novel part of your thesis and directly addresses the "spiking-inspired models" requirement.
    