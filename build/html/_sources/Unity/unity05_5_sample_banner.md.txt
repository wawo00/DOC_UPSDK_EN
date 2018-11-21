

## Unity Plugin Banner Ad

#### 1.Show Banner Ad

```csharp
/*
* Show banner ads in top of screen
* cpPlaceId is Ad ad unitentifier, make sure it correctly
*/
public static void showBannerAdAtTop(string cpPlaceId);

/*
* Show banner ads in bottom of screen
*/
public static void showBannerAdAtBottom(string cpPlaceId);
```


#### Sample：
```csharp
// Show a banner ads named 'banner_aaa' in top of screen
public void onBtnBanner_Top_Click()
{
    // Add support to iphonex （32 just for testing）
    UPSDK.setTopBannerForIphonex(32);
    // Add support to huaweiP20
    UPSDK.setTopBannerForHuaWeiP20(75);
    // show banner
    UPSDK.showBannerAdAtTop("banner_aaa");
}

// Show a banner ads named 'banner_aaa' in bottom of screen
public void onBtnBanner_Bottom_Click()
{
    UPSDK.showBannerAdAtBottom("banner_bbb");
}
```

> Banner ads do not need to determine the status, call it at the appropriate time, the SDK will automatically load, and automatically show the ad after the successful loading .
Although the Banner ad is automatically load and displayed, this method should be called as early as possible to get enough time to load ads.


#### 2.Hide Banner Ad
```csharp
// Hiding current top banner ads
public static void hideBannerAdAtTop();

// Hiding current bottom banner ads
public static void hideBannerAdAtBottom();
```
>  Banner can be displayed again by showBannerAdAtTop() or showBannerAdAtBottom() without reloading.


#### 3.Remove Banner Ad
```csharp
// Remove the Banner ad based on the palcementid and reload the ad when re-displaying.
public static void removeBannerAdAt(string cpPlaceId);
```

#### Sample:

```csharp
//  Remove banner ad named 'banner_aaa'
public void onBtnBanner_TopRemove_Click()
{
    UPSDK.removeBannerAdAt("banner_aaa");
}

```
#### 4.Adjust the position of top banner

```csharp
// only for iphonex
void setTopBannerForIphonex(int padding);
// only for huaweiP20
void setTopBannerForHuaWeiP20(int padding);
```
Sample:
```csharp
// Top Banne moves down 32 pixels
UPSDK.setTopBannerForIphonex (32);
```