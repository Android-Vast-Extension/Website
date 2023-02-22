# 上下文

`ContextHelper` 用来获取应用的 `application` 和全局 `Context` 对象

## 初始化

`ContextHelper` 的初始化由 `ToolsConfig` 执行。

```kotlin
class App: Application() {
    override fun onCreate() {
        super.onCreate()
        ToolsConfig.init(this)
    }
}
```

## 获取Application

```kotlin
ContextHelper.getApp()
```

## 获取全局Context

```kotlin
ContextHelper.getAppContext()
```
