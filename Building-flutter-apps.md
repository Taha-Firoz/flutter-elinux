**Currently, x64 and Wayland target is only supported.**

## How to build
Use `--target-backend-type` option to select display backends.

|Target arch|Target backend|Build mode| Command |
| --------- | ------------ | -------- | ------- |
| x64       | wayland      | release  | `flutter-elinux build elinux` |
| x64       | x11          | release  | `flutter-elinux build elinux --target-backend-type=x11` |
| x64       | gbm          | release  | `flutter-elinux build elinux --target-backend-type=gbm` |
| x64       | eglstream    | release  | `flutter-elinux build elinux --target-backend-type=eglstream` |
| x64       | wayland      | debug    | `flutter-elinux build elinux --debug` |
| x64       | x11          | debug    | `flutter-elinux build elinux --debug --target-backend-type=x11` |
| x64       | gbm          | debug    | `flutter-elinux build elinux --debug --target-backend-type=gbm` |
| x64       | eglstream    | debug    | `flutter-elinux build elinux --debug --target-backend-type=eglstream` |

## How to cross-build
Use `--target-arch` option to cross-build for arm64 targets on x64 hosts.

|Target arch|Target backend|Build mode| Command |
| --------- | ------------ | -------- | ------- |
| arm64     | wayland      | release  | `flutter-elinux build elinux --target-arch=arm64` |
| arm64     | x11          | release  | `flutter-elinux build elinux --target-arch=arm64 --target-backend-type=x11` |
| arm64     | gbm          | release  | `flutter-elinux build elinux --target-arch=arm64 --target-backend-type=gbm` |
| arm64     | eglstream    | release  | `flutter-elinux build elinux --target-arch=arm64 --target-backend-type=eglstream` |
| arm64     | wayland      | debug    | `flutter-elinux build elinux --debug --target-arch=arm64` |
| arm64     | x11          | debug    | `flutter-elinux build elinux --debug --target-arch=arm64 --target-backend-type=x11` |
| arm64     | gbm          | debug    | `flutter-elinux build elinux --debug --target-arch=arm64 --target-backend-type=gbm` |
| arm64     | eglstream    | debug    | `flutter-elinux build elinux --debug --target-arch=arm64 --target-backend-type=eglstream` |

## Build artifacts
The artifacts will be put in `build/${target-arch}/${build-mode}/bundle`.