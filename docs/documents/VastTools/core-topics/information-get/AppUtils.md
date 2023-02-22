# 应用信息获取

`AppUtils` 用来获取和App有关的相关信息。

## 获取应用包名

示例代码

```kotlin
Log.i("VU",AppUtils.getPackageName()?:"")
```

运行结果

```kotlin
2022-02-08 12:15:42.888 28668-28668/com.gcode.vastutils I/VU: com.gcode.vastutils
```

## 获取应用名

示例代码

```kotlin
Log.i("VU",AppUtils.getAppName()?:"")
```

运行结果

```kotlin
2022-02-08 12:16:34.509 29223-29223/com.gcode.vastutils I/VU: VastUtilsSampleDemo
```

## 获取版本名

示例代码

```kotlin
Log.i("VU",AppUtils.getVersionName()?:"")
```

运行结果

```kotlin
2022-02-08 12:21:32.561 586-586/com.gcode.vastutils I/VU: 1.0
```

## 获取版本号

示例代码

```kotlin
Log.i("VU",AppUtils.getVersionCode().toString())
```

运行结果

```kotlin
2022-02-08 12:24:11.924 6275-6275/com.gcode.vastutils I/VU: 1
```

## 判断应用是否是Debug状态

示例代码

```kotlin
Log.i("VU",AppUtils.getAppDebug().toString())
```

运行结果

```kotlin
2022-02-08 12:24:48.678 7578-7578/com.gcode.vastutils I/VU: true
```

## 获取应用图标

```kotlin
// iv是一个imageView控件
iv.setImageBitmap(AppUtils.getAppBitmap())
```

## build.gradle配置

```groovy
defaultConfig {
  applicationId "com.gcode.vastutils"
  ... //sdk version
  versionCode 1
  versionName "1.0"

  testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
}
```
