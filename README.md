# 🏃‍♂️ Player Re-Identification from Football Match Video

**Assignment Submission — Computer Vision Tracking System**

## 🎯 Problem Statement

Design a player tracking system that can:

* Detect football players in a match video, and
* Assign consistent player IDs across frames (i.e., re-identify them even after motion or occlusion).

## ✅ Evaluation Criteria Checklist

| Criteria                                           | Addressed?                                        |
| -------------------------------------------------- | ------------------------------------------------- |
| ✔️ **Accuracy & Reliability of Re-identification** | ✅ Yes (Scope of Improvement)                |
| ✔️ **Simplicity, Modularity, Clarity of Code**     | ✅ Yes                                             |
| ✔️ **Documentation Quality**                       | ✅ Included below                                  |
| ✔️ **Runtime Efficiency and Latency (Bonus)**      |  Reasonable performance with optimization scope |
| ✔️ **Thoughtfulness and Creativity of Approach**   | ✅ Combined Yolov11(given) + ResNet innovatively             |


## 🧠 Approach Summary

I chose to **combine two models** to get the best of both worlds:

### 1. **YOLOv8/YOLOv11 for Player Detection**

* My YOLO model (`best.pt`) detects all objects, but I filter only for the `player` class.
* Bounding boxes are extracted frame-by-frame for those detections.

### 2. **ResNet18 for Appearance Embedding**

* Each detected player is cropped and passed through ResNet18 (without the final layer).
* This returns a feature vector that represents how the player "looks" — helpful for re-identification.

### 3. **ID Matching Logic**

* Compared current player's embedding to previously seen ones using **cosine similarity**.
* Also added a **spatial proximity check** to ensure we don’t match players who are far apart.
* If no match found, I assign a new ID.

---

## 📦 Output

The output is saved as `output.avi` — with every player shown along with a consistent ID throughout the video.
(Kindly download the video above in repo)

# Snapshots from output video:

<img width="894" alt="image" src="https://github.com/user-attachments/assets/a88f67e8-f89a-4d3f-b3af-b71dcf202814" />

<img width="890" alt="image" src="https://github.com/user-attachments/assets/61cf1a0f-98a9-49c8-9bbf-a9ba2ed7bee3" />




---

## 🚀 How to Run

1. Install dependencies:

```bash
pip install ultralytics torch torchvision opencv-python
```

2. Place these in your folder:

* `best.pt` (given detection model (given in the assignment, Kinldy downlowad from there))
* `15sec_input_720p.mp4` (input video)

3. Run the Python script:

```bash
python solution.py
```

---

## 📈 Performance & Limitations

* **Performs well** when players are not too similar in appearance and are not occluded for too long.
* May struggle with **very similar jerseys** or long-term occlusions (since no temporal smoothing like DeepSORT is used).
* Still, it handles basic re-identification tasks with good reliability and is **lightweight**.

## 🤝 Acknowledgments

This was a really interesting assignment — I learned a lot about combining object detection with re-ID embeddings. I tried to strike a balance between **simplicity and reliability**, and I'm happy with the current result.
