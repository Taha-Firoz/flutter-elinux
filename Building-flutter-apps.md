## 1. How to build your flutter app
### Self-building
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

### Cross-building from x64 to arm64
Cross-building requires knowledge (Not easy, you might get build errors). You need to prepare your sysroot which is for cross-building for your target device by using `--target-sysroot`. Also, Use `--target-arch` option to specify arm64 targets. Default is current host CPU architecture. 

```Shell
$ flutter-elinux build elinux --target-arch=arm64 --target-sysroot=<path_to_target's_sysroot>
```

There are some ways to create a sysroot like Yocto, buildroot, and so on. Here, we show an example using a sysroot for arm64v8/ubuntu:18.04 docker image, but using sysroot and toolchain for your target device is better.

#### Create sysroot for arm64
First, install Docker by following [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/).

```Shell
S sudo apt install qemu-user-static
```

```Shell
$ sudo docker run -it arm64v8/ubuntu:18:04
In docker:
# apt install clang cmake build-essential pkg-config libegl1-mesa-dev libxkbcommon-dev libgles2-mesa-dev
# apt install libwayland-dev wayland-protocols
# exit

$ sudo docker ps -a

$ sudo docker cp 
```

## 2. Build artifacts
The artifacts will be put in `build/${target-arch}/${build-mode}/bundle`.