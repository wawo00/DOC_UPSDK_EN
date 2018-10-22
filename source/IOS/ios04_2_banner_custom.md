## Customizing Banner Ad

UPSDK offers two banner advertisements, one based on the long bar of the *UPBannerStripWrapper* class and the other based on a rectangle of *UPBannerRectangleWrapper*. When using, please instantiate the Wrapper class of the ad according to the actual situation.

### Import .h file of banner

There are two header files of banner : UPBannerStripWrapper.h and UPBannerRectangleWrapper.h. The header file is introduced as follows:

```objective-c
#import    <UPSDK/UPSDK.h>
```

<br>

### Instantiate a Wrapper object

> You can set parameter `Placement ID` to any significative name you want. If you not sure about should discussed with our **support engineer**. You should use different `Placement ID` for different ads placement. We provide revenue from each  `Placement ID` in the feature.
> Eg: You may use "Pause" or "Menu" when initial our SDK in the pause scene of your game.


### Construction method：

The banner object constructed by this method can freely control the display position of the banner view.

```objective-c
/**
* 1. avidPlacement：NSString，placemntid, Required
* 2. vc:UIViewController，Used to control Banner click ,Required
*/
- (instancetype)initWithPlacement:(NSString *)avidPlacement controller:(UIViewController*)vc;
```

Sample:

In a ViewController.m, initialize a rectangular Banner object and set the callback proxy.

```objective-c
- (void)viewDidLoad {
	// …
	// Initialize wrapper
    _bottomRectBanner = [[UPBannerRectangleWrapper alloc] initWithPlacement:@"banner_rect_bottom” controller:self];
	// set callback
    _bottomRectBanner.delegate = self;
	// Initialize a UIView for displaying banner ads, size unknown
    _bannerRectView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 0, 0)];
    [self.view addSubview:_bannerRectView];
    // Get the UIView object of the ad and load it
    UIView *view = [_bottomRectBanner getView];
    [_bannerRectView addSubview:view];
	// …
}
```


<br>

### Callback of Banner Ad

UPBannerWrapperProtocol is the callback of Banner, which mainly contains two following  interface .

```objective-c
- (void)bannerAdClick:(id)wrapper;

- (void)bannerAdDidShow:(id)wrapper size:(CGSize)size;
```

Description：

1.  -(void)bannerAdClick:(id)wrapper
Used to monitor whether the banner is clicked. When the banner is clicked by the user, the wrapper will send a message to the interface.

2. -(void)bannerAdDidShow:(id)wrapper size:(CGSize)size;
When the banner can be displayed, the wrapper will send a message to this interface. The size of the parameter is the actual size of the currently displayed banner. The layout of the banner is usually adjusted through this interface.

Sample：
```objective-c
/**
 *  
 *
 *  @param wrapper ad onject
 */
- (void)bannerAdDidShow:(id)wrapper size:(CGSize)size{
    if (_bottomRectBanner == wrapper){
        CGRect frame = _bannerRectView.frame;
        frame.size = size;
        // Let _bannerRectView be central in the parent class
        frame.origin.x = (self.view.frame.size.width - frame.size.width)/2;
        frame.origin.y = self.view.frame.size.height - frame.size.height;
        _bannerRectView.frame = frame;
        // show _bannerRectView
        _bannerRectView.hidden = NO;
    }
}


/**
 *  Click ad
 *
 *  @param wrapper wrapper object
 */
- (void)bannerAdClick:(id)wrapper{
    // TODO
}
```

<br>

### Recycle memory：

Please set banner to nil for recyele when the ViewController where the banner view is located is destroyed (such as, removed in the interface, popped from nav, memory is recycled)

<br>

