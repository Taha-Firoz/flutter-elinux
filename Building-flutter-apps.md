## 1. How to build your flutter app
### Self-building
Use `--target-backend-type` option to select display backends. Default is Wayland.

|Target backend|Build mode| Command |
| ------------ | -------- | ------- |
| wayland      | release  | `flutter-elinux build elinux` |
| x11          | release  | `flutter-elinux build elinux --target-backend-type=x11` |
| gbm          | release  | `flutter-elinux build elinux --target-backend-type=gbm` |
| eglstream    | release  | `flutter-elinux build elinux --target-backend-type=eglstream` |
| wayland      | debug    | `flutter-elinux build elinux --debug` |
| x11          | debug    | `flutter-elinux build elinux --debug --target-backend-type=x11` |
| gbm          | debug    | `flutter-elinux build elinux --debug --target-backend-type=gbm` |
| eglstream    | debug    | `flutter-elinux build elinux --debug --target-backend-type=eglstream` |

### Cross-building from x64 to arm64
Cross-building is not easy so it requires knowledge. You need to prepare your sysroot which is for cross-building for your target device by using `--target-sysroot`. Also, Use `--target-arch` option to cross-build for arm64 targets on x64 hosts. Default is current host CPU architecture. 

```Shell
$ flutter-elinux build elinux --target-arch=arm64 --target-sysroot=<path_to_target's_sysroot>
```



## 2. Build artifacts
The artifacts will be put in `build/${target-arch}/${build-mode}/bundle`.