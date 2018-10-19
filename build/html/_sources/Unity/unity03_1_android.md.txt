## Access for Android

### I. Declaration
Android Platform, supports Unity 5.0.0 or higher version

### II. Checking Assets Catalog in Unity Project
When Unity plugin for Android finishes to be import, please check whether `PolyADSDK/Plugins/Android` exists under Assets catalog.

- 3.0.02 and lower plugin version
Soon after the successful import, there will be like as below in Assets catalog:
![import](http://docc.upltv.com/uploads/201804/5acc569aeb642_5acc569a.png "工程结构")

#### 1. `libs_res`
This directory includes `AvidlyAdsSdk_2.0.xx_dex.aar`, `support-v4-24.1.1.aar`, and `proguard-project.txt` files.
> 	The support-v4 library must be added. The version of V24.1.1 is the version recommended by the plug-in. If there are other higher-level v4 libraries in the project, you can directly replace the recommended version.

#### 2.`thirdlibs`
`thirdlibs/aar` is the directory used to reference some network library that does not support dynamic loading,such as: appcompat-v7-24.1.1.jar.

#### 3.`avidly_android`
This directory includes many third-party networdk that named like 'dex_xxx.jar' for dynamic loading at runtime.

- 3.0.03 (included) and higher plugin version
Soon after the successful import, there will be like as below in  `Assets` catalog:
![工程结构](http://docc.upltv.com/uploads/201805/5b026a7687a70_5b026a76.jpeg "55333")

In 3.0.03 and higher plugin version, in order to Simplify access steps,we remove`avidly_android` and change `AvidlyAdsSdk_x.x.xx_dex.aar` to `UPAdsSdk_3.0.xx_dex.aar`。

### III. Adaption for Unity specific version
1、 5.1.1, during compile-build-package, unity can not find error for armeabi structure-----it needs to remove armeabi structure in .arr(using unarchiver to open it and delete armeabi folder directly)；

2、5.0.0，during the apk packaging process, merge AndroidManifest.xml jurisdiction losses-----it needs to add AndroidManifest.xml into \Assets\Plugins\Android\
Download page:  [5.0.0 AndroidManifest Download Page](http://docs.upltv.com/docs/show/50 "SDKDownLoad")
> If you have not found any needed file, please contact our technical colleagues for supports.

### IV. Compile Error for Unity Project 
Regarding to the solution for Unity compile error, please refer to Android [Problem Resolution for Integration](http://docs.upltv.com/docs/show/105 "常见问题") for suggestion.

### V. Unity Android proguard configuration
Regarding to the projects with proguard configuration, please copy `proguard-project.txt` into your proguard file, to avoid importing the wrong package name which proguard which may caused programme crashes.

### VI. The Problems of Android overmuch-method for Unity Project 
AS Android has 65535-limitation issue, when projects import third-party *.jar or *.aar mothod overmuch and in the condition that subpackage can not work. Please delete those unnecessary third-party library, and apply the following suggestions until the probelms solved. 
- If your plugin version is lower than 2.0.24, please update it to the latest version. Because version 2.0.24 or higher ones acheive dex dymatc-loading modole for Android to avoid some aar imported by third-party library.
- If the problem is still unsolved, please try to delete aar files in `thirdlibs/aar/fb/`.
- If the prolem is still, please contact our technical colleagues for support. We will make further decision whether to delete arr in `thirdlibs/aar/china/` to reduce method.
