# 屏幕信息

## 获取屏幕长宽的方法

```kotlin
val screenWidth = ScreenSizeUtils.getMobileScreenWidth()
val screenHeight = ScreenSizeUtils.getMobileScreenHeight()
```

## 获取状态栏高度

```kotlin
val statusBarHeight = ScreenSizeUtils.getStatusBarHeight(this@MainActivity)
```

## 获取屏幕方向

```kotlin
val screenOrientation = ScreenSizeUtils.getScreenOrientation()
```
