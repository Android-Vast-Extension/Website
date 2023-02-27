# Request

`Request` 基于 `Call` 封装并进行了拓展。

## 基本使用

- 参考概览部分，实现 `ResponseApi`

- 创建网络请求的接口。

    ```java
    public interface QRService {
        @POST("/login/qr/key")
        Request<QRCodeKey> generateQRCode(@Query("timestamp") String timestamp);
    }
    ```

- 使用 `RequestBuilder` 创建实例 。

    === "kotlin"

        ```kotlin
        class NetworkRetrofitBuilder: RequestBuilder() {

            override fun setBaseUrl(): String {
                return Constant.ROOT_URL
            }

        }
        ```

    === "java"

        ```java
        public class NetworkRetrofitBuilder extends RequestBuilder {
            @NonNull
            @Override
            public String setBaseUrl() {
                return Constant.ROOT_URL;
            }
        }
        ```

- 监听网络请求结果。

    ```java
    new NetworkRetrofitBuilder().create(QRService.class).generateQRCode(DateUtils.getCurrentTime()).request(listener -> {
        listener.setOnSuccess(qrCodeKey -> {
            LogUtils.i(getDefaultTag(),qrCodeKey.getData().getUnikey());
            return null;
        });
        return null;
    });
    ```

## 配合 ResponseLiveData 使用

### 创建 ResponseLiveData 对象

```kotlin
// 创建StateLiveData对象
val qRCodeKey = ResponseLiveData<QRCodeKey>()
```

### 手动设置状态

> 具体使用可以参考 [更新 ResponseLiveData 对象](https://www.entropy2020.cn/VastDocs/document/zh/StateLiveData.html#%E6%9B%B4%E6%96%B0StateLiveData%E5%AF%B9%E8%B1%A1)

我们在获取到请求成功的结果后，使用 `postValueAndSuccess` 方法手动的改变状态。

```kotlin
fun getQRCode(timestamp:String){
    NetworkRetrofitBuilder().create(QRService::class.java).generateQRCode(timestamp)
        .request{
            onSuccess = {
                qRCodeKey.postValueAndSuccess(it)
            }
        }
}
```

### 自动设置状态

将 `qRCodeKey` 作为 `request` 的参数，该方法目前会监听以下状态 `Error` `Empty` `Success` `Failed` 。

```kotlin
fun getQRCode(timestamp:String){
    NetworkRetrofitBuilder().create(QRService::class.java).generateQRCode(timestamp)
        .request(qRCodeKey)
}
```

### 监听StateLiveData的状态

> 具体使用参考 [观察状态发生变化](https://www.entropy2020.cn/VastDocs/document/zh/StateLiveData.html#%E8%A7%82%E5%AF%9F%E7%8A%B6%E6%80%81%E5%8F%91%E7%94%9F%E5%8F%98%E5%8C%96)
