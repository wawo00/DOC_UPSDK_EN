## Quick Banner Ad

### Scene of applying UPGameEasyBannerWrapper
If you only need to add banner ads on the top or bottom place in your project and the activity of the banner ads is the activity of your current project, we recommand you to follow the suggestions below to integrate in a quick and brief way.
Regarding to this situation, UPSDK will package the following objects further:
`com.up.ads.wrapper.banner.UPGameEasyBannerWrapper`

### Introduction of UPGameEasyBannerWrapper API interface
  UPGameEasyBannerWrapper is designed in single-row pattern, please use `UPGameEasyBannerWrapper.getInstance().XXXX()` method to call the api interface as followed.

```java
   /**
   * Please adopt this method correctly in priority, to finish the initialization for game banner
   * @param gameActivity can not be empty, the activity which current banner ads depend on
   */
   public void initGameBannerWithActivity(Activity gameActivity);

   /**
   * Depending on the placement of ads, display the banner on the top of current activity
   * Please adopt this method after actvity onresume, to avoid BadTokenException: Unable to add window -- token null is not valid;
   * @param cpPlaceId banner ad placement is normally used for marking business types of some ads
   */
    public void showTopBannerAtADPlaceId(String cpPlaceId);

   /**
   * Depending on the placement of ads, placing the banner in the bottom of current activity
   * Please adopt this method after onresume to avoid BadTokenException: Unable to add window -- token null is not valid;
   * @param cpPlaceId banner ad placement is normally used for marking business types of some ads
   */
   public void showBottomBannerAtADPlaceId(String cpPlaceId);

   /**
   * Depending on the placement of ads, adding callback agent for banner
   * @param cpPlaceId banner ad placement, is normally used for marking business types of some ads
   * @param callback banner callback
   */
   public void addBannerCallbackAtADPlaceId(String cpPlaceId, UPBannerAdListener callback);

   /**
   * Depending on the placement of ads, remove the banner ad without deleting relevant callback
   * If the ad placement does not exist, it will not lead any actual operation for the misson   
   * Once the banner ad has been removed, it will load again while next show is coming.
   * If the current banner ad is hidden only, please call hideTopBanner() or hideBottomBanner()
   * @param cpPlaceId banner ad placement, is normally used for marking business types of some ads
   */
   public void removeGameBannerAtADPlaceId(String cpPlaceId);

   /**
   * Hiding current top banner ad
   * No need to distinguish placements of banner
   * While next show is coming, you need to call showBottomBannerAtADPlaceId()
   * Start to support from 2037
   */
    public void hideBottomBanner();

   /**
   * Hiding current bottom banner ad
   * No need to distinguish placements of banner
   * While next show is coming, you need to call showTopBannerAtADPlaceId()
   * Start to support from 2037
   */
    public void hideBottomBanner();
```

### Direction for using UPGameEasyBannerWrapper 

The content below is a simple way to build a banner in the bottom of current activity

```java

protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_banner);
        // Initialize banner
        UPGameEasyBannerWrapper.getInstance().initGameBannerWithActivity(this);
        // Add callback interface
        UPGameEasyBannerWrapper.getInstance().addBannerCallbackAtADPlaceId("banner_aaa", new UPBannerAdListener() {
            @Override
            public void onClicked() {
                Log.i(TAG, "banner_aaa onClicked ");
            }

            @Override
            public void onDisplayed() {
                Log.i(TAG, "banner_aaa onDisplayed ");
            }
        });
        // Time delays for 0.2 second and the banner will be shown, demo can only guarantee to call showBottomBannerAtADPlaceId() after activity onresume
        (new Handler(Looper.getMainLooper())).postDelayed(new Runnable() {
            @Override
            public void run() {
                UPGameEasyBannerWrapper.getInstance().showBottomBannerAtADPlaceId("banner_aaa");
            }
        }, 200);
}
```