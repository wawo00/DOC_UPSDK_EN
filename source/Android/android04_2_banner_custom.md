## Customizing Banner Ad
### Ad Object Initialization 
Two banner layouts are supported, "Full Banner" and "Square". Please choose the right style for your product.

> You can set the parameter `Placement ID` to any significative name you want. If you're not sure, please discuss with our **support engineer**. You should use a different `Placement ID` for different ads placement. We provide revenue from each  `Placement ID` in the feature.
> Eg: You may use "Pause" or "Menu" when initializing our SDK in the pause scene of your game.

For "Full Banner", use the following code to initialize ads object.

    mBannerAd = new UPBannerAd(this, "Your Placement ID");

For "Square", use the following code to initialize.

    mRectangleAd = new UPRectangleAd(this, "Your Placement ID");

### Show Banner Ads
Imagine we are trying to show a "Full Banner" ad. First, you should add the parent view of ads in your layout file, like this.

    <LinearLayout
        android:id="@+id/banner_container"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"/>

Then, you can call `getBannerView()` to get the ad view and add it to parent view. It will display once the ads have been successfully loaded.

    banner_container = (LinearLayout) findViewById(R.id.banner_container);
    banner_container.addView(mBannerAd.getBannerView());

### Callback
You can use interface `setUPBannerAdListener` to setup callback function. This is optional. You can ignore it if there are no any special requirements.

    mBannerAd.setUPBannerAdListener(new UPBannerAdListener() {
        @Override
        public void onClicked() {
            // click callback
        }

        @Override
        public void onDisplayed() {
            // impression callback
        }
    });
