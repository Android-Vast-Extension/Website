# 初始化

你需要在 `Application` 内初始化 `VastTools` 。

```kotlin
class App: Application() {

    override fun onCreate() {
        super.onCreate()
        ToolsConfig.init(this)
    }

}
```
