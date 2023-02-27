# Activity Management

`ActivityUtils` is responsible for managing `Activity`.

## Add Activity

```kotlin
ActivityUtils. addActivity(this@MainActivity)
```

## Remove Activity

```kotlin
ActivityUtils. removeActivity(this@MainActivity)
```

## Get the corresponding Activity according to the given Class

```kotlin
ActivityUtils.getActivity(MainActivity::class.java)
```

## Find the available Activity at the top of the stack

```kotlin
ActivityUtils. getCurrentActivity()
```

## Get all stored activities

```kotlin
val activities = ActivityUtils. getActivities()
```

## End all activities

```kotlin
ActivityUtils. finishAllActivity()
```

## Exit App

```kotlin
ActivityUtils. exitApp()
```