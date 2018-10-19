## Use Unity

Unity 5.5 and above support multidex, no need to export to Android Studio project, complete the subcontracting settings directly in Unity IDE.

### 1.Open `Gradle build system`

- Open `Build Settings` in`Unity Editor`  ( File > Build Settings…)
- Select `Android` in list
- Set `Build System` as `Gradle (new)`

Maybe **Build Settings** are slightly different in many Unity IDE , please be flexible to complete this process

![666](http://docc.upltv.com/uploads/201807/5b39e51a967db_5b39e51a.jpeg "666")

### 2.Modify `Gradle settings`
####  (1)  s For Unity2017.2 and above, you can open `Player Settings` and check the `Custom Gradle Template` checkbox as follows. For other versions, you need to copy the `mainTemplate.gradle` file (search for the mainTemplate in the Unity installation directory) to `Assets/Plugins/Android/mainTemplate.gradle`.
![777](http://docc.upltv.com/uploads/201807/5b39ec4b74539_5b39ec4b.jpeg "777")

#### (2) Add **multiDexEnabled true** in **defaultConfig**

```groovy
defaultConfig {
    targetSdkVersion **TARGETSDKVERSION**
    applicationId '**APPLICATIONID**'
    multiDexEnabled true
    ndk {
            abiFilters **ABIFILTERS**
        }
}
```

#### (3) Add **com.android.support:multidex:1.0.1** in dependencies
**com.android.support:multidex:1.0.1**。
```groovy
dependencies {
    compile 'com.android.support:multidex:1.0.1'
    compile fileTree(dir: 'libs', include: ['*.jar'])
}
```

#### (4) Remove minifyEnabled and useProguard setting
If there is an error `shrinking/minification is not supported with Multidex`，please remove the useProguard parameter and even remove the minifyEnabled parameter.

### 3.Initialize Multidex 
If AndroidManifest.xml does not exist in `Assets/Plugins/Android/ `, copy the default AndroidManifest.xml from the Unity installation directory to this directory. If the **application** tag of AndroidManifest.xml does not have a subclass of MultiDexApplication or MultiDexApplication as `android:name`, add `android.support.multidex.MultiDexApplication` as `android:name`

```xml
 <?xml version="1.0" encoding="utf-8"?>
 <manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.myapp">
     <application
            android:name="android.support.multidex.MultiDexApplication" >
        ...
     </application>
 </manifest>
```
