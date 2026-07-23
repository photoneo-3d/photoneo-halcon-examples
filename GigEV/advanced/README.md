# Advanced examples

Point cloud reconstruction, alternate trigger/texture modes, and device
configuration workflows. These build directly on the concepts in the
[basic examples](../basic/README.md) and the GenICam vocabulary described in
the [GigEV README](../README.md) — read those first if a term here (component,
`Scan3dOutputMode`, chunk data) is unfamiliar.

| Example | Demonstrates |
| --- | --- |
| [`hw_trigger.hdev`](hw_trigger.hdev) | Hardware-triggered acquisition: `TriggerSource` set to `Line1` instead of `Software`, with a longer grab timeout suited to an external trigger signal of unknown period. |
| [`pointcloud_with_calibratedABC.hdev`](pointcloud_with_calibratedABC.hdev) | Reconstructing a textured 3D point cloud the simplest way: `Scan3dOutputMode = CalibratedABC_Grid` gives direct X/Y/Z per pixel, which is combined with the `Intensity` component into a HALCON 3D object model (`xyz_to_object_model_3d`) and rendered with `visualize_object_model_3d`. |
| [`pointcloud_with_projectedC.hdev`](pointcloud_with_projectedC.hdev) | Reconstructing the same point cloud from `Scan3dOutputMode = ProjectedC` (depth-only `Range`), which is cheaper to transfer. Pre-fetches `CoordinateMapA`/`CoordinateMapB` and the `Scan3dFocalLength`/`Scan3dAspectRatio`/`Scan3dPrincipalPointU`/`Scan3dPrincipalPointV` features once, then reuses them every frame to derive X/Y from the depth map in-process — see [Static coordinate maps](../README.md#static-coordinate-maps) for the math. |
| [`pointcloud_with_normals_and_texture.hdev`](pointcloud_with_normals_and_texture.hdev) | Enabling the `Normal` component alongside `Range`, and attaching both per-point intensity and per-point normal vectors (`point_normal_x/y/z`) as 3D object model attributes. |
| [`pointcloud_with_marker_space.hdev`](pointcloud_with_marker_space.hdev) | Using Photoneo's marker-plate recognition (`CoordinateSpace = MarkerSpace`, `RecognizeMarkers`) to compute a camera-to-marker 3D pose from the `CurrentCameraToCoordinateSpaceTransformation` chunk, then applying that pose to rigidly transform (`rigid_trans_object_model_3d`) the reconstructed point cloud into marker space. |
| [`show_confidence_map.hdev`](show_confidence_map.hdev) | Enabling the `Confidence` component next to `Range`/`Intensity` to retrieve the per-pixel `Confidence8` reliability map for each point. |
| [`show_texture.hdev`](show_texture.hdev) | Surveying the different ways to retrieve a 2D texture/intensity image depending on device family (PhoXi, MotionCam-3D, MotionCam-3D Color) — `TextureSource`/`CameraTextureSource`, `Mono10`/`Mono12`/`RGB8`/`Mono16` pixel formats — plus the color camera unit's own `ColorCamera` component and `CameraSpace` reprojection. |
| [`ycocg_color_convert.hdev`](ycocg_color_convert.hdev) | Decoding the compact `Mono16` YCoCg-encoded `ColorCamera` payload back into an RGB8 image via bit manipulation — used when `Mono16` is chosen over `RGB8` for faster color transfer (see [Color texture](../README.md#color-texture)). |
| [`user_sets.hdev`](user_sets.hdev) | Changing device settings (`ShutterMultiplier`, `LaserPower`, `LEDPower`, `HardwareTrigger`, `MaxInaccuracy`) and persisting them on-device to `UserSet1` via `UserSetSave`, for later recall with `UserSetLoad`. |
