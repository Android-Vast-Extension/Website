# 系统信息

`SystemUtils` 为你提供了获取系统信息的一些方法

## 获取系统语言

```kotlin
LogUtils.i("VU", systemLanguage)
```

运行结果

```kotlin
2022-02-10 22:06:24.272 24641-24641/com.gcode.vastutils I/class (MainActivity.kt:52): zh
```

## 返回所有已安装语言环境的数组

```kotlin
for(locale in systemLanguageList){
    // to do something
}
```

## 返回系统的安卓版本

```kotlin
LogUtils.i("VU", systemAndroidVersion)
```

运行结果

```kotlin
2022-02-10 22:12:03.397 29894-29894/com.gcode.vastutils I/class (MainActivity.kt:52): 12
```

## 返回最终产品的最终用户可见名称

```kotlin
// 该设备是REDMI K40
2022-02-10 22:15:53.820 4584-4584/com.gcode.vastutils I/class (MainActivity.kt:52): M2012K11AC
```

## 返回与产品/硬件相关联的消费者可见品牌（如果有）

```kotlin
LogUtils.i("VU", deviceBrand)
```

运行结果

```kotlin
2022-02-10 22:17:47.494 6086-6086/com.gcode.vastutils I/class (MainActivity.kt:52): Redmi
```

```kotlin
LogUtils.i("VU", SystemUtils.getAvailableMemory().toString())
```