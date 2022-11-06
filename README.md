# PG Releaser Package

Template application for packaging self-contained Java application.

`jpackage.txt` and `jpackage.properties` files are used for testing of jpackage tool directly

```shell
  jpackage --add-launcher DMK=jpackage.properties "@jpackage-windows-latest.txt"
```

The macOS JPackage has restriction for the version

**Bundler Mac DMG Package skipped because of a configuration problem: The first number in an app-version cannot be zero or negative.**  
