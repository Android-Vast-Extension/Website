# ViewModel拓展

## 使用示例

`reflexViewModel` 通过反射来获取 `ViewModel` 对象。

- 定义 `BaseActivity`

    ```kotlin
    abstract class BaseActivity<VM : ViewModel> : AppCompatActivity() {

        protected val mViewModel: VM by lazy {
            reflexViewModel{
                return@reflexViewModel getViewModel()
            }
        }

        protected abstract fun getViewModel():VM

    }
    ```

- 继承 `BaseActivity`

    ```kotlin
    class IntentActivity : BaseActivity<BasicViewModel>() {

        override fun getViewModel(): BasicViewModel = BasicViewModel(NetworkRepository())
        
    }
    ```

## 默认ViewModel获取

```kotlin
private val mViewModel:BasicViewModel by lazy {
    reflexViewModel()
}
```

## 含参ViewModel获取

```kotlin
private val mViewModel:BasicViewModel by lazy {
    reflexViewModel{
        return@reflexViewModel BasicViewModel(NetworkRepository())
    }
}
```

## ViewModelStoreOwner设置

当 `reflexViewModel` 在 `Fragment` 内使用时，其提供了参数 `vmBySelf` 。当 `vmBySelf` 为 **true** 时，意味着 ViewModelStoreOwner 是 `Fragment` 本身。当您希望 ViewModelStoreOwner 成为此片段当前关联的 `FragmentActivity` 时，请将 `vmBySelf` 设置为 **false** 。

```kotlin
private val mViewModel: BasicViewModel by lazy {
    reflexViewModel(true){
        return@reflexViewModel BasicViewModel(NetworkRepository())
    }
}
```
