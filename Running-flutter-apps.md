If you use the `run` sub-command, the `build` sub-command will be also done automatically. We prepare two devices for Linux desktops, which are `elinux-wayland` and `elinux-x11`.

## 1. Use Wayland Flutter runner
Note: you need to install a Wayland compositor such as Weston and launch it before launching your Flutter apps.

### Debug mode
You can Dart debugger and profiler in this mode.

```Shell
$ flutter-elinux run -d elinux-wayland
```

### Profile mode
You can Dart profiler in this mode.

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

## 4. Run without the flutter-elinux command
The executable binary can be found in your project under `./build/<target_arch>/<build_mode>/bundle`.

```Shell:
# Checks command options
$ ./build/<target_arch>/<build_mode>/bundle/<your_app_name> --help
# Run your flutter app
$ ./build/<target_arch>/<build_mode>/bundle/<your_app_name>
```

See also:
- [How to run Flutter apps](https://github.com/sony/flutter-embedded-linux/wiki/How-to-run-Flutter-apps)
- [Build artifacts](https://github.com/sony/flutter-elinux/wiki/Building-flutter-apps#2-build-artifacts)