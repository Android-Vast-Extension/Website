# Activity 管理

`ActivityUtils` 负责对 `Activity` 进行管理。

## 添加 Activity

```kotlin
ActivityUtils.addActivity(this@MainActivity)
```

## 移除 Activity

```kotlin
ActivityUtils.removeActivity(this@MainActivity)
```

## 根据给定的 Class 获取对应的 Activity

```kotlin
ActivityUtils.getActivity(MainActivity::class.java)
```

## 找到位于栈顶的可用 Activity

```kotlin
ActivityUtils.getCurrentActivity()
```

## 获取全部存储的 Activity

```kotlin
val activities = ActivityUtils.getActivities()
```

## 结束全部的 Activity

```kotlin
ActivityUtils.finishAllActivity()
```

## 退出 App

```kotlin
ActivityUtils.exitApp()
```
