## 1. Self-building
Use `--target-backend-type` option to select display backends. Default is Wayland.

### Note:
- We do **not** expect to use `x11` in embedded products, it is just for **debugging** on Linux desktops.
- In general, few devices support `EGLStream` (NVIDIA only?). Check it is supported or not before using it on your target devices.
  - See also: [Tested devices](https://github.com/sony/flutter-embedded-linux#tested-devices)
- `gbm` and `eglstream` will basically work but they are still development phase (have some issues).
  - See: [sony/flutter-embedded-linux/issues for DRM](https://github.com/sony/flutter-embedded-linux/issues?q=is%3Aissue+is%3Aopen+label%3Adrm)

|Build mode |Target backend| Command |
| --------- | ------------ | ------- |
| release   | wayland      | `flutter-elinux build elinux` |
|           | x11          | `flutter-elinux build elinux --target-backend-type=x11` |
|           | gbm          | `flutter-elinux build elinux --target-backend-type=gbm` |
|           | eglstream    | `flutter-elinux build elinux --target-backend-type=eglstream` |
| debug     | wayland      | `flutter-elinux build elinux --debug` |
|           | x11          | `flutter-elinux build elinux --debug --target-backend-type=x11` |
|           | gbm          | `flutter-elinux build elinux --debug --target-backend-type=gbm` |
|           | eglstream    | `flutter-elinux build elinux --debug --target-backend-type=eglstream` |
| profile   | wayland      | `flutter-elinux build elinux --profile` |
|           | x11          | `flutter-elinux build elinux --profile --target-backend-type=x11` |
|           | gbm          | `flutter-elinux build elinux --profile --target-backend-type=gbm` |
|           | eglstream    | `flutter-elinux build elinux --profile --target-backend-type=eglstream` |

## 2. Build artifacts
The artifacts will be put in your project under `./build/<target_arch>/<build_mode>/bundle`. Alongside your executable binary in the bundle directory there are two directories:
- `lib/` contains the required .so library files
- `data/` contains the application’s data assets, such as fonts or images

![artifacts](https://github.com/sony/flutter-elinux/blob/main/doc/images/artifact-relationships.png)

### Pre-built images
flutter-elinux download the Flutter engine artifacts such as `libflutter_engine.so` and `libflutter_elinux_wayland.so` to `<flutter-elinux_install_path>/flutter/bin/cache/artifacts/engine` directory automatically when you build your Flutter app. These .so files are download from [sony/flutter-embedded-linux/releases](https://github.com/sony/flutter-embedded-linux/releases) built with a specific toolchain. Therefore, if you want to use your toolchain, you need to build it yourself.

For reference, the toolchain that the current .so files are built is below.

| .so file  | toolchain | sysroot | glibc |
| --------- | --------- | ------- | ----- |
| libflutter_engine.so | clang/llvm (Google Chromium) | Google Chromium | 2.29 |
| libflutter_elinux_*.so | clang/llvm (Ubuntu 18.04) | Ubuntu 18.04 for arm64 | 2.27 |

### How to build libflutter_engine.so and libflutter_elinux_*.so
See the following links.
- libflutter_engine.so: [Building Flutter Engine from source](https://github.com/sony/flutter-embedded-linux/wiki/Building-Flutter-Engine-from-source)
- libflutter_elinux_wayland.so: [Building Embedded Linux embedding for Flutter](https://github.com/sony/flutter-embedded-linux/wiki/Building-Embedded-Linux-embedding-for-Flutter)


## 3. Cross-building from x64 to arm64
Cross-building requires knowledge (Not easy, you might get build errors). You need to prepare your sysroot which is for cross-building for your target device by using `--target-sysroot`. Also, use `--target-arch` option to specify arm64 targets. Default is current host CPU architecture. 

```Shell
$ flutter-elinux build elinux --target-arch=arm64 --target-sysroot=<path_to_target's_sysroot>
```

### Use cases
There are some ways to cross-build, and are some ways to create a sysroot like Yocto, buildroot, and so on.
1. [Use Docker + QEMU](#case-1-use-docker--qemu)
2. [Use Yocto SDK](#case-2-use-yocto-sdk)
3. Use buildroot

### Case 1: Use Docker + QEMU
Here, we show an example using a sysroot for arm64v8/ubuntu:18.04 docker image and a host's toolchain, but using sysroot and toolchain for your target device is better.

#### Install cross-build tools
```Shell
$ sudo apt install gcc-aarch64-linux-gnu g++-aarch64-linux-gnu
$ sudo apt install libstdc++-8-dev-arm64-cross
```

#### Create sysroot for arm64
First, install Docker by following [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/).

```Shell
S sudo apt install qemu-user-static
```

```Shell
$ sudo docker run -it arm64v8/ubuntu:18.04
```

In docker:
```Shell
apt update
apt install clang cmake build-essential \
            pkg-config libegl1-mesa-dev \
            libxkbcommon-dev libgles2-mesa-dev
apt install libwayland-dev wayland-protocols
apt install libdrm-dev libgbm-dev libinput-dev libudev-dev libsystemd-dev
exit
```

Copy sysroot from the container to host:
```Shell
$ sudo docker ps -a
CONTAINER ID   IMAGE                 COMMAND   CREATED       STATUS                   PORTS     NAMES
f367a6b0316f   arm64v8/ubuntu:18.04  "bash"    4 hours ago   Exited (0) 4 hours ago   interesting_knuth
$ mkdir ubuntu18-arm64-sysroot
$ sudo docker cp f367a6b0316f:/ ubuntu18-arm64-sysroot
```

#### Build flutter apps
```Shell
$ flutter-elinux build elinux --target-arch=arm64 \
     --target-sysroot=<Absolute_path_to>/ubuntu18-arm64-sysroot
```

#### Troubleshooting
If you get the following error, use `--system-include-directories` option.
```
/usr/bin/../lib/gcc-cross/aarch64-linux-gnu/9/../../../../include/c++/9/casse
rt:43:10: fatal error: 'bits/c++config.h' file not found
#include <bits/c++config.h>
         ^~~~~~~~~~~~~~~~~~
```

```Shell
$ flutter-elinux build elinux --target-arch=arm64 \
     --target-sysroot=<Absolute_path_to>/ubuntu18-arm64-sysroot \
     --system-include-directories=/usr/aarch64-linux-gnu/include/c++/${version}/aarch64-linux-gnu
```

### Case 2: Use Yocto SDK

Use `target-compiler-triple` option to set `CMAKE_C_COMPILER_TARGET` and `CMAKE_CXX_COMPILER_TARGET` in the toolchain cmake configuration file make it use the right compiler path and filename.

```Shell
$ flutter-elinux build elinux --target-arch=arm64 \
     --target-compiler-triple=aarch64-poky-linux
```

See also: https://github.com/sony/flutter-embedded-linux/issues/4#issuecomment-1090157925