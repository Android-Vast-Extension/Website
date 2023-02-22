# 文件路径获取

`UriUtils` 允许你通过 `Uri` 获取文件的真实路径。

```kotlin
private val openGalleryLauncher =
        registerForActivityResult(ActivityResultContracts.GetContent()) {
            val real = UriUtils.getRealPath(it!!)
        }
```
