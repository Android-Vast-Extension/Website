# 概览

`VastTools` 对网络请求进行了封装，根据你的项目实际需求请选择对应的网络请求方式：

## ResponseApi

`ResponseApi` 接口提供了四个拓展方法，以便你在之后对请求结果进行监听。

### isSuccessful

你可以通过重写 `isSuccessful` 方法来指定数据请求成功条件。

```kotlin
data class QRCodeKey(
    val code: Int,
    val data: Data?
) : ResponseApi {

    override fun isSuccessful(): Boolean {
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
) : ResponseApi {

    override fun isEmpty(): Boolean {
        return data == null
    }

}
```

### code 和 message

`code` 和 `message` 用于指定数据请求信息和代码。

```kotlin
data class QRCodeKey(
    val code: Int,
    val data: Data?
) : ResponseApi {

    data class Data(
        val code: Int,
        val unikey: String
    )

    override fun isSuccessful(): Boolean {
        return code == 200
    }

    override fun isEmpty(): Boolean {
        return data == null
    }

    override fun code(): Int? {
        return data?.code
    }

    override fun message(): String? {
        return data?.unikey
    }

}
```
