# 媒体图像

`ImageMgr` 目前主要负责处理手机上的媒体图像。

## Uri获取文件

通过 `getFileByUri` 方法可以将给定的 `Uri` 转为 `File` 对象。

## 通过File获取Uri

在使用诸如相机裁剪等功能时，你需要指定输出 Uri ， `ImageMgr` 为你提供了三种方式取获取与 `File` 文件对应的 `Uri` 。

```kotlin
val intent = Intent("com.android.camera.action.CROP").apply {
    .... // 其他设置
    val output = File("avatar.jpg").let {
        if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.R){
            ImageMgr.getFileUriAboveApi30(it)
        } else if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.N){
            ImageMgr.getFileUriAboveApi24(it,null)
        } else {
            ImageMgr.getFileUriOnApi23(it)
        }
    }
    putExtra(MediaStore.EXTRA_OUTPUT, output)
}
```
