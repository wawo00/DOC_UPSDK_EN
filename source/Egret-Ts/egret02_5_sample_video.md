## Reward video Ad

### 1. Load callback of Reward video
This API is used to listen for the loading results of the current excited video. Once this interface is called back, the internal will be automatically released, and the callback interface needs to be reset when listening again.

```javascript
// Obtain result of loading
//@param loadsuccess  Motivate the callback when the video is //loaded loadsuccess(cpadid, msg)
//@param failCall    Motivate the callback when the video is //loaded failed，locadfail(cpadid, msg)
    static getRewardAdLoadResult(success:(cpPlaceId:string,message:string)=>void,failure:(cpPlaceId:string,message:string)=>void)
```

Sample: 
```javascript
upltv.getRewardAdLoadResult(function(cpid:string,msg:string){
//success
},function(cpid:string, msg:string){
//failure
});
```

### 2. Show callback of Reward video Ad
     Set up the callback interface of video show to listen to the callback of the event (click, close, reward, etc.) of the video advertisement. Reward video shows that the reference to the callback interface is stored internally and not released, so you only need to set it once.
```javascript
// Callback of showing
// @param cpPlaceId placementid
    static rewardAdDidOpen(callback:(cpPlaceId:string)=>void)

// Callback of clicking
// @param cpPlaceId placementid
    static rewardAdDidClick(callback:(cpPlaceId:string)=>void)

// Callback of closing
// @param cpPlaceId placementid
    static rewardAdDidClose(callback:(cpPlaceId:string)=>void)

// Callback of sending reward successfully
// @param cpPlaceId placementid
    static rewardAdDidGiven(callback:(cpPlaceId:string)=>void)

// Callback of failing to send reward 
// @param cpPlaceId placementid
    static rewardAdDidAbandon(callback:(cpPlaceId:string)=>void)
```

#### 3. Judge if the Reward Video ad is ready
Synchronously return Boolean results, true means that the AD is ready to be displayed, and false indicates that the AD is not show and still  in the request
```javascript
// Usually call this method before showRewardVideo(cpPlaceId)
    static isRewardAdReady(callback:(ready:boolean)=>void)
```

#### 4. Show Reward Video Ad 
When show the Reward Video ad, you need to upload a cpPlaceId, which is the placementid , used for business management, in order to distinguish the source of revenue.

```javascript
// @param cpPlaceId placementid
    static showRewardAd(cpPlaceId:string)
```

#### 5. Debug view of Reward Video Ad
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.

```javascript
showRewardDebugUI : function()
```