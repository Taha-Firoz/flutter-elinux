## Create a new flutter project
### Flutter app project
```Shell
$ flutter-elinux create <your_app_project_name>
```

### Flutter plugin project
```Shell
$ flutter-elinux create -t plugin <your_plugin_project_name>
```

After creating the plugin template, you need to modify `pubspec.yaml` file. Open it and replace the `some_platform`: map with `elinux`:
```Yaml
elinux:
  pluginClass: PluginNamePlugin
```

## flutter-elinux with existing projects
If you would like to use flutter for elinux for existing flutter projects, you need to prepate `elinux` directory.

```Shell
$ cd <your_existing_flutter_project>
$ flutter-elinux create .
```