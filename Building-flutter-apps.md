
## How to build
|Target arch|Target backend|Build mode| Command |
| --------- | ------------ | -------- | ------- |
| x64       | wayland      | release  | `flutter-elinux build elinux` |
| x64       | x11          | release  | `flutter-elinux build elinux --target-backend-type=x11` |
| x64       | gbm          | release  | `flutter-elinux build elinux --target-backend-type=gbm` |
| x64       | eglstream    | release  | `flutter-elinux build elinux --target-backend-type=eglstream` |
| x64       | wayland      | debug    | `flutter-elinux build elinux --debug` |

## How to cross-build
|Target arch|Target backend|Build mode| Command |
| --------- | ------------ | -------- | ------- |
| arm64     | wayland      | release  | `flutter-elinux build elinux --target-arch=arm64` |
| arm64     | wayland      | debug  | `flutter-elinux build elinux --target-arch=arm64 --debug` |

## Build artifacts
The artifacts will be put in `build/${target-arch}/${build-mode}/bundle`.