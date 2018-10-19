
## Eclipse

### I.Structure of UPSDK CppPlugin 
For projects built with Eclipse, UPSDK is imported into the project as `*.jar`. Download UPSDK CppPlugin in ( [Android-CPPSDK下载](http://ads-sdk-doc.haloapps.com/docs/show/13 "download"))and unzip：

![ec-1-1](http://docc.upltv.com/uploads/201805/5afd3722e5ab6_5afd3722.png "ec-1-1")


- `Eclipse`
   This directory mainly contains the ad dependency library files required for Eclipse project access.
- `cpp` 
   This directory mainly contains some *.cpp source files for bridging the current Cocos2d-X cpp project with the UPSDK interface call.
- `Android Studio`
   If you build project through,please ignore this directory.
- `proguard-project.txt`
   The configuration file of confusion,if you need to obfuscate code, add the contents of this file to the file that the project depends on.
  

### II.Import UPSDK main package
#### 1.Add files of UPSDK
Take UPSDK v3.0.03 as an example. In the `upsdk_ads` directory, there are three directories: `libs`, `res` and `assets`. Please copy the contents of the directory to the corresponding directory of your Eclipse main project ( If there is no libs directory, create a libs directory with the same level as src in the app folder).

As follows：

![ec-2-1](http://docc.upltv.com/uploads/201805/5afd39e93c234_5afd39e9.png "ec-2-1")
> `UPAdsSdk_Cpp_3.0.03.jar`just for reference

#### 2.Check minSdkVersion and targetSdkVersion in `Manifest`
UPSDK requires that minSdkVersion cannot be lower than 15, and targetSdkVersion cannot be higher than 26, so check it in the `build.gradle` file，as follows：
```groovy
 < uses-sdk android:minSdkVersion="16" android:targetSdkVersion="24" />
```
#### 3.Make sure *.so files are aligned
There are 3 types of .so files of the cpu type in folder name `libs`：
- armeabi
- armeabi-v7a
- x86

According to your needs, just delete the unwanted CPU architecture in the libs directory.

### III.Add ad networdks
#### 1.Add Google Ads SDK
Please refer to**Add files of UPSDK** to add Google Ads into your porject,as follows：

![ec-3-1](http://docc.upltv.com/uploads/201805/5afd45a3b7d61_5afd45a3.png "ec-3-1")
> In particular, if your project already has a different version of google play service, use the higher version.

#### 2.Add other networdks

To ensure you get more revenue, add as many ad libraries as possible to your project.
Folder named `optional_ads` contents  network dependencies file that exists in the form of `*.jar`. Please refer to **Add files of UPSDK** to add it to your project, and copy the contents of the AndroidManifest file to your project's Manifest file.


### IV. Add Android Support library 
The display of the ad requires the support of the `support` library, so please bring it into your project. We have the corresponding `xxx.jar` file for you in the `android_support_library/libs` folder. You just need to added those files into the `libs` directory,as follows：
![ec-4-1](http://docc.upltv.com/uploads/201805/5afd4483c57c1_5afd4483.png "ec-4-1")


### V. Modify AndroidManifest.xml file
Please duplicate the content of `AndroidManifest.xml` file into the related location in your project.


### Ⅵ. Add *.cpp files

#### 1.Add files in project
The UPSDK implements cross-platform calls to the native interface via the *cpp source file, so all *.cpp and *.h files in `cpp/upltv` must be copied to the current project.


Cocos2d-x 3.16 version can be copied to the Classes folder. If there are differences in other versions, please refer to the modification. The effect is as follows：

![classes](http://docc.upltv.com/uploads/201804/5acac9170fddc_5acac917.png "classes")
>This article is based on cocos2dx-3.16. If your directory does not match this, ask our support team for help.

### 2.Modify android.mk in jni directory
Open the android.mk file which in the jni directory of project.
Please copy **UpltvAndroid.cpp，CocosUpLtv.cpp，UpltvBridge.cpp** those files into **LOCAL_SRC_FILES**。
Take Cocos2d-X 3.16 as an example. The addition method is as follows. For other versions, please modify the relative path.:

```groovy
LOCAL_SRC_FILES := hellocpp/main.cpp \
                   ../../Classes/AppDelegate.cpp \
                   ../../Classes/upltv/UpltvAndroid.cpp \
                   ../../Classes/upltv/CocosUpLtv.cpp \
                   ../../Classes/upltv/UpltvBridge.cpp \
                   ../../Classes/HelloWorldScene.cpp
```

### Ⅶ.Modify Proguard setting 
If your project used `proguard`.
You have to copy contents from `proguard-project.txt` to right location of your project.


### Ⅷ.Demo Project
To help you integrate ads SDK easier and faster, here we provide you a simple [Demo Project ](https://github.com/AvidlyGit/AdSdkDemo-Studio "Demo project")。
