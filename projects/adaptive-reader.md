# 🔬 Adaptive Reader — AI Eye-Tracking Reading Assistant

> A Google Chrome Extension that detects when you're struggling with a word and automatically shows its definition — just by watching your eyes.

## 🎯 Core Idea

Adaptive Reader is designed to make web reading more accessible without requiring keyboard or mouse interaction.

```text
Stare at a difficult word
        ↓
AI tracks your gaze
        ↓
Repeated rereading / hesitation is detected
        ↓
A glass popup appears
        ↓
Definition + Listen button
```

## 🧠 How It Works

1. The webcam captures the user's face.
2. Google MediaPipe Face Landmarker detects facial and iris landmarks.
3. A one-time 5-point calibration learns the relationship between eye position and screen coordinates.
4. An affine transform converts gaze measurements into an estimated webpage position.
5. The extension identifies the word nearest to the gaze point.
6. A **Struggle Score** combines repeated visits, dwell time, regressions, and word complexity.
7. When the score crosses a threshold, Adaptive Reader displays a definition card.
8. The user can listen to the word using Chrome's Web Speech API.

## ✨ Features

| Feature | Details |
|---|---|
| 📸 Eye Tracking | Tracks iris landmarks from MediaPipe face mesh data |
| 🎯 5-Point Calibration | Uses least-squares affine transformation for gaze mapping |
| 🏃 Head Movement Compensation | Helps maintain gaze accuracy when the user moves |
| 🔵 Blue Gaze Dot | Shows the estimated gaze position |
| 🟩 Green Word Box | Highlights the word closest to the gaze |
| 🧮 Struggle Score | Uses repeated visits, dwell time, regressions, and complexity |
| 💬 Popup Cards | Up to 3 cards, with 8-second timers and hover-to-pause |
| 🌍 6 Languages | English, Tamil, Hindi, Telugu, Malayalam, and French |
| 🔊 Text-to-Speech | Reads the detected word in the selected language |
| 📷 Camera Panel | Draggable and collapsible acrylic-glass panel |
| 🎨 Glassmorphism UI | Frosted-glass interface across the extension |

## 🔧 Tech Stack

- **Chrome Extension — Manifest V3**
- **Google MediaPipe Tasks Vision 0.10.3**
- **Face Landmarker float16 model**
- **Vanilla JavaScript** — zero frameworks, zero npm
- **Web Speech API**
- **Free Dictionary API** — `api.dictionaryapi.dev`
- **CSS Glassmorphism** with `backdrop-filter: blur`
- **Custom affine-transform mathematics**

## 📁 Project Structure

```text
adaptive-reader/
├── manifest.json          # Chrome extension configuration
├── content.js             # Eye tracking, word detection, scoring, popup UI
├── mediapipe-runner.js    # MediaPipe model loading and frame processing
├── background.js          # Minimal extension service worker
├── popup.html             # Extension toolbar popup
├── popup.js               # Toolbar interaction logic
├── popup.css              # Toolbar styling
├── rules.json             # Extension security/network rules
├── rebuild.js              # Developer helper script
└── suffix.js               # Developer helper script
```

## 🚀 Installation

1. Clone or download the project.
2. Open Chrome and navigate to `chrome://extensions/`.
3. Enable **Developer Mode**.
4. Select **Load Unpacked** and choose the `adaptive-reader` folder.
5. Open any webpage.
6. Click the extension icon and choose **Start Calibration**.
7. Stare at each calibration dot for about 2 seconds.
8. Start reading and let Adaptive Reader assist when it detects difficulty.

## 🔒 Design Notes

Adaptive Reader is intended to work locally in the browser for gaze estimation and interaction. Webcam access is required for eye tracking, and users should understand that gaze estimation from a normal webcam is approximate rather than medical-grade eye tracking.

## 💡 Why This Project?

The goal is to explore how computer vision and human-computer interaction can reduce friction for people who struggle with reading difficult vocabulary. Instead of requiring the reader to stop, select a word, and search for its meaning, the interface attempts to provide assistance from natural reading behavior.

## 🛣️ Future Improvements

- Improve gaze calibration robustness across different webcams and lighting conditions.
- Add personalized struggle-score thresholds.
- Add more language and dictionary providers.
- Improve word-level gaze estimation on complex webpages.
- Add privacy controls and clearer camera-status indicators.
- Package the extension for easier installation and distribution.
