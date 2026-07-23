# Basic examples

Minimal, single-feature scripts. Start here if you are integrating a Photoneo
device with HALCON for the first time — each example isolates one concept
from the [common example structure](../README.md#genicam-features) so it's
easy to see what changes.

| Example | Demonstrates |
| --- | --- |
| [`connect_and_grab.hdev`](connect_and_grab.hdev) | The minimal connect → configure → grab → close flow. Connects, applies the `Default` user set, negotiates the GVSP packet size, switches to software trigger, and grabs both a single image (`grab_image_async`) and a full multi-part payload (`grab_data_async`) for 5 frames. Good template for a new script. |
| [`freerun.hdev`](freerun.hdev) | Continuous (freerun) acquisition with `TriggerMode` set to `Off`, using the blocking `grab_image` / `grab_data` calls instead of the `_start`/`_async` pair. |
| [`read_chunk_data.hdev`](read_chunk_data.hdev) | Reading per-frame GenICam chunk data: enables `ChunkModeActive` and pulls the `Temperature` and `MainCameraCalibrationData` chunks (camera matrix, distortion coefficients, sensor axis/position) alongside each grabbed payload. |
| [`read_write_data.hdev`](read_write_data.hdev) | Reading and writing plain device parameters (`ShutterMultiplier`, `Width`/`Height`, `LaserPower`, `LEDPower`, `MaximumFPS`, `MaxInaccuracy`) — no image is grabbed, only feature access. |
| [`threaded_scanning.hdev`](threaded_scanning.hdev) | Driving two devices concurrently. Factors connection/freerun/software-trigger logic into reusable procedures (`connect_to_device`, `freerun`, `software_trigger`) and runs one device in freerun and another under software trigger in parallel via `par_start`/`par_join`. |

See the [GigEV README](../README.md) for the GenICam vocabulary (components,
trigger configuration, `Scan3dOutputMode`) these scripts build on.
