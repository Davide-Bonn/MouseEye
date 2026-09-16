<div align="center">

<img src="logo.svg" alt="MouseEye Logo" width="280" />

# MouseEye

**Control your mouse cursor with your eyes — hands-free**

Move the cursor by looking around. Blink your left eye to left-click, right eye to right-click.

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Face%20Mesh-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://mediapipe.dev)
[![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)](https://opencv.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

---

</div>

## Overview

MouseEye uses MediaPipe's Face Mesh with its 478-point model to track your face in real time. It maps iris landmark positions to screen coordinates for cursor movement and detects eye blinks via the Eye Aspect Ratio (EAR) to trigger mouse clicks — all without touching a mouse or keyboard.

---

## How It Works

```
Webcam --> Face Mesh (478 pts) --> Iris Center --> Cursor Position (pyautogui)
                                   Eye Aspect Ratio (EAR) --> Click Events
```

| Step | Detail |
|:---|:---|
| Iris Tracking | Iris center landmarks are mapped to screen coordinates using `pyautogui` |
| Blink Detection | Eye Aspect Ratio (EAR) drops below threshold when an eye closes |
| Left Click | Blink left eye (EAR of left eye falls below `BLINK_THRESHOLD`) |
| Right Click | Blink right eye (EAR of right eye falls below `BLINK_THRESHOLD`) |
| Smoothing | Cursor position is smoothed over frames to reduce jitter |
| Cooldown | A cooldown period prevents repeated accidental clicks |

---

## Quick Start

```bash
git clone https://github.com/Davide-Bonn/MouseEye.git
cd MouseEye
pip install -r requirements.txt
python mouse_eye.py
```

Press `q` to quit.

---

## Configuration

| Parameter | Default | Description |
|:---|:---|:---|
| `SMOOTHING` | `0.5` | Cursor smoothing factor (0 = no smoothing, 1 = maximum) |
| `BLINK_THRESHOLD` | `0.21` | EAR value below which a blink is registered |
| `CLICK_COOLDOWN` | `1.0` | Seconds between consecutive clicks to prevent repeats |
| `CAM_INDEX` | `0` | Webcam device index |

---

## Key Landmarks

| Eye | Landmarks | Iris Landmarks |
|:---|:---|:---|
| Right | 159 (top), 33-133 (sides), 145 (bottom) | 468-472 |
| Left | 386 (top), 263-362 (sides), 374 (bottom) | 473-477 |

---

## Dependencies

- `mediapipe`
- `opencv-contrib-python`
- `pyautogui`
- `numpy`

---

## License

MIT
