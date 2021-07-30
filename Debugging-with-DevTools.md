See also: [DevTools -Flutter](https://flutter.dev/docs/development/tools/devtools)

## 1. Run your Flutter app

```
$ flutter-elinux run -d elinux-x11
Launching lib/main.dart on eLinux in debug mode...
Building an eLinux application with x11 backend in debug mode for x64 target...        13.3s
Syncing files to device eLinux...                                        491ms

Flutter run key commands.
r Hot reload. 🔥🔥🔥
R Hot restart.
h List all available interactive commands.
d Detach (terminate "flutter run" but leave application running).
c Clear the screen
q Quit (terminate the application on the device).

💪 Running with sound null safety 💪

An Observatory debugger and profiler on eLinux is available at:
http://127.0.0.1:44541/mS6Wmf1jTCk=/
The Flutter DevTools debugger and profiler on eLinux is available at:
http://127.0.0.1:9100?uri=http://127.0.0.1:44541/mS6Wmf1jTCk=/
```

## 2. Open DevTools and connect to the target app
Open `http://127.0.0.1:9100?uri=http://127.0.0.1:44541/mS6Wmf1jTCk=/` on your browser.
![Screenshot from 2021-07-30 17-18-27](https://user-images.githubusercontent.com/62131389/127624155-bad79120-8ab6-4704-acbe-e0e1c50ab566.png)
