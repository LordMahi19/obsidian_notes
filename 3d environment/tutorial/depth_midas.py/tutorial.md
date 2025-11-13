# Tutorial: `depth_midas.py` - Seeing in 3D with a Single Eye

This script is where we perform a bit of computer vision magic. We take a flat, 2D image and estimate the distance of every object in it from the camera. This is called **monocular depth estimation**. The output is a "depth map", which is an image where the color of each pixel represents its distance (e.g., white for close, black for far).

We use a powerful, pre-trained model called **MiDaS** to do this. A pre-trained model is like a student who has already studied millions of examples and is now an expert. We don't have to train it ourselves; we just need to use its knowledge.

---

### The `import` Statements

```python
import cv2
import torch
import numpy as np
import os
from utils import ensure_dir
```

-   **`import cv2`**: We import OpenCV again, this time to read our image files and to do some image manipulations.
-   **`import torch`**: This is one of the most popular libraries for deep learning. MiDaS is built using PyTorch, so we need this library to load and run the model.
-   **`import numpy as np`**: NumPy is a fundamental library for numerical computing in Python. It's great at handling large arrays of numbers, which is what images and depth maps are.
-   **`import os`**: Our trusty file system helper.
-   **`from utils import ensure_dir`**: We import our helper function to make sure our output directory exists.

---

### The `run_midas` Function

```python
def run_midas(image_path, output_dir):
    """
    Runs the MiDaS model to estimate depth for a single image.
    """
    ensure_dir(output_dir)

    # ... rest of the function
```

This function takes the path to an image and an output directory as input. Its goal is to create a depth map for that image and save it.

---

### Loading the MiDaS Model

```python
    # Load the MiDaS model
    try:
        model_type = "MiDaS_small"
        midas = torch.hub.load("intel-isl/MiDaS", model_type)
    except Exception as e:
        # ... error handling ...
```

-   **`model_type = "MiDaS_small"`**: MiDaS comes in different sizes. We choose the "small" version because it's faster, which is good for our goal of a lightweight pipeline.
-   **`midas = torch.hub.load("intel-isl/MiDaS", model_type)`**: This is the key line for loading the model. `torch.hub.load()` is a feature of PyTorch that allows you to easily download and load pre-trained models from the internet (in this case, from GitHub).
    -   `"intel-isl/MiDaS"`: The GitHub repository where the MiDaS model is hosted.
    -   `model_type`: The specific model we want to load from that repository.
-   **`try...except`**: This is an error handling block. We wrap the model loading in a `try` block because it relies on an internet connection. If something goes wrong (like no internet), the code in the `except` block will run, printing an error message instead of crashing the program.

---

### Setting up the Model and Device

```python
    # Move model to GPU if available
    device = torch.device("cuda") if torch.cuda.is_available() else torch.device("cpu")
    midas.to(device)
    midas.eval()
```

-   **`device = ...`**: This line checks if your computer has a compatible NVIDIA GPU (which PyTorch calls "cuda").
    -   `torch.cuda.is_available()`: Returns `True` if a GPU is available.
    -   If a GPU is available, we set `device` to `"cuda"`. Otherwise, we set it to `"cpu"`.
-   **`midas.to(device)`**: Deep learning models can run on either the CPU or the GPU. GPUs are much, much faster for this kind of work. This line moves the MiDaS model to the selected device (preferably the GPU).
-   **`midas.eval()`**: This tells the model that we are in "evaluation mode". This is important because some models behave differently during training (when they are learning) versus evaluation (when they are making predictions).

---

### Preparing the Image

```python
    # Load the appropriate transform
    midas_transforms = torch.hub.load("intel-isl/MiDaS", "transforms")
    transform = midas_transforms.small_transform if model_type == "MiDaS_small" else midas_transforms.dpt_transform

    # Read and transform the input image
    img = cv2.imread(image_path)
    img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    input_batch = transform(img).to(device)
```

-   **`midas_transforms = ...`**: The MiDaS model expects the input image to be in a specific format (e.g., a certain size, with pixel values in a certain range). This line loads a set of "transforms" that will prepare our image for the model.
-   **`img = cv2.imread(image_path)`**: We read the image file from disk.
-   **`img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)`**: OpenCV reads images in BGR format (Blue, Green, Red), but PyTorch models usually expect RGB (Red, Green, Blue). This line converts the color channels to the correct order.
-   **`input_batch = transform(img).to(device)`**: This applies the transform to our image, which prepares it for the model. The `.to(device)` part moves the prepared image data to the same device (CPU or GPU) as the model.

---

### Making the Prediction

```python
    with torch.no_grad():
        prediction = midas(input_batch)
        prediction = torch.nn.functional.interpolate(
            prediction.unsqueeze(1),
            size=img.shape[:2],
            mode="bicubic",
            align_corners=False,
        ).squeeze()
```

-   **`with torch.no_grad():`**: This is a performance optimization. It tells PyTorch that we are not training the model, so it doesn't need to calculate gradients (which are only needed for learning).
-   **`prediction = midas(input_batch)`**: This is where the actual prediction happens! We "call" the `midas` model with our prepared image as input. The model outputs its prediction, which is the depth map.
-   **`prediction = torch.nn.functional.interpolate(...)`**: The output from the model might be a different size than our original image. This line resizes the prediction back to the original image's dimensions.

---

### Saving the Results

```python
    depth_map = prediction.cpu().numpy()

    # Save the depth map as a .npy file
    base_name = os.path.splitext(os.path.basename(image_path))[0]
    npy_path = os.path.join(output_dir, f"{base_name}_depth.npy")
    np.save(npy_path, depth_map)

    # Save the depth map as a visual image
    depth_map_visual = cv2.normalize(depth_map, None, 255,0, cv2.NORM_MINMAX, cv2.CV_8U)
    depth_map_visual = cv2.cvtColor(depth_map_visual, cv2.COLOR_GRAY2BGR)
    png_path = os.path.join(output_dir, f"{base_name}_depth.png")
    cv2.imwrite(png_path, depth_map_visual)

    print(f"Saved depth map to {npy_path} and {png_path}")
```

-   **`depth_map = prediction.cpu().numpy()`**: The prediction from the model is a PyTorch tensor on the GPU (if available). We move it back to the CPU (`.cpu()`) and convert it to a NumPy array (`.numpy()`) so we can work with it using NumPy and OpenCV.
-   **`np.save(...)`**: We save the raw `depth_map` data to a `.npy` file. This is a NumPy-specific format that preserves the numerical data accurately, which is essential for the next step (point cloud generation).
-   **`cv2.normalize(...)`**: To save a human-readable image, we first need to convert the depth values (which can be any range of numbers) to a visual range (0-255). `cv2.normalize` does this by scaling the values.
-   **`cv2.imwrite(...)`**: We save the normalized, visual depth map as a PNG image. This is just for us to look at and verify that the depth estimation is working.
-   **`print(...)`**: Finally, we let the user know where the files were saved.
