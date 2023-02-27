# Activity

`VastActivity` 组件为你提供了开发所必须的 `Activity` 组件。

## 快速使用

我们以 `VastVbVmActivity` 为例，你无需去手动初始化 `ViewBinding` 和 `ViewModel` 。

下面展示了基本使用

```kotlin
class ExampleActivity : VastVbVmActivity<ActivityExampleBinding, SampleSharedVM>() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        getBinding().addOne.setOnClickListener {
            getViewModel().addOne()
        }

        getViewModel().count.observe(this){
            getBinding().count.text = it.toString()
        }
    }
}
```

<figure markdown>
  ![快速使用](../../../img/vba_eg_1.gif){ width="200" }
  <figcaption>快速使用</figcaption>
</figure>

## 隐藏ActionBar

`enableActionBar` 必须在 `super.onCreate` 之后调用。

```kotlin
class ExampleActivity : VastVbVmActivity<ActivityExampleBinding, SampleSharedVM>() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableActionBar(false) // 不显示ActionBar
        ... // 其他设置
    }

}
```

<figure markdown>
  ![隐藏ActionBar](../../../img/vba_eg_2.jpg){ width="200" }
  <figcaption>隐藏ActionBar</figcaption>
</figure>

## 启动全面屏模式

`enableFullScreen` 必须在 `super.onCreate` 之后调用。

```kotlin
class ExampleActivity : VastVbVmActivity<ActivityExampleBinding, SampleSharedVM>() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableFullScreen(false) // 启用全面屏
        ... // 其他设置
    }

}
```

<figure markdown>
  ![使用全面屏](../../../img/vba_eg_3.jpg){ width="200" }
  <figcaption>使用全面屏</figcaption>
</figure>

## 含参数ViewModel的创建

如果 `ViewModel` 含有参数，你应该重写 `createViewModel` 方法。

```kotlin
class ParamVM(val param:String): ViewModel()
```

```kotlin
class ThemeActivity : VastVbVmActivity<ActivityThemeBinding, ParamVM>() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        ... // 其他设置
    }

    override fun createViewModel(modelClass: Class<out ViewModel>): ViewModel {
        return ParamVM("This is a param")
    }

}
```

## 设置启动页面

下面展示了如何设置启动页面，必须在 `super.onCreate` 前面调用。

```kotlin
class MainActivity : VastVbActivity<ActivityMainBinding>() {

    private lateinit var mSplashScreen: SplashScreen

    override fun onCreate(savedInstanceState: Bundle?) {
        mSplashScreen = installSplashScreen()
        super.onCreate(savedInstanceState)
        ... // 其他设置
    }

}    
```

## 默认日志标志

你可以通过 `defaultTag` 作为日志的默认TAG，是 `Activity` 的名字。

```kotlin
LogUtils.i(getDefaultTag(),"This is a log.")
```

## Snackbar

`VastVbActivity` `VastVbVmActivity` `VastVmActivity` 提供了默认的 `Snacker` 对象 `mSnackbar` 。

```kotlin
getSnackbar().setText(ResUtils.getString(R.string.loading_page)).show()
```

<figure markdown>
  ![Snackbar](../../../img/vba_eg_4.jpg){ width="200" }
  <figcaption>Snackbar</figcaption>
</figure>


## Context

你可以通过 `getContext()` 对象获取 `Activity` 上下文。
