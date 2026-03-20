# 🧵 TextileAI — Predictive Maintenance for Embroidery Machines

# Chapter 1 — Problem Definition

## 1. Objective
TextileAI implements **unsupervised time series anomaly detection** for predictive maintenance in a small textile setup of 4 embroidery machines.

- Each machine has 4 sensors:
  - Temperature
  - Vibration
  - Motor RPM
  - Thread Tension

Total features:
4 machines × 4 sensors = 16-dimensional multivariate time series

---

## 2. Learning Approach

We use **unsupervised learning (reconstruction-based)**:

- Train only on **normal operating data**
- Learn normal patterns
- Detect anomalies via **reconstruction error**

---

# Chapter 2 — System Architecture

Pipeline:

Raw Sensor Data → Preprocessing → Windowing → RevIN Normalization → Conv1D Embedding → Transformer Encoder → Linear Decoder → Reconstruction Error → Anomaly Detection

---

# Chapter 3 — Data Ingestion (NEW — Not in Paper)

## 1. Sensor Data Collection

Each machine generates data every second.

Example:

| Timestamp | Temp | Vibration | RPM | Tension |
|----------|------|----------|-----|--------|
| 10:00:00 | 65°C | 0.12 | 1200 | 0.45 |

---

## 2. Data Volume Estimation

Per machine:

- 1 reading/sec → 86400/day
- 4 machines → 345,600 rows/day

Monthly:

~10 million rows

---

## 3. Data Transmission (MQTT)

We use **MQTT protocol**:

- Lightweight
- Ideal for IoT setups

Flow:

Sensors → Edge Device → MQTT Broker → Backend

Example JSON:

{
  "machine_id": "M1",
  "temp": 65,
  "vibration": 0.12,
  "rpm": 1200,
  "tension": 0.45,
  "timestamp": "2026-01-01T10:00:00"
}

---

## 4. Storage

Options:

| Option | Use Case |
|------|--------|
| CSV | Simple setup |
| SQLite | Local DB |
| InfluxDB | Time-series optimized |

---

# Chapter 4 — Preprocessing

## 1. Normalization

We use **Z-score normalization**:

x' = (x - μ) / σ

Example:

Temp = [60, 65, 70]
μ = 65, σ ≈ 4.08

Normalized(70) = (70-65)/4.08 ≈ 1.22

---

## 2. Sliding Window Segmentation

Window size = 60 (seconds)

Example:

[1,2,3,4,5] → [1,2,3], [2,3,4], [3,4,5]

Shape:

(N, L, V)

N = windows
L = 60
V = 16

---

## 3. Segment-Level Normalization (RevIN)

Each window normalized independently.

Purpose:
- Handle non-stationarity
- Remove scale shifts

---

# Chapter 5 — Model Architecture

## 1. Embedding (Conv1D)

- Kernel size = 3
- Output dim = 64

---

## 2. Transformer Encoder

Parameters (scaled for our setup):

| Parameter | Value |
|----------|------|
| Layers | 2 |
| Heads | 4 |
| Model Dim | 64 |
| FF Dim | 128 |
| Dropout | 0.1 |

---

## 3. Decoder

- Linear layer
- Maps 64 → 16

---

# Chapter 6 — Training Strategy

## 1. Loss Function

We use **Mean Squared Error (MSE)**:

Loss = ||x - x̂||²

Example:

Actual: [1200, 1210, 1190]  
Pred:   [1198, 1205, 1185]

Error:
(2² + 5² + 5²) = 54

---

## 2. Training Type

- Batch training (offline)
- Train on 1–2 weeks of normal data

---

# Chapter 7 — Inference Strategy

## 1. Batch vs Real-time

- Training: batch
- Inference: near real-time (streaming windows)

---

## 2. Anomaly Score

score = ||x - x̂||²

---

## 3. Threshold

threshold = mean + 3×std

Example:

Mean = 10  
Std = 5  

Threshold = 25

---

## 4. Decision

if score ≥ threshold → anomaly

---

# Chapter 8 — Example Scenario

Normal:

RPM = [1200,1210,1195] → error = 8

Fault:

RPM = [1200,800,300] → error = 120 → anomaly

---

# Chapter 9 — Practical Notes

- No positional encoding (as per paper)
- RevIN improves performance
- Window size is critical hyperparameter
