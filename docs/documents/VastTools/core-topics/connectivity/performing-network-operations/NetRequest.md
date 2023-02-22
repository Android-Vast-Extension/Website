# 执行网络操作

## 概览

`VastTools` 对网络请求进行了封装，根据你的项目实际需求请选择对应的网络请求方式：

![netrequest](../assets/images/netrequest.png)

## BaseApiRsp

`BaseApiRsp` 接口提供了四个拓展方法，以便你在之后对请求结果进行监听。

### isSuccess

你可以通过重写 `isSuccess` 方法来指定数据请求成功条件。

```kotlin
data class QRCodeKey(
    val code: Int,
    val data: Data?
): BaseApiRsp {
    override fun isSuccess(): Boolean {
        return code == 200
    }
}
```

### isEmpty

你可以通过重写 `isEmpty` 方法来指定数据为空条件。

```kotlin
data class QRCodeKey(
    val code: Int,
    val data: Data?
): BaseApiRsp {
    override fun isEmpty(): Boolean {
        return data == null
    }
}
```

### getErrorCode和getErrorMsg

`getErrorCode` 和 `getErrorMsg` 用于指定数据请求错误信息和错误代码。

```kotlin
data class QRCodeKey(
    val code: Int,
    val data: Data?
): BaseApiRsp {
    override fun getErrorCode(): Int? {
        return data.errorCode
    }

    override fun getErrorMsg(): String? {
        return data.errorMsg
    }
}
```
