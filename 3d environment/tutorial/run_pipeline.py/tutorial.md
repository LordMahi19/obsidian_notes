# Tutorial: `run_pipeline.py` - The Conductor of the Orchestra

This is the most important file in our project. It's the "main" script that you will actually run. Think of it as the conductor of an orchestra. It doesn't play any instruments itself, but it tells all the other musicians (our `src` files) what to do and in what order.

This script brings together everything we've built to create a single, functioning application.

---

### The `import` Statements

```python
import argparse
import os
import sys
import glob
```

-   **`import argparse`**: This library is used to parse command-line arguments. It's how we can give our script inputs when we run it from the terminal (like the path to the video file).
-   **`import os`**: Our file system helper, used extensively here to build paths.
-   **`import sys`**: This library gives us access to system-specific parameters and functions. We'll use it to modify the Python path.
-   **`import glob`**: This library is used to find all the pathnames matching a specified pattern. We'll use it to get a list of all our extracted frame files.

---

### The Magic of `sys.path`

```python
# Add src directory to path
sys.path.append(os.path.join(os.path.dirname(__file__), '..', 'src'))
```

This is a very important and common trick in Python projects.

-   When you `import` something, Python looks for the file in a list of directories. This list is stored in `sys.path`.
-   Our `run_pipeline.py` script is in the `scripts` folder, but all our helper functions are in the `src` folder. Python won't know to look in the `src` folder by default.
-   This line of code adds the `src` folder to Python's path.
    -   `__file__`: A special variable that holds the path to the current file (`run_pipeline.py`).
    -   `os.path.dirname(__file__)`: Gets the directory of the current file (`.../scripts`).
    -   `os.path.join(..., '..', 'src')`: This goes up one level (`..`) from `scripts` to the project root, and then goes down into `src`. The result is the full path to the `src` directory.
    -   `sys.path.append(...)`: This adds the `src` directory path to the list of places Python will look for imports.

Because of this, we can now directly import our modules from the `src` folder.

---

### Importing Our Modules

```python
from frame_extract import extract_frames
from depth_midas import run_midas
from yolo_detect import run_yolo
from depth_to_3d import depth_to_point_cloud
from fit_boxes import fit_boxes_to_detections
from renderer import render_scene
from profiler import Profiler
```

Thanks to the `sys.path` trick, we can now import all the functions and classes we wrote in the `src` directory. We are gathering all our "musicians" before the performance begins.

---

### The `main` Function

```python
def main():
    # ... all the logic ...
```

We put all of our main logic inside a function, usually called `main`. This is a standard convention that keeps the code organized.

---

### Parsing Command-Line Arguments

```python
    parser = argparse.ArgumentParser(description="3D Scene Reconstruction from Monocular Video")
    parser.add_argument("--video", required=True, help="Path to the input video file")
    args = parser.parse_args()
```

-   **`parser = argparse.ArgumentParser(...)`**: We create a parser object. The `description` is a helpful message that will be shown if the user asks for help.
-   **`parser.add_argument(...)`**: We tell the parser what arguments to expect.
    -   `"--video"`: The name of the argument. The `--` means it's an optional flag, but...
    -   `required=True`: ...we make it mandatory. The user *must* provide a video file.
    -   `help="..."`: A helpful message explaining what this argument is for.
-   **`args = parser.parse_args()`**: This line does the actual parsing. It looks at the arguments provided in the terminal, checks if they are valid, and stores them in the `args` object. We can then access our video path with `args.video`.

---

### Setting up Variables

```python
    profiler = Profiler()
    profiler.start()

    video_path = args.video
    frames_dir = "data/frames"
    depth_dir = "results/depth"
    detections_dir = "results/detections"
    exports_dir = "results/exports"
```

-   **`profiler = Profiler()`**: We create a new object from our `Profiler` class.
-   **`profiler.start()`**: We start the master stopwatch.
-   We then define a set of variables to hold the paths to all our data and results folders. This makes the code much cleaner and easier to read than typing out the full path every time.

---

### The Main Loop: Processing Each Frame

The rest of the script is a big loop that processes each frame one by one.

```python
    # Step 1: Extract frames from video
    print("Step 1: Extracting frames...")
    extract_frames(video_path, frames_dir)
    profiler.record("Frame Extraction")

    # Get the list of frames
    frame_files = sorted(glob.glob(os.path.join(frames_dir, "*.png")))
    
    # The Loop
    for frame_file in frame_files:
        # ... process one frame ...
```

1.  **Extract Frames**: First, we call `extract_frames` to slice our video into images. We then `record` how long this took.
2.  **Get Frames**: We use `glob.glob(os.path.join(frames_dir, "*.png"))` to get a list of all files in the `frames_dir` that end with `.png`. `sorted()` ensures they are in alphabetical (and therefore chronological) order.
3.  **`for frame_file in frame_files:`**: We start a loop that will execute once for every frame we extracted.

Inside the loop, for each `frame_file`, we call our functions in order:
-   `run_midas()`
-   `run_yolo()`
-   `depth_to_point_cloud()`
-   `fit_boxes_to_detections()`
-   `render_scene()`

After each step, we call `profiler.record()` to time that specific operation. Notice how we pass information from one step to the next using file paths. For example, `depth_to_point_cloud` needs the path to the depth map that `run_midas` just created.

---

### Finishing Up

```python
    print("\nPipeline complete.")
    profiler.report()
```

-   After the loop has finished processing all the frames, we print a completion message.
-   **`profiler.report()`**: We call the `report` method on our profiler object to print the final performance summary.

---

### The `if __name__ == "__main__":` block

```python
if __name__ == "__main__":
    main()
```

This is a very common and important construct in Python.

-   When you run a Python file directly from the terminal, Python sets a special internal variable, `__name__`, to the string `"__main__"`.
-   If the file is being `import`ed by another script, `__name__` is set to the name of the file (e.g., `"run_pipeline"`).

-   This `if` statement checks: "Am I being run directly by the user?" If the answer is yes, it calls the `main()` function. This ensures that the code inside `main()` only runs when you execute the script directly, not when it's imported by another script. It's the standard way to make a Python file both a reusable module and an executable script.

```