# 拓展与委托

## 概述

我们知道有时候你的 `Activity` 已经有继承对象，因此对你而言继承 `VastActivity` 组件显然是不合适的，因而你可以使用下面的方法来拓展其功能。

## 获取 ViewBinding

!!! note "reflexViewBinding"

    `reflexViewBinding` 会利用反射构建 `ViewBinding` 对象并调用 `Activity.setContentView` 方法。

```kotlin
private val mBinding by reflexViewBinding<ActivityFragmentsBinding>()
```

## 获取 ViewModel

```kotlin
private val mViewModel by viewModels<SampleSharedVM>()
```

## 获取类名为默认日志 tag

```kotlin
private val mLogTag = defaultLogTag()
```

## 设置全屏模式

`screenConfig` 提供了 `mEnableActionBar` 和 `mEnableFullScreen` 两个参数。

- `mEnableActionBar` : 如果要显示 ActionBar ，则为 true，否则为 false
- `mEnableFullScreen` : 如果你想设置全屏则为 true ，否则为 false 。 **全面屏模式下不会显示 ActionBar**

```kotlin
class FragmentsActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        screenConfig(false,true)
        ... // 其他设置
    }

}
```