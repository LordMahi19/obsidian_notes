# Tutorial: `renderer.py` - Visualizing Our 3D Scene

This script brings our 3D creation to life. Its job is to take the 3D point cloud and the 3D bounding boxes and create a 2D image of them, as if we were taking a picture of the 3D scene. This is called **rendering**.

This is incredibly useful for debugging and for creating visuals for our final project. We will again use the **Open3D** library, which has powerful and easy-to-use visualization tools.

---

### The `import` Statements

```python
import open3d as o3d
import json
import os
from utils import ensure_dir
```

-   **`import open3d as o3d`**: The star of the show, used for all 3D operations.
-   **`import json`**: We need this to read the `.json` file that contains our bounding box parameters.
-   **`import os`**: For file and path manipulation.
-   **`from utils import ensure_dir`**: Our directory helper.

---

### The `render_scene` Function

```python
def render_scene(pcd_path, bbox_path, output_dir):
    """
    Renders a 3D scene with a point cloud and bounding boxes, and saves it to an image.
    """
    ensure_dir(output_dir)
    # ...
```

This function takes the path to the point cloud (`.ply`), the path to the bounding boxes (`.json`), and the directory where we want to save our rendered image.

---

### Loading the 3D Data

```python
    # Load point cloud
    pcd = o3d.io.read_point_cloud(pcd_path)

    # Load bounding boxes
    bboxes = []
    if os.path.exists(bbox_path):
        with open(bbox_path, 'r') as f:
            bbox_params = json.load(f)
        
        for params in bbox_params:
            bbox = o3d.geometry.AxisAlignedBoundingBox(
                min_bound=params["min_bound"],
                max_bound=params["max_bound"]
            )
            bboxes.append(bbox)
```

-   **`pcd = o3d.io.read_point_cloud(pcd_path)`**: We load the point cloud file that we generated earlier.
-   **`bboxes = []`**: We create an empty list to hold our Open3D bounding box objects.
-   **`if os.path.exists(bbox_path):`**: We check if the bounding box file exists. It might not if YOLO didn't detect any objects.
-   **`with open(...)`**: We open and read the JSON file containing the list of bounding box parameters.
-   **`for params in bbox_params:`**: We loop through each set of parameters.
-   **`bbox = o3d.geometry.AxisAlignedBoundingBox(...)`**: For each set of parameters, we reconstruct the Open3D `AxisAlignedBoundingBox` object.
-   **`bboxes.append(bbox)`**: We add the reconstructed box to our list.

---

### Setting up the Visualizer

```python
    # Create a visualizer
    vis = o3d.visualization.Visualizer()
    vis.create_window(visible=False) # Use a non-blocking visualizer
    vis.add_geometry(pcd)
    for bbox in bboxes:
        vis.add_geometry(bbox)
```

This is where we set up the 3D scene.

-   **`vis = o3d.visualization.Visualizer()`**: We create a `Visualizer` object. This is our virtual 3D world.
-   **`vis.create_window(visible=False)`**: We create a window for our visualizer. By setting `visible=False`, we are telling Open3D that we don't need to see the window on the screen. This is called "headless" or "off-screen" rendering, and it's perfect for saving images automatically without any user interaction.
-   **`vis.add_geometry(pcd)`**: We add our point cloud to the scene.
-   **`for bbox in bboxes: vis.add_geometry(bbox)`**: We loop through our list of bounding boxes and add each one to the scene.

---

### Setting the Camera Angle

```python
    # Set camera view
    vis.get_render_option().background_color = [0, 0, 0]
    ctr = vis.get_view_control()
    ctr.set_zoom(0.8)
    ctr.set_lookat([0, 0, 0])
    ctr.set_up([0, -1, 0])
    ctr.set_front([0, 0, -1])
```

Just like a real photographer, we need to position our virtual camera to get a good shot.

-   **`vis.get_render_option().background_color = [0, 0, 0]`**: We set the background color of our scene. `[0, 0, 0]` is black.
-   **`ctr = vis.get_view_control()`**: We get the "view control" object, which allows us to manipulate the camera.
-   **`ctr.set_zoom(0.8)`**: We set the zoom level.
-   **`ctr.set_lookat([0, 0, 0])`**: This tells the camera where to point. We're telling it to look at the origin of the scene, `(0, 0, 0)`.
-   **`ctr.set_up([0, -1, 0])`**: This defines the "up" direction for the camera. `[0, -1, 0]` means the negative Y-axis is pointing up. This is because we transformed our point cloud earlier.
-   **`ctr.set_front([0, 0, -1])`**: This defines the direction the camera is facing.

---

### Capturing the Image

```python
    # Capture and save image
    base_name = os.path.splitext(os.path.basename(pcd_path))[0]
    image_path = os.path.join(output_dir, f"{base_name}_render.png")
    vis.capture_screen_image(image_path, do_render=True)
    vis.destroy_window()

    print(f"Saved rendered scene to {image_path}")
```

-   **`base_name = ...`**: We get the base filename for our output image.
-   **`image_path = ...`**: We construct the full path for our output image file.
-   **`vis.capture_screen_image(image_path, do_render=True)`**: This is the command to take the picture! It renders the current view of the scene and saves it to the specified `image_path`.
-   **`vis.destroy_window()`**: This is a crucial cleanup step. It closes the visualizer window and releases the system resources it was using.
-   **`print(...)`**: We print a final confirmation message.
