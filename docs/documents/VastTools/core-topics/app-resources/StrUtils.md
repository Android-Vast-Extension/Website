# 字符串工具

## 字符串依次相加

```kotlin
LogUtils.i(defaultTag,StrUtils.strConcat("1","2","3"))
```

```kotlin
123
```

## 获取带单位的字符串

目前支持下列单位

| 单位   | 示例值 |
| :----: | :------: |
| 角度 | 39° |
| 摄氏度 | 36℃ |
| 千米/时 | 2km/h |
| 千米 | 2km |
| 米 | 2m |
| 米/秒 | 2m/s |
| 百分比 | 77％ |

```kotlin
// 获取千米单位数值
val value = StrUtils.getUnitStr("2", StrUtils.Unit.Kilometer)
```
