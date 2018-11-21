## Interstitial API
### 1. Set the interstitial load callback 
Load results (success or failure) to listen for the current interstitial ad .This interface is automatically released once a callback is made, and the callback interface needs to be reset when listening again.
```javascript
// Obtain result of loading
//@param loadsuccess  Motivate the callback when the video is //loaded loadsuccess(cpadid, msg)
//@param failCall    Motivate the callback when the video is //loaded failed，locadfail(cpadid, msg)
    static getInterstitialAdLoadResult(cpPlaceId:string,
                                       success:(cpPlaceId:string,message:string)=>void,
                                       failure:(cpPlaceId:string,message:string)=>void)
```

Sample：
```javascript
upltv.getInterstitialAdLoadResult("ilLoadCall",function(cpid:string,msg:string){
//success
},function(cpid:string,msg:string){
//failure
});
```

### 2.Callback of Interstitial Ad
Set up the callback interface for the display of interstitial ad which is used to listen to the callback of showing .The  interstitial ad shows that references to the callback interface are stored  and not released.

```javascript
//Callback of showing
    static interstitialAdDidShow(callback:(cpPlaceId:string)=>void)
//Callback of clicking
    static interstitialAdDidClick(callback:(cpPlaceId:string)=>void)
//Callback of Closing
    static interstitialAdDidClose(callback:(cpPlaceId:string)=>void)
```

### 3. Judge if the interstitial ad is ready
Judge if the interstitial ad is ready accroding ad unit, and  return Boolean results synchronously, true means that the AD is ready to be displayed, and false means that the AD is not show and still in the request.

```javascript
// @param cpPlaceId ad unit
// @param cpPlaceId callback,callback ,such as callback(true) or callback(false)
    static isInterstitialAdReady(cpPlaceId:string, callback:(ready:boolean)=>void)
```

### 4. Show interstitial AD
show a interstitial ad according to the ad ad unit.
```javascript
// @param cpPlaceId ad unit
    static showInterstitialAd(cpPlaceId:string)
```

### 5. Debug view of Interstital Ad 
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.
```javascript
// Open debug view
    static showInterstitialAdDebugUI()
```
