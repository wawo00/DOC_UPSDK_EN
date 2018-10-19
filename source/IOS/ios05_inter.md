
## Interstitial Ad  

Related methods and delegate interfaces was defined in file `UPIntersitialWrapper.h`
### Reference header file
```objective-c
#import   <UPSDK/UPSDK.h>
```
### Methods of implementation class

> You can set parameter `Placement ID` to any significative name you want. If you not sure about should discussed with our **support engineer**. You should use different `Placement ID` for different ads placement. We provide revenue from each  `Placement ID` in the feature.
> Eg: You may use "Pause" or "Menu" when initial our SDK in the pause scene of your game.

```objective-c
@interface UpIntersitialWrapper : NSObject

/**
* Initial method 
* @ param avidPlacement：Placement ID
**/
- (instancetype)initAvidPlacement:(NSString *)avidPlacement;

/**
* Setup delegate callback object 
* @ param delegate：UpIntersitialDelegate 
**/
- (void)setDelegate:(id<UpIntersitialDelegate>)delegate;

/**
* Check if Video Ads was ready to play
**/
- (BOOL)isReady;

/**
* Setup delegate callback object 
* @ param viewController：UIViewController Object, to control redirection when clicked 
**/
- (BOOL)show:(UIViewController *)viewController;

/**
 * Callback of loading ads
 * @param delegate，delegate for callback
 **/
 - (void)load:(id<UPIntersitialLoadDelegate>)delegate;
@end
```
### UpIntersitialDelegate Callback protocol 
It's not necessary to implement callback protocol of Interstitial Ad. You can implement it by your situation.
```objective-c
@protocol UpIntersitialDelegate <NSObject>

/**
 * method will be called when Interstitial successful displaied
 * @ param wrapper ：sender, UpIntersitialWrapper object
 */
- (void)interstitialAdDidShow:(UpIntersitialWrapper *)wrapper;

/**
 * When Interstitial Ad closed
 * @ param wrapper sender, UpIntersitialWrapper object
 */
- (void)interstitialAdDidClose:(UpIntersitialWrapper *)wrapper;

/**
 * When Interstitial Ad clicked
 * @ param wrapper sender, UpIntersitialWrapper object
 */
- (void)interstitialAdDidClick:(UpIntersitialWrapper *)wrapper;

@end

```

## Demo code - Xcode

In demo project of XCode, declare `STInterstitialViewController` class, to display Interstitial Ads. Define class `STInterstitialViewController.h` first. The code here is pretty simple.

```objective-c
@interface STInterstitialViewController : UIViewController

@end
```

In `STInterstitialViewController.m`, you need a few lines of code to finish Interstitial ad loading and impression.

First, define a object of `UpIntersitialWrapper`: `_intersitialWrapper`. We can use this object to control Interstitial ad loading and impression.

In most of case, you should use different object of  `UpIntersitialWrapper` for different Interstitial ad placement.

Code:

```objective-c
@interface STInterstitialViewController () <UpIntersitialDelegate>
{
//Declare a wrapper object, you can declare more object if needed
    UpIntersitialWrapper *_intersitialWrapper;
}
@end
```

Add following code:

```objective-c

- (void)viewDidLoad  {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    // Add a button in viewDidLoad to test Interstitial ad loading and impression
    UIButton *button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
    button.backgroundColor = [UIColor orangeColor];
    button.frame = CGRectMake(self.view.frame.size.width/2 - 250/2, 100, 250, 40);
    [button setTitle:@"Interstital Ad Test" forState:UIControlStateNormal];
    // intersitialClick will be triggered when button clicked
    [button addTarget:self action:@selector(intersitialClick) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
    
}

- (void)intersitialClick {
    // Let's use "inter_bbb"  as placement id of _intersitialWrapper
    _intersitialWrapper = [[UpIntersitialWrapper alloc] initAvidPlacement:@"inter_bbb"];
    // setup callback delegate 
    [_intersitialWrapper setDelegate:self];
    
    // Check if interstitial ads was ready to show
    if ([_intersitialWrapper isReady]) {
        [_intersitialWrapper show:self];
    }
    else
    {
        NSLog(@"Intersitial no ready");
    }
}
```

There are only 3 steps to show and control a interstitial ad by following code.
1. Declare global object, for example:
```objective-c
 UpIntersitialWrapper *_intersitialWrapper;
```
2. Initial object 
As following example, "inter_bbb" is a real exist ad placement. Wrong placement id will caused a failure on ads loading.
```objective-c
_intersitialWrapper = [[UpIntersitialWrapper alloc] initAvidPlacement:@"inter_bbb"];
```
3. Show Ads
Use following code to display Ad
```objective-c
if ([_intersitialWrapper isReady]) {
     [_intersitialWrapper show:self];
}
```
