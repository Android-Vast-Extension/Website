# DateUtils

## 支持的时间格式

```kotlin
const val FORMAT_YYYY_MM_DD = "yyyy-MM-dd"
const val FORMAT_YYYY_MM_DD_HH_MM_SS = "yyyy-MM-dd HH:mm:ss"
const val FORMAT_YYYY_MM = "yyyy-MM"
const val FORMAT_YYYY = "yyyy"
const val FORMAT_HH_MM = "HH:mm"
const val FORMAT_HH_MM_SS = "HH:mm:ss"
const val FORMAT_MM_SS = "mm:ss"
const val FORMAT_MM_DD_HH_MM = "MM-dd HH:mm"
const val FORMAT_MM_DD_HH_MM_SS = "MM-dd HH:mm:ss"
const val FORMAT_YYYY_MM_DD_HH_MM = "yyyy-MM-dd HH:mm"
const val FORMAT_YYYY2MM2DD = "yyyy.MM.dd"
const val FORMAT_YYYY2MM2DD_HH_MM = "yyyy.MM.dd HH:mm"
const val FORMAT_MMCDDC_HH_MM = "MM月dd日 HH:mm"
const val FORMAT_MMCDDC = "MM月dd日"
const val FORMAT_YYYYCMMCDDC = "yyyy年MM月dd日"
```

## 支持的时区

```kotlin
const val GMT_PLUS_ZONE = "GMT+00:00"
const val GMT_PLUS_ONE = "GMT+01:00"
const val GMT_PLUS_TWO = "GMT+02:00"
const val GMT_PLUS_THREE = "GMT+03:00"
const val GMT_PLUS_FOUR = "GMT+04:00"
const val GMT_PLUS_FIVE = "GMT+05:00"
const val GMT_PLUS_SIX = "GMT+06:00"
const val GMT_PLUS_SEVEN = "GMT+07:00"
const val GMT_PLUS_EIGHT = "GMT+08:00"
const val GMT_PLUS_NINE = "GMT+09:00"
const val GMT_PLUS_TEN = "GMT+10:00"
const val GMT_PLUS_ELEVEN = "GMT+11:00"
const val GMT_PLUS_TWELVE = "GMT+12:00"
const val GMT_MINUS_ONE = "GMT-01:00"
const val GMT_MINUS_TWO = "GMT-02:00"
const val GMT_MINUS_THREE = "GMT-03:00"
const val GMT_MINUS_FOUR = "GMT-04:00"
const val GMT_MINUS_FIVE = "GMT-05:00"
const val GMT_MINUS_SIX = "GMT-06:00"
const val GMT_MINUS_SEVEN = "GMT-07:00"
const val GMT_MINUS_EIGHT = "GMT-08:00"
const val GMT_MINUS_NINE = "GMT-09:00"
const val GMT_MINUS_TEN = "GMT-10:00"
const val GMT_MINUS_ELEVEN = "GMT-11:00"
const val GMT_MINUS_TWELVE = "GMT-12:00"
```

## 按照指定格式获取当前时间

```kotlin
LogUtils.i(defaultTag,DateUtils.getCurrentTime(DateUtils.FORMAT_HH_MM))
```

```kotlin
2022-09-08 02:23:10.644 27118-27118 class (Da...y.kt:38)  I  method: onCreate() key: DateActivity content: 02:23
```

## 获取当前时间之前或之后的天数

```kotlin
LogUtils.i(defaultTag,DateUtils.getDayBeforeOrAfterCurrentTime(DateUtils.FORMAT_MM_DD_HH_MM_SS,-2))
```

```kotlin
2022-09-08 02:23:10.645 27118-27118 class (Da...y.kt:39)  I  method: onCreate() key: DateActivity content: 09-06 02:23:10
```

## 获取设备当前所在时区

```kotlin
Log.i("VU",DateUtils.currentTimeZone)
```

```kotlin
2022-09-08 02:23:10.645 27118-27118 class (Da...y.kt:40)  I  method: onCreate() key: DateActivity content: GMT+08:00
```

## 获取当前最小日期的Date对象

```kotlin
val date: Date = DateUtils.minDate()
```

## 按照指定格式解析的最小日期字符串

```kotlin
// 不添加参数，则默认按照yyyy-MM-dd HH:mm:ss的格式解析
LogUtils.i(defaultTag,DateUtils.minDateToString())
// 添加格式参数，只返回小时和分钟
LogUtils.i(defaultTag,DateUtils.minDateToString(DateUtils.FORMAT_HH_MM))
```

```kotlin
// 默认格式
2022-09-08 02:23:10.645 27118-27118 class (Da...y.kt:41)  I  method: onCreate() key: DateActivity content: 1900-02-01 02:23:10
// 给定格式运行结果
2022-09-08 02:23:10.646 27118-27118 class (Da...y.kt:42)  I  method: onCreate() key: DateActivity content: 02:23
```

## 根据给定的时间字符串和格式获取Date对象

```kotlin
val date: Date? = DateUtils.datetimeFromString("14:18", FORMAT_HH_MM)
```

## 将给定的Date解析为时间字符串

```kotlin
// 获取一个Date对象
val date: Date? = DateUtils.datetimeFromString("14:18", DateUtils.FORMAT_HH_MM)
// 在日志中打印时间字符串
LogUtils.i(defaultTag,DateUtils.datetimeToString(date!!, DateUtils.FORMAT_HH_MM_SS))
```

```kotlin
2022-09-08 02:23:10.646 27118-27118 class (Da...y.kt:44)  I  method: onCreate() key: DateActivity content: 14:18:00
```

## 根据给定的时区和时间格式返回对应的字符串

```kotlin
// 默认情况下，按照yyyy-MM-dd HH:mm:ss和当前所处的时区获取字符串
LogUtils.i(defaultTag,DateUtils.dateTimeToGMT())
// 设置时区为东六区，时间格式为yyyy.MM.dd HH:mm
LogUtils.i(defaultTag,DateUtils.dateTimeToGMT(DateUtils.GMT_PLUS_SIX,DateUtils.FORMAT_YYYY2MM2DD_HH_MM))
```

```kotlin
// 默认情况下
2022-09-08 02:23:10.647 27118-27118 class (Da...y.kt:45)  I  method: onCreate() key: DateActivity content: 2022-09-08 02:23:10
// 设置参数
2022-09-08 02:23:10.648 27118-27118 class (Da...y.kt:46)  I  method: onCreate() key: DateActivity content: 2022.09.08 00:23
```

## 根据给定的UTC时间和格式解析出当前时间

```kotlin
LogUtils.i(defaultTag,DateUtils.dateTimeFromGMT("07:01",DateUtils.FORMAT_HH_MM))
```

```kotlin
2022-09-08 02:23:10.648 27118-27118 class (Da...y.kt:47)  I  method: onCreate() key: DateActivity content: 15:01
```

## 获取本周开始(或结束)时间，周一是第一天

```kotlin
// 获取开始时间
LogUtils.i(defaultTag,DateUtils.weekStartTime())
// 获取结束时间
LogUtils.i(defaultTag,DateUtils.weekEndTime())
```

```kotlin
// 开始时间
2022-09-08 02:23:10.649 27118-27118 class (Da...y.kt:48)  I  method: onCreate() key: DateActivity content: 2022-09-05 02:23:10
// 结束时间
2022-09-08 02:23:10.649 27118-27118 class (Da...y.kt:49)  I  method: onCreate() key: DateActivity content: 2022-09-11 02:23:10
```

## 获取本周开始(或结束)的时间戳，周日是第一天

```kotlin
// 开始时间戳
LogUtils.i(defaultTag,DateUtils.getWeekStartTime())
// 结束时间戳
LogUtils.i(defaultTag,DateUtils.getWeekEndTime())
```

```kotlin
// 开始时间戳
2022-09-08 02:23:10.649 27118-27118 class (Da...y.kt:50)  I  method: onCreate() key: DateActivity content: 2022-09-04 02:23:10
// 结束时间戳
2022-09-08 02:23:10.650 27118-27118 class (Da...y.kt:51)  I  method: onCreate() key: DateActivity content: 2022-09-10 02:23:10
```