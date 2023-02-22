# 屏幕信息

## 获取屏幕长宽的方法

```kotlin
val screenWidth = ScreenSizeUtils.getMobileScreenWidth()
val screenHeight = ScreenSizeUtils.getMobileScreenHeight()
```

```kotlin
LogUtils.i("VU","$screenWidth $screenHeight")

2022-02-10 21:47:37.265 4463-4463/com.gcode.vastutils I/class (MainActivity.kt:43): method: onCreate() key: VU content: 1080 2340
```

## 获取状态栏高度

```kotlin
val statusBarHeight = ScreenSizeUtils.getStatusBarHeight(this@MainActivity)
```

## 获取屏幕方向

```kotlin
val screenOrientation = ScreenSizeUtils.getScreenOrientation()
```
