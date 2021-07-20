You need to install the following dependent libraries to use this software. Here introduce how to install the libraries on Debian-based systems like Ubuntu.

## Supported Host/OS
Currently, this tool supports only **Linux** desktop (not supoort Windows and macOS).

- [x] x64 Linux desktop
- [ ] arm64 Linux desktop

## Dependent libraries
- curl
- git
- clang
- cmake
- pkg-config

```Shell
$ sudo apt install curl git clang cmake pkg-config
```

## How to install flutter-elinux
```Shell
$ git clone https://github.com/sony/flutter-elinux.git
$ sudo mv flutter-elinux /opt/
$ export PATH=$PATH:/opt/flutter-elinux/bin
```

## doctor command

```Shell
$ flutter-elinux doctor
```