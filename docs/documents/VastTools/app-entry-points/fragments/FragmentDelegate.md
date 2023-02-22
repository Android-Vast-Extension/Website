# FragmentDelegate

## 概述

我们知道有时候你的 `Fragment` 已经有继承对象，因此对你而言继承 `VastFragment` 组件显然是不合适的，因而你可以使用 `FragmentDelegate` 对象来拓展其功能。

目前有 `FragmentVbDelegate` ， `FragmentVbVmDelegate` 和 `FragmentVmDelegate` 可供使用。

## 使用示例

### 创建一个委托对象

```kotlin
// 自定义类实现 FragmentVmDelegate
private inner class FVD : FragmentVmDelegate<SampleSharedVM>(this) {
    override fun setVmBySelf(): Boolean {
        return false
    }
}

// 声明委托对象
private var mFragmentDelegate by NotNUllVar<FVD>()
```

### 通过委托对象调用拓展方法

```kotlin
class SampleVmFragment : Fragment() {

    private inner class FVD : FragmentVmDelegate<SampleSharedVM>(this) {
        override fun setVmBySelf(): Boolean {
            return false
        }
    }

    private lateinit var tv: TextView
    private lateinit var count: MaterialTextView
    private var mFragmentDelegate by NotNUllVar<FVD>()


    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        mFragmentDelegate = FVD()
        return inflater.inflate(R.layout.fragment_sample_vm, container, false)
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)

        tv = view.findViewById(R.id.tv)
        count = view.findViewById(R.id.count)

        tv.text = mFragmentDelegate.getViewModel().tag

        mFragmentDelegate.getViewModel().count.observe(requireActivity()) {
            count.text = it.toString()
        }
    }

}
```
