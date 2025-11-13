# Tutorial: `yolo_detect.py` - Finding Objects in the Scene

This script is our object detector. Its job is to look at an image and identify the location and type of various objects, like chairs, tables, or people. We use a popular and powerful pre-trained model called **YOLOv8** (You Only Look Once) for this task.

Like MiDaS, YOLO is a deep learning model that has been trained on a massive dataset of images, so it already knows how to recognize a wide variety of objects.

---

### The `import` Statements

```python
from ultralytics import YOLO
import os
import json
from utils import ensure_dir
```

-   **`from ultralytics import YOLO`**: This imports the `YOLO` class from the `ultralytics` library. This library provides a very easy-to-use interface for working with YOLO models.
-   **`import os`**: Our file system helper.
-   **`import json`**: We'll use this to save our detection results in a structured JSON file.
-   **`from utils import ensure_dir`**: Our helper function to create directories.

---

### The `run_yolo` Function

```python
def run_yolo(image_path, output_dir):
    """
    Runs YOLOv8 object detection on a single image and saves the results as a JSON file.
    """
    ensure_dir(output_dir)

    # ... rest of the function
```

This function takes the path to an image and an output directory. It will find all the objects in the image and save their information to a JSON file.

---

### Loading the Model and Running Detection

```python
    # Load the YOLOv8 model
    model = YOLO("yolov8n.pt")  # Using the nano model for speed

    # Run detection
    results = model(image_path)
```

-   **`model = YOLO("yolov8n.pt")`**: This line creates an instance of the YOLO model.
    -   `"yolov8n.pt"`: This is the name of the pre-trained model file. The 'n' stands for "nano", which is the smallest and fastest version of the YOLOv8 model. The first time you run this code, the `ultralytics` library will automatically download this file for you.
-   **`results = model(image_path)`**: This is how simple it is to run the detection! We just "call" the `model` object with the path to our image. The model takes care of loading the image, preparing it, running the detection, and giving us the results.

---

### Processing the Results

```python
    # Process results
    detections = []
    for r in results:
        boxes = r.boxes
        for box in boxes:
            b = box.xyxy[0].tolist()  # get box coordinates
            c = int(box.cls)
            conf = float(box.conf)
            label = model.names[c]
            detections.append({
                "label": label,
                "confidence": conf,
                "box": b
            })
```

The `results` object contains a lot of information. We need to extract the parts we care about: the object's label, its bounding box, and the model's confidence in its prediction.

-   **`detections = []`**: We create an empty list to store the information for each object we find.
-   **`for r in results:`**: The `results` can contain information for multiple images if we passed in more than one, so we loop through it. In our case, there will only be one result.
-   **`boxes = r.boxes`**: We get the `boxes` attribute from the result, which contains all the bounding box information.
-   **`for box in boxes:`**: We loop through each individual bounding box found in the image.
-   **`b = box.xyxy[0].tolist()`**: This gets the coordinates of the bounding box in the format `[x1, y1, x2, y2]`, where `(x1, y1)` is the top-left corner and `(x2, y2)` is the bottom-right corner. `.tolist()` converts it to a standard Python list.
-   **`c = int(box.cls)`**: This gets the "class" of the detected object. It's a number that corresponds to a specific type of object (e.g., 0 might be 'person', 56 might be 'chair').
-   **`conf = float(box.conf)`**: This gets the confidence score, a number between 0 and 1 that represents how sure the model is about its prediction.
-   **`label = model.names[c]`**: We use the class number `c` to look up the actual human-readable name of the object (e.g., "chair") from the model's list of names.
-   **`detections.append({...})`**: We create a dictionary to hold all the information for this one detection and add it to our `detections` list. A dictionary is a way of storing data with key-value pairs, which is very organized.

---

### Saving the Detections

```python
    # Save detections to a JSON file
    base_name = os.path.splitext(os.path.basename(image_path))[0]
    json_path = os.path.join(output_dir, f"{base_name}_detections.json")
    with open(json_path, 'w') as f:
        json.dump(detections, f, indent=4)

    print(f"Saved {len(detections)} detections to {json_path}")
```

-   **`base_name = ...`**: We get the original filename of the image without its extension, so we can create a corresponding JSON filename.
-   **`json_path = ...`**: We create the full path for our output JSON file.
-   **`with open(json_path, 'w') as f:`**: We open the file in "write mode" (`'w'`). If the file already exists, it will be overwritten.
-   **`json.dump(detections, f, indent=4)`**: This function from the `json` library writes our `detections` list to the file `f`.
    -   `indent=4`: This makes the JSON file nicely formatted and easy for humans to read by adding indentation.
-   **`print(...)`**: We print a confirmation message to the user.
