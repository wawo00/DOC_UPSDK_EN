## Android Eclipse


### I.Structure of UPSDK LuaPlugin
For projects built with Eclipse, UPSDK is imported into the project as `*.jar`. Download UPSDK LuaPlugin in ( [Android-LuaSDK](http://doc.upltv.com/en/master/chapters/chapter09.html "download"))and unzip：


![ec-1-1](http://docc.upltv.com/uploads/201805/5afe9bd143673_5afe9bd1.png "ec-1-1")
- `Eclipse`
  This directory mainly contains the ad dependency library files required for Eclipse project access.
- `lua`文件夹
  This directory mainly contains some *.lua source files for bridging the current Cocos2d-X lua project with the UPSDK interface call.
- `Android Studio`
If you build project through,please ignore this directory.
- `proguard-project.txt`
  The configuration file of confusion,if you need to obfuscate code, add the contents of this file to the file that the project depends on.
  

### II.Import UPSDK main package
#### 1.Add files of UPSDK
Take UPSDK v3.0.03 as an example. In the `upsdk_ads` directory, there are three directories: `libs`, `res` and `assets`. Please copy the contents of the directory to the corresponding directory of your Eclipse main project ( If there is no libs directory, create a libs directory with the same level as src in the app folder).
> for non-*. so files, please be careful when the duplicate file appears when copying: ** can only be overridden when the duplicate file is the original file of AvidlyAdsSdk. ** when the file name conflict is not present in this case, you can resolve it at your own discretion based on experience (for example, the file in the res/values/ directory can be renamed), or you can find a solution directly to our technical feedback problem.

As follow：

![ec-2-1](http://docc.upltv.com/uploads/201805/5afe9cf8d18fd_5afe9cf8.png "ec-2-1")
> `UPAdsSdk_Lua_3.0.03.jar`just for reference

#### 2.Check minSdkVersion and targetSdkVersion in `Manifest`
UPSDK requires that minSdkVersion cannot be lower than 15, and targetSdkVersion cannot be higher than 26, so check it in the `build.gradle` file，as follows：
```groovy
 < uses-sdk android:minSdkVersion="16" android:targetSdkVersion="25" />
```
#### 3.Make sure *.so files are aligned
There are 3 types of .so files of the cpu type in folder name `libs`：
- armeabi
- armeabi-v7a
- x86

According to your needs, just delete the unwanted CPU architecture in the libs directory.

### III.Add ad networdks
#### 1.Add Google Ads SDK
Please refer to**Add files of UPSDK** to add Google Ads into your porject,as follows：：

![ec-3-1](http://docc.upltv.com/uploads/201805/5afea0b542f2f_5afea0b5.png "ec-3-1")
> In particular, if your project already has a different version of google play service, use the higher version.

#### 2.Add other networdks
To ensure you get more revenue, add as many ad libraries as possible to your project.
Folder named `optional_ads` contents  network dependencies file that exists in the form of `*.jar`. Please refer to **Add files of UPSDK** to add it to your project, and copy the contents of the AndroidManifest file to your project's Manifest file.

### IV.Add Android Support library
The display of the ad requires the support of the `support` library, so please bring it into your project. We have the corresponding `xxx.jar` file for you in the `android_support_library/libs` folder. You just need to added those files into the `libs` directory,as follows：

![ec-4-1](http://docc.upltv.com/uploads/201805/5afea104016ef_5afea104.png "ec-4-1")

### V.Modify AndroidManifest.xml file
Please duplicate the content of `AndroidManifest.xml` file into the related location in your project.

### Ⅵ.Modify.mk file

### 1、Modify the application.mk in the jni directory
Open the application.mk file under the current project jni directory and add the following information:
```groovy
APP_SHORT_COMMANDS := true
NDK_TOOLCHAIN_VERSION=4.9
APP_PLATFORM=android-14
```

### Ⅶ.Modify Proguard setting
If your project used `proguard`.
You have to copy contents from `proguard-project.txt` to right location of your project.

### Ⅷ.Demo Project
To help you integrate ads SDK easier and faster, here we provide you a simple [DemoProject]
(https://github.com/AvidlyGit/AdSdkDemo-Studio "Demo工程")。

