# ApiCall

`ApiCall` 基于 `Call` 封装并进行了拓展。

## 基本使用

- 参考概论部分，实现BaseApiRsp。
- 创建网络请求的接口。

    ```java
    public interface UserService {
        @POST("/login/qr/key")
        ApiCall<QRCodeKey> generateQRCode(@Query("timestamp") String timestamp);
    }
    ```

- 监听网络请求结果。

    ```java
    userService.generateQRCode(DateUtils.getCurrentTime(DateUtils.FORMAT_MM_DD_HH_MM)).request(RspListener -> {
        RspListener.setOnSuccess(qrCodeKey -> {
            LogUtils.i(getDefaultTag(),qrCodeKey.getData().getUnikey());
            return null;
        });
        return null;  
    });
    ```

## 配合StateLiveData使用

首先创建 `StateLiveData` 对象

```java
// 创建StateLiveData对象
public StateLiveData<QRCodeKey> qRCodeKey;
```

### 手动设置状态

> 具体使用可以参考 [更新StateLiveData对象](https://www.entropy2020.cn/VastDocs/document/zh/StateLiveData.html#%E6%9B%B4%E6%96%B0StateLiveData%E5%AF%B9%E8%B1%A1)

我们在获取到请求成功的结果后，使用 `postValueAndSuccess` 方法手动的改变状态。

```java
userService.generateQRCode(DateUtils.getCurrentTime(DateUtils.FORMAT_MM_DD_HH_MM)).request(RspListener -> {
    RspListener.setOnSuccess(qrCodeKey -> {
        getViewModel().qRCodeKey.postValueAndSuccess(qrCodeKey); // 自动切换状态
        return null;
    });
    return null;
});
```

### 自动设置状态

将 `qRCodeKey` 作为 `request` 的参数，该方法目前会监听以下状态 `Error` `Empty` `Success` `Failed` 。

```java
public void getQRCode(){
    userService.generateQRCode(DateUtils.getCurrentTime(DateUtils.FORMAT_MM_DD_HH_MM)).request(qRCodeKey);
}
```

### 监听StateLiveData的状态

> 具体使用参考 [观察状态发生变化](https://www.entropy2020.cn/VastDocs/document/zh/StateLiveData.html#%E8%A7%82%E5%AF%9F%E7%8A%B6%E6%80%81%E5%8F%91%E7%94%9F%E5%8F%98%E5%8C%96)
