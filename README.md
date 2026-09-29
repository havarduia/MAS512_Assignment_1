# MAS512 Assignment 1 – Group 1

The main notebook is `MAS512_assignment1_gr1.ipynb`.

## Before running: unzip the data

Two data folders are shipped as zip files to keep the hand-in small. The notebook
expects them unzipped in place, so extract both before running anything:

| Zip file                          | Unzip to                        | Used by        |
|-----------------------------------|---------------------------------|----------------|
| `assignment1.v2i.yolov11.zip`     | `assignment1.v2i.yolov11/`      | Q1 (training)  |
| `bin/ajit_test_data.zip`          | `bin/ajit_test_data/`           | Q2 (tracking)  |

From the project root (Linux/macOS):

```bash
unzip assignment1.v2i.yolov11.zip -d assignment1.v2i.yolov11
unzip bin/ajit_test_data.zip -d bin
```

On Windows, right-click each zip → *Extract All…* and pick the target folder from
the table above.

After unzipping, the layout should look like this:

```
MAS512_Assignment_1/
├── MAS512_assignment1_gr1.ipynb
├── assignment1.v2i.yolov11/
│   ├── data.yaml
│   ├── train/
│   ├── valid/
│   └── test/
└── bin/
    ├── track_30s.mp4
    └── ajit_test_data/
        ├── color_video/color_video.avi
        ├── depth_raw/
        └── depth_scale_json/
```

If you end up with a doubled folder (e.g. `bin/ajit_test_data/ajit_test_data/`),
move the inner folder's contents up one level.

## Environment

Python version is given in `python-version`. Install dependencies with:

```bash
pip install -r requirements.txt
```

## Outputs

- Videos and trained weights are written to `runs/`
- Figures are saved to `q2_figures/` … `q6_figures/`
