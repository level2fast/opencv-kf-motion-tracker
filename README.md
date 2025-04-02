# opencv-kf-motion-tracker
Sample project that uses OpenCV and Kalman filters to estimate a drones position from noisy IMU and GPS sensor measurements

Kalman Filtering of IMU
- Retrieve real-time IMU data (Roll, Pitch, Yaw) from MAVProxy/DroneKit.
- Apply a Kalman Filter to smooth out accelerometer/gyroscope noise.
- Visualize filtered vs raw IMU data to compare performance.

Kalman Filter of GPS
- Get simulated GPS data from ArduPilot using DroneKit.
- Apply a Kalman Filter to smooth GPS Latitude, Longitude, and Altitude.
- Compare raw vs filtered GPS data in real time.

Example: IMU Tracking Steps
--
🔍 Explanation

1️⃣ Get IMU Data from ArduPilot
DroneKit retrieves real-time Roll, Pitch, Yaw from ArduPilot.

This data comes from accelerometer + gyroscope, but it's noisy.

2️⃣ Kalman Filter for Smoothing
State Vector (6D) → [Roll, Pitch, Yaw, dRoll, dPitch, dYaw]

Measurement (3D) → [Roll, Pitch, Yaw]

The transition model assumes a constant motion model.

Process Noise Covariance is tuned for gradual corrections.

3️⃣ Apply Kalman Filtering
Predict the next state based on motion.

Correct the estimate using real IMU measurements.

Example: GPS Tracking Steps
--
🔍 Explanation

1️⃣ Get GPS Data from ArduPilot
DroneKit retrieves real-time Latitude, Longitude, and Altitude.

GPS data is often noisy, causing small fluctuations.

2️⃣ Kalman Filter for GPS
State Vector (6D) → [Lat, Lon, Alt, dLat, dLon, dAlt]

Measurement (3D) → [Lat, Lon, Alt]

Process Noise Covariance (1e-3) allows smooth transitions.

Measurement Noise Covariance (1e-2) helps correct jumps.

3️⃣ Apply Kalman Filtering
Predict next position based on motion.

Correct with actual GPS readings.

Output smoothed GPS coordinates.
