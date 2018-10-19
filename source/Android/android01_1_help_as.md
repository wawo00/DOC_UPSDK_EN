## Android Studio

Regarding to the supports for Studio, this article will explain in four sections as following.

### I. Structure of UPSDK Directory
Regarding to Android Studio or Gradle built project, UPSDK suggests it should be import by other main project in `*.aar` format. You will see the structure of directory for UPSDK Studio when you unzip it:

![as_91](http://docs.upltv.com/uploads/201808/5b7fdca87b9ae_5b7fdca8.png "as_91")

#### 1. Main Package of UPSDK
Please refer to the screenshot above, the file named `UPAdsSdk_x.x.xx.aar` is the main package of UPSDK, you have to add it into your main project.

#### 2. Networks Dependencies of UPSDK
The relationships between UPSDK and other networks are loose and coupled. You could remove some ads dependencies from the main project to reduce the size of application.

The dependencies of networks except Admob and Facebook, they are existing in xxxx_ads.aar format.

#### 3. Ads Dependencies of Admob and Facebook
Among UPSDK local files, it provides aar dependencies for Admob and Facebook in case of the situation of bad internet or other unexpected problems happened. Even so, we still suggest you to update the dependencies online from gradle of Admob and Facebook long-distance warehouse.
    > Regarding to the specification of how to integrate with Admob and Facebook, it will be particularly introduced later in this section.

### II. Using Gradle of Android Studio to import the main package of UPSDK

Please refer to the introduction above, add the downloaded files which named  `UPAdsSdk_x.x.xx.aar` into `libs` directory in your project.
After they are added, the effects of Studio project acts like the following screenshot:

![as_02](http://docs.upltv.com/uploads/201808/5b7fddd4a0a05_5b7fddd4.png "as_02")

> `UPAdsSdk_3.0.03.aar` is specified only for example

To make sure aar package which in libs directory could be import correctly by the project, please check the following configuration parameter in `build.gradle` files/folder under `app` directory:

    repositories {
        flatDir {
            dirs 'libs'
        }
    }

At last, please add aar into compile method

    dependencies {
    // your other setting
    // Please replace UPAdsSdk_3.0.03 with the real file name
     compile(name: 'UPAdsSdk_3.0.03', ext: 'aar')
    }

So far, aar package of UPSDK has been successfully configurated in your project. Please wait gradle compile works. But the work of importing UPSDK has not been finished yet, the final step is very significant to do: **add other dependencies**.

> As an excellent and powerful mediation platform, UP SDSDK can be flexibly compatible with the runtime library of third-party affiliate networks. So that it can help you yield the greatest returns. As a conclusion, if you want UPSDK to yield the greatest returns, please add the third-party dependencies correctly.

If you are using Gradle of Android Studio to build your project. First of all, you have to import all files like `UPAdsSdk_x.x.xx.aar` from `for_studio` directory to you project.
Each `xxx_ads.aar` file in directory means a affiliate network which supported by us. 
Since we always choose the best affiliate networks over the world, you can import all of them into your project without any hesitation.
Also, you still can remove some of them by your own reason , like too much library will make your game size getting big.

### III. Add dependencies of affiliate networks

The SDKs of some affiliate networks need to depend on some public third-party libraries. The project which is built by Android Studio could import the dependent third-party library by the following mothods.

**In principle, we suggest you to import dependent third-party library all in your project. But in some cases, you can choose to add some libraries of affiliate networks to reduce the size of your project. But no matter how to make sure the libraries of affiliate networks you added must completely meet the external conditions of current ads on shown. Or, it will leads crashes because it's lack of some neccessary supports.**

If you want to remove the supports from some affiliate networks, but you do not know how to operate. Please give priority to contact our support team to acheive your goal.

#### 1. Add *.aar of affiliate networks
Among the downloaded target files, files named  `xxx_ads.aar` are the dependent files for the affiliate networks in use. Please refer to **Import UPSDK aar files** to add them in your project.

#### 2. Add other external dependencies
Because of requiring some extra Android Api supports by some affiliate networks, so you have to add external dependencies as followed.

#### 1. Configure jcenter code repository
Find `build.gradle` file in your main project. Add `jcenter`  in `repositories` section of the file.

```groovy
buildscript {
    repositories {
        mavenCentral();
        // ******** add jcenter ********
        jcenter()
        maven {
            url 'https://maven.google.com/'
            name 'Google'
        }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.1.3'
    }
}

allprojects {
    repositories {
        jcenter()
        maven {
            url 'https://maven.google.com/'
            name 'Google'
        }
    }
}
```

#### 2.  Add Android Support library 
Every affiliate needs `android.support.xxx`, so please import it to your project. If you are using Android Studio in your project, you can modify `build.gradle` file to add
```groovy
dependencies {
    compile 'com.android.support:recyclerview-v7:26.1.0'
    compile 'com.android.support:support-v4:26.1.0'
    compile 'com.android.support:appcompat-v7:26.1.0'
    compile 'com.android.support:support-annotations:26.1.0'
    compile  'com.android.support:customtabs:26.1.0'
    compile 'com.android.support:cardview-v7:26.1.0'
    //gson-2.7.jar in android_support_library folder
    compile(name: 'gson-2.7', ext: 'jar')
}
```

#### 3. Add Google Ads SDK
If you want to add Admob ads in your project, you need to add Google Ads support in your project. You can follow the following steps to add dependencies:
```groovy
    dependencies {
        compile 'com.google.android.gms:play-services-ads:15.0.1'
    }

```
> If you only want to add aar files which gms play depends on locally. You could ignore this configuration in gradle file.
> Specially, if the version of gms play-service in your project is different from UPSDK dependencies, please use the higher version. 

#### 4. Add Facebook Ads SDK
If you want to add Facebook interstitial ads in your project, you need to add Facebook Ads support in your project. You can follow the following steps to add dependencies:

    dependencies {
        compile 'com.facebook.android:audience-network-sdk:4.99.1'
    }
    



### IV. Modify Proguard setting 
If your project used `proguard`.
You have to copy contents from `proguard-project.txt` to right location of your project.

### V. Demo Project
To help you integrate ads SDK easier and faster, here we provide you a simple [Demo Project](https://github.com/UPGit/AdSdkDemo-Studio "Demo")。