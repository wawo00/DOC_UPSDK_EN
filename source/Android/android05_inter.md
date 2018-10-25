## Interstitial Ad

### Ads Object Initial 

Use the following code to initialize Interstitial Ads
> You can set the parameter `Placement ID` to any significative name you want. If you're not sure, please discuss with our **support engineer**. You should use a different `Placement ID` for different ads placement. We provide revenue from each  `Placement ID` in the feature.
> Eg: You may use "Pause" or "Menu" when initializing our SDK in the pause scene of your game.

    mInterstitialAd = new UPInterstitialAd(this, "Placement ID");
    
### Load Callback
You can use interface `load` to check process of loading. This is optional. You can ignore it if there are no special requirements.
```java
public void load(UPInterstitialLoadCallback callback)
```
Sample codes:
```java
UPInterstitialAd mInterstitialAdAAA = new UPInterstitialAd(InterstitialActivity.this, "inter_aaa");
final UPInterstitialLoadCallback callback = new UPInterstitialLoadCallback() {
        @Override
        public void onLoadSuccessed(String placement) {
            Log.i(TAG, "InterstitialAd " + placement + " onLoadSuccessed:");

            if (placement.equals("inter_aaa")) {
                // load successed,could show 
            }
        }

        @Override
        public void onLoadFailed(String placement) {
            Log.i(TAG, "InterstitialAd " + placement + " onLoadFailed:");
            if (placement.equals("inter_aaa")) {
                // load failed
            }
        }
    };

// set callback
mInterstitialAdAAA.load(callback);
```
### Action Callback
You can use interface `setUPInterstitialAdListener` to setup callback functions. This is optional. You can ignore it if there are no special requirements.

    mInterstitialAd.setUPInterstitialAdListener(new UPInterstitialAdListener() {
        @Override
        public void onClicked() {
            // click callback
        }

        @Override
        public void onClosed() {
            // close callback
        }

        @Override
        public void onDisplayed() {
            // impression callback
        }
    });
    
    
    
### Show Interstitial Ads
Call `show` method to display ads whenever you want in your game.

**Note: Call `isReady` before `show` to make sure everything is ready**

    if (mInterstitialAd != null && mInterstitialAd.isReady()) {
        mInterstitialAd.show();
    }
### Debug Page
In order to make you understand the working and loading status for video ads easily, we provide you "Video Ads Debug
" page to help you know the working condition of video ads, you could adjust by using the following code:

    if (mInterstitialAd != null) {
        mInterstitialAd.showInterstitialDebugActivity(this);
    }

 The page looks like this. Columns (left to right):
- Affiliate name
- Is this Affiliate SDK integrated?
- Is this Affiliate opened by server side configuration?
- Did this Affiliate Ads successfully load?

You can play ads by clicking the item if the ads successfully loaded.

<img src="http://docc.upltv.com/uploads/201810/5bcd4065a93a4_5bcd4065.png">
<img src="http://docc.upltv.com/uploads/201810/5bcd408d13bcb_5bcd408d.png">