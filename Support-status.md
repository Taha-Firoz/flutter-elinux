## Supported platforms
This software supports x64 and Arm64 (aarch64, ARMv8) architectures on Linux which supports either Wayland backend or DRM backend.

## Tested devices
| Board / SoC | Vendor | OS / BSP | Backend | Status |
| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: |
| [Jetson Nano](https://developer.nvidia.com/embedded/jetson-nano-developer-kit) | NVIDIA | JetPack 4.3 | Wayland | :heavy_check_mark: |
| [Jetson Nano](https://developer.nvidia.com/embedded/jetson-nano-developer-kit) | NVIDIA | JetPack 4.3 | DRM | :heavy_check_mark: ([#1](https://github.com/sony/flutter-embedded-linux/issues/1))|
| [Raspberry Pi 4 Model B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/) | Raspberry Pi Foundation | Ubuntu 20.10 | Wayland | :heavy_check_mark: |
| [Raspberry Pi 4 Model B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/) | Raspberry Pi Foundation | Ubuntu 20.10 | DRM | :heavy_check_mark: ([#9](https://github.com/sony/flutter-embedded-linux/issues/9)) |
| [i.MX 8MQuad EVK](https://www.nxp.com/design/development-boards/i-mx-evaluation-and-development-boards/evaluation-kit-for-the-i-mx-8m-applications-processor:MCIMX8M-EVK) | NXP | Sumo (kernel 4.14.98) | Wayland | :heavy_check_mark: |
| [i.MX 8M Mini EVKB](https://www.nxp.com/design/development-boards/i-mx-evaluation-and-development-boards/evaluation-kit-for-the-i-mx-8m-mini-applications-processor:8MMINILPD4-EVK) | NXP | Zeus (kernel 5.4.70) | Wayland | :heavy_check_mark: |
| [RB5 Development Kit](https://developer.qualcomm.com/qualcomm-robotics-rb5-kit) | Qualcomm | Ubuntu 18.04.05 | DRM | :heavy_check_mark: |
| Zynq | Xilinx | - | - | Not tested |
| Desktop (x86_64) | Intel | Ubuntu 20.04 | Wayland | :heavy_check_mark: |
| Desktop (x86_64) | Intel | Ubuntu 20.04 | DRM | :heavy_check_mark: |
| Desktop (x86_64) | Intel | Ubuntu 20.04 | X11 | :heavy_check_mark: |
| QEMU (x86_64) | QEMU | [AGL (Automotive Grade Linux)](https://wiki.automotivelinux.org/) koi | Wayland | :heavy_check_mark: |
| QEMU (x86_64) | QEMU | [AGL (Automotive Grade Linux)](https://wiki.automotivelinux.org/) koi | DRM | :heavy_check_mark: |

Note
 - i.MX 8M platforms don't support applications using EGL on GBM, which means the DRM-GBM backend won't work on i.MX 8M devices.

## Tested Wayland compositors
|||||||||||
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
[Weston](https://gitlab.freedesktop.org/wayland/weston/-/blob/master/README.md) | :heavy_check_mark: | [Sway](https://swaywm.org/) | :heavy_check_mark: | [Wayfire](https://wayfire.org/) | :heavy_check_mark: | [Gnome](https://www.gnome.org/) | :heavy_check_mark: | [Phosh](https://source.puri.sm/Librem5/phosh) | :heavy_check_mark: |
| [Cage](https://www.hjdskes.nl/projects/cage/) | :heavy_check_mark: | [Lomiri](https://lomiri.com/) | :heavy_check_mark: | [Plasma Wayland](https://community.kde.org/Plasma/Wayland) | :heavy_check_mark: | [Plasma Mobile](https://www.plasma-mobile.org/) | :heavy_check_mark: | [GlacierUX](https://wiki.merproject.org/wiki/Nemo/Glacier) | :heavy_check_mark: |