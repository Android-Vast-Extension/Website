# 消息框

`ToastUtils` 为你提供了快捷的弹窗设置

## 弹出长Toast

!!! 弹出长Toast

    === "Kotlin"

        ```kotlin
        ToastUtils.showLongMsg(this, "Hello") // 直接使用字符
        ToastUtils.showLongMsg(this, R.string.app_name) // 使用str id
        ```

    === "Java"

        ```java
        ToastUtils.showLongMsg(this, "Hello") // 直接使用字符
        ToastUtils.showLongMsg(this, R.string.app_name) // 使用str id
        ```

## 弹出短Toast

!!! 弹出短Toast

    === "Kotlin"

        ```kotlin
        ToastUtils.showShortMsg(this, "Hello") // 直接使用字符
        ToastUtils.showShortMsg(this, R.string.app_name) // 使用str id
        ```

    === "Java"

        ```java
        ToastUtils.showShortMsg(this, "Hello") // 直接使用字符
        ToastUtils.showShortMsg(this, R.string.app_name) // 使用str id
        ```
