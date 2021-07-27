You need to install the following dependent libraries to use this software. Here introduce how to install the libraries on Debian-based systems like Ubuntu.

## System requirements
### Operating Systems
Currently, this tool supports only **Linux** desktop (not supoort Windows and macOS). We recommend using Ubuntu 18 or 20.

- [x] x64 Linux desktop
- [ ] arm64 Linux desktop

### Dependent libraries
- curl
- git
- clang
- cmake
- pkg-config

```Shell
$ sudo apt install curl git clang cmake pkg-config
```

## flutter-elinux install
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