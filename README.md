# Predictive Maintenance System for Automated Embroidery Machines.


## Overview
Traditional machine monitoring systems rely on sensor-thresholds based alerts such as, raise alarm if temperature > threshold or vibration > threshold and so on. These alerts happen **after the problem has already occurred**, leading to sudden machine shutdown, production downtime and production delays.

Instead, Predictive maintenance aims to:

- Detect anomaly patterns early.
- Schedule maintenance before failure.
- Hence, reduce unexpected downtime and improve production reliability.

We use a **lighweight transformer encoder** architecture to learn normal machine operation patterns across time and across multiple sensors, in an unsupervised learning framework. Hence, deviations from these normal operating patterns, will indicate impending machine failure and alert us beforehand.

**Why Unsupervised Learning?**
Since labeled data is rarely available in industrial environments, the model learns **normal machine operation** patterns from **multivariate time series stream** of sensor data.

**Why Transformer Encoder?**

A **lightweight Transformer encoder** is trained on sliding windows of sensor data to learn temporal relationships between machine signals. During inference, deviations from learned normal behavior are detected and flagged as potential anomalies.

Training data consists only of **normal machine operation data**. The model learns the structure of the time-series using a prediction objective : past sensor window → predict next timestep
Large prediction errors indicate abnormal behavior and generate anomaly scores.


## End-to-End Machine Learning Architecture
The current setup monitors **4 automated embroidery machines** with the following 4 sensors each :

- Vibration
- Temperature
- Thread Tension
- Motor RPM




## Future Directions
- Trying Self-Supervised learning framework
- Transformer architecture optimization
- Visualization dashboard for machine health monitoring
