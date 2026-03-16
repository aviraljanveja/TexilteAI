# Predictive Maintenance System for Automated Embroidery Machines.


## Problem Statement
Traditional machine monitoring systems rely on fixed sensor-thresholds such as:

- temperature > threshold
- vibration > threshold
- motor overload

These alerts happen **after the problem has already occurred**, leading to sudden machine shutdown, production downtime and production delays.

Predictive maintenance aims to:

- Detect anomalies early.
- Schedule maintenance before failure.
- Reduce unexpected downtime.
- Improve production reliability.


## Solution Overview
We use a **lighweight encoder only transformer** architecture to learn normal machine operation patterns across time and across multiple sensors, in an unsupervised learning framework. Thereby detecting deviations from normal operating patterns, which may indicate impending machine failure.

**Why Transformer Encoder?**

**Why Unsupervised Learning?**
Since labeled data is rarely available in industrial environments, the model learns **normal machine operation** patterns from **multivariate time series stream** of sensor data.

A **lightweight Transformer encoder** is trained on sliding windows of sensor data to learn temporal relationships between machine signals. During inference, deviations from learned normal behavior are detected and flagged as potential anomalies.

Training data consists only of **normal machine operation data**. The model learns the structure of the time-series using a prediction objective : past sensor window → predict next timestep
Large prediction errors indicate abnormal behavior and generate anomaly scores.


## High-Level System Design
The current setup monitors **4 automated embroidery machines** with the following 4 sensors each :

- Vibration
- Temperature
- Thread Tension
- Motor RPM / Current


## Goals of This Project
- Build an explainable predictive maintenance system
- Apply Transformer models to industrial time-series data
- Detect anomalies before failure occurs
- Demonstrate an end-to-end ML pipeline for manufacturing environments


## Future Work
- Trying Self-Supervised learning framework
- Transformer architecture optimization
- Visualization dashboard for machine health monitoring
