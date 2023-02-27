# ContextHelper

`Contexthelper` is used to obtain the `application` and global `context` .

## Initialize

The initialization of `ContextHelper` is performed by `ToolsConfig`.

```kotlin
class App: Application() {
    override fun onCreate() {
        super.onCreate()
        ToolsConfig.init(this)
    }
}
```

## Get application

```kotlin
ContextHelper.getApp()
```

## Get global context

```kotlin
ContextHelper.getAppContext()
```
