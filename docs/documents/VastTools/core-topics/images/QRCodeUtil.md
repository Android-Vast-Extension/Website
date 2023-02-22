# 二维码工具类

`QRCodeUtil` 基于 [zxing](https://github.com/zxing/zxing) 实现，通过 `createQRCodeBitmap` 方法你可以将指定内容转换为二维码。

```kotlin
QRCodeUtil.createQRCodeBitmap("Hello",50,50)
```