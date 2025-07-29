# 📹 Real-Time Video-Based Crowd Detection & Alert System (YOLOv5)

This project simulates real-time video stream processing to detect people and trigger crowd alerts using the YOLOv5 object detection model.

It processes every 3rd frame from a video, detects the number of people (class 0), and raises an alert if 3 or more people appear in 5 consecutive processed frames. Alerts are logged with timestamps and visualized on a timeline plot.

---

## 🚀 Features

- 🎥 Real-time video stream simulation using OpenCV  
- 🤖 People detection using YOLOv5 (via PyTorch Hub)  
- ⏱️ Frame skipping: processes every 3rd frame for speed  
- 🚨 Alert trigger: ≥3 people in 5 consecutive frames  
- 📝 Logs alerts with timestamp in JSON format (`alerts.json`)  
- 📊 Plots timeline of alerts using Matplotlib (`alert_timeline.png`)  
- 💾 Saves output video with overlayed bounding boxes and alert messages (`output.avi`)

---

## 🧰 Technologies Used

- Python 3.x  
- OpenCV  
- PyTorch  
- YOLOv5 (Ultralytics)  
- Matplotlib  
- JSON

---

## 📁 Project Structure

.
├── alerts.json               # JSON file logging all detected crowd alerts

├── alert_timeline.png        # Timeline plot of alert occurrences

├── output.avi                # Exported video with detection overlays

├── video_input.mp4           # Input video file (rename your actual file to this)

├── crowd_detection.py        # Main Python script (real-time detection logic)

├── requirements.txt          # List of required Python packages (optional)

└── README.md                 # Project documentation



## 📌 How It Works

1. **Video Stream Simulation**  
   The video is loaded using OpenCV. Every frame is resized for faster processing.

2. **Frame Skipping**  
   To reduce computational load, only every **3rd frame** is processed.

3. **People Detection (YOLOv5)**  
   - The YOLOv5 model (medium version) is loaded via `torch.hub`.  
   - It detects objects in each frame, filtering to only **class 0 (person)**.  
   - Bounding boxes are drawn around detected people.

4. **Crowd Detection Logic**  
   - Maintains a rolling list of person counts for the last **5 processed frames**.  
   - If **3 or more people** are detected in **all 5 frames**, a "Crowd Detected" alert is triggered.

5. **Alert Handling**  
   - When a crowd is detected:  
     - An alert message is displayed on the video frame.  
     - A timestamped alert is saved to `alerts.json`.

6. **Output Generation**  
   - The processed video is saved as `output.avi` with overlays.  
   - A visual timeline of alerts is plotted and saved as `alert_timeline.png`.

7. **Exit Control**  
   - Press `Q` during the video to quit early.


## 📸 Output Examples

### 1. 👁️ Real-Time Detection Frame
Bounding boxes around detected people are shown in blue. When a crowd is detected, a red alert message is overlaid.

---

### 2. 📝 JSON Alert Log (`alerts.json`)
Alerts are logged with timestamps:

```json
[
  {
    "time": "2025-07-29 12:05:33",
    "alert": "Crowd Detected"
  },
  {
    "time": "2025-07-29 12:06:41",
    "alert": "Crowd Detected"
  }
]

