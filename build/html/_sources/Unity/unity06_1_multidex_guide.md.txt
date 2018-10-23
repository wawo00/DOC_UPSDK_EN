## 65535 Limitation

When the number of methods exceeds the limit of 65535, the following failures occur when apk is generated:

![222](http://docc.upltv.com/uploads/201807/5b39ca2058b2a_5b39ca20.png "222")

> `trouble writing output: Too many method references to fit in one dex file: 67449; max is 65536.`

In order to solve this problem, Unity has supported Multidex since 5.5 and is solved by Dex subcontracting.

### 1. [Use Android Studio ](http://docs.upltv.com/docs/show/251 "Android Studio分包")
In the Android Studio project, it is possible to flexibly complete apk packaging via gradle, provided that Android Studio 2.2.3 or higher is required.

### 2. [Use UnityIDE ](http://docs.upltv.com/docs/show/252 "UnityIDE分包")
Simply copy the necessary files and initial settings to complete the subcontracting.