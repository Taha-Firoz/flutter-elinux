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
Use `--target-arch` option to cross-build for arm64 targets on x64 hosts. Default is current host CPU architecture.

|Target backend|Build mode| Command |
| ------------ | -------- | ------- |
| wayland      | release  | `flutter-elinux build elinux --target-arch=arm64` |
| x11          | release  | `flutter-elinux build elinux --target-arch=arm64 --target-backend-type=x11` |
| gbm          | release  | `flutter-elinux build elinux --target-arch=arm64 --target-backend-type=gbm` |
| eglstream    | release  | `flutter-elinux build elinux --target-arch=arm64 --target-backend-type=eglstream` |
| wayland      | debug    | `flutter-elinux build elinux --debug --target-arch=arm64` |
| x11          | debug    | `flutter-elinux build elinux --debug --target-arch=arm64 --target-backend-type=x11` |
| gbm          | debug    | `flutter-elinux build elinux --debug --target-arch=arm64 --target-backend-type=gbm` |
| eglstream    | debug    | `flutter-elinux build elinux --debug --target-arch=arm64 --target-backend-type=eglstream` |

## 2. Build artifacts
The artifacts will be put in `build/${target-arch}/${build-mode}/bundle`.