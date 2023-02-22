# 应用快捷方式

## 创建快捷方式

下面的示例向你展示了如何创建一个应用快捷方式

```kotlin
AppShortcutsUtils.createShortCut(
    MainActivity::class.java,
    "987654321",
    R.mipmap.ic_launcher,
    "测试快捷方式",
)
```

## 为快捷方式设置resultIntent

> Android版本要求在26以上

### 创建广播接收者

```kotlin
class ShortcutReceiver: BroadcastReceiver() {

    companion object{
        const val CREATE_SHORT_CUT = "com.gcode.vastutils.SHORTCUT_ADDED"
    }

    override fun onReceive(context: Context?, intent: Intent?) {
        if(intent?.action == CREATE_SHORT_CUT){
            throw RuntimeException("Hello")
        }
    }

}
```

### 调用setPinnedShortcutResult

调用 `setPinnedShortcutResult` ，传入一个 `PendingIntent` 对象，用于被广播接收。

```kotlin
AppShortcutsUtils.setPinnedShortcutResult {
    return@setPinnedShortcutResult PendingIntent.getBroadcast(this@IntentActivity.getContext(),0, Intent(CREATE_SHORT_CUT),PendingIntent.FLAG_IMMUTABLE)
}.createPinnedShortcut(
    MainActivity::class.java,
    "987654321",
    R.mipmap.ic_launcher,
    "测试快捷方式",
    this@IntentActivity.getContext()
)
```
