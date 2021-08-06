## 1. Install extensions
Install the VS Code extension to Flutter:
https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter

## 2. Getting the Observatory port
You will find the following message in the console when you run Flutter apps. You need to attach a debugger to this port when you want to debug it. **Note that the URI changes every time after launching**.

```Shell
flutter: Observatory listening on http://127.0.0.1:43377/390I4oPyQ0U=/
```

### Fixed observatory-port and disable auth-service in Dart VM
If you want to fix always same observatory URI, you can use the following command options. Note that this option is only available in debug/profile mode.

```Shell
$ flutter-elinux run -d elinux-x11 --device-vmservice-port=12345 --disable-service-auth-codes

(snip)

flutter: Observatory listening on http://127.0.0.1:12345/
```

## 3. Create `launch.json`
Create a [launch.json file](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations) like the following.

```Json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "dart",
      "name": "Flutter eLinux desktop Attach",
      "request": "attach",
      "deviceId": "flutter-tester",
      "observatoryUri": "http://127.0.0.1:43377/390I4oPyQ0U=/"
    }
  ]
}
```

## 4. Flutter attach debugger
Click `Run and Debug`
![Screenshot from 2021-07-30 16-57-33](https://user-images.githubusercontent.com/62131389/127621220-995ad1bc-4d28-4b9f-975f-be5513259374.png)
