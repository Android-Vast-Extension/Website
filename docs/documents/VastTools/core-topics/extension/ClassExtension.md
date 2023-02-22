# Class转换为Map

## 默认转换

通过使用 `convertClassToDefaultMap` ，你可以将对应的类以键值对的形式返回，例如：

```kotlin
val person = Person("张","三")
val map = person.convertClassToDefaultMap()
```

此时打印 `map` 可以看到

```kotlin
firstName 张
lastName 三
```

## 更改键名

如果你不想使用**属性名**作为默认键名，可以使用 `@MapKey` 注解来实现，例如：

```kotlin
class Person(
    @MapKey("fn") val firstName: String,
    @MapKey("ln") val lastName: String
)
```

使用 `convertClassToMap` 获取转换后的键值对

```kotlin
ln 三
fn 张
```

## 使用字符串替代枚举变量

如果你想用自定义字符串作为转换后的map中的值，可以使用 `MapEnumValue` 来实现

```kotlin
// 定义性别枚举类
enum class Gender{
    @MapEnumValue("m") MAN,
    @MapEnumValue("wm") WOMAN
}

class Person(
    @MapKey("fn") val firstName: String,
    @MapKey("ln") val lastName: String,
    @MapKey("g") val gender: Gender
)
```

使用 `convertClassToMap` 获取转换后的键值对

```kotlin
ln 三
g m
fn 张
```
