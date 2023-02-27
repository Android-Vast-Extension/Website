# NetState

With `NetStateUtils` you can easily check some network status about your device

## Check if the network is available

```kotlin
// True is available, otherwise False
val available = isNetworkAvailable()
```

## Check if it is connected to WIFI

```kotlin
// True is in WIFI connection, otherwise False
val isWifi = isWIFI()
```

## Check if you are on the mobile network

```kotlin
// True is in the mobile network connection, otherwise False
val isMobile = isMobile()
```

## Check WIFI signal strength

```kotlin
// signalStrength is the signal strength
val signalStrength = getWifiDBM()
```
