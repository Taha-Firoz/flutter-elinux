## How to create a new flutter app project
```Shell
$ flutter-elinux create <your_app_project_name>
```

## How to create a new flutter plugin project
```Shell
$ flutter-elinux create -t plugin <your_plugin_project_name>
```

After creating the plugin template, you need to modify `pubspec.yaml` file. Open it and replace the `some_platform`: map with `elinux`:
```Yaml
elinux:
  pluginClass: PluginNamePlugin
```