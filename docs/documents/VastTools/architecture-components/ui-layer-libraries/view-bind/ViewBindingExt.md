# 视图绑定拓展

## 获取ViewBinding

`reflexViewBinding` 通过反射来获取 `ViewBinding` 对象。

- 定义 `BaseActivity`

    ```kotlin
    abstract class BaseActivity<VB : ViewBinding> : AppCompatActivity() {

        protected val mBinding: VB by lazy {
            reflexViewBinding()
        }

        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            setContentView(mBinding.root)
        }

    }
    ```

- 继承 `BaseActivity`

    ```kotlin
    class IntentActivity : BaseActivity<ActivityIntentBinding>() {
        
    }
    ```
