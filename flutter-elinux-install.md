You need to install the following dependent libraries to use this software. Here introduce how to install the libraries on Debian-based systems like Ubuntu.

## 1. System requirements
### Operating Systems
Currently, this tool supports only **Linux** desktop (not supoort Windows and macOS). **Ubuntu 20.04 or higher** is recommended. Also, x64 and Arm64 Linux desktop are supported.

### Dependent libraries
- curl
- git
- clang
- cmake
- pkg-config

```Shell
$ sudo apt install curl git clang cmake pkg-config
```

## 2. flutter-elinux install
```Shell
$ git clone https://github.com/sony/flutter-elinux.git
$ sudo mv flutter-elinux /opt/
$ export PATH=$PATH:/opt/flutter-elinux/bin
```

### Run flutter doctor
```Shell
$ flutter-elinux doctor
```

### Run flutter-elinux devices
`elinux-wayland` is the flutter app runner for Wayland desktops, and `linux-x11` is the flutter runner for X11 desktops.

```Shell
$ flutter-elinux devices
2 connected devices:

eLinux (desktop) • elinux-wayland • flutter-tester • Ubuntu 20.04.2 LTS 5.8.0-63-generic
eLinux (desktop) • elinux-x11     • flutter-tester • Ubuntu 20.04.2 LTS 5.8.0-63-generic
```

## 3. Installing dependent libraies for flutter-elinux runner (core library/embedder)
See also: https://github.com/sony/flutter-embedded-linux/wiki/Installing-dependent-libraries

### Mandatory
- EGL
- OpenGL ES (>=2.0)
- xkbcommon

```Shell
$ sudo apt install libegl1-mesa libgles2-mesa libxkbcommon-dev
```

## Only when using flutter runner for Wayland
- libwayland

```Shell
$ sudo apt install libwayland-dev
```

## Only when using flutter runner for DRM
- libdrm
- libgbm
- libinput
- libudev
- libsystemd

```Shell
$ sudo apt install libdrm-dev libgbm-dev libinput-dev libudev-dev libsystemd-dev
```