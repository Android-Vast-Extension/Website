# App shortcut

## Create Shortcut

The following example shows you how to create an application shortcut

```kotlin
AppShortcutsUtils.createPinnedShortcut(
    MainActivity::class.java,
    "987654321",
    R.mipmap.ic_launcher,
    "Test short cut",
    this
)
```

## Set resultIntent for shortcut

!!! warning 
    
    The Android version is required to be above 26

### Create a broadcast receiver

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

### Call setPinnedShortcutResult

Call `setPinnedShortcutResult` and pass in a `PendingIntent` object for being received by the broadcast.

```kotlin
AppShortcutsUtils.setPinnedShortcutResult {
    return@setPinnedShortcutResult PendingIntent.getBroadcast(this@IntentActivity.getContext(),0, Intent(CREATE_SHORT_CUT),PendingIntent.FLAG_IMMUTABLE)
}.createPinnedShortcut(
    MainActivity::class.java,
    "987654321",
    R.mipmap.ic_launcher,
    "Test short cut",
    this@IntentActivity.getContext()
)
```
