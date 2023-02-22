# 常见Intent

`IntentUtils` 为你提供了一些常见 [Intent](https://developer.android.com/guide/components/intents-common?hl=zh-cn) 的快捷启动

注意：如果你的设备是Android 11(API>=30)，你应该在清单中做出如下声明，否则可能会找不到对应的Activity。例如：

```xml
<queries>
    <intent>
        <action android:name="android.intent.action.DIAL"/>
    </intent>
</queries>
```

## 快速开始

!!! Intent快捷使用

    === "Kotlin"

        ```kotlin
        mBinding.callBtn.setOnClickListener {
            dialPhoneNumber(this, "12345678910")
        }

        mBinding.searchWeb.setOnClickListener {
            searchWeb(this, "12345678910")
        }

        mBinding.openWebPage.setOnClickListener {
            openWebPage(this, "http://www.baidu.com")
        }

        mBinding.sendMmsMessage.setOnClickListener {
            sendMmsMessage(this, "123456", "1238489")
        }

        mBinding.sendEmail.setOnClickListener {
            openEmail(this, arrayOf("12345678910@qq.com"))
        }

        mBinding.createAlarm.setOnClickListener {
            val alarmConfig = IntentUtils.AlarmConfig()
                .setMsg("你好")
                .setHour(12)
                .setMinutes(30)
            createAlarm(this, alarmConfig)
        }

        mBinding.wifiSetting.setOnClickListener {
            openWirelessSettings(this)
        }
        ```

    === "Java"

        ```java
        phoneCall.setOnClickListener(view -> 
            dialPhoneNumber(this, myUserProfile.getPhone())
        );
        ```
