# 应用文件管理

## 存储路径的获取

```kotlin
LogUtils.i(defaultTag, appInternalFilesDir().path)
LogUtils.i(defaultTag, appInternalCacheDir().path)
LogUtils.i(defaultTag, appExternalFilesDir(null)?.path)
LogUtils.i(defaultTag, appExternalCacheDir()?.path)
```

```kotlin
/data/user/0/com.gcode.vastutils/files
/data/user/0/com.gcode.vastutils/cache
/storage/emulated/0/Android/data/com.gcode.vastutils/files
/storage/emulated/0/Android/data/com.gcode.vastutils/cache
```

## 保存文件

```kotlin
saveFile(File(appInternalFilesDir().path,"save.txt"))
```

## 创建文件夹

```kotlin
makeDir(File(appInternalFilesDir().path,"makeDir"))
```

## 删除文件夹以及文件夹内的内容

```kotlin
deleteDir(File(appInternalFilesDir().path,"makeDir2"))
```

## 对文本文件进行写入

```kotlin
writeFile(File(appInternalFilesDir().path, "save.txt"),
            object : FileUtils.WriteEventListener {
                override fun writeEvent(fileWriter: FileWriter) {
                    fileWriter.write("Hello")
                }
            })
```
