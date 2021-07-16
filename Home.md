Welcome to the flutter-elinux wiki! All documentation for this software is collected here.

## 💻 Contents
### 1. Setup your development environment
- [Installing flutter-elinux](https://github.com/sony/flutter-elinux/wiki/Installing-flutter-elinux)

### 2. How to use

- [Commands]()

### 3. Support status

### 1. Flutter version check
```Shell
$ flutter-elinux --version
```

### 2. build command
#### Build with wayland backend for x64 targets in release mode
```Shell
$ flutter-elinux build elinux
```

#### Build with wayland backend for x64 targets in debug mode
```Shell
$ flutter-elinux build elinux --debug
```

### 3. run command
#### Debug mode
```Shell
$ flutter-elinux run -d elinux
```

#### Release mode
```Shell
$ flutter-elinux run -d elinux --release
```
