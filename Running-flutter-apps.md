If you use the `run` sub-command, the `build` sub-command will be also done automatically.

## Use Flutter runner for Wayland
Note: you need to install a Wayland compositor such as Weston and launch it before launching your Flutter apps.

### Debug mode
```Shell
$ flutter-elinux run -d elinux-wayland
```

### Release mode
```Shell
$ flutter-elinux run -d elinux-wayland --release
```

## Use Flutter runner for X11

### Debug mode
```Shell
$ flutter-elinux run -d elinux-x11
```

### Release mode
```Shell
$ flutter-elinux run -d elinux-x11 --release
```
