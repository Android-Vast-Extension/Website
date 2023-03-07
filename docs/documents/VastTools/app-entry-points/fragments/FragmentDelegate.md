# 拓展与委托

## 概述

我们知道有时候你的 `Fragment` 已经有继承对象，因此对你而言继承 `VastFragment` 组件显然是不合适的，因而你可以使用下面的方法来拓展其功能。

## 获取 ViewBinding

!!! warning 

    因为 `reflexViewBinding` 是通过反射调用 `ViewBinding.bind` 方法，所以请注意 `mBinding` 的调用范围。

```kotlin
class SampleFragment : Fragment() {

    private val mBinding by reflexViewBinding<FragmentSampleBinding>()

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
    }

}
```

## 获取 ViewModel

```kotlin
private val mViewModel by viewModels<SampleSharedVM>()
```

## 获取类名为默认日志 tag

```kotlin
private val mLogTag = defaultLogTag()
```
