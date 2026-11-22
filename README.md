# YOLO ByteTrack Trajectory Tracking

Real-time multi-object detection, tracking, and trajectory visualization in Python using [Ultralytics YOLO](https://docs.ultralytics.com/) and the ByteTrack tracker, rendered with OpenCV.

Each detected object receives a persistent track ID, a unique color, and a trailing path that shows where it has moved over the most recent frames.

## Demo

https://github.com/user-attachments/assets/a4d2bbdb-94c7-4d6c-ae49-2c60e26e92c2

**Keywords:** object tracking, multi-object tracking (MOT), trajectory visualization, YOLO, Ultralytics, ByteTrack, OpenCV, computer vision, object detection, vehicle tracking, pedestrian tracking, Python, video analytics

## Features

- Object detection with a YOLO model (`yolo26n.pt` by default)
- Multi-object tracking with persistent IDs using ByteTrack
- Per-object trajectory trails with a configurable length
- Bounding boxes, class labels, track IDs, and center points drawn on each frame
- Consistent random color assigned to each track ID
- Live preview window; press `q` to quit

## Requirements

- Python 3.8 or newer
- [ultralytics](https://pypi.org/project/ultralytics/)
- [opencv-python](https://pypi.org/project/opencv-python/)
- [numpy](https://pypi.org/project/numpy/)

## Installation

```bash
git clone https://github.com/mabdullahkhurshid/yolo-bytetrack-trajectory-tracking.git
cd yolo-bytetrack-trajectory-tracking
pip install -r requirements.txt
```

Ultralytics downloads the model weights automatically on first run if they are not found locally.

## Usage

1. Place your input video in the project folder and set `VIDEO_PATH` in `trajectory.py` to its file name (the default is `03.mp4`).
2. Run:

```bash
python trajectory.py
```

3. A window titled **Trajectory Tracking** opens. Press `q` to stop.

## Configuration

All settings are constants at the top of `trajectory.py`:

| Setting | Default | Description |
| --- | --- | --- |
| `MODEL_PATH` | `yolo26n.pt` | YOLO model weights file |
| `VIDEO_PATH` | `03.mp4` | Input video file |
| `TRAJECTORY_LENGTH` | `100` | Number of recent positions kept per object |
| `LINE_THICKNESS` | `3` | Thickness of trajectory lines (px) |
| `BOX_THICKNESS` | `2` | Thickness of bounding boxes (px) |
| `FONT_SCALE` | `0.7` | Label text size |

To use a different model, set `MODEL_PATH` to any compatible Ultralytics weights file (for example, a larger variant for higher accuracy or a custom-trained model).

## How It Works

1. Each video frame is read with OpenCV and resized to 1280x720.
2. `model.track()` runs YOLO detection and ByteTrack association with `persist=True`, so IDs stay consistent across frames.
3. The center point of every tracked bounding box is appended to a per-ID `deque` capped at `TRAJECTORY_LENGTH`.
4. Consecutive stored points are connected with lines to draw each object's path.
5. Each annotated frame is shown in a live window.

## Project Structure

```
.
├── trajectory.py      # Detection, tracking, and visualization script
├── requirements.txt   # Python dependencies
└── README.md
```

## Troubleshooting

- **"Unable to open video."**: Check that `VIDEO_PATH` points to an existing, readable video file.
- **No window appears on a headless server**: `cv2.imshow` requires a display. Run on a machine with a GUI.
- **Slow playback**: Use a smaller model or run on a machine with a supported GPU.

## Author

[Muhammad Abdullah](https://github.com/mabdullahkhurshid)

## Acknowledgements

- [Ultralytics YOLO](https://github.com/ultralytics/ultralytics)
- [ByteTrack](https://github.com/ifzhang/ByteTrack)
- [OpenCV](https://opencv.org/)
