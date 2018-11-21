## API description 
### Use UPSDK Unity Plugin

```csharp
using Polymer.PolyADSDK ;
```

> API and callback interfaces (Actions) are defined as static methods, which can be accessed from other model directly.

### API reference

```csharp

		/*
		* Get Plugin version number 
		*/
		public static string getVersionOfPlugin();
		
		/*
		* Get the version number of supported platform for current plugin
		 Get iOS and Android versions currently supportted. Automaticly matched by complie environment at runtime
		public static string getVersionOfPlatform();
		*/
		public static string getVersionOfPlatform();

		/*
		* Initial  SDK
		* versions older than 2030, please use this method to initialize
		*/
		public static string initPolyAdSDK();
		 
		 /*
		* initalize Avidly SDK
		* @param zone:0, areas except China (CN)；1, China；2, judging the types of users automatically depending on ip
		* version 2030 and later versions, could use his method to initialize 
		*/
		public static string initPolyAdSDK(int zone);
		
		/*
		* initialize abtest configuration for upsdk ads
        * @param gameAccountId        accountid in game（required）
        * @param completeTask         complete the novice task in the game?
        * @param isPaid               Paying users?，0 means No
        * @param promotionChannelName Channel
        * @param gender               "M", "F"
        * @param age                  -1 means unknown
        * @param tags                 
		*/
		public static void initAbtConfigJson(string gameAccountId, bool completeTask, int isPaid, string promotionChannelName,  string gender, int age, string[] tags) ;
		
		/*
		* Get abtest configuration of upsdk ads
		* returned result could be Json character string, posiblity could be null
		* Before invoking this API, pl;ease invoke initAbtConfigJson() to finish the initialization for abtest configuration
		*/
		public static string getAbtConfig(string ad unit);
		
		/*
		 * Check if interstitial ad ready or not
		 */
		public static bool isInterstitialReady(string cpPlaceId);
		
		/*
		* Check if rewarded video ad ready or not
		*Please do not call this method continuously in your code, such as updating the state of the UI button. For this case, set the callback listener with setRewardVideoLoadCallback().
		*/
		public static bool isRewardReady();
		
		/*
		* Show Rewarded video ad, cpCustomId is CP defined identifier,it is required
		*/
		public static void showRewardAd(string cpCustomId);
		
		/*
		* Show interstitial ad
		* cpPlaceId is Ad ad unitentifier, make sure it correctly
		*/
		public static void showInterstitialAd(string cpPlaceId);
		
		/*
		* Show banner ads in top of screen
		* cpPlaceId is Ad ad unitentifier, make sure it correctly
		*/
		public static void showBannerAdAtTop(string cpPlaceId);
		
		/*
		* Show banner ads in bottom of screen
		*/
		public static void showBannerAdAtBottom(string cpPlaceId);
		
		/*
		 * Hiding current top banner ad
		 * No need to distinguish units of ad
		 * While next show is coming, you need to call showBannerAdAtTop()
		 */
		public static void hideBannerAdAtTop();
		
		/*
		 * Hiding current bottom banner ad
		 * No need to distinguish units of ad
		 * While next show is coming, you need to call showBannerAdAtBottom()
		 * Start to support from 2037
		 */
		public static void hideBannerAdAtBottom();
		
		/*
		* Delete a banner ad
		*/
		public static void removeBannerAdAt(string cpPlaceId);
		
		/*
		* Set Android manifest.xml defined packagename
		*/
		public static void setManifestPackageName(string packagename);
		
		/*
		* Show exit ad (only android)
		*/
		public static void onBackPressed();
	
		
		/*
		 * Adding callback API for loading rewarded video ads 
		 * @param success  callback of successful loading
		 * @param fail     callback of failed loading
		 * 
		 * Types of callback parameters: Action <string,string>
		 * The first one is cpPlaceId, ad unit of ads, could be empty or null; The second parameter is the decribed info, could be empty or null
		 * supported from 2028
		 */
		public static void setRewardVideoLoadCallback(Action <string,string> success, Action <string, string> fail);
		
		/*
		 * Adding callback API for loading Intersitial ads
		 * @param cpPlaceId:  the symbol of interstitial ads, could not be empty or null
		 * @param success  callback of successful loading
		 * @param fail t   callback of failed loading
		 * 
		 * Types of callback parameters: Action <string,string>
		 * The first one is cpPlaceId, ad unit of ads, could be empty or null: The second parameter is described info, could be empty or null
		 * supported from 2028
		 */
		public static void setIntersitialLoadCallback(string cpPlaceId, Action <string,string> success, Action <string, string> fail)
		
		/*
		 * It is using for showing reward video debug info 
		 * supported from 2028
		 */

		public static void showRewardDebugView();
		
		/*
		 * It is using for showing interstitial debug info 
		 * supported from 2028
		 */
		public static void showInterstitialDebugView();
        

         /**
         * Don't want to automatic loading ads when initializing sdk 
         * Required：When sdk disables the automatic loading of ads, and the background of upltv also turns off this fuction.
         * supported from 3002
         */
         public static void loadAvidlyAdsByManual() ;
         
         /**
         * Only for IphoneX, when the top Banner is blocked by the status bar, you can solve this problem by adjusting the offset value of the top Banner.
         * @param padding: The offset of the top Banner, such as 75, will be offset          downward by 75 pixels.
         * supported from 3002
         */
         public static void setTopBannerForIphonex(int padding);
         
         /**
          * Only for hawei P20, when the top Banner is blocked by the status bar, you can solve this problem by adjusting the offset value of the top Banner.
          * @param padding: The offset of the top Banner, such as 75, will be offset downward by 75 pixels.
          * supported from 3004
          */
          public void setTopBannerForHuaWeiP20(int padding);
         
         /**
         * pop up Dialog to ask authorizing
         * @param callback
         * Version 3003 and above support this method
         */
         public static void notifyAccessPrivacyInfoStatus(Action <UPConstant.         UPAccessPrivacyInfoStatusEnum, string> callback);
         
         /**
         * Conducting the GDPR authorization and notice the authorization results to UPSDK,which should be called before the initial UPSDK
         * @param enumValue
         * Version 3003 and above support this method
         */
         public static void updateAccessPrivacyInfoStatus(UPConstant.         UPAccessPrivacyInfoStatusEnum enumValue);
         
         /**
         * Get user authorization results, which should be called before the initial UPSDK
         * return UPConstant.UPAccessPrivacyInfoStatusEnum
         * Version 3003 and above support this method
         */
         public static UPConstant.UPAccessPrivacyInfoStatusEnum          getAccessPrivacyInfoStatus();
         
         /**
         * If the user belongs to the EU
         * Asynchronous callback, which should be called before the initial UPSDK
         * Version 3003 and above support this method
         */
         public static void isEuropeanUnionUser(Action <bool, string> callback);
         
```

### Specific Methods

#### 1、Supporting banner ads only
In the condition of using Unity plugin, **Supporting banner ads only**, and the location for showing is in **the top or bottom** of current interface

#### 2、**setManifestPackageName**(string packagename)

This API only works for Android. In AndroidManifest, if the package name of application is different from the pratical name after packaging, please use this API for SDK to set **AndroidManifest** correspinding **package name**!!!



