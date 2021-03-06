## Android Studio

### I.Structure of  UPSDK JavaScriptPlugin

Regarding to Android Studio or Gradle built project, UPSDK suggests it should be import by other main project in  *.aar  format. Download UPSDK CppPlugin( [Android-LayaboxJsSDK](http://doc.upltv.com/en/master/chapters/chapter09.html "SDKDownLoad") UPSDK JsPlugin)You will see the structure of directory when you unzip it:


![](http://docc.upltv.com/uploads/201809/5b98ed83ade86_5b98ed83.png)
yyy
> The UPSDK JsPlugin main package is named`UPAdsSdk_LayaJs_x.x.xx_dex.aar`.

- `Android Studio`
   This directory mainly contains the ad dependency library files required for Android Studio.
- `js`
   This directory mainly contains some *.js source files for bridging the current Layabox Js project with the UPSDK interface .
- `Eclipse`
   This directory contains some jars and resource files. Please ignore this directory if you use  Android Studio to build apk.
- `proguard-project.txt`
   The configuration file of confusion,if you need to obfuscate code, add the contents of this file to the file that the project depends on.

### II.Import UPSDK main package
#### 1.Add files of UPSDK

According to the above introduction, find the file named `UPAdsSdk_LayaJs_x.x.xx_dex.aar` in the file directory you downloaded and add it to the `libs` directory of the project (Note: If there is no this directory, try to  create it and in the same directory as src.
After adding, it looks like this:

![](http://docc.upltv.com/uploads/201809/5b98f0d13705b_5b98f0d1.png)
> `UPAdsSdk_LayaJs_3.0.05_dex`just for reference

To ensure that the aar package in the libs directory is correctly referenced by the project, check the `build.gradle` file in the `app` directory to add the following  parameters:


```groovy
repositories {
        flatDir {
             dirs 'libs'
        }
}

```
Finally add aar to the dependencies scope


```groovy
dependencies {
// Please replace UPAdsSdk_LayaJs_3.0.03_dex with the actual file name.
compile(name: 'UPAdsSdk_LayaJs_3.0.05_dex', ext: 'aar')
}
```

#### 2.Check minSdkVersion and targetSdkVersion in `build.gradle`
UPSDK requires that minSdkVersion cannot be lower than 15, and targetSdkVersion cannot be higher than 26, so check it in the `build.gradle` file .

Sample：

```groovy
 defaultConfig {
        minSdkVersion 16
        targetSdkVersion 26
}
```

#### 3.Make sure *.so files are aligned
There are 3 types of .so files of the cpu type in `UPAdsSdk_LayaJs_x.x.xx_dex.aar`：
- armeabi
- armeabi-v7a
- x86

Please add abiFilters configuration to the `gradle.build` file according to the cup type supported by the project ,that can ensure these files are aligned.

If the current project only supports armeabi-v7a, please refer to the following modifications:
```
defaultConfig {
        ndk {
            abiFilters 'armeabi-v7a'
        }
 }
```

>abiFilters 'armeabi-v7a' means this app will be supported in devices which base on armeabi-v7a architecture.

### III.Add ad networdks

#### 1.Add Google Ads SDK

In the `build.gradle` , download the gms play-service16.0.0 package from Google's remote repository via the compile command.Like this:
    
    dependencies {
        compile 'com.google.android.gms:play-services-ads:17.2.0'
    }

> In particular, if your project already has a different version of google play service, use the higher version.

#### 2.Add other networdks
To ensure you get more revenue, add as many ad libraries as possible to your project.
Please refer to the following method to add the file named `xxx_ads.aar` in `Android Studio/aar` to the project.

###### Global except China
The build.gradle is as follows下：
```groovy
dependencies {
    //other ads-libs
    //gson-2.7.jar in folder named android_support_library
    compile(name: 'gson-2.7', ext: 'jar')
    compile(name: 'facebook_ads', ext: 'aar')
    compile(name: 'facebook_exo_player', ext: 'aar')

    compile(name: 'mobvista_ads', ext: 'aar')
    compile(name: 'unity_ads', ext: 'aar')
    compile(name: 'vungle_ads', ext: 'aar')
    compile(name: 'chartboost_ads', ext: 'aar')
    compile(name: 'ironsource_ads', ext: 'aar')
    
    compile(name: 'adcolony_ads', ext: 'aar')
    compile(name: 'applovin_ads', ext: 'aar')
    compile(name: 'playable_ads', ext: 'aar')
    compile(name: 'tapjoy_ads', ext: 'aar')
}
```

###### Only in China
The build.gradle is as follows：
```groovy
dependencies {
    //other ads-libs
    //gson-2.7.jar in folder named android_support_library
    compile(name: 'gson-2.7', ext: 'jar')
    compile(name: 'centrixlink_ads', ext: 'aar')

    compile(name: 'mobvista_ads', ext: 'aar')
    compile(name: 'vungle_ads', ext: 'aar')
    compile(name: 'chartboost_ads', ext: 'aar')
    
    compile(name: 'inmobi_ads', ext: 'aar')
    compile(name: 'oneway_ads', ext: 'aar')
    compile(name: 'playable_ads', ext: 'aar')
}
```
###### Global
Merge the above two files into one file.

### IV.Add Android Support library
Every affiliate needs `android.support.xxx`, so please import it to your project. If you are using Android Studio in your project, you can modify `build.gradle` file to add

Starting with the 3004 version of UPSDK, we recommend the 26.1.0 version of the Android support library (including v4 and v7) because of the upgrade of Admob and other networks. Of course, in special cases, it is also possible to use a lower one such as v25.3.1 of  Android support library.

#### 1.Import Android Support library
In the `build.gradle` , download the support libraries  from Google's remote repository via the compile command.Like this:

```groovy
dependencies { 
    //core lib
    compile(name: 'UPAdsSdk_Js_3.0.04_dex', ext: 'aar')
    //support libs
    compile 'com.android.support:recyclerview-v7:26.1.0'
    compile 'com.android.support:support-v4:26.1.0'
    compile 'com.android.support:appcompat-v7:26.1.0'
    compile 'com.android.support:support-annotations:26.1.0'
    compile  'com.android.support:customtabs:26.1.0'
    compile 'com.android.support:cardview-v7:26.1.0'
}

```
**【Attention】Android Support
 Support libraries must be imported into your project!**

### V.Add *.js files

#### 1.Add files in project

The UPSDK implements cross-platform calls to the native interface via the *js source file, so all *.js and *.h files in `js/upltv` must be copied to the current project.

1) Copy `upltv` to the `src` folder of the Layabox project, leaving only the `.js` file

2) Add the reference to `UPLTV.js`, `UPLTVIos.js` in index.html which in the bin folder of the Layabox project.


As following:
![](http://docc.upltv.com/uploads/201809/5b98f2c8af661_5b98f2c8.png)

### Ⅵ.Modify Proguard setting 
If your project used `proguard`.
You have to copy contents from `proguard-project.txt` to right location of your project.

### Ⅶ.Fix up 65535 limitation

If the number of methods exceeds 65535 due to access to the UPSDK and cannot be builded correctly, please use the `MultiDex` . If you have any questions about it, please read the [MultiDex Scheme](http://docs.upltv.com/docs/show/78 "Fix up 65535").
