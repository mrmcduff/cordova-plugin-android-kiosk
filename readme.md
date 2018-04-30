# cordova-plugin-android-kiosk
Cordova single purpose applicaion plugin for Android. This is a fork of https://github.com/shougao/cordova-plugin-android-kiosk, with the only notable change being
that the app can no longer act as the home screen.

## install
```
cordova plugin add cordova-plugin-android-kiosk-nohome
```

## usage
``Kiosk`` is a ``cordova.plugin.kiosk.Kiosk`` to lock or unlock you app to the Only one app.

lock or unlock the app to Single Pourse device
```
function success(message){
    console.log("success");
}

function error(message){
    console.log("error: reason is " + message);
}

Kiosk.lock(success, error, boolean enable); // the boolean parameter is enable or disable this mode.
```
check the current lock state.
```
function success(message){
    console.log("locked = " + message); //true or false.
}
Kiosk.isLocked(success)
```

you have to set you app to the device owner forllow google AOSP design.
```
adb shell dpm set-device-owner com.example.template/.kiosk.plugin.MyAdmin
```
the setting will sotren at ``/data/system/device_policy.xml``(before android 6.0)
``/data/system/device_policy_2.xml``(> android 6.0)

First, create a file device_owner.xml with following content:
```
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<root>
    <device-owner package="com.myDomain.myPackage" name="" component="com.example.template/com.example.template.kiosk.plugin.MyAdmin" userRestrictionsMigrated="true" />
</root>
```
on android 8.0
```
/data/system # cat device_owner_2.xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<root>
<device-owner package="com.example.template" name="" component="com.example.template/com.example.template.kiosk.plugin.MyAdmin" userRestrictionsMigrated="true" />
<device-owner-context userId="0" />
</root>
```
chown system:system device_owner.xml

the cordova plugin source and target tag in plugin.xml is sutable for my project, the package name is ``com.example.template``, if your project name is different, please using your pakcage name instand of it.
