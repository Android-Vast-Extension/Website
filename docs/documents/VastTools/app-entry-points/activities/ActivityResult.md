# 与其他应用交互

## 同时获取相册的照片和视频

```kotlin
private val openGalleryLauncher =
    registerForActivityResult(GetMediaActivityResultContract()) {
        getBinding().videoView.apply {
            setVideoURI(it)
            start()
        }
    }
```
