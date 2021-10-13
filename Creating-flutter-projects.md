## 1. Create a new flutter project
### Flutter app project
```Shell
$ flutter-elinux create <your_app_project_name>
```

### Flutter plugin project
```Shell
$ flutter-elinux create --platforms elinux --template plugin <your_plugin_project_name>
```

After creating the plugin template, you need to modify `pubspec.yaml` file. Open it and replace the `some_platform`: map with `elinux`:
```Yaml
elinux:
  pluginClass: PluginNamePlugin
```

## 2. Use existing official flutter projects
If you would like to use flutter for elinux for existing flutter projects, you need to prepate `elinux` directory.

```Shell
$ cd <your_existing_flutter_project>
$ flutter-elinux create .
```