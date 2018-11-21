

## Unity Plugin Ad Show

#### Show Intersitial Ad
```csharp
public static void showIntersitialAd(string cpPlaceId);
```
> parameters：ccpPlaceId is Ad ad unit, make sure it correctly

> This method will query whether the corresponding ad exists according to the cpPlaceId, and if exists, further determines whether ad is ready. Intersitial Ad will only be displayed if both are true. In other words, showIntersitialAd() will call the isInterstitialReady() 

#### Detect Interstitial Ad status
In general, the showIntersitialAd() method can be called directly to display the advertisement. If you want to control whether a button is displayed based on the state of the Interstitial ad, you can do this use this method.

    public static bool isInterstitialReady(string cpPlaceId)

#### Sample
“**inter_bbb**” and “**inter_ccc**” are two ad unit of Interstitial ad.

```csharp
public void onBtnIntertitialClick() 
{ 
    if (UPSDK.isInterstitialReady("inter_bbb")) {
        UPSDK.showIntersitialAd("inter_bbb");
    }
}

public void onBtnIntertitial_CCC_Click()
{
    if (UPSDK.isInterstitialReady("inter_ccc")) {
        UPSDK.showIntersitialAd("inter_ccc");
    }
}
```


#### Show RewardVideo Ad

```csharp
public static void showRewardAd(string cpCustomId)
```
parameter：cpCustomId means an User-defined identifier
It is also checks if the video ad is ready when calling showRewardAd

#### Detect RewardVideo Ad status

In general, the showRewardAd() method can be called to display the RewardVideo Ad. This method is similar to isInterstitialReady() and is also provided to meet special requirements.

```csharp
public static bool isRewardReady()
```

#### Sample:
```csharp
public void onBtnReward_aaa_Click()
{
    if (UPSDK.isRewardReady()) {
         UPSDK.showRewardAd("aaa");
    }
}
```

>The parameter "aaa" is a user-defined identifier ,it will be used for statistics.