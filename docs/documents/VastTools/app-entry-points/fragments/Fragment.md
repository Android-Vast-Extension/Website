# VastFragment

`VastFragment` 是基于 [Fragment](https://developer.android.com/reference/androidx/fragment/app/Fragment.html) 进行封装的。

## 快速使用

我们以 `VastVbVmFragment` 为例，向你展示了如何将其添加到你的项目当中：

```kotlin
class SampleVbVmFragment : VastVbVmFragment<FragmentSampleVbVmBinding, SampleSharedVM>() {

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view,savedInstanceState)

        mBinding.tv.setOnClickListener {
            ... //click event
        }
    }

}
```

当然，如果你的项目中没有采用 [ViewBinding](https://developer.android.com/topic/libraries/view-binding?hl=zh-cn) ，你可以继承 `VastVmFragment` ，在此情况下你需要将 `layoutId` 设定为对应的布局id，例如：

```kotlin
class SampleVmFragment(override val layoutId: Int = R.layout.fragment_sample_vm) : 
    VastVmFragment<SampleSharedVM>() {

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        ... //Something to do
    }

}
```

## 含参数ViewModel的创建

如果 `ViewModel` 含有参数，你应该重写 `createViewModel` 方法。

```kotlin
class SampleVbVmFragment : VastVbVmFragment<FragmentSampleVbVmBinding, SampleSharedVM>() {
    
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        
    }

    override fun createViewModel(modelClass: Class<out ViewModel>): ViewModel {
        return SampleSharedVM(defaultTag)
    }

}
```

## ViewModel Owner

当 `setVmBySelf` 为 true 时，表示 Fragment 的 ViewModel 会自行保留。当您希望 ViewModel 被其关联的 Activity 保留时，请将 `setVmBySelf` 设置为 false。

```kotlin
override fun setVmBySelf(): Boolean = false
```

## 默认日志标志

你可以通过 `defaultTag` 作为日志的默认TAG，是 `Activity` 的名字。

```kotlin
LogUtils.i(defaultTag,this@SampleVbVmFragment::class.java.simpleName)
```

## DialogFragment

如果你使用 `DialogFragment` ，请参考:

```kotlin
class SampleDialogFragment : VastVbVmDialogFragment<FragmentSampleDialogBinding, BasicViewModel>() {

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        ... // do something
    }

}
```
