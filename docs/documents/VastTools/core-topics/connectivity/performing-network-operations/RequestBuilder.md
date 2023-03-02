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

## 设置超时时间

通过重载 `setTimeOut` 方法，你可以设置 `call` ， `read` ， `connect` ， `write` 的超时时间。

```kotlin
override fun setTimeOut(): Long {
    return 10L
}
```

## 自定义客户端

```kotlin
override fun handleOkHttpClientBuilder(builder: OkHttpClient.Builder) {
    builder.apply { 
        ... // 自定义OKHttpClient的配置
    }
}
```

## 注册日志拦截器

```kotlin
override fun registerLoggingInterceptor(): Interceptor? {
    
}
```