# Transformer based unsupervised predictive maintenance system for the textile industry.
We use a lightweight **transformer encoder** to learn the normal operating patterns of automatic embroidery machines across time and sensors, in an **unsupervised learning** framework. Deviation from this learned normal behavior, indicates impending machine failure and alerts us beforehand to schedule predictive maintenance.


### Why predictive maintenance?
Traditional machine monitoring systems rely on sensor-thresholds based alerts such as, raise alarm if temperature > threshold or vibration > threshold and so on. These alerts happen **after the problem has already occurred**, leading to sudden machine shutdown, production downtime and production delays.

Instead, Predictive maintenance aims to:

- Detect anomaly patterns early.
- Schedule maintenance before failure.
- Hence, reduce unexpected downtime and improve production reliability.


### Why unsupervised learning?
Since labeled data is rarely available in industrial environments, the model learns **normal machine operation** patterns from **multivariate time series stream** of sensor data.


### Why transformer encoder?
A **lightweight Transformer encoder** is trained on overlaping sliding windows of sensor data to learn temporal relationships between machine signals. During inference, deviations from learned normal behavior are detected and flagged as potential anomalies.


### End-to-End ML pipeline
The current setup monitors **4 automated embroidery machines** with the following 4 sensors each :

- Vibration
- Temperature
- Thread Tension
- Motor RPM
