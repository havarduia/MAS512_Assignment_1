# MAS512 Assignment 1 – Group 1

Repository: <https://github.com/havarduia/MAS512_Assignment_1>

| Deliverable  | File                                  |
|--------------|---------------------------------------|
| Notebook     | `MAS512_assignment1_gr1.ipynb`        |
| Presentation | `MAS512 - Assignment 1 - Group 1.pdf` |

Each question is solved in **one code cell**. Running a cell reproduces that
question's outputs. The cells are independent of each other, apart from Q1.b,
Q1.c and Q2, which use the YOLO weights that Q1.a trained (already committed
in `runs/q1_model/weights/best.pt`).

## Questions

| Q  | Task | Data | Outputs |
|----|------|------|---------|
| 1a | Train YOLO11n on the swinging load and plot its KPIs on the test split | `assignment1.v2i.yolov11/` | `runs/q1_model*/` |
| 1b | Five random test-video frames with bounding box and centre | `bin/ajit_test_data/color_video/` | inline |
| 1c | Box centre and aligned depth for every test-video frame | `bin/ajit_test_data/` (colour + raw depth) | inline |
| 2  | Track the load and draw its trajectory; 3D path in the XY and XZ planes | `bin/ajit_test_data/` | `runs/q2_tracking.mp4`, `q2_figures/` |
| 3  | Person segmentation, tracking, counting in the scene and in a region | `bin/track_30s.mp4` | `runs/q3_counting.mp4`, `q3_figures/` |
| 4  | CNN for motor state of health vs. the class baseline | `fault-classification-class/` | `q4_figures/` |
| 5  | CIFAR-10: model fusion, transfer learning, fine-tuning, comparison | downloaded by Keras | `q5_figures/` |
| 6  | Dense autoencoder: original, latent vector, reconstruction, error per class | `fault-classification-class/` | `q6_figures/` |

## Setup

Python 3.10 (see `python-version`), then:

```bash
pip install -r requirements.txt
```

The notebook is written for an NVIDIA GPU. `requirements.txt` explains the
CUDA pins for Linux and Windows.

## Unzip the data first

Two data folders are shipped as zip files. Run these from the project root:

```bash
unzip assignment1.v2i.yolov11.zip      # -> assignment1.v2i.yolov11/
unzip bin/ajit_test_data.zip -d bin    # -> bin/ajit_test_data/
```

Both zips already contain their top-level folder, so do **not** extract them
into a new folder of the same name. On Windows, choose *Extract All…* with the
project root as the target for the first zip and `bin\` for the second. If you
end up with a doubled folder (for example
`assignment1.v2i.yolov11/assignment1.v2i.yolov11/`), move the inner folder's
contents up one level.

Expected layout:

```
MAS512_Assignment_1/
├── MAS512_assignment1_gr1.ipynb
├── assignment1.v2i.yolov11/
│   ├── data.yaml
│   ├── train/  valid/  test/
├── bin/
│   ├── track_30s.mp4
│   └── ajit_test_data/
│       ├── color_video/color_video.avi
│       ├── depth_raw/
│       └── depth_scale_json/
├── fault-classification-class/
│   ├── training/  testing/
└── runs/q1_model/weights/best.pt
```

## Running notes

- **Q1.a retrains YOLO**: about 12 min on a GPU, with `device=0`. A re-run
  writes to a new folder (`runs/q1_model2`, …) and never overwrites the
  committed run. Q1.b, Q1.c and Q2 always load `runs/q1_model/weights/best.pt`.
- **Q3** downloads `yolo11n-seg.pt` on first use if it is missing.
- **Q5** downloads CIFAR-10 (~170 MB) on the first run and trains three
  models. It is by far the longest cell.
- All figures are written to `q2_figures/` … `q6_figures/` and videos to
  `runs/`.

## Results

| Q | Key result |
|---|------------|
| 1a | Test split: mAP50 0.995, mAP50-95 0.854, precision 1.000, recall 1.000 |
| 1c | Load found in 284 of 300 test-video frames, depth 2.6–4.1 m |
| 4 | Proposed CNN 0.995 accuracy with 1,681 parameters; class baseline 0.980 with 9,339 |
| 5 | Test accuracy: model fusion 0.901, fine-tuning 0.890, transfer learning 0.864 |
