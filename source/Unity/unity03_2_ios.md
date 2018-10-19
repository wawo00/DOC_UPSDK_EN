## Access for IOS

### I、Declaration
When we tested with different versions among Unity 5.x, we found that only 5.1.0 and higher version could work stably on Mac. Thus, 5.1.0 or lower version could not finish adaption test. If the version of your project is lower than 5.1.0, we recommend you to update it to the latest version; If you have some difficult problems with updating, please try to import. Please contact us if you need any support from our technical colleagues.

### II、Inspect iOS Frameworks under Assets catalog in Unity project
When Unity plugin for iOS has been successfully  import, please check under Assets catalog:
Do `PolyADSDK/Plugins/IOS/frameworks` and `PolyADSDK/Plugins/IOS/resources` these two catalogs really exist. If not, it means plugin has not been successfully impor. 

After plugin for iOS has been successfully import, files will be like the structure below under Assets: 

![aaa](http://docc.upltv.com/uploads/201805/5af573a34f61b_5af573a3.png "aaa")


From the screenshot above which showing the structure, please check whether the following files exist: 
#### 1. UPSDK ADSDK Main Package
`PolyADSDK/Plugins/IOS/frameworks/UPSDKAdsSDK.framework` is the main package of UPSDK ADSDK. If this file is missing, please contact our relevant colleagues for supports.

#### 2. UPSDK ADSDK Dependency for Ad Networks 
Under `PolyADSDK/Plugins/IOS/frameworks` catalog, except UPSDK ADSDK main package, there must be series of dependency for Ad Networks. They exist in *.framework formation, like AdCoony.framework,UnityAds.framework; some exist *.a or *.h formation, like OneWaySDK,Domob-SDK. 

#### 3. UPSDK ADSDK Resource Package
`PolyADSDK/Plugins/IOS/resources` is the resource files which UPSDK ADSDK ads rely on, such as rewarded video ads UI interact some icon resources. If it is lack of resouces, it will lead operation unnormal or failure, and it may affect the monetization revenue.

#### 4. XUPorter
XUPorter is a open source. It is used for dynamically editing configuration parameter which export by Xcode. It contains adding dependency package and resource package.
If it is lack of this catalog, it will lead a unautomatically adaption. But you could export resources manually. More details will be mentioned in the following section.


### Xcode Configuration Inspection
When you failed to export Xcode in a project, please inspect all adaption configuration refering to the steps below:

#### 1. Deployent Target Settings
In Target->General panel, set Deployent Target 7.0 or higher. Some frameworks which the third-party rely on required 7.0 or higher.

Examples：
![ios-target](http://ads-sdk-doc.haloapps.com/uploads/201706/59535d81cf339_59535d81.png "ios-target")

#### 2. Link Binary with Libraries inspection
In Build Phases -> Link Binary with Libraries, inspect whether you have added framework and .a files which plugin contained.

After the successful addition, the library files marked in red box in the following screenshot, will be added.
![ios-lib](http://ads-sdk-doc.haloapps.com/uploads/201706/595361be1b87e_595361be.png "ios-lib")

If missing some library files in `PolyADSDK/Plugins/IOS/frameworks`, please manually add files which `PolyADSDK/Plugins/IOS/frameworks` contain in the project by using Xcode project. 

**Among them：
`libsqlite3.tbd`, `libxml2.tbd`, `libz.tbd`, `libstdc++.tbd`, `WebKit.framework` and `JavaScriptCore.framework` are system library, they must be added. Because some third-party Ad Networks depend on them. If they are missing, please add manually.**

#### 3. bundle resources inspection
In Build Phases -> Copy Bundle Resources, inspecting whether you add resources which plugin contained.

After the successful addition, resource files will be added. Please refer to the screenshot marked in red box.
![ios-resources](http://ads-sdk-doc.haloapps.com/uploads/201706/59536339b4e91_59536339.png "ios-resources")

If the resources which `PolyADSDK/Plugins/IOS/resources` should contain is missing, please manually add the resources of `PolyADSDK/Plugins/IOS/resources` in the project by Xcode project.

#### 4. Other Linker Flag Inspection
Following the steps: Build Settings -> Linking -> Other Linker Flags.
Please inspect whether add `-ObjC` and `-fobjc-arc` configuration.

After the successful additon, configuration parameters marked in red box in the following screenshot will be added. If they are missing, please add them manually.
![ios-link-set](http://ads-sdk-doc.haloapps.com/uploads/201706/59536443253fc_59536443.png "ios-link-set")

#### 5. Solution to Compatibility problems for some Unity versions

1、Regarding to versions from 5.4.2 to 5.4.0 , if failed to import Framwork(marked in red), please import code library and resource library under following catalog into the project manually:
`PolyADSDK/Plugins/IOS/frameworks`
 `PolyADSDK/Plugins/IOS/resources`
 
 2、 Regarding to il2cpp-config.h happened noreturn definited wrongly in 5.3.1 and some other versions, please refer to the following suggestions:
```cpp
 #define NORETURN __declspec(noreturn)
Replace 
#define NORETURN __attribute__((noreturn))
```
3、Regarding to **does not contain bitcode** error happened in 5.1.4 and other versions, please set NO for Enable Bitcode.

#### 6. Clean Project, Re-Compile
After finishing the inspections, please compile after Product->Clean !!!

If the errors still exist, please contact us for technical supports with the error evidence/information (including screenshots and log.