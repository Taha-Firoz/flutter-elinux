In embedded development, we usually install software to remote target devices. In that case, the `custom-devices` feature helps you develop your flutter apps. This feature is the extension to official custom-devices. Special thanks to [ardera](https://github.com/ardera). See also: [Using custom embedders with the Flutter CLI](https://github.com/flutter/flutter/wiki/Using-custom-embedders-with-the-Flutter-CLI)

## 1. Create `~/.flutter_custom_devices.json`
`${localPath}`, `${appName}`, `${hostPort}`, `${devicePort}` are the system reserved vars, which are automatically determined by flutter-elinux tool. Set each value appropriately according to your target device. Also, you can add multi devices to the JSON file.

| name            | description     | type            | default         |
| --------------- | --------------- | :-------------: | :-------------: |
| id              | A unique, short identification string for this device. Used for example as an argument to the flutter-elinux run command. | string | - |
| label           | A more descriptive, user-friendly label for the device. | string | "" |
| sdkNameAndVersion | Additional information about the device. For other devices, this is the SDK (for example Android SDK, Windows SDK) name and version. | string | "" |
| enabled | If false, this device will be ignored completely by the flutter SDK and none of the commands configured will be called. You can use this as a way to comment out device configs you're still working on, for example. | boolean | true |
| platform | The platform of the target device. | [x64, arm64] | arm64 |
| backend | The displaybackend of the target device. | [wayland, x11, gbm, eglstream] | wayland |
| ping | The command to be invoked to ping the device. Used to find out whether its available or not. Every exit code unequal 0 will be treated as \"unavailable\". On Windows, consider providing a \"pingSuccessRegex\" since Windows' ping will also return 0 on failure. Make sure the command times out internally since it's not guaranteed the flutter SDK will enforce a timeout itself. | array | - |
| pingSuccessRegex | When the output of the ping command matches this regex (and the ping command finished with exit code 0), the ping will be considered successful and the pinged device reachable. If this regex is not provided the ping command will be considered successful when it returned with exit code 0. The regex syntax is the standard dart syntax. | string | - |
| install | The command to be invoked to install the app on the device. The path to the directory / file to be installed (copied over) to the device is available via the ${localPath} string interpolation and the name of the app to be installed via the ${appName} string interpolation. | string | - |
| uninstall | The command to be invoked to remove the app from the device. Invoked before every invocation of the app install command. The name of the app to be removed is available via the ${appName} string interpolation. | string | - |
| runDebug | The command to be invoked to run the app in debug mode. The name of the app to be started is available via the ${appName} string interpolation. Make sure the flutter cmdline output is available via this commands stdout/stderr since the SDK needs the \"Observatory is now listening on ...\" message to function. If the forwardPort command is not specified, the observatory URL will be connected to as-is, without any port forwarding. In that case you need to make sure it is reachable from your host device, possibly via the \"--observatory-host=<ip>\" engine flag. | array | - |
| forwardPort | The command to be invoked to forward a specific device port to a port on the host device. The host port is available via ${hostPort} and the device port via ${devicePort}. On success, the command should stay running for the duration of the forwarding. The command will be terminated using SIGTERM when the forwarding should be stopped. When using ssh, make sure ssh quits when the forwarding fails since thats not the default behaviour. | array | - |
| forwardPortSuccessRegex | A regular expression to be used to classify a successful port forwarding. As soon as any line of stdout or stderr of the forward port command matches this regex, the port forwarding is considered successful. The regex syntax is the standard dart syntax. This value needs to be present & non-null when \"forwardPort\" specified. | array | - |

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
