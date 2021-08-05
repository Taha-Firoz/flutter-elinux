In embedded development, we usually install software to remote target devices. In that case, the `custom-devices` feature helps you develop your flutter apps.

## 1. Create `~/.flutter_custom_devices.json`
`${localPath}`, `${appName}`, `${hostPort}`, `${devicePort}` are the system reserved vars, which are automatically determined by flutter-elinux tool. Set each value appropriately according to your target device. Also, you can add multi devices to the JSON file.

| name            | description     | type            | default         |
| :-------------: | --------------- | :-------------: | :-------------: |
| id              | A unique, short identification string for this device. Used for example as an argument to the flutter-elinux run command. | string | - |
| label           | A more descriptive, user-friendly label for the device. | string | "" |

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
        "ssh", "user@192.168.0.100", "/tmp/${appName}/${appName}"
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
Make sure that the devices found by the `ping` command are listed.

```Shell
$ flutter-elinux devices
3 connected devices:

eLinux (desktop) • elinux-wayland • flutter-tester • Ubuntu 20.04.2 LTS 5.8.0-63-generic
eLinux (desktop) • elinux-x11     • flutter-tester • Ubuntu 20.04.2 LTS 5.8.0-63-generic
eLinux (mobile)  • raspberry-pi4  • flutter-tester • Rasberry Pi 4
```

## 3. Build your flutter apps for target devices
Build for the target device. See also: [Cross-building from x64 to arm64](https://github.com/sony/flutter-elinux/wiki/Building-flutter-apps#2-cross-building-from-x64-to-arm64)

```Shell
flutter-elinux build elinux --target-arch=arm64 --target-sysroot=/opt/arm64-sysroot \
    --system-include-directories=/usr/aarch64-linux-gnu/include/c++/9/aarch64-linux-gnu \
    --debug
```

## 4. Run your flutter apps on your target device
```Shell
$ flutter-elinux run -d raspberry-pi4
Launching lib/main.dart on eLinux in debug mode...
Uninstall sample from raspberry-pi4.
user@192.168.0.100's password: 
Uninstallation Success
Install sample (build/elinux/arm64/debug/bundle) to raspberry-pi4
user@192.168.0.100's password: 
Installation Success
Launch sample.name on raspberry-pi4
user@192.168.0.100's password: 
user@192.168.0.100's password: 
Syncing files to device eLinux...                                  202ms

Flutter run key commands.
r Hot reload. 🔥🔥🔥
R Hot restart.
h List all available interactive commands.
d Detach (terminate "flutter run" but leave application running).
c Clear the screen
q Quit (terminate the application on the device).

💪 Running with sound null safety 💪

An Observatory debugger and profiler on eLinux is available at: http://127.0.0.1:43237/xd6sW5hdEoE=/
Activating Dart DevTools...                                      1,830ms
The Flutter DevTools debugger and profiler on eLinux is available at:
http://127.0.0.1:9100?uri=http://127.0.0.1:43237/xd6sW5hdEoE=/
```

## 5. Other commands

### Install your flutter app bundle to the target device
```Shell
$ flutter-elinux install -d raspberry-pi4
```

### Uninstall your flutter app bundle to the target device
```Shell
$ flutter-elinux uninstall -d raspberry-pi4
```
