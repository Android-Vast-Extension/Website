# 位图工具类

`BmpUtils` 主要为你提供了关于 [Bitmap](https://developer.android.com/reference/kotlin/android/graphics/Bitmap?hl=en) 的一些方法

## 位图合并

> 位图合并代码来自:
> [Android将两个bitmap合并](https://blog.csdn.net/brian512/article/details/50562193)
> 在此表示感谢。

### 把两个位图覆盖合成为一个位图，以底层位图的长宽为基准

```kotlin
iv.setImageBitmap(mergeBmp(getAppBitmap(this)!!,bitmap))
```

<figure markdown>
  ![位图合并](../../../img/mergeBmp.png){ width="200" }
  <figcaption>位图合并</figcaption>
</figure>

### 把两个位图覆盖合成为一个位图，左右拼接

```kotlin
// iv是一个ImageView控件
// 我们使用AppInfoUtils里面的方法获取应用Bmp图标
iv.setImageBitmap(mergeBmpLR(getAppBitmap(this)!!,getAppBitmap(this)!!,true))
```

<figure markdown>
  ![位图合并](../../../img/mergeBmpLR.png){ width="200" }
  <figcaption>位图合并</figcaption>
</figure>

### 把两个位图覆盖合成为一个位图，上下拼接

```kotlin
// iv是一个ImageView控件
// 我们使用AppInfoUtils里面的方法获取应用Bmp图标
iv.setImageBitmap(mergeBmpTB(getAppBitmap(this)!!,getAppBitmap(this)!!,true))
```

<figure markdown>
  ![位图合并](../../../img/mergeBmpTB.png){ width="200" }
  <figcaption>位图合并</figcaption>
</figure>

## 通过Base64获取位图

通过 `getBitmapFromBase64` 方法将 **base64**字符串转换成 `Bitmap` 对象。

```kotlin
val base64 = .....
val bitmap = BmpUtils.getBitmapFromBase64(base64)
```

## 通过Drawable获取位图

`getBitmapFromDrawable` 可以将 `Drawable` 转换成 `Bitmap` 对象。
