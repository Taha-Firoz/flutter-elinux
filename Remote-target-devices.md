In embedded development, we usually install software to remote target devices. In that case, the `custom-devices` feature helps you develop your flutter apps.

## 1. Create `.flutter_custom_devices.json`

`.flutter_custom_devices.json` example:
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


## 3. Build your flutter apps for target devices

## 4. Run your flutter apps on your target device
