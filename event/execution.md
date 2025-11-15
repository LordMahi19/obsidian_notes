# Phase 2: Custom Data Collection and Conversion

This phase covers the process of creating your own custom, real-world dataset. This involves recording videos of the DVS128 gestures and then converting them into an event-based format using the `v2e` tool.

## Step 1: Identify and List Target Gestures

First, you need to know which gestures to record. The DVS128 Gesture dataset includes 11 classes. You should aim to record examples for all of them. You can confirm the exact class names and order from the `dvsgesture_config.json` file you created in Phase 1.

Example `class_names` from the config file:
```json
"class_names": [
    "hand_clapping",
    "right_hand_wave",
    "left_hand_wave",
    "right_arm_clockwise",
    "right_arm_counter_clockwise",
    "left_arm_clockwise",
    "left_arm_counter_clockwise",
    "arm_roll",
    "air_guitar",
    "air_drums",
    "other_gestures"
]
```
*(Note: The actual names in your file might vary slightly; always refer to your specific `dvsgesture_config.json` file.)*

## Step 2: Record Custom Videos

The goal is to capture data that is *different* from the clean, lab-style data in the original dataset.

### Recording Setup
*   **Camera:** A standard smartphone camera or webcam is sufficient.
*   **Resolution & Frame Rate:** Aim for a decent resolution (e.g., 720p or 1080p) and a standard frame rate (30 or 60 fps). Higher frame rates can provide more temporal information for `v2e`.
*   **File Format:** Save videos in a common format like `.mp4`.

### Recording Guidelines
For each gesture, record multiple short video clips (e.g., 3-5 seconds each). Introduce the following variations across the clips:

*   **Angles:** Record from the front, from a 45-degree angle, slightly from above, and slightly from below.
*   **Distances:** Record close-up shots, medium shots, and shots from further away.
*   **Lighting:** Record in bright, even light, but also in more challenging conditions like dim light, or with a light source behind the person (backlighting).
*   **Backgrounds:** Use a plain wall for some recordings, but also use cluttered backgrounds (a busy room, an outdoor scene).
*   **Speed:** Perform the gestures at a normal speed, a faster speed, and a slower speed.
*   **Subject Variation:** If possible, have more than one person perform the gestures.

### File Organization
Create a structured directory to keep your recordings organized. This is crucial for the next steps.

```
custom_rgb_data/
├── hand_clapping/
│   ├── angle1_dist1_lighting1_001.mp4
│   ├── angle2_dist2_lighting2_002.mp4
│   └── ...
├── right_hand_wave/
│   ├── angle1_dist1_lighting1_001.mp4
│   └── ...
└── ...
```

## Step 3: Convert Videos to Event Data with `v2e`

`v2e` (video to events) is a tool that simulates a DVS camera's output from standard video.

### Installation
1.  **Clone the repository:**
    ```bash
    git clone https://github.com/uzh-rpg/v2e.git
    ```
2.  **Install dependencies:**
    ```bash
    cd v2e
    pip install -r requirements.txt
    ```
    *(You may need to install other system dependencies like `ffmpeg` if you don't have them already.)*

### Conversion Process
The core of `v2e` is a command-line script. You will run this script on each video you recorded.

1.  **Basic Command:**
    ```bash
    python v2e.py -i /path/to/your/video.mp4 -o /path/to/output/dir/
    ```

2.  **Important `v2e` Parameters:**
You must simulate a DVS camera with the same resolution as the DVS128 Gesture dataset (128x128). You will also need to experiment with the contrast sensitivity thresholds (`--pos_thres` and `--neg_thres`).

    *   `--dvs_resolution HEIGHT WIDTH`: **Crucial.** Set this to `128 128`.
    *   `--pos_thres` / `--neg_thres`: The brightness change threshold to generate a positive/negative event. A good starting point is `0.15` or `0.2`. You should experiment. Lower values mean more events (more sensitive), higher values mean fewer events (less sensitive).
    *   `--output_format`: The format for the output events. `aedat4` is a modern standard that is compatible with Tonic.
    *   `--overwrite`: Add this flag to allow overwriting existing output files.

3.  **Example Conversion Command:**
Let's say you have a video at `../custom_rgb_data/hand_clapping/rec_001.mp4`. You want to save the output to `../custom_event_data/hand_clapping/`.

    ```bash
    # From inside the v2e directory
    python v2e.py \
        -i ../custom_rgb_data/hand_clapping/rec_001.mp4 \
        --dvs_resolution 128 128 \
        --pos_thres 0.2 \
        --neg_thres 0.2 \
        --output_format aedat4 \
        --overwrite \
        --output_folder ../custom_event_data/hand_clapping/
    ```

### Batch Conversion (Optional)
To convert all your videos automatically, you can use a simple shell script. You can find examples of batch processing scripts in the `v2e` repository or create your own to loop through your `custom_rgb_data` directory.

## Final Output of Phase 2

At the end of this phase, you should have a new directory, `custom_event_data`, with the same sub-folder structure as your `custom_rgb_data`, but filled with `.aedat4` event files. This data is now ready to be used in Phase 3.
