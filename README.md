
# MovPed: Multi-Modal Dataset for Moving Pedestrian Detection

MovPed is a multi-modal perception dataset for **moving pedestrian detection** in urban driving scenarios. It provides synchronized data from a Dynamic Vision Sensor (DVS) event camera and a standard RGB camera, along with depth maps and precomputed detection results. This dataset is designed to facilitate research on event-based and frame-based sensor fusion for robust, low-latency pedestrian detection in autonomous driving.

## Dataset Structure

Each sequence (scene) in MovPed is organized in a directory containing the following files and sub-folders:

- **camera_rgb/** – RGB camera images for the scene (one image per frame).
- **depth_cam/** – Depth maps corresponding to each RGB frame.
- **events.aedat4** – DVS event stream recording for the entire scene in **AEDAT 4** format. Each event is a tuple `[t, x, y, p]` representing timestamp, pixel coordinates, and polarity. Recommended viewer: [dv-processing](https://dv-processing.inivation.com/rel_1_7/index.html).
- **instance_segmentation_middle/** – Contains instance-level semantic segmentation masks of pedestrians for each RGB frame from the middle camera viewpoint.
- **instance_segmentation_middle_gt/** – Ground-truth bounding boxes derived from the instance segmentation masks. These can be used to evaluate detection models or train segmentation-aware pedestrian classifiers.
- **yolo_det_pro/** – YOLO detection results with APP (Active Pixel Percentage) values computed via epipolar constraint filtering.
- **scene_meta.json** – Scene-level metadata including sensor configuration and scenario details.

```
MovPed/
├── scene_01/
│   ├── camera_rgb/
│   ├── depth_cam/
│   ├── yolo_det_pro/
│   ├── events.aedat4
│   └── scene_meta.json
├── scene_02/
└── ...
```

## scene_meta.json Example

```json
{
  "DVS_FPS": 1000,
  "Intensity_Threshold": 0.2,
  "RGB_FPS": 100,
  "Xs": 0.1,
  "ego_velocity": 5,
  "fov": 90,
  "image_h": 260,
  "image_w": 346,
  "pedestrian_delay": 0.0,
  "pedestrian_direction": "cross",
  "pedestrian_veloctiy": 2
}
```

## Data Subset Note

This repository contains a **subset** of the full MovPed dataset for academic use. Full dataset release may be considered in future updates.

## Tools and Dependencies

- [dv-processing](https://dv-processing.inivation.com/rel_1_7/index.html) for reading `.aedat4` event files
- Python 3.x, OpenCV, NumPy for image/data handling


## License

This dataset is shared under the **CC BY 4.0** license.

