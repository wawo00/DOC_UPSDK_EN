## Use Android Studio

Unity 5.5 starts to support the Gradle build system. For the 65535 excess error, you can export the project to AndroidStudio,and solve this problem by gradle.


### 1.Import project to AndroidStudio

![3333](http://docs.upltv.com/uploads/201807/5b39cc6bd83bb_5b39cc6b.png "3333")


### 2.Open AndroidStudio
AndroidStudio 2.2.3 or above must be installed.

![4444](http://docs.upltv.com/uploads/201807/5b39ccc80a994_5b39ccc8.png "4444")

### 3.Configure build.gradle
AndroidStudio 2.2.3 or above must be installed.
![555](http://docs.upltv.com/uploads/201807/5b39cd2136c17_5b39cd21.png "555")

Add the subcontract settings in the build.gradle file:：

```groovy
android {
    defaultConfig {
        ...
        minSdkVersion 16 
        targetSdkVersion 26
        multiDexEnabled true
    }
    ...
}
dependencies {
  compile 'com.android.support:multidex:1.0.1'
}
```

edit **AndroidManifest.xml **：
```groovy
 <application
            android:name="android.support.multidex.MultiDexApplication" >
        ...
 </application>
```

### 4.Fix OutOfMemory
Add the following configuration to solve OutOfMemory problem in gradle.build when run the project.
 
```groovy
android {
    defaultConfig {
        ....
    }
    dexOptions {
        javaMaxHeapSize "4g"
    }
}
```

### 5. Modify Proguard setting
When the `Build-in class shrinker and multidex are not supported yet`error message appears in AndroidStudio, most of the cases are caused by the useProguard field. Try using useProguard instead of minifyEnabled.

```groovy
android {
    buildTypes {
        release {
            minifyEnabled true
        }
    }
}
```
>If you do not need to confuse，just remove settting of minifyEnabled or set it as false.