# StateLiveData

## StateLiveData的数据状态

`StateLiveData` 目前支持七种状态：

- Start 可以用来表示开始请求数据
- Completion 可以用来表示数据请求结束
- Success 可以表示数据获取成功
- Failed 可以表示数据获取失败
- Error 可以表示数据获取错误
- Empty 可以表示获取的是空数据
- Clear 可以表示清除状态

## 使用StateLiveData对象

> 关于 `StateLiveData` 完整使用示例代码，你可以参考 [Music-Voice/StartVM](https://github.com/SakurajimaMaii/Music-Voice/blob/master/app/src/main/kotlin/cn/govast/vmusic/viewModel/StartVM.kt)

### 创建StateLiveData对象

```kotlin
val qrCodeCheck = StateLiveData<QRCodeCheck>()
```

### 观察StateLiveData对象

#### 观察对象值发生变化

对于 `qrCodeCheck` ，你可以使用 `observe` 将其添加到观察者列表中。

```kotlin
getViewModel().qrCodeCheck.observe(viewLifecycleOwner) {
    if (it.code == QRCodeCheckState.SURE.code) {
        findNavController().navigate(R.id.mainActivity)
    } else {
        getViewModel().checkQRCode(qrCodeKey)
    }
}
```

#### 观察状态发生变化

对于 `qrCodeCheck` ，调用 `getState()` 方法获取状态并调用 `observeState` 方法将状态添加到观察者列表中。

```kotlin
getViewModel().qrCodeCheck.getState().observeState(this){
    onSuccess = {
        
    }
    onError = {

    }
}
```

### 更新StateLiveData对象

`StateLiveData` 只提供了 `postValueAndSuccess` 方法来更新对象值，其它情况下你只能更新 `StateLiveData` 对象的状态。

> `onFailed` 提供了两个参数允许你传递**错误代码**和**错误信息**两个内容。
> `postError` 提供了一个参数允许你传递**异常信息**。

```kotlin
getRequestBuilder()
    .suspendWithListener({
        UserRepository.checkQRCode(key)
    }) {
        onSuccess = {
            qrCodeCheck.postValueAndSuccess(it)
        }
        onFailed = { errorCode, errorMsg ->
            qrCodeCheck.postFailed(errorCode, errorMsg)
        }
        onError = {
            qrCodeCheck.postError(it)
        }
    }
```
