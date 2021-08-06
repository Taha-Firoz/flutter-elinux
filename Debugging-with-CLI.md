It is possible to do most things, including source-level debugging, profiling and hot reload when you debug Flutter apps for eLinux.

## 1. Getting the Observatory port
You will find the following message in the console when you run Flutter apps. You need to attach a debugger to this port when you want to debug it. **Note that the URI changes every time after launching**.

```Shell
flutter: Observatory listening on http://127.0.0.1:43377/390I4oPyQ0U=/
```

### Fixed observatory URI
If you want to fix always same observatory URI, you can use the following command options. Note that this option is only available in debug/profile mode.

```Shell
$ flutter-elinux run -d elinux-wayland \
    --device-vmservice-port=12345 --host-vmservice-port=42771 --disable-service-auth-codes

(snip)

An Observatory debugger and profiler on eLinux is available at: http://127.0.0.1:42771/
```

## 2. Flutter attach debugger

```Shell
$ cd <path_to_flutter_project>/
$ flutter-elinux attach --device-id=flutter-tester --debug-uri=http://127.0.0.1:43377/390I4oPyQ0U=/
Syncing files to device Flutter test device...                      8.5s

Flutter run key commands.
r Hot reload. 🔥🔥🔥
R Hot restart.
h List all available interactive commands.
d Detach (terminate "flutter run" but leave application running).
c Clear the screen
q Quit (terminate the application on the device).

💪 Running with sound null safety 💪

An Observatory debugger and profiler on Flutter test device is available at: http://127.0.0.1:43377/390I4oPyQ0U=/.,
The Flutter DevTools debugger and profiler on Flutter test device is available at:
http://127.0.0.1:9102?uri=http://127.0.0.1:43377/390I4oPyQ0U=/.,
```
