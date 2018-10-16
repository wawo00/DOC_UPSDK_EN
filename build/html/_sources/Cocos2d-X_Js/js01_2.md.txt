## Eclipse

### I.Structure of UPSDK CppPlugin 
For projects built with Eclipse, UPSDK is imported into the project as `*.jar`. Download UPSDK JavaScriptPlugin in ( [Android-JsSDK下载](http://ads-sdk-doc.haloapps.com/docs/show/13 "download"))and unzip：

![ec-1-1](http://docs.upltv.com/uploads/201805/5af3e73af0172_5af3e73a.png "ec-1-1")
- `Eclipse`
   This directory mainly contains the ad dependency library files required for Eclipse project access.
- `js`文件夹
	This directory mainly contains some *.js source files for bridging the current Cocos2d-X js project with the UPSDK interface call.
- `AndroidStudio`文件夹
    If you build project through,please ignore this directory.
- `proguard-project.txt`文件
	The configuration file of confusion,if you need to obfuscate code, add the contents of this file to the file that the project depends on.
	

### II.Import UPSDK main package

#### 1.Add files of UPSDK
Take UPSDK v3.0.03 as an example. In the `upsdk_ads` directory, there are three directories: `libs`, `res` and `assets`. Please copy the contents of the directory to the corresponding directory of your Eclipse main project ( If there is no libs directory, create a libs directory with the same level as src in the app folder).

As follows:

![ec-2-1](http://docs.upltv.com/uploads/201805/5af3e8f29e3c9_5af3e8f2.png "ec-2-1")

> `UPAdsSdk_Js_3.0.03.jar`just for reference

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

![ec-3-1](http://docs.upltv.com/uploads/201805/5af3ebc528686_5af3ebc5.png "ec-3-1")
> In particular, if your project already has a different version of google play service, use the higher version.


#### 2.Add other networdks
To ensure you get more revenue, add as many ad libraries as possible to your project.
Folder named `optional_ads` contents  network dependencies file that exists in the form of `*.jar`. Please refer to **Add files of UPSDK** to add it to your project, and copy the contents of the AndroidManifest file to your project's Manifest file.


### IV. Add Android Support library 

The display of the ad requires the support of the `support` library, so please bring it into your project. We have the corresponding `xxx.jar` file for you in the `android_support_library/libs` folder. You just need to added those files into the `libs` directory,as follows：
![ec-4-1](http://docs.upltv.com/uploads/201805/5af3e9c639e11_5af3e9c6.png "ec-4-1")

### V. Modify AndroidManifest.xml file
Please duplicate the content of `AndroidManifest.xml` file into the related location in your project.

### Ⅵ. Add *.js files

#### 1.Add files in project
The UPSDK implements cross-platform calls to the native interface via the *js source file, so all *.js files in `js/upltv` must be copied to the project.

For Cocos2d-x 3.16 version ,we can copy files  to assets/sr. If there are differences in other versions, please refer to the modification, as follows：
![ec-4-1](http://docs.upltv.com/uploads/201805/5af3ea86801bf_5af3ea86.png "ec-4-1")
>This article is based on cocos2dx-3.16. If your directory does not match this, ask our support team for help.

### 2.Modify android.mk in jni directory

Add following codes in application.mk file which located in jni folder.
```groovy
APP_SHORT_COMMANDS := true
NDK_TOOLCHAIN_VERSION=4.9
APP_PLATFORM=android-14
```

### Ⅶ.Modify Proguard setting 
If your project used `proguard`.
You have to copy contents from `proguard-project.txt` to right location of your project.

### Ⅷ.Demo Project
To help you integrate ads SDK easier and faster, here we provide you a simple [Demo Project ](https://github.com/AvidlyGit/AdSdkDemo-Studio "Demo工程")。
