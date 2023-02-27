# 下载

`DownloadUtils` 是基于 [OKHttp3](https://github.com/square/okhttp) 和 [ProgressManager](https://github.com/JessYanCoding/ProgressManager) 构建的下载工具类。

## 快速开始

你可以使用 `DownloadUtils` 下载你想要的内容了，以下为演示示例：

!!! 下载示例

    === "Kotlin"

        ```kotlin
        DownloadUtils
            .createConfig()
            .setDownloadUrl(downloadUrl)
            .setSaveDir(saveDir)
            .setDownloading { progress->
                LogUtils.i(getDefaultTag(), "downloading ${progress?.percent?.toFloat()}")
                getBinding().downloadCv.setProgress((progress?.percent?.toFloat() ?: 0f) / 100f)
            }
            .setDownloadFailed {
                LogUtils.i(getDefaultTag(), "download failed:" + it?.message)
            }
            .setDownloadSuccess {
                LogUtils.i(getDefaultTag(), "download success.")
                getBinding().downloadCv.setProgress(1f)
            }
            .download()
        )
        ```

    === "Java"

        ```java
        DownloadUtils.createConfig()
            .setDownloadUrl(downloadUrl)
            .setSaveDir(saveDir)
            .setDownloading(progressInfo -> {
                LogUtils.INSTANCE.i(getDefaultTag(), "downloading" + progressInfo.getPercent());
                return null;
            })
            .setDownloadFailed(it -> {
                LogUtils.INSTANCE.i(getDefaultTag(), "download failed:" + it.getMessage());
                return null;
            })
            .setDownloadSuccess(() -> {
                LogUtils.INSTANCE.i(getDefaultTag(), "download success.");
                return null;
            })
            .download();
        ```
