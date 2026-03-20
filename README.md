# 🧵 TextileAI — Predictive Maintenance for Embroidery Machines

## 📌 Overview

**TextileAI** is a practical machine learning project that implements **unsupervised time-series anomaly detection** for predictive maintenance in a small textile setup.

We monitor **4 automated embroidery machines**, each equipped with **4 sensors**:

- Temperature
- Vibration
- Motor RPM
- Thread Tension

The system learns **normal machine behavior** and detects anomalies using a **Transformer-based autoencoder**, inspired by recent research on time-series anomaly detection.

---

## 🎯 Objective

To build a **real-world ML system** that:

1. Collects sensor data from embroidery machines  
2. Learns normal operational patterns  
3. Detects anomalies in real time  
4. Enables early maintenance and reduces downtime  

---

## 🏭 System Setup

### Machines and Sensors

| Machine | Sensors |
|--------|--------|
| M1 | Temp, Vibration, RPM, Thread Tension |
| M2 | Temp, Vibration, RPM, Thread Tension |
| M3 | Temp, Vibration, RPM, Thread Tension |
| M4 | Temp, Vibration, RPM, Thread Tension |

### Total Features

4 machines × 4 sensors = 16 features (multivariate time series)

---

## 📊 Example Sensor Data

A single timestamp snapshot:

| Time | M1_Temp | M1_Vib | M1_RPM | M1_Tension | ... | M4_Tension |
|------|--------|--------|--------|------------|-----|------------|
| t₁ | 65°C | 0.12 | 1200 | 0.45 | ... | 0.50 |
| t₂ | 66°C | 0.11 | 1195 | 0.47 | ... | 0.49 |

---

## 🧠 Core Idea

We use an **unsupervised learning approach**:

- Train model only on **normal machine data**
- Model learns how normal patterns look
- Any deviation → **anomaly (potential fault)**

---

## 🏗️ System Architecture

Raw Sensor Data → Preprocessing → Sliding Window Segmentation → Segment Normalization (RevIN) → Conv1D Embedding → Transformer Encoder → Linear Decoder → Reconstruction Error → Anomaly Detection → Maintenance Alert

---

## ⚙️ Step-by-Step Methodology

### 1. Data Collection

Sensor data is collected at fixed intervals (e.g., every second).

Example:

{
  "timestamp": "2026-01-01 10:00:00",
  "M1_temp": 65,
  "M1_vibration": 0.12,
  "M1_rpm": 1200,
  "M1_tension": 0.45
}

---

### 2. Preprocessing

Z-score normalization:

x' = (x - μ) / σ

Example:
Temp values: [60, 65, 70]
Mean = 65, Std ≈ 4.08
Normalized 70 ≈ 1.22

---

### 3. Sliding Window Segmentation

Window size = 5

[1,2,3,4,5]
[2,3,4,5,6]
[3,4,5,6,7]

Shape: (N, L, V)

---

### 4. Segment-Level Normalization (RevIN)

Handles non-stationary signals by normalizing each segment independently.

---

### 5. Embedding Layer (Conv1D)

Captures local temporal patterns using kernel size 3.

---

### 6. Transformer Encoder

Learns temporal dependencies using attention mechanism.

---

### 7. Decoder (Linear Layer)

Reconstructs input with minimal complexity.

---

### 8. Training Strategy

Loss = ||x - x̂||²

Example:
Error = 54

---

### 9. Anomaly Detection

score = ||x - x̂||²

if score > threshold → anomaly

---

### 10. Threshold Selection

threshold = mean + 3 × std

Example:
Mean = 10, Std = 5 → Threshold = 25

---

## 🚨 Example Anomaly Scenario

Normal:
Error = 8 → normal

Fault:
Error = 120 → anomaly

---

## 📦 Repository Structure

TextileAI/
├── data/
├── sensors/
├── preprocessing/
├── models/
├── training/
├── inference/
├── utils/
├── notebooks/
└── README.md

---

## ⚡ Why This Approach Works

| Challenge | Solution |
|----------|---------|
| No labels | Unsupervised learning |
| Temporal patterns | Transformer |
| Non-stationarity | RevIN |
| Overfitting | Simple decoder |

---

## 🔧 Future Improvements

- Real-time streaming
- Dashboard
- Edge deployment
- Semi-supervised learning

---

## 🎯 Key Takeaways

- End-to-end ML system
- Industrial use case
- Strong ML portfolio project

---

## 📚 References

- Vanilla Transformer Encoder for TS Anomaly Detection
- https://github.com/chatterboy/revisitVanillaTransEncUnsupTSAD

---

## 🤝 Contributing

Pull requests welcome.

---

## 📌 Author

A hands-on ML engineering project.
