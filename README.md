# Drowsiness-and-distraction-detection-while-driving
The project tries to use AI &amp; Computer Vision to create a seamless pipeline enabling drowsiness and distraction detection and raising alert under critical situations.
# Driver Drowsiness & Distraction Detection 🚗💤📱

An end-to-end pipeline for detecting **driver drowsiness and distraction** using the **YawDD dataset** and **YOLOv8n (COCO pretrained weights)**.  
This project integrates multiple detectors — **Eye Aspect Ratio (EAR)**, **Mouth Aspect Ratio (MAR)**, **Head Pose Estimation**, and **Phone Detection** — into a unified alert system with visualization, metrics, and Streamlit deployment.

---

## 📂 Project Workflow

| Step | Description |
|------|-------------|
| 1–2  | Environment setup, package installation, GPU check, Drive mount |
| 3–4  | Kaggle API configuration, YawDD dataset download |
| 5–7  | Frame extraction, EDA, Train/Val/Test split |
| 8–9  | Detector initialization (EAR, MAR, Head Pose, Phone) + pipeline |
| 10   | Sanity check on YawDD frames |
| 11   | Load YOLOv8n COCO (class 67 = phone) |
| 12   | Full inference on test video |
| 13–16| Metrics dashboard, ablation study, confusion matrix, FPS benchmark |
| 17–19| Save models/configs, Streamlit-ready bundle |

---

## 🧠 Why YOLOv8n?

- **Pretrained on COCO**: YOLOv8n already includes robust detection for **cell phones (class 67)**, eliminating the need for retraining.
- **Lightweight (nano version)**: Optimized for **real-time inference** on resource-constrained environments (e.g., T4 GPU, edge devices).
- **Speed vs Accuracy Trade-off**: YOLOv8n balances detection accuracy with high FPS, critical for **driver monitoring systems** where latency can be life-threatening.
- **Integration**: Seamlessly plugs into the pipeline alongside MediaPipe-based detectors for eyes, mouth, and head pose.

---

## 📊 Metrics & Evaluation

We used **Precision, Recall, and F1-score** because:

- **Precision**: Measures how many detected drowsy/distraction events were correct. Important to avoid false alarms that could annoy drivers.
- **Recall**: Measures how many actual drowsy/distraction events were detected. Critical to minimize missed detections that could lead to accidents.
- **F1-score**: Harmonic mean of Precision and Recall. Provides a balanced metric when both false positives and false negatives are costly.

### Example: EAR Ablation Study
- Thresholds between **0.15–0.42** were tested.
- Best F1-score achieved at ~**0.25**, aligning with literature on eye aspect ratio thresholds for drowsiness.

---

## 📈 Key Features

- **EAR Detector**: Identifies prolonged eye closure.
- **MAR Detector**: Detects yawning events.
- **Head Pose Detector**: Flags when driver looks away from the road.
- **YOLOv8n Phone Detector**: Recognizes phone usage with confidence scores.
- **Alert Fusion Engine**: Combines signals into **Safe / Warning / Critical** levels.
- **HUD Overlay**: Real-time visualization of metrics and alerts.
- **Metrics Dashboard**: EAR/MAR plots, head pose angles, alert timeline, FPS tracking.
- **Confusion Matrix**: System-level evaluation of alert predictions.
- **FPS Benchmark**: Compares PyTorch vs ONNX vs full pipeline inference speed.

---

## 📦 Streamlit Deployment

Artifacts saved for Streamlit app:
- `config.json` → Detector thresholds & weights
- `metrics_summary.json` → Inference statistics
- `yolov8n.pt` & `yolov8n.onnx` → Phone detection models
- Result plots → EDA, sanity check, metrics dashboard, ablation, confusion matrix, FPS benchmark

Results and visualizations 
<img width="1055" height="789" alt="image" src="https://github.com/user-attachments/assets/4efcb278-388a-4689-ad4c-22ff43b0fd21" />
<img width="1470" height="789" alt="image" src="https://github.com/user-attachments/assets/74fe0a6b-cac7-42ca-8caf-23986e005114" />
<img width="1489" height="1083" alt="image" src="https://github.com/user-attachments/assets/22ec7d5d-f69f-42da-ae50-1ec0facce9ac" />
<img width="1290" height="396" alt="image" src="https://github.com/user-attachments/assets/88f17b4d-0a0d-4d10-bc33-0cd53637ea81" />
<img width="1154" height="396" alt="image" src="https://github.com/user-attachments/assets/3a4e178c-df32-4088-9bec-14a5f7f66f0e" />
<img width="989" height="390" alt="image" src="https://github.com/user-attachments/assets/93ab96ef-1cd0-4158-a0a9-d3b17eb1101f" />

Run the app:
```bash
streamlit run app.py
