## Banner Ad

Banner ads are divided into top banner and bottom banner, and JavascriptPlugin further simplifies the implementation of banner ads, providing interfaces such as display, hide, remove, and event callbacks.
ht 
### 1.Callback of Banner
Banner ad needs to set up the show of banner ad, click and remove the callback interface of events. The callback interface is saved internally by the plug-in, so you don't need to set it up multiple times, only calling upltv.removeBannerAdAt(cpPlaceId) will be deleted.

```javascript
//callback of showing banner
    static bannerAdDidShow(callback:(cpPlaceId:string)=>void)
//callback of clicking banner
    static bannerAdDidClick(callback:(cpPlaceId:string)=>void)
//callback of removing
    static bannerAdDidRemove(callback:(cpPlaceId:string)=>void)
```

### 2.Show top banner ads
Show the banner at the top of the screen according to the ad unit.

```javascript
// @param cpPlaceId ad unit
    static showBannerAdAtTop(cpPlaceId:string)
```

**It should be noted that when the top Banner of the Iphonex phone is blocked by the status bar, it can be solved by adjusting the displacement of the top Banner.**
```javascript
/**
* On an Iphonex phone, when the top Banner is blocked by the status bar, you can solve this problem by adjusting the displacement of the top banner
* @param padding: The top Banner's offset value, such as 32, will shift down 32 pixels
* This feature is not supported on the Android platform
* supported from 3002
*/
static setTopBannerPading(padding)
```

### 3.Hide top banner ads
```javascript
// @param cpPlaceId ad unit
    static hideBannerAdAtTop()
```

### 4. Show bottom banner ads
```javascript
// @param cpPlaceId ad unit
    static showBannerAdAtBottom(cpPlaceId:string)
```

### 5. Hide bottom banner ads

```javascript
    static hideBannerAdAtBottom()
```

### 6.Remove banner ads
```javascript
// @param cpPlaceId ad unit
    static removeBannerAdAt(cpPlaceId:string)
```