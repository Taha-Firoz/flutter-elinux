## Install extensions
Install the VS Code extension to Flutter:
https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter

## Create `launch.json`
Create a [launch.json file](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations) like the following.

```Json
{
  "version": "0.2.0"
  "configurations": [
    {
      "type": "dart",
      "name": "Flutter eLinux desktop Attach",
      "request": "attach",
      "deviceId": "flutter-tester",
      "observatoryUri": "http://127.0.0.1:40409/k8IUol2dnPI=/"
    }
  ]
}
```

## Flutter attach debugger
Click `Run and Debug`
![Screenshot from 2021-07-30 16-57-33](https://user-images.githubusercontent.com/62131389/127621220-995ad1bc-4d28-4b9f-975f-be5513259374.png)
