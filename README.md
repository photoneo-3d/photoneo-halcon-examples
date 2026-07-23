# Photoneo MVTec HALCON examples
![image](https://photoneo.com/files/dw/dw/github/Personal_Linkedin_banner_v4.png)

#### Prerequisites

[MVTec HALCON 21.11.0.0](https://www.mvtec.com/products/halcon) or newer, opened via the HDevelop IDE. <br />

![image](https://www.photoneo.com/wp-content/uploads/2018/09/halcon.png)

## Introduction
This repository provides the building blocks necessary for developing your custom MVTec HALCON application for working with [Photoneo](https://www.photoneo.com/) devices.
You may start your development based on one of the examples and modify it to suit your specific needs.

Each example is a single, self-contained `.hdev` script (an HDevelop procedure
named `main`) — there is no shared library code to import. Open the file
directly in HDevelop, replace the placeholder device ID with your device's,
and run it.

## Examples

Examples are grouped by the acquisition interface they use. Currently:

- **[GigEV](GigEV/README.md)** — acquisition over the GigE Vision protocol using HALCON's `GigEVision2` interface and Photoneo's GenICam feature set.
  - **[basic](GigEV/basic/README.md)** — connect & grab, freerun acquisition, chunk data, reading/writing device parameters, threaded multi-device scanning.
  - **[advanced](GigEV/advanced/README.md)** — point cloud reconstruction, surface normals, marker-space transforms, hardware trigger, texture/color modes, user sets.

## Getting started

1. Find your device's ID by running `info_framegrabber ('GigEVision2', 'info_boards', Information, device_list)` in HDevelop (see the leading comment in any example for expected output) or check `DeviceUserID` if you have one configured.
2. Open an example `.hdev` file and replace the placeholder `device_id := '<mac-addr>_Photoneo_<device-type>'` with your device's actual ID.
3. Run the script in HDevelop.

#### Support
Visit [www.photoneo.com](https://www.photoneo.com/) for the most up-to-date information and documents. If you encounter any issues while using the examples, please do not hesitate to contact our dedicated Support team at our [Help Center](https://www.photoneo.com/Help-Center) for prompt assistance.

#### License
Photoneo examples are distributed under the [BSD License](https://github.com/photoneo-3d/photoneo-halcon-examples/blob/main/LICENSE).
