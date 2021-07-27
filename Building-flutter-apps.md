## 1. Self-building
Use `--target-backend-type` option to select display backends. Default is Wayland.

|Target backend|Build mode| Command |
| ------------ | -------- | ------- |
| wayland      | release  | `flutter-elinux build elinux` |
| x11          | release  | `flutter-elinux build elinux --target-backend-type=x11` |
| gbm          | release  | `flutter-elinux build elinux --target-backend-type=gbm` |
| eglstream    | release  | `flutter-elinux build elinux --target-backend-type=eglstream` |
| wayland      | debug    | `flutter-elinux build elinux --debug` |
| x11          | debug    | `flutter-elinux build elinux --debug --target-backend-type=x11` |
| gbm          | debug    | `flutter-elinux build elinux --debug --target-backend-type=gbm` |
| eglstream    | debug    | `flutter-elinux build elinux --debug --target-backend-type=eglstream` |
| wayland      | profile  | `flutter-elinux build elinux --profile` |
| x11          | profile  | `flutter-elinux build elinux --profile --target-backend-type=x11` |
| gbm          | profile  | `flutter-elinux build elinux --profile --target-backend-type=gbm` |
| eglstream    | profile  | `flutter-elinux build elinux --profile --target-backend-type=eglstream` |

## 2. Cross-building from x64 to arm64
Cross-building requires knowledge (Not easy, you might get build errors). You need to prepare your sysroot which is for cross-building for your target device by using `--target-sysroot`. Also, Use `--target-arch` option to specify arm64 targets. Default is current host CPU architecture. 

```Shell
$ flutter-elinux build elinux --target-arch=arm64 --target-sysroot=<path_to_target's_sysroot>
```

### Example
There are some ways to create a sysroot like Yocto, buildroot, and so on. Here, we show an example using a sysroot for arm64v8/ubuntu:18.04 docker image, but using sysroot and toolchain for your target device is better.

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
$ sudo docker run -it arm64v8/ubuntu:18:04
```

In docker:
```Shell
apt install clang cmake build-essential \
            pkg-config libegl1-mesa-dev \
            libxkbcommon-dev libgles2-mesa-dev
apt install libwayland-dev wayland-protocols
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

## 3. Build artifacts
The artifacts will be put in `build/${target-arch}/${build-mode}/bundle`.