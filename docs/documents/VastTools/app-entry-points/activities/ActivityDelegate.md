# ActivityDelegate

## 概述

我们知道有时候你的 `Activity` 已经有继承对象，因此对你而言继承 `VastActivity` 组件显然是不合适的，因而你可以使用 `ActivityDelegate` 对象来拓展其功能。

目前有 `ActivityVbDelegate` ，`ActivityVbVmDelegate` 和 `ActivityVmDelegate` 可供使用。

## 使用示例

### 创建一个委托对象

```kotlin
// 自定义类实现 ActivityVbVmDelegate
private inner class AVVD:ActivityVbVmDelegate<ActivityFragmentsBinding, SampleSharedVM>(this)

// 声明委托对象
private var mActivityDelegate by NotNUllVar<AVVD>()
```

### 通过委托对象调用拓展方法

```kotlin
class FragmentsActivity : AppCompatActivity() {

    private inner class AVVD:ActivityVbVmDelegate<ActivityFragmentsBinding, SampleSharedVM>(this)

    private var mActivityDelegate by NotNUllVar<AVVD>()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        mActivityDelegate = AVVD()
        mActivityDelegate.getBinding().vp2.apply {
            adapter = VastFragmentAdapter(this@FragmentsActivity,ArrayList<Fragment>().apply {
                add(SampleVbVmFragment())
                add(SampleVmFragment())
                add(SampleVbFragment())
            })
        }
    }

}
```
