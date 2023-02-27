# ResponseLiveData

## ResponseLiveData 的数据状态

`StateLiveData` 目前支持七种状态：

- Start 可以用来表示开始请求数据
- Completion 可以用来表示数据请求结束
- Success 可以表示数据获取成功
- Failed 可以表示数据获取失败
- Error 可以表示数据获取错误
- Empty 可以表示获取的是空数据
- Clear 可以表示清除状态

## 快速开始

### 创建 ResponseLiveData

```kotlin
class NetVM: VastViewModel() {

    val qRCodeKey = ResponseLiveData<QRCodeKey>()

    /**
     * 自动检测数据请求的状态
     * 目前支持 Error Failed Successful Empty 四种状态
     *
     * @param timestamp 时间戳
     */
    fun getQRCode_1(timestamp:String){
        NetworkRetrofitBuilder().create(QRService::class.java).generateQRCode(timestamp).request(qRCodeKey)
    }

    /**
     * 手动检测数据请求的状态
     *
     * @param timestamp 时间戳
     */
    fun getQRCode_2(timestamp:String){
        NetworkRetrofitBuilder().create(QRService::class.java).generateQRCode(timestamp)
            .request{
                onSuccess = {
                    qRCodeKey.postValueAndSuccess(it)
                }
            }
    }

}
```

### 观察 ResponseLiveData

#### 观察对象值发生变化

对于 `qRCodeKey` ，你可以使用 `observe` 将其添加到观察者列表中。

=== "kotlin"

    ```kotlin
    class NetStateActivity : VastVbVmActivity<ActivityNetStateBinding, NetVM>() {

        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            getViewModel().qRCodeKey.observe(this){ value ->
                
            }
        }

    }
    ```

=== "java"

    ```java
    public class NetStateActivity extends VastVbVmActivity<ActivityNetStateBinding, NetVM> {

        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            getViewModel().getQRCodeKey().observe(this, value -> {

            });
        }

    }
    ```

#### 观察状态发生变化

对于 `qRCodeKey` ，调用 `getState()` 方法获取状态并调用 `observeState` 方法将状态添加到观察者列表中。

!!! note 关于 onSuccess 方法的说明

    对于 `onSuccess` 来说，你只能观察到值对应的状态而并非数据值。

=== "kotlin"

    ```kotlin
    getViewModel().qRCodeKey.getState().observeState(this){
        onSuccess = {

        }
        onError = {

        }
    }
    ```

=== "java"

    ```java
    getViewModel().getQRCodeKey().getState().observeState(this, listener -> {
        listener.setOnError(throwable -> {
            
            return null;
        });
        return null;
    });
    ```

### 更新 ResponseLiveData

`ResponseLiveData` 只提供了 `postValueAndSuccess` 方法来更新对象值，其它情况下你只能更新 `ResponseLiveData` 对象的状态。

> `onFailed` 提供了两个参数允许你传递**错误代码**和**错误信息**两个内容。
> `postError` 提供了一个参数允许你传递**异常信息**。

```kotlin
/**
 * 手动检测数据请求的状态
 *
 * @param timestamp 时间戳
 */
fun getQRCode_2(timestamp:String){
    NetworkRetrofitBuilder().create(QRService::class.java).generateQRCode(timestamp)
        .request{
            onSuccess = {
                qRCodeKey.postValueAndSuccess(it)
            }
            onFailed = { errorCode, errorMsg ->
                qRCodeKey.postFailed(errorCode, errorMsg)
            }
            onError = {
                qRCodeKey.postError(it)
            }
        }
}
```
