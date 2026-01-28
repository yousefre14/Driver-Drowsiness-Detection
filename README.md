# Driver Drowsiness Detection System

A real-time computer vision system that detects driver drowsiness using facial landmarks and eye aspect ratio (EAR) analysis. The system monitors eye closure patterns and triggers an alarm when prolonged drowsiness is detected.

## 🎯 Project Overview

This project implements a drowsiness detection system using OpenCV and dlib's facial landmark detection. By calculating the Eye Aspect Ratio (EAR) in real-time, the system can determine when a driver's eyes have been closed for a dangerous duration and sound an alarm to alert them.

## ✨ Features

- **Real-time face detection** using dlib's HOG-based detector
- **Eye Aspect Ratio (EAR) calculation** for precise drowsiness detection
- **Configurable thresholds** for sensitivity adjustment
- **Audio alarm system** with threading support
- **Visual feedback** displaying EAR values and drowsiness alerts
- **Webcam support** with configurable camera index
- **Live video feed** with eye contour visualization

## 🔧 How It Works

The system uses the Eye Aspect Ratio (EAR) metric to detect eye closure:

1. **Face Detection**: Detects faces in the video stream using dlib's frontal face detector
2. **Landmark Detection**: Identifies 68 facial landmarks, focusing on the eye regions
3. **EAR Calculation**: Computes the eye aspect ratio using the formula:
   ```
   EAR = (||p2 - p6|| + ||p3 - p5||) / (2 * ||p1 - p4||)
   ```
   where p1-p6 are the eye landmark coordinates
4. **Drowsiness Detection**: Monitors EAR over consecutive frames
5. **Alarm Trigger**: Sounds an alarm when eyes remain closed beyond the threshold

### Eye Aspect Ratio Explained

The EAR value decreases significantly when the eye is closed. The system:
- Uses a threshold of **0.3** to detect closed eyes
- Monitors for **48 consecutive frames** (approximately 1.6 seconds at 30 FPS) before triggering
- Averages EAR values from both eyes for more robust detection

## 📋 Requirements

### Python Version
- Python 3.6 or higher

### Dependencies

```
scipy
imutils
dlib
opencv-python (cv2)
playsound
numpy
```

### Additional Files Required

- **Facial Landmark Predictor**: Download `shape_predictor_68_face_landmarks.dat` from dlib's model repository
- **Alarm Sound** (optional): A `.wav` file for the alarm sound

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/driver-drowsiness-detection.git
   cd driver-drowsiness-detection
   ```

2. **Install required packages**
   ```bash
   pip install scipy imutils dlib opencv-python playsound numpy
   ```

3. **Download the facial landmark predictor**
   
   Download the pre-trained model from:
   - [dlib models repository](http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2)
   
   Extract and place the file in your project directory.

4. **Add an alarm sound** (optional)
   
   Place a `.wav` file in your project directory for the alarm sound.

## 💻 Usage

### Basic Usage

```bash
python detect_drowsiness.py --shape-predictor shape_predictor_68_face_landmarks.dat
```

### With Alarm Sound

```bash
python detect_drowsiness.py \
    --shape-predictor shape_predictor_68_face_landmarks.dat \
    --alarm alarm.wav
```

### With Custom Webcam

```bash
python detect_drowsiness.py \
    --shape-predictor shape_predictor_68_face_landmarks.dat \
    --alarm alarm.wav \
    --webcam 1
```

### Command-line Arguments

| Argument | Short | Required | Default | Description |
|----------|-------|----------|---------|-------------|
| `--shape-predictor` | `-p` | Yes | - | Path to facial landmark predictor |
| `--alarm` | `-a` | No | "" | Path to alarm `.WAV` file |
| `--webcam` | `-w` | No | 0 | Index of webcam on system |

## ⚙️ Configuration

You can adjust the detection sensitivity by modifying these constants in the code:

```python
EYE_AR_THRESH = 0.3           # Eye aspect ratio threshold for closed eyes
EYE_AR_CONSEC_FRAMES = 48     # Number of consecutive frames for alarm trigger
```

**Tuning Tips:**
- **Lower EYE_AR_THRESH**: More sensitive (triggers with partially closed eyes)
- **Higher EYE_AR_THRESH**: Less sensitive (requires more closed eyes)
- **Lower EYE_AR_CONSEC_FRAMES**: Faster alarm trigger
- **Higher EYE_AR_CONSEC_FRAMES**: Reduces false positives

## 🎬 Demo

When running, the system displays:
- **Live video feed** with green contours around detected eyes
- **EAR value** in the top-right corner
- **"DROWSINESS ALERT!"** message when drowsiness is detected
- **Audio alarm** (if configured) when drowsiness persists

### Controls
- Press **`q`** to quit the application

## 📊 Technical Details

### Facial Landmarks

The system uses dlib's 68-point facial landmark detector:
- **Left eye**: Points 36-41
- **Right eye**: Points 42-47

### Performance Considerations

- **Frame Rate**: Processes at approximately 30 FPS on modern hardware
- **Face Detection**: May slow down with multiple faces in frame
- **Lighting**: Works best in well-lit conditions
- **Head Orientation**: Most accurate when facing the camera directly

## 🛠️ Troubleshooting

### Common Issues

**Problem**: "Cannot find shape_predictor file"
- **Solution**: Ensure the path to `shape_predictor_68_face_landmarks.dat` is correct

**Problem**: "Webcam not found"
- **Solution**: Try different webcam indices (0, 1, 2) or check camera permissions

**Problem**: "Alarm not playing"
- **Solution**: Ensure the alarm file is a valid `.wav` format and the path is correct

**Problem**: "EAR value seems incorrect"
- **Solution**: Ensure good lighting and face the camera directly

**Problem**: "Too many false alarms"
- **Solution**: Increase `EYE_AR_CONSEC_FRAMES` value or adjust `EYE_AR_THRESH`

## 🔬 Algorithm Details

### Eye Aspect Ratio Formula

The EAR is calculated using vertical and horizontal eye landmarks:

```
     p2    p3
   p1         p4
     p6    p5

EAR = (d(p2,p6) + d(p3,p5)) / (2 * d(p1,p4))
```

Where `d(x,y)` is the Euclidean distance between points x and y.

### Detection Logic

1. Calculate EAR for both eyes
2. Average the two EAR values
3. If EAR < threshold:
   - Increment frame counter
   - If counter >= consecutive frame threshold:
     - Trigger alarm (if not already on)
     - Display warning
4. If EAR >= threshold:
   - Reset counter
   - Turn off alarm

## 🤝 Contributing

Contributions are welcome! Here are some ways you can contribute:

- Report bugs and issues
- Suggest new features or improvements
- Submit pull requests with enhancements
- Improve documentation

### Development Setup

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👏 Acknowledgments

- [dlib](http://dlib.net/) for the facial landmark detection model
- [OpenCV](https://opencv.org/) for computer vision tools
- [imutils](https://github.com/jrosebr1/imutils) for convenient video processing
- Original paper on Eye Aspect Ratio: [Real-Time Eye Blink Detection using Facial Landmarks](http://vision.fe.uni-lj.si/cvww2016/proceedings/papers/05.pdf)

## 📧 Contact

For questions, suggestions, or issues, please open an issue on GitHub or contact [your-email@example.com]

## 🚗 Safety Disclaimer

This system is designed as a research and educational project. While it can help detect drowsiness, it should NOT be relied upon as the sole safety mechanism in vehicles. Always:
- Get adequate rest before driving
- Take regular breaks on long journeys
- Pull over safely if you feel drowsy
- Use this system as an additional safety tool, not a replacement for alertness

## 📚 References

- [dlib facial landmark detection](http://blog.dlib.net/2014/08/real-time-face-pose-estimation.html)
- [Eye Aspect Ratio for Blink Detection](https://pyimagesearch.com/2017/05/08/drowsiness-detection-opencv/)
- [Facial Landmarks Research](https://www.cv-foundation.org/openaccess/content_cvpr_2014/papers/Kazemi_One_Millisecond_Face_2014_CVPR_paper.pdf)

---

**Made with ❤️ for safer driving**
