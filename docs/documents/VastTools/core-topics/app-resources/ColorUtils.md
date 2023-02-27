# 颜色转换

`ColorUtils` 为你提供了 Color 不同格式之间的转换方法。

## 解析颜色字符串

解析颜色字符串，并返回对应的颜色整数，否则为 COLOR_PARSE_ERROR。

```kotlin
val colorInt = ColorUtils.colorHex2Int("#12c2e9")
```

## 将颜色十六进制字符串转换为 RGB 数组

```kotlin
val rgb:IntArray = ColorUtils.colorHex2RGB("#12c2e9")
```

## 将 color-int 转换为十六进制字符串

```kotlin
val colorHex:String = ColorUtils.colorInt2Hex(-15547671)
```

## 将 color-int 转换为RGB数组

```kotlin
val rgb:IntArray = ColorUtils.colorInt2RGB(-15547671)
```

## 将 RGB 数组转换为颜色十六进制字符串

```kotlin
val colorHex:String = ColorUtils.colorRGB2Hex(intArrayOf(63,226,197))
```

## 将 RGB 数组转换为 color-int

```kotlin
val colorHex:Int = ColorUtils.colorRGB2Int(intArrayOf(63,226,197))
```

## 判断是否是十六进制颜色字符串

```kotlin
val isColorHex = ColorUtils.isColorHex("#12c2e9")
```

## 获得具有透明度的颜色

```kotlin
ColorUtils.getColorWithTransparency(50,-15547671)
```
