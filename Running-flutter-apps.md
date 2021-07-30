If you use the `run` sub-command, the `build` sub-command will be also done automatically. We prepare two devices for Linux desktops, which are `elinux-wayland` and `elinux-x11`.

## 1. Use Wayland Flutter runner
Note: you need to install a Wayland compositor such as Weston and launch it before launching your Flutter apps.

### Debug mode
```Shell
$ flutter-elinux run -d elinux-wayland
```

### Profile mode
```Shell
$ flutter-elinux run -d elinux-wayland --profile
```

### Release mode
```Shell
$ flutter-elinux run -d elinux-wayland --release
```

## 2. Use X11 Flutter runner
```Shell
$ flutter-elinux run -d elinux-x11
```

## 3. Use custom-devices
You can install, uninstall, debug, and so on to remote arm64 devices such as Raspberry Pi4 from host desktops. See [Remote target devices](https://github.com/sony/flutter-elinux/wiki/Remote-target-devices)