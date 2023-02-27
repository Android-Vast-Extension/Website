# Color conversion

`ColorUtils` provides you with methods for converting Color between different formats.

## Parse the color string

Parse the color string and return the corresponding color integer, otherwise COLOR_PARSE_ERROR.

```kotlin
val colorInt = ColorUtils. colorHex2Int("#12c2e9")
```

## Convert color hex string to RGB array

```kotlin
val rgb:IntArray = ColorUtils. colorHex2RGB("#12c2e9")
```

## Convert color-int to hex string

```kotlin
val colorHex:String = ColorUtils. colorInt2Hex(-15547671)
```

## Convert color-int to RGB array

```kotlin
val rgb:IntArray = ColorUtils.colorInt2RGB(-15547671)
```

## Convert RGB array to color hex string

```kotlin
val colorHex:String = ColorUtils.colorRGB2Hex(intArrayOf(63,226,197))
```

## Convert RGB array to color-int

```kotlin
val colorHex:Int = ColorUtils.colorRGB2Int(intArrayOf(63,226,197))
```

## Determine whether it is a hexadecimal color string

```kotlin
val isColorHex = ColorUtils.isColorHex("#12c2e9")
```

## Get a color with transparency

```kotlin
ColorUtils.getColorWithTransparency(50,-15547671)
```
