# 可变非空变量

有的时候需要创建可变非空变量，这就需要使用 `NotNUllVar` 来实现。

```kotlin
private var age by NotNUllVar<Int>()
```

`NotNUllVar` 同时提供一个属性 `once` ，如果你希望该变量只能被初始化一次，可以指定 `once` 为 `true`

```kotlin
private var age by NotNUllVar<Int>()
```
