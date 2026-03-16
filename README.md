# Predictive Maintenance System for Automated Embroidery Machines using Transformer based Multivariate Time-Series Anomaly Detection.

---

## Overview

Industrial embroidery machines operate continuously in textile manufacturing units and unexpected failures can cause significant production downtime.

This project develops a **machine learning based predictive maintenance system** that monitors sensor data from embroidery machines and detects early signs of abnormal machine behavior.

Instead of relying on simple threshold alarms from individual sensors, the system learns **normal operational patterns across multiple sensors and time** and detects deviations that may indicate future machine failure.

---

## Problem Statement

Traditional machine monitoring systems rely on fixed thresholds such as:

- temperature > threshold
- vibration > threshold
- motor overload

These alerts occur **after the problem has already occurred**, leading to sudden machine shutdown and production delays.

Predictive maintenance aims to:

- detect abnormal machine behavior earlier
- schedule maintenance before failure
- reduce unexpected downtime
- improve production reliability

---

## System Setup

The current setup monitors **4 automated embroidery machines** with the following sensors:

- Vibration
- Temperature
- Thread Tension
- Motor RPM / Current

Each machine produces a **multivariate time series stream** of sensor readings.

---

## Machine Learning Approach

The system uses an **unsupervised anomaly detection framework**.

Since labeled failure data is rarely available in industrial environments, the model learns patterns of **normal machine operation** from historical sensor data.

A **lightweight Transformer encoder** is trained on sliding windows of sensor data to learn temporal relationships between machine signals.

During inference, deviations from learned normal behavior are detected and flagged as potential anomalies.

---

## Learning Framework

Training data consists only of **normal machine operation data**.

The model learns the structure of the time-series using a prediction objective : past sensor window → predict next timestep
Large prediction errors indicate abnormal behavior and generate anomaly scores.

---

## High-Level Architecture

Machine Sensors
↓
Data Collection
↓
Sliding Window Generation
↓
Transformer Encoder Model
↓
Prediction Error
↓
Anomaly Score
↓
Operator Alert
---

## Goals of This Project

- Build an explainable predictive maintenance system
- Apply Transformer models to industrial time-series data
- Detect machine anomalies before failures occur
- Demonstrate an end-to-end ML pipeline for manufacturing environments

---

## Future Work

- Sensor data simulation and dataset creation
- Transformer architecture optimization
- Advanced anomaly scoring strategies
- Visualization dashboard for machine health monitoring
