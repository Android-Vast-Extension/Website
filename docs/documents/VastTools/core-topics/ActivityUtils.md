# Activity管理

`ActivityUtils` 负责对 `Activity` 进行管理。

## 添加Activity

```kotlin
ActivityUtils.addActivity(this@MainActivity)
```

## 移除Activity

```kotlin
ActivityUtils.removeActivity(this@MainActivity)
```

## 根据给定的Class获取对应的Activity

```kotlin
ActivityUtils.getActivity(MainActivity::class.java)
```

## 获取全部存储的Activity

```kotlin
val activities = ActivityUtils.getActivities()
```

## 结束全部的Activity

```kotlin
ActivityUtils.finishAllActivity()
```

## 退出App

```kotlin
ActivityUtils.exitApp()
```
