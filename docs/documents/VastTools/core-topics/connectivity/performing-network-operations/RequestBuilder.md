# RequestBuilder

`RequestBuilder` 主要用来构建请求示例。

## 快速开始

```kotlin
abstract class BaseServiceCreator: RequestBuilder() {

    override fun setBaseUrl(): String {
        return Constant.ROOT_URL
    }

}
```