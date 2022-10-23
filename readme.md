# Bluetooth Low Energy Server with ANDROID-BLESSED library (original)

This is the original BLE Peripheral (server) example using the code in 
https://github.com/weliem/bluetooth-server-example.

The code is minimal changed to get a basis for further enhancements.

The library in use (ANDROID-BLESSED) is available here: https://github.com/weliem/blessed-android 
provided by **Martijn van Welie**.

For a general overview on Bluetooth Low Energy (BLE) see this perfect article "The Ultimate Guide to Android Bluetooth Low Energy", 
available as PDF in the docs folder as well: https://punchthrough.com/android-ble-guide/.


![client_view_after_connect](https://github.com/MichaelsPlayground/BleServerBlessedOriginal/blob/master/docs/client01.png?raw=true)


To check that the server is up and running I recommend to install another app on a second device that 
allows to connect to the "Server", I'm using **nRF Connect for Mobile** and it is available on the 
Google's PlayStore:  https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp&hl=de&gl=US. I 
provide a simple manual on how to work with the nRF Connect-app here:
[nRFConnect_manual](nrfconnect_manual.md)

To get the Server app to build you need 2 additional dependencies, add them in build.gradle(app):
```plaintext
    implementation 'com.jakewharton.timber:timber:5.0.1'
    implementation 'com.github.weliem:blessed-android:2.3.4'
```

Additionally a new line is necessary in the settings.gradle file (project settings):
```plaintext
add the line maven { url 'https://jitpack.io' }:

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

You may notice that the AndroidManifest.xml does not contain any Bluetooth related permissions - they are all  
set within the library but you are asked to grant some runtime permissions during startup (depending on the Android 
SDK version running on your Smartphone the server is running on).

Notice regarding a bug in the blessed-library's log system: in BluetoothServer.java you will notice an 
"error" on line 185 ("Cannot resolve method 'plant(timber.log.Timber.DebugTree)'"):
```plaintext
Timber.plant(new Timber.DebugTree());
```
This error is filed as a Timber issue and may get corrected in a newer version. The good news is - you 
can build your app regardless of this error and you still see the logged messages in your LogCat.

**Important notice when working with an emulated device running on a Smartphone (e.g. the BleServerBlessedOriginal): 
For security reasons the address the server can get connected is changing very often so when using a client app 
like the nRF Connect-app it is often necessary to (re)run a scan AND choose the newest entry (mostly the most  
bottom down one).**


Some technical details on this app:
```plaintext
minimum SDK is 21
compiled/target SDK is 33
Gradle version is 7.4
```


