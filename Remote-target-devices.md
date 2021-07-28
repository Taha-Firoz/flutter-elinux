In embedded development, we usually install software to remote target devices. In that case, the `custom-devices` feature helps you develop your flutter apps.

## 1. Create `~/.flutter_custom_devices.json`

`~/.flutter_custom_devices.json` example:
```Json
{
  "custom-devices": [
    {
      "id": "raspberry-pi4",
      "label": "Rasberry Pi 4",
      "sdkNameAndVersion": "Rasberry Pi 4",
      "enabled": true,
      "platform": "arm64",
      "backend": "wayland",
      "ping": [
        "ping", "-w", "500", "-c", "1", "192.168.0.100"
      ],
      "pingSuccessRegex": "ttl=",
      "install": [
        "scp", "-r", "${localPath}", "user@192.168.0.100:/tmp/${appName}"
      ],
      "uninstall": [
        "ssh", "user@192.168.0.100", "rm -rf \"/tmp/${appName}\""
      ],
      "runDebug": [
        "ssh", "user@192.168.0.100", "/tmp/${appName}/${appName} -b ."
      ],
      "forwardPort": [
        "ssh", "-o", "ExitOnForwardFailure=yes",
        "-L", "127.0.0.1:${hostPort}:127.0.0.1:${devicePort}", "user@192.168.0.100"
      ],
      "forwardPortSuccessRegex": "Linux"
    }
  ]
}
```

## 2. Device discovery

```Shell
$ flutter-elinux devices
3 connected devices:

eLinux (desktop) • elinux-wayland • flutter-tester • Ubuntu 20.04.2 LTS 5.8.0-63-generic
eLinux (desktop) • elinux-x11     • flutter-tester • Ubuntu 20.04.2 LTS 5.8.0-63-generic
eLinux (mobile)  • raspberry-pi4  • flutter-tester • Rasberry Pi 4
```

## 3. Build your flutter apps for target devices
See also: [Cross-building from x64 to arm64](https://github.com/sony/flutter-elinux/wiki/Building-flutter-apps#2-cross-building-from-x64-to-arm64)
```Shell
flutter-elinux build elinux --target-arch=arm64 --target-sysroot=/opt/arm64-sysroot \
    --system-include-directories=/usr/aarch64-linux-gnu/include/c++/9/aarch64-linux-gnu \
    --debug
```

## 4. Run your flutter apps on your target device
Note that `run` sub-command for custom-devices is supported `debug` mode only.

```Shell
$ flutter-elinux run -d raspberry-pi4
```

## 5. Other commands

### Install
```Shell
$ flutter-elinux install -d raspberry-pi4
```

### Uninstall
```Shell
$ flutter-elinux uninstall -d raspberry-pi4
```
