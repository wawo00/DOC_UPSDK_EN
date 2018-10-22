## Initial SDK

Only used Xcode engineering  as an example for explanation. If you are using other projects, please refer to Xcode engineering operation. 
The UPLTV SDK is very simple to initialize.

```typescript
/*
* Please be sure to complete the SDK initialization before using the other API interfaces of the SDK
* @param zone product distribution area, 0 overseas, 1 mainland China, 2 automatically according to IP positioning
* @param callback return turn means initial upsdk successful
*/
static initSDK(zone: number, callback?:(res:boolean)=>void)
```
Sample:
```typescript
let initButton = new eui.Button();
initButton.label = "initButton";
this.addChild(initButton);
initButton.addEventListener(egret.TouchEvent.TOUCH_TAP, this.initButtonClick, this);

initButtonClick(e: egret.TouchEvent){
        upltv.initSDK(0);
}
```