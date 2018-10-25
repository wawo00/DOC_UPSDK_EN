## Eclipse

### I. Structure of UPSDK Directory
If you are using Eclipse or Ant to build Android project, it will be more complex than using Android Studio to build. The structure of UPSDK Eclipse version is like following when after unarchive:

![](http://docc.upltv.com/uploads/201808/5b8756d508084_5b8756d5.png)


Main package of UPSDK Eclipse is located in `upsdk_ads` folder, please refer to the screenshot, `upsdk_ads` is the main package of Eclipse project, it must be added into your porject.

### II. Duplicate main package of UPSDK Eclipse into your project
In the directory of `upsdk_ads`, there are `libs` and `res`, and other folders. Please duplicate all content to
these folder into equivalent folders of your Eclipse project.

> Regarding to the files are not *.so, when you find repeated names of files after duplication, please carefully operate: **Only operate to cover the repeated names of files which are the original files of UpAdsSdk.** If the conflicts of duplication of names is not as above, please refer to your experience to handle(for example, files under res/values/ directories can be re-named). Of course, you could turn to our technical team for resolution and supports.

### III. Add other dependencies
The SDKs of some affiliate networks need to depend on some public third-party libraries, so you may need to include them in your project manually. These library files are existing as  `xxx_ads`folders among the folders you downloaded.
The relationships between UPSDK and other networks are loose and coupled. If you do not want to import some affiliate networks, you do not need to import those files.

`batmobi_ads` as the sample, if your project needs filled with Mobvista ads, please duplicate related files under the directories of `batmobi_ads/libs/` and `batmobi_ads/res/` into the directories of `libs` and `res` in your project,plus,add content of `AndroidManifest_Inmobi`  into  `manifest.xml` which in your project.

**Please make sure to follow the suggestions below to import 3rd-party libraries which UPSDK needs to depend on in your project. Or the system may crash due to lacking of some neccessary supports.**

#### IV. Add Android Support library 

The display of the ad requires the support of the `support` library, so please bring it into your project. We have the corresponding `xxx.jar` file for you in the `android_support_library/libs` folder. You just need to added those files into the `libs` directory.

**Android Support library is a forced dependency，please include it into your project ,or the game might crash !**

#### V. Add Google Ads SDK
If your project will be published globally, we suggest you to inlude Google Ads supports. We have provided related `play-services-xxx.jar` files in the directory of `admob_xxx/libs`.

At the same time, please check whether your AndroidManifest.xml includes the definitions below:

	<!-- admob -->
	<meta-data	
		android:name="com.google.android.gms.version"
		android:value="@integer/google_play_services_version"/>

	<activity
		android:name="com.google.android.gms.ads.AdActivity"
		android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize"
		android:multiprocess="true"
		android:theme="@android:style/Theme.Translucent"/>
	<!-- admob -->


### VI. Modify AndroidManifest.xml file
Please duplicate the content of `AndroidManifest.xml` file into the related location in your project.

### VII. Modify Proguard setting 
If your project used `proguard`.
You have to copy contents from `proguard-project.txt` to right location of your project.

### VIII. Demo Project
To help you integrate ads SDK easier and faster, here we provide you a simple[Demo Project](https://github.com/AvidlyGit/AdSdkDemo-Eclipse "Demo").
