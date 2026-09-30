# Supplementary data - NBV-RPFL: Next-Best-View Planning with Reflectivity Prediction and Full-cycle Lookahead for Remanufacturing PCB Products

This dataset contains the research data used for the article "NBV-RPFL: Next-Best-View Planning with Reflectivity Prediction and Full-cycle Lookahead for Remanufacturing PCB Products".
The dataset contains 2D and 3D images of four different printed circuit board (PCB) workpieces and the corresponding robot capture poses.

## Content

The dataset contains the depth maps and 2D images caputred by an Ensenso N35 active stereo camera mounted on a UR5e robot arm.

```txt
├── README.md
├── workpieces.csv
├── Workpiece A
│   ├── depth-maps.csv
│   ├── depth-maps
│   │   ├── depth-map-1.tiff
│   │   └── ...
│   └── left-sensor-images
|       ├── left-image-1.png
│       └── ...
└── ...
```

## File descriptions

### `README.md`

This Readme file.

### `workpieces.csv`

Contains data about the workpieces.

Columns:

- `name`: workpiece name used in this dataset and the paper
- `width`: width of the workpiece in millimiters
- `depth`: depth of the workpiece in millimiters
- `n`: number of capture positions (thus 2D images and depth captures) for the workpiece

### `Workpiece */depth-maps.csv`

A csv file containing a list of capture robot poses for "Workpiece *".

Columns:

- `index`: index of the depth capture
- `x`: x coordinate of the position of the robot arm's tool center point (TCP) in millimiters (relative to the robot base)
- `y`: y coordinate of the position of the robot arm's tool center point (TCP) in millimiters (relative to the robot base)
- `z`: z coordinate of the position of the robot arm's tool center point (TCP) in millimiters (relative to the robot base)
- `rx`: rotation of the robot arm's tool center point (TCP) around the X axis in radians
- `ry`: rotation of the robot arm's tool center point (TCP) around the Y axis in radians
- `rz`: rotation of the robot arm's tool center point (TCP) around the Z axis in radians
- `q1`: joint position of the robot arm's first joint in radians
- `q2`: joint position of the robot arm's second joint in radians
- `q3`: joint position of the robot arm's third joint in radians
- `q4`: joint position of the robot arm's fourth joint in radians
- `q5`: joint position of the robot arm's fifth joint in radians
- `q6`: joint position of the robot arm's sixth joint in radians

### `Workpiece */depth-maps/depth-map-*.tiff`

Each TIFF file contains one depth capture, numbered as in `Workpiece */depth-maps.csv`.
The image has three channels stored in the RGB slots, but they do not represent colors, but rather the X, Y and Z coordinates of the point observed at each pixel, as 32-bit floating-point values.
Coordinates are in millimeters, expressed relative to the robot base.
Pixels with no valid measurement are set to NaN.

### `Workpiece */left-sensor-images/left-image-*.png`

The Ensenso camera's left sensor image at recorded at the same time as the depth capture.
From the [Ensenso manual](https://manual.ensenso.com/latest/guides/getting-3d-data/aligning-images-with-3d-data.html):
"The pixels of a camera’s left sensor images can be aligned with the structured 3D data in the disparity and point map."
This means that the depth maps and the left images can be overlayed and the corresponding data in different images are at the same pixel positions.
