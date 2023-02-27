# DownloadCircleView

`DownloadCircleView` 是圆形下载进度条。

<figure markdown>
  ![圆形下载进度条](../../../img/dlcv_eg_1.gif){ width="200" }
  <figcaption>圆形下载进度条</figcaption>
</figure>

## 快速使用

### xml使用

```xml
<com.ave.vastgui.tools.view.downloadcircle.DownloadCircleView
    android:id="@+id/downloadCv"
    android:layout_width="200dp"
    android:layout_height="200dp"
    app:progress_background_width="20dp"
    app:progress_text_size="12sp"/>
```

### 属性设置

`DownloadCircleView` 目前支持你自定义以下内容：

- 进度条起始点颜色
- 进度条结束点颜色
- 进度条背景色
- 进度条颜色（支持渐变色）
- 进度条文字颜色
- 进度条文字大小
- 进度条是否显示起始点和结束点
- 进度条样式

```kotlin
// Here is an example
getBinding().downloadCv.apply {
    setProgressShader(
        LinearGradient(
            -700f, 0f, 700f, 0f,
            colors, pos,
            Shader.TileMode.CLAMP
        )
    )
    setProgressStrokeCap(Paint.Cap.ROUND)
    setProgressEndColor(ColorUtils.colorHex2Int("#4286f4"))
    setProgressStartAndEndEnabled(false)
}
```