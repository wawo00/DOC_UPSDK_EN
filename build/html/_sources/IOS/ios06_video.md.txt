## Rewarded Video Ad  

All Rewarded video interfaces and protocol were defined in file `UPRewardWrapper.h`

Add header file `UPRewardWrapper.h` in your XCode project:
```objective-c
#import    <UPSDK/UPSDK.h>
```

The only difference between Rewarded Video and Interstitial Ad was **"Rewarded Video was using Singleton design model"**.
But their interfaces and methods are looks very similar.

*UPRewardWrapper.h* methods：

    @interface UPRewardWrapper : NSObject
    
    /*
     * Get Singleton object of Wrapper
     */
    + (instancetype)shareInstance;
    
    /*
     * Setup callback delegate (optional)
     */
    - (void)setDelegate:(id<UPRewardDelegate>)delegate;
    
    /*
     * Check if video was reay to show or not
     */
    - (BOOL)isReady;
    
    /**
     * Show video
     * @param viewController, used for redireaction, must be correctly set
     * @param adid, Ad Placement ID, used for tracking and analysis, you can customize it yourself 
     **/
    
    - (BOOL)show:(UIViewController *)viewController placeId:(NSString*)adId;
    /**
    * callback of loading ads
    * @param delegate,delegate of callback
    **/
    - (void)load:(id<UPRewardLoadDelegate>)delegate;
    @end

As what Interstitial Ad and Banner Ad did, Rewarded video Ads also defined callback delegate protocol. `UPRewardDelegate` was also declared in `UPRewardWrapper.h`.

```objective-c
@protocol UPRewardDelegate <NSObject>

/*
 * Rewarded Video Open
 */
- (void)UPRewardVideoAdDidOpen;

/*
 * Rewarded Video Click
 */
- (void)UPRewardVideoAdDidCilck;

/*
 * Rewarded Video Close
 */
- (void)UPRewardVideoAdDidClose;

/*
 * Ready to reward
 * @param reward: data for reward
 */
- (void)UPRewardVideoAdDidRewardUserWithReward:(NSDictionary *)reward;

/*
 * Fail to meet the condition, no reward
 * @param error: detail reasons
 */
- (void)UPRewardVideoAdDontReward:(NSError *)error;

@end
```

### Code example

Define a class `STRewardViewController` to test rewarded video
> Only for XCode project 
    
    @interface STRewardViewController : UIViewController
    
    @end

>  Add a button to `STRewardViewController`, show rewarded video when clicked. So, it's that simple.

Add following codes in file `STRewardViewController.m`.

```objective-c

#import    <UPSDK/UPSDK.h>

@interface STRewardViewController () <UPRewardDelegate>

@end
```

> `STRewardViewController` will implement protocol `UPRewardDelegate`, to monitor video events happened.

Continue add following code,

```objective-c
- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    UIButton *button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
    button.backgroundColor = [UIColor orangeColor];
    button.frame = CGRectMake(self.view.frame.size.width/2 - 250/2, 100, 250, 40);
    [button setTitle:@"Reward Video" forState:UIControlStateNormal];
    [button addTarget:self action:@selector(rewardClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
    
    [[UPRewardWrapper shareInstance] setDelegate:self];
}

- (void)rewardClick
{
    if ([[UPRewardWrapper shareInstance] isReady]) {
        [[UPRewardWrapper shareInstance] show:self placeId:@"aaaa"];
    }
    else
    {
        NSLog(@"Reward no ready");
    }
}

```

Now, you've finished main testing code of rewarded video. Click "Rewarded Video" button after run this project. You will see video ads.
If you see a tips "Reward not ready", that means video ads was not ready to play, please check your network status.

At last, add code for video delegate protocol.

```objective-c
#pragma mark - UPRewardDelegate
//Ad Show
- (void)UPRewardVideoAdDidOpen
{
    NSLog(@"UPRewardVideoAdDidOpen");
}

//Ad click
- (void)UPRewardVideoAdDidCilck
{
    NSLog(@"UPRewardVideoAdDidCilck");
}

//Ad Close
- (void)UPRewardVideoAdDidClose
{
    NSLog(@"UPRewardVideoAdDidClose");
}

//Reward
- (void)UPRewardVideoAdDidRewardUserWithReward:(NSDictionary *)reward
{
    NSLog(@"UPRewardVideoAdDidRewardUserWithReward");
}

//No Reward
- (void)UPRewardVideoAdDontReward:(NSError *)error
{
    NSLog(@"UPRewardVideoAdDontReward");
}
```
> You can watch logs after video displaied, to make sure every event was correctly happened or not.

<font color=#DC143C>Attention：you can send reward to players when you receive`UPRewardVideoAdDidRewardUserWithReward:`，</font>

### Callback of loading

Please use `[[UPRewardWrapper shareInstance] isReady]` to know Whether ads  loaded successfully.


But if you need ad load callback, we provide the following ways.

```
// Declare the UPRewardLoadDelegate protocol in the corresponding class and call the method
[[UPRewardWrapper shareInstance] load:self];
```

```
// Load succesful callback
- (void)UPRewardVideoAdDidLoad {
    NSLog(@"reward video ad loaded successfully");
}
//Load failed callback
- (void)UPRewardVideoAdDidLoadFail {
    NSLog(@"reward video ad failed to load");
}
```
