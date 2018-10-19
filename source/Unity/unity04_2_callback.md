
## PolyADSDK Callback interfaces


### 1. Callback interfaces for RewardVideo：
#### API reference

```csharp
public static Action <bool, string> UPSDKInitFinishedCallback = null;

/*
* Rewarded Video Ads
* trigger on ad open
*/
public static Action <string, string> UPRewardDidOpenCallback = null;

/*
* trigger on ad click
*/
public static Action <string, string> UPRewardDidClickCallback = null;

/*
* trigger on ad close
*/
public static Action <string, string> UPRewardDidCloseCallback = null;  

/*
* trigger on ad reward OK
*/
public static Action <string, string> UPRewardDidGivenCallback = null;

/*
* trigger on ad reward FAIL or not match reward conditions
*/
public static Action <string, string> UPRewardDidAbandonCallback = null;

```
### Sequence  of Callback interface  
#### 1. UPRewardDidOpenCallback
As long as the display of the RewardVideo is successful.
#### 2. UPRewardDidClickCallback
Called only when  user clicks  RewardVideo.
#### 3. UPRewardDidGivenCallback/UPRewardDidAbandonCallback
As long as the display is successful,there will generate rewards or not issue events based on the results. The UPRewardDidGivenCallback is called when the bonus is issued, UPRewardDidAbandonCallback  is called when the bonus is not issued, and only one of the two is invoked.
#### 4. UPRewardDidCloseCallback
The UPRewardDidCloseCallback is always called back when the RewardVidero  closed, and it is the callback that was last executed.
> To sum up：RewardDidOpen->RewardDidClick(if have)->RewardDidGiven(or RewardDidAbandon)->RewardDidClose.

### 2. Callback for Interstitial:
#### API reference

```csharp
/*
* Interstitial Ad 
* trigger on ad display 
*/
public static Action <string, string> UPInterstitialDidShowCallback = null;

/*
* trigger on ad click
*/
public static Action <string, string> UPInterstitialDidClickCallback = null;

/*
* trigger on ad close
*/
public static Action <string, string> UPInterstitialDidCloseCallback = null;

```

### Sequence  of Callback interface  
#### 1. UPInterstitialDidShowCallback
As long as the display of the Interstitial ad is successful.
#### 2. UPInterstitialDidClickCallback
Called only when  user clicks ad.
#### 3. UPInterstitialDidCloseCallback
The UPInterstitialDidCloseCallback is called back when the Interstitial ad  closed, and it is the callback that was last executed.
> To sum up：InterstitialDidShow->InterstitialDidClick(if have)->InterstitialDidClose.

### 3. Callback for Banner:

UPBannerDidShowCallback is only called when the banner is displayed at first time, UPBannerDidClickCallback is called each time when banner is clicked. UPBannerDidRemoveCallback is called when the banner ad is removed.
```csharp

/*
* Banner Ad
* trigger on ad display 
*/
public static Action <string, string> UPBannerDidShowCallback = null;

/*
* trigger on ad click
*/
public static Action <string, string> UPBannerDidClickCallback = null;

/*
* trigger on ad delete
*/
public static Action <string, string> UPBannerDidRemoveCallback = null;

