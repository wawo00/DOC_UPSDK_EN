## FAQ

### I. Android Studio AndroidManfiest.xml confliction declarations

#### 1. com.google.android.gms.version confliction or deletion error
In **Android Studio** version, in order to avoid this kind of confliction, from 2.0.21 Studio Version, Avidly ADSDK has romoved the following declarations in AndroidManfiest.xml:
```asp
<!-- admob -->
<meta-data
            android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version"/>
```
Thus, for those versions which are older than 2.0.21, if gms.version occurs, please contact our technical colleagues for help.

However, in **Android Elipse** version, you need to add the following declarations in AndroidManfiest.xml：
```asp
<!-- admob -->
<meta-data
            android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version"/>
```
Specially, please check whether if the xml format files in *res/values* content have *google_play_services_version* definition. Generally, Avidly ADSDK defined this kind in *version_ad.xml* files. If there is no definition for it, please copy *version_ad.xml* to *res/values* content.

*version_ad.xml* content：
```asp
<?xml version="1.0" encoding="utf-8"?>
<resources>
	// defined the value of gms version, the kind of integer
	// if the current version is not 9080000, please change to the correct version.
    <integer name="google_play_services_version">11020000</integer>
</resources>
```

#### 2. activity confliction or deletion error
In Android Studio versions, Avidly ADSDK from 2.0.21 Studio Version,  has removed the Activity declarations which relied on Admob and Facebook Ads in AndroidManfiest.xml:
```asp
<!-- admob -->

<activity
android:name="com.google.android.gms.ads.AdActivity"
            android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"
android:multiprocess="true"
android:theme="@android:style/Theme.Translucent"/>
<!-- admob -->


<!-- facebook -->
<activity
android:name="com.facebook.ads.InterstitialAdActivity"
android:configChanges="keyboardHidden|orientation|screenSize"
android:multiprocess="true"/>
```

The reason why we removed the declaration is when Admob and Facebook work in Studio porject, will import in aar formation and declare relevant components in AndroidManfiest.xml.

On the contrary, regarding to Eclipse project and Studio project which integrated in jar package, you need to add Acticity manually in AndroidManfiest.xml of main project.

### II. Admob gms Confliction

#### 1. Due to Facebook Ads rely on Admob Ad, confliction happens.
When Facebook Ads compile to update audience-network-sdk online, they will not only download audience-network-sdk relevant aar files, but also download the following google gms repository files. 
- play-services-ads-8.4.0
- play-services-basement-8.4.0

If google gms service is updating dependency in another version(such as 10.0.1 version) , Studio Gradle will automatically remove these two 8.4.0; But if google gms service (not 8.4.0) import in **local**, play-services-ads and play-services-basement will occur in the project, **it causes some class repeated-quoted conflictions for gms**.

Thus, please avoid the flowing conditions:
1. google gms service and facebook audience-network-sdk are updating together;
2. google gms service and facebook audience-network-sdk import local aar;
3. When google gms service is updating online, facebook audience-network-sdk imports from local aar or jar package. 

#### 2.Other Conflictions

Admob Ads need gms play service support. Thus regarding to the projects which want to support Admob Ads, must add relevant gms dependencies and configurations.

Avidly ADSDK for supporting Admob, should rely on the following gms player service library:
- play-services-ads-x.x.x
- play-services-ads-lite-x.x.x
- play-services-base-x.x.x
- play-services-basement-x.x.x
- play-services-tasks-x.x.x

> Current built-in gms version of Avidly ADSDK is play-services-ads:11.0.4，If the version is different from the main project gms version, please keep the higher gms version. To prevent unnecessary errors, no matter which version you keep, please make sure those five dependencies mentioned above should be at the same version. Or it will cause some class repeated-quoted conflictions.


### III. xxx.so missing probelms
AvidlyAdsSDK_x.x.x.aar and adcolony_ads.aar supply the following three kinds of cpu-typed .so files:
- armeabi
- armeabi-v7a
- x86

If your project (for example, games developed by cococs engine generally support armeabi only）support less than, more than or different from the above three kinds, when the procedure runs, following errors may occur.



```
java.lang.UnsatisfiedLinkError:
Couldn't load cocos2dlua from loader dalvik.system.PathClassLoader
    [DexPathList[[zip file "/data/app/org.cocos2dx.xxxxx-1.apk"],
    nativeLibraryDirectories=[/data/app-lib/org.cocos2dx.xxxxx-1, 
    /vendor/lib, /system/lib, /data/datalib]]]: findLibrary returned null
              at java.lang.Runtime.loadLibrary(Runtime.java:358)
              at java.lang.System.loadLibrary(System.java:555)
              at org.cocos2dx.lib.Cocos2dxActivity.onLoadNativeLibraries(Cocos2dxActivity.java:248)
              at org.cocos2dx.lib.Cocos2dxActivity.onCreate(Cocos2dxActivity.java:264)
              at org.cocos2dx.lua.AppActivity.onCreate(AppActivity.java:57)

```
The reason is .so files **unaligned**。

Second method for solving:
1. Regarding to gradle project, please directly add to support framework in gradle.build file under app catalog :
```asp
defaultConfig {
 
        ndk {
            // The assumption is if the app support four kinds of CPU as followed
            abiFilters 'armeabi' ,'armeabi-v7a', 'x86', 'arm64-v8a'
        }

    }
```
> The CPU framework which is added under abiFilters, is the supporting framework for current project.

2.Regarding to Eclipse and grandle.build project which cannot be modified, please delete invalid CPU framework under libs catalog. Regarding to aar files, please open it in RAR software and delete unnessessary CPU frameword.




