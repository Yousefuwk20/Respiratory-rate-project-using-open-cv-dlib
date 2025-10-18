# Respiratory Rate Detection using OpenCV and Dlib

A real-time respiratory rate monitoring system that uses computer vision techniques to detect and measure breathing patterns from video input. This project implements a non-contact method for respiratory rate estimation based on chest movement analysis.


## 🔍 Overview

This project implements a computer vision-based approach to measure respiratory rate (breaths per minute) from video recordings. It uses facial detection to identify the subject and analyzes chest movement patterns to calculate breathing frequency. The system provides both live video capture and pre-recorded video analysis capabilities through an intuitive GUI interface.

**Research Foundation:** This implementation is based on the research paper available at: https://pubmed.ncbi.nlm.nih.gov/33175740/

## ✨ Features

- **Real-time Video Capture**: Record live video from webcam for respiratory analysis
- **Pre-recorded Video Analysis**: Analyze existing video files (supports .avi, .mp4, .MOV formats)
- **Automated Face Detection**: Uses Dlib's face detector to automatically locate the subject
- **Chest Region Tracking**: Automatically identifies and tracks the chest region for analysis
- **Signal Processing**: Implements Butterworth bandpass filtering for noise reduction
- **Peak Detection**: Identifies breathing cycles using scipy peak detection
- **Visual Feedback**: Displays filtered signal with detected peaks in real-time
- **User-friendly GUI**: Tkinter-based interface for easy interaction
- **Respiration Rate Calculation**: Provides BPM (Breaths Per Minute) measurement

## 🔧 How It Works

1. **Face Detection**: The system uses Dlib's frontal face detector to locate the subject's face in the video frame
2. **Chest Region Identification**: Based on face position, the chest region is automatically calculated and tracked
3. **Video Processing**: The chest region is cropped and analyzed frame-by-frame
4. **Signal Extraction**: Pixel intensity values are summed for each frame to create a temporal signal
5. **Signal Filtering**: A Butterworth bandpass filter (0.16-0.5 Hz) removes noise and isolates breathing frequency
6. **Peak Detection**: Breathing cycles are identified by detecting peaks in the filtered signal
7. **Rate Calculation**: Respiratory rate (BPM) is calculated based on the number of detected peaks over time

## 📦 Requirements

### Dependencies

- Python 3.x
- numpy
- opencv-python (cv2)
- dlib
- scipy
- matplotlib
- Pillow (PIL)
- tkinter (usually comes with Python)

### System Requirements

- Webcam (for live video capture)
- Sufficient lighting for clear video capture
- Background image file: `18143510_1006.webp` (for GUI background)

## 💻 Usage

### Running the Application

1. **Launch the GUI application**
   ```bash
   jupyter notebook Res_rate_project.ipynb
   ```
   Run all cells in the notebook to start the GUI.

2. **Using the Interface**

   The application provides two main options:

   #### Option 1: Analyze Pre-recorded Video
   - Click the **"Select Video"** button
   - Browse and select a video file (.avi, .mp4, or .MOV)
   - The system will process the video and display:
     - Face and chest region detection
     - Cropped chest region video
     - Filtered signal with detected peaks
     - Calculated respiration rate (BPM)

   #### Option 2: Analyze Live Video
   - Click the **"Live Video"** button
   - The webcam will activate for 30 seconds
   - Position yourself so your face and chest are visible
   - Press 'q' to stop recording early, or wait for automatic stop
   - The captured video will be automatically analyzed
   - Results will be displayed in the GUI

### Expected Output

- **Respiration Rate (BPM)**: Displayed in the GUI
- **Visualization**: Graph showing filtered signal with detected breathing peaks
- **Processed Video**: Saved in `output/output.mp4` (cropped chest region)
- **Live Recording**: Saved as `live_video.mp4` (if using live capture)

## 🔬 Technical Details

### Signal Processing Pipeline

1. **Normalization**
   ```python
   normalized_data = (data - min(data)) / (max(data) - min(data))
   ```

2. **Butterworth Bandpass Filter**
   - Type: Bandpass
   - Order: 5
   - Frequency Range: 0.16 - 0.5 Hz (corresponds to 9.6 - 30 BPM)
   - Nyquist Frequency: 15 Hz (half of 30 fps sampling rate)

3. **Peak Detection**
   - Uses scipy's `find_peaks` function
   - Detects local maxima in the filtered signal
   - Each peak represents one breathing cycle

4. **Rate Calculation**
   ```python
   respiration_rate = (number_of_peaks / video_duration) × 60
   ```

### Chest Region Calculation

The chest region is determined relative to the detected face:
- **Horizontal**: Extends 75% of face width on each side
- **Vertical**: Starts 30% below face bottom, extends one face-length downward

### Video Parameters

- **Default FPS**: 30 frames per second
- **Default Resolution**: 640x480 (live capture)
- **Recording Duration**: 30 seconds (configurable)
- **Video Codec**: MP4V

## 📊 Results

The system provides:
- **Respiration Rate**: Measured in breaths per minute (BPM)
- **Visual Analysis**: Real-time plot showing filtered breathing signal
- **Peak Markers**: Red 'x' markers indicating detected breath cycles
- **Processed Video**: Cropped chest region for visual verification

### Accuracy Considerations

- Works best with stable camera position
- Requires adequate lighting
- Subject should remain relatively still
- Loose-fitting clothing improves detection
- Normal breathing rate: 12-20 BPM for adults

---

**Disclaimer**: This project is for educational and research purposes only. It is not intended for medical diagnosis or clinical use. Always consult healthcare professionals for medical advice.
