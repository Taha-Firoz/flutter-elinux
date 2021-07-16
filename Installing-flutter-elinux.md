You need to install the following dependent libraries to use this software. Here introduce how to install the libraries on Debian-based systems like Ubuntu.

## Supported host OS
Currently, this tool supports only Linux desktop hosts (not supoort Windows and macOS).

## Dependent libraries
- curl
- git

```Shell
$ sudo apt install curl git
```

## How to install flutter-elinux
```Shell
$ git clone https://github.com/sony/flutter-elinux.git
$ sudo mv flutter-elinux /opt/
$ export PATH=$PATH:/opt/flutter-elinux/bin
```
