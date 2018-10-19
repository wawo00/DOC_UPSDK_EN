## Unity Plugin initialization
```csharp
/*
 * Initialize UPSDK
 * Upsdk will only be initialized once even if it is called multiple times.
 * @param zone:0, areas except China (CN)；1, China；2, judging the types of users automatically depending on ip
* Since version 3003, please call the constant through the UPConstant class: SDKZONE_FOREIGN, SDKZONE_CHINA, SDKZONE_AUTO;
* Previous versions prior to 3003 still call the constants via the PolyADSDK class.
 */
public static string initPolyAdSDK(int zone)
```
#### Sample
In the demo code, the onButton_init_Click() method is called by clicking the initialization button on the UI. Even if the initialization button is clicked multiple times, ** repeatedly calls UPSDK.initPolyAdSDK()**, but the SDK will only be initialized once**.
```csharp
public void onButton_init_Click()
{
    //TextEditor text = GameObject.Find ("CallText").GetComponent<TextEditor>();


    if (!inited) {
        UPSDK.UPSDKInitFinishedCallback = new System.Action&ltbool, string>(actionForSdkInitFinish);
        UPSDK.UPInterstitialDidClickCallback = new System.Action&ltstring, string>(actionForInterstitialDidClick);
        UPSDK.UPInterstitialDidCloseCallback = new System.Action&ltstring, string>(actionForInterstitialDidClose);
        UPSDK.UPInterstitialDidShowCallback = new System.Action&ltstring, string>(actionForInterstitialDidShow);

        UPSDK.UPBannerDidShowCallback = new System.Action&ltstring, string>(actionForSdkBannerDidShow);
        UPSDK.UPBannerDidClickCallback = new System.Action&ltstring, string>(actionForSdkBannerDidClick);
        UPSDK.UPBannerDidRemoveCallback = new System.Action&ltstring, string>(actionForSdkBannerRemove);

        UPSDK.UPRewardDidOpenCallback = new System.Action&ltstring, string>(actionForSdkRewardDidOpen);
        UPSDK.UPRewardDidClickCallback = new System.Action&ltstring, string>(actionForSdkRewardDidClick);
        UPSDK.UPRewardDidCloseCallback = new System.Action&ltstring, string>(actionForSdkRewardDidClose);
        UPSDK.UPRewardDidGivenCallback = new System.Action&ltstring, string>(actionForSdkRewardDidGiven);
        UPSDK.UPRewardDidAbandonCallback = new System.Action&ltstring, string>(actionForSdkRewardDidAbandon);

        #if UNITY_ANDROID && !UNITY_EDITOR

            UPSDK.UPExitAdDidShowCallback = new System.Action&ltstring> (actionForSdkExitAdDidShow);
            UPSDK.UPExitAdDidClickCallback = new System.Action&ltstring> (actionForSdkExitAdDidClick);
            UPSDK.UPExitAdDidClickMoreCallback = new System.Action&ltstring> (actionForSdkExitAdDidClickMore);
            UPSDK.UPExitAdOnExitCallback = new System.Action&ltstring> (actionForSdkExitAdOnExit);
            UPSDK.UPExitAdOnCancelCallback = new System.Action&ltstring> (actionForSdkExitAdOnExit);

        #endif
    }
    inited = true;

    string tt = UPSDK.initPolyAdSDK (0);
    Debug.Log ("initPolyAdSDK ====> " + tt);
}
```

The implementation of the callback interface is as followings：
The code for the sample project illustrates the role of each interface and the meaning of the parameters.Plus callback interface is not required to be implemented if you do not need it.


```csharp
#if UNITY_ANDROID && !UNITY_EDITOR
private void actionForSdkExitAdDidShow(string msg) {
    Debug.Log ("===> actionForSdkExitAdDidShow Callback");
}

private void actionForSdkExitAdDidClick(string msg) {
    Debug.Log ("===> actionForSdkExitAdDidClick Callback");
}

private void actionForSdkExitAdDidClickMore(string msg) {
    Debug.Log ("===> actionForSdkExitAdDidClickMore Callback");
}

private void actionForSdkExitAdOnExit(string msg) {
    Debug.Log ("===> actionForSdkExitAdOnExit Callback");
}

private void actionForSdkExitAdDidOnCancel(string msg) {
    Debug.Log ("===> actionForSdkExitAdDidOnCancel Callback");
}
#endif

// test for reward video callback
private void actionForSdkRewardDidOpen(string placeId, string msg) {
    Debug.Log ("===> actionForSdkRewardDidOpen Callback at: " + placeId);
}

private void actionForSdkRewardDidClick(string placeId, string msg) {
    Debug.Log ("===> actionForSdkRewardDidClick Callback at: " + placeId);
}

private void actionForSdkRewardDidClose(string placeId, string msg) {
    Debug.Log ("===> actionForSdkRewardDidClose Callback at: " + placeId);
}

private void actionForSdkRewardDidGiven(string placeId, string msg) {
    Debug.Log ("===> actionForSdkRewardDidGiven Callback at: " + placeId);
}

private void actionForSdkRewardDidAbandon(string placeId, string msg) {
    Debug.Log ("===> actionForSdkRewardDidAbandon Callback at: " + placeId);
}

private void actionForSdkBannerRemove(string placeId, string msg) {
    Debug.Log ("===> actionForSdkBannerRemove Callback at: " + placeId);
}

private void actionForSdkBannerDidClick(string placeId, string msg) {
    Debug.Log ("===> actionForSdkBannerDidClick Callback at: " + placeId);
}

private void actionForSdkBannerDidShow(string placeId, string msg) {
    Debug.Log ("===> actionForSdkBannerDidShow Callback at: " + placeId);
}

private void actionForSdkInitFinish(bool result, string msg) {
    Debug.Log ("===> actionForSdkInitFinish Callback r: " + result + ", msg: " + msg);
}

private void actionForInterstitialDidShow(string placeId, string msg) {
    Debug.Log ("===> actionForInterstitialDidShow Callback at: " + placeId);
}

private void actionForInterstitialDidClick(string placeId, string msg) {
    Debug.Log ("===> actionForInterstitialDidClick Callback at: " + placeId);
}

private void actionForInterstitialDidClose(string placeId, string msg) {
    Debug.Log ("===> actionForInterstitialDidClose Callback at: " + placeId);
}
```