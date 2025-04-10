# Smart Traffic Management System

## Overview
The **Smart Traffic Management System** is a Python-based application that uses the YOLOv12n model to manage traffic at a four-way crossroad. It processes video feeds from four directions (North, East, South, West) in a 2x2 grid, detects and tracks vehicles, and controls traffic signals with dynamic timers based on traffic density. The system displays red, green, and yellow lights with integer timers, including countdowns for red lights indicating when they will turn green.

### Features
- **Video Display**: Four video feeds arranged in a 2x2 grid (North, East, South, West).
- **Vehicle Detection**: Uses YOLOv12n to detect vehicles (`bicycle`, `car`, `motorcycle`, `bus`, `truck`) in non-green frames.
- **Vehicle Tracking**: Assigns unique IDs to detected vehicles using a custom `Tracker` class.
- **Traffic Signal Logic**:
  - Green light duration: 60s if max vehicle distance > 250px, otherwise 6s per 25px.
  - Yellow light: 5s after green to clear traffic.
  - Red light: Displays countdown to green based on the sequence.
- **Visualization**: 
  - Bounding boxes with class names and IDs on scanning frames.
  - Max distance of the farthest vehicle from the bottom of each video.
  - Traffic signals with integer timers.

## Prerequisites
- **Python 3.8+**
- **Dependencies**:
  - `opencv-python` (for video processing and display)
  - `numpy` (for array operations)
  - `ultralytics` (for YOLOv12n model)
  - Standard libraries: `time`, `math`
- **Hardware**: Webcam or pre-recorded videos; decent CPU/GPU for real-time processing.

## Installation
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/Smart-Traffic-Management.git
   cd smart-traffic-management
   ```
2. **Install Dependencies**:
   ```bash
   pip install opencv-python numpy ultralytics

3. **Download YOLOv12n Model**:
   - Obtain yolo12n.pt from the Ultralytics YOLO repository.
   - Place it in the project directory.

4. **Add Video Files**:
   - Place the following video files in the project directory:
     - traffic1.mp4 (North)
     - traffic2.mp4 (East)
     - traffic3.mp4 (South)
     - traffic4.mp4 (West)
   - Ensure they are valid MP4 files with traffic footage.

## Usage
1. **Run the Script**:
   ```bash
   python traffic_management.py

2. **Controls**:
   - Press `q` to exit the application

3. **Output**:
   - **Traffic Videos Window**: 2x2 grid of video with vehicle detection and max distace.
   - **Trafic Signals Window**: Four traffic lights with Integer timers.

## File Structure
   
smart-traffic-management/   
  ├── Untitled1.py          # Main script with embedded Tracker class   
  ├── yolo12n.pt            # YOLOv12n model file (not included)   
  ├── traffic1.mp4          # North direction video (not included)   
  ├── traffic2.mp4          # East direction video (not included)   
  ├── traffic3.mp4          # South direction video (not included)   
  ├── traffic4.mp4          # West direction video (not included)   
  └── README.md             # This documentation   

## How it works
1. **Initialization**:
   - Loads four video feeds and the YOLOv12n model.
   - Starts with North (Frame 0) green, others red with calculated countdowns.
   
2. **Vehicle Detection**:
   - Detects vehicles in non-green frames, filtering for specified COCO classes.

3. **Tracking**:
   - Assigns IDs using the Tracker class based on vehicle center points (distance threshold: 35px).

4. **Trafic Signal Logic**
   - Green duration adjusts dynamically based on the farthest vehicle’s distance.
   - Yellow follows green for 5s.
   - Red timers show the time until green, updated in sequence.

5. **Display**:
   - Video grid shows bounding boxes, class names, IDs, and max distance.
   - Signal window displays lights with integer timers.

## Limitations
   - **Performance**: Depends on hardware; may lag with high-resolution videos.
   - **Model Compatibility**: Assumes YOLOv12n uses COCO indices [1, 2, 3, 6, 8] for vehicles.
   - **Video Looping**: Short videos may loop frequently, affecting timer continuity.
## Future Enhancements
   - Add vehicle count statistics for traffic analysis.
   - Support live camera feeds.
   - Implement adaptive yellow light timing.
## Contributing
Fork the repository, make improvements, and submit a pull request
