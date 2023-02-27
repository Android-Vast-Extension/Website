# Download

`DownloadUtils` is based on [OKHttp3](https://github.com/square/okhttp) and [ProgressManager](https://github.com/SakurajimaMaii/ProgressManager) to help you download files.

Using `DownloadUtils` to download what you want, the following is a demo example:

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
