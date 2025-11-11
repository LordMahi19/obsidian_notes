## 📂 File Structure Recap

```
2_5D_Reconstruction/
├── data/
│   └── test_video.mp4
├── src/
│   └── vo.py        ← we’ll create this now
├── output/
└── models/
```

---

## ⚙️ Step 1. Write the VO script

Create a new file:  
`src/vo.py`

Paste this full code in:

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# --- Parameters ---
VIDEO_PATH = "../data/test_video.mp4"
MIN_MATCH_COUNT = 150  # adjust for your video
FOCAL_LENGTH = 718.8560  # can be approximate
PRINCIPAL_POINT = (607.1928, 185.2157)  # center of image (change if needed)

# --- Load Video ---
cap = cv2.VideoCapture(VIDEO_PATH)
if not cap.isOpened():
    print("❌ Error: Cannot open video.")
    exit()

# --- Initialize Feature Detector ---
orb = cv2.ORB_create(3000)

# --- Read first frame ---
ret, old_frame = cap.read()
if not ret:
    print("❌ Error: Cannot read video.")
    exit()

old_gray = cv2.cvtColor(old_frame, cv2.COLOR_BGR2GRAY)
kp1, des1 = orb.detectAndCompute(old_gray, None)

# --- Pose estimation setup ---
R_f = np.eye(3)
t_f = np.zeros((3, 1))

# --- Visualization setup ---
trajectory = np.zeros((600, 600, 3), dtype=np.uint8)

frame_idx = 0
while True:
    ret, frame = cap.read()
    if not ret:
        break

    frame_gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    kp2, des2 = orb.detectAndCompute(frame_gray, None)

    # --- Match features using brute force matcher ---
    bf = cv2.BFMatcher(cv2.NORM_HAMMING, crossCheck=True)
    matches = bf.match(des1, des2)
    matches = sorted(matches, key=lambda x: x.distance)
    good_matches = matches[:MIN_MATCH_COUNT]

    # --- Extract matched points ---
    pts1 = np.float32([kp1[m.queryIdx].pt for m in good_matches])
    pts2 = np.float32([kp2[m.trainIdx].pt for m in good_matches])

    # --- Compute Essential matrix ---
    E, mask = cv2.findEssentialMat(pts2, pts1, focal=FOCAL_LENGTH, pp=PRINCIPAL_POINT, method=cv2.RANSAC, prob=0.999, threshold=1.0)
    if E is None:
        continue

    _, R, t, mask = cv2.recoverPose(E, pts2, pts1, focal=FOCAL_LENGTH, pp=PRINCIPAL_POINT)

    # --- Accumulate motion ---
    scale = 1.0  # we assume constant scale (monocular limitation)
    t_f += scale * R_f.dot(t)
    R_f = R.dot(R_f)

    # --- Draw trajectory ---
    x, z = t_f[0][0], t_f[2][0]
    draw_x, draw_y = int(x) + 300, int(z) + 300
    cv2.circle(trajectory, (draw_x, draw_y), 1, (0, 255, 0), 2)
    cv2.imshow("Trajectory", trajectory)
    cv2.imshow("Frame", frame)

    # --- Prepare for next iteration ---
    old_gray = frame_gray.copy()
    kp1, des1 = kp2, des2
    frame_idx += 1

    key = cv2.waitKey(1)
    if key == 27:  # ESC to stop
        break

cap.release()
cv2.destroyAllWindows()
```

---

## 🧠 How It Works

|Step|Description|
|---|---|
|1️⃣ Detect features|Uses **ORB** (fast feature detector) to find keypoints in each frame|
|2️⃣ Match features|Finds correspondences between two consecutive frames|
|3️⃣ Estimate motion|Uses the **Essential Matrix** to recover **rotation (R)** and **translation (t)**|
|4️⃣ Accumulate motion|Adds each new motion to the camera’s global position|
|5️⃣ Visualize|Draws your estimated trajectory in real time|

---

## 🧪 Step 2. Run it

From your terminal (in the project root):

```bash
cd src
python vo.py
```

You should see:

- One window showing your **camera feed**
    
- Another showing your **green trajectory path**
    

If it works, you’re officially running **monocular VO** 🎉

---

## 🔧 Step 3. Next Up (Once this Runs)

Next, we’ll add:

- ✅ Object detection using YOLOv8
    
- ✅ Fuse YOLO detections with the camera pose
    
- ✅ Create a **live 2D “map”** of detected objects + trajectory (your 2.5D prototype)
    

---

Would you like me to walk you through the **next step (YOLO object detection + live overlay)** now?  
Or do you first want to test and fine-tune the VO output (e.g., improve stability, adjust parameters)?