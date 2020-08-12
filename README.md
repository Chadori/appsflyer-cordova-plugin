
<img src="https://www.appsflyer.com/wp-content/uploads/2016/11/logo-1.svg"  width="600">

# Cordova AppsFlyer plugin 6.0.1-Beta for Android and iOS. 

[![npm version](https://badge.fury.io/js/cordova-plugin-appsflyer-sdk.svg)](https://badge.fury.io/js/cordova-plugin-appsflyer-sdk)
[![Build Status](https://travis-ci.org/AppsFlyerSDK/appsflyer-cordova-plugin.svg?branch=master)](https://travis-ci.org/AppsFlyerSDK/appsflyer-cordova-plugin)

----------
**❗️Important** <br>
Cordova AppsFlyer plugin version **4.4.0** and higher are meant to be used with **cordova-android@7.0.0**
<br>For lower versions of cordova-android please use plugin version 4.3.3 available @ https://github.com/AppsFlyerSDK/cordova-plugin-appsflyer-sdk/tree/4.3.3

----------
🛠 In order for us to provide optimal support, we would kindly ask you to submit any issues to support@appsflyer.com

*When submitting an issue please specify your AppsFlyer sign-up (account) email , your app ID , reproduction steps, code snippets, logs, and any additional relevant information.*

----------

## Table of content

- [SDK versions](#plugin-build-for)
- [Installation](#installation)
- [Guides](#guides)
- [Setup](#setup)
- [API](#api) 
- [Demo](#demo)  
- [Ionic](#ionic)


### <a id="plugin-build-for"> This plugin is built for

- iOS AppsFlyerSDK **v6.0.1-Beta**
- Android AppsFlyerSDK **v5.4.3**


## <a id="installation">📲Installation


To install cordova v6.0.1-beta manually from this branch check out the doc [here](/docs/Installation.md).

***steps:***<br>
1. Add ```#import <AppTrackingTransparency/AppTrackingTransparency.h>``` in your ```AppDelegate.m``` file<br>
2.Add the ATT pop-up for IDFA collection. your ```AppDelegate.m``` should look like this:


```javascript
-(BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
{
    self.viewController = [[MainViewController alloc] init];
    if (@available(iOS 14, *)) {
        [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
            //If you want to do something with the pop-up
        }];
    }
    return [super application:application didFinishLaunchingWithOptions:launchOptions];
}
```

3. Add ```Privacy - Tracking Usage Description``` inside your ```.plist``` file in Xcode.<br>
4.For more info see section ***3.4*** in the Support integration guide [Here](https://support.appsflyer.com/hc/en-us/articles/360011451918#integration)



 ## <a id="guides"> 📖 Guides

Great installation and setup guides can be viewed [here](/docs/Guides.md).
- [init SDK Guide](/docs/Guides.md#init-sdk)
- [Deeplinking Guide](/docs/Guides.md#deeplinking)
- [Uninstall Guide](/docs/Guides.md#uninstall)


## <a id="setup"> 🚀 Setup

####  Set your App_ID (iOS only), Dev_Key and enable AppsFlyer to detect installations, sessions (app opens) and updates.  
> This is the minimum requirement to start tracking your app installs and is already implemented in this plugin. You **MUST** modify this call and provide:  
 **devKey** - Your application devKey provided by AppsFlyer.<br>
**appId**  - ***For iOS only.*** Your iTunes Application ID.


Add the following lines to your code to be able to initialize tracking with your own AppsFlyer dev key:


```javascript
document.addEventListener('deviceready', function() {

   window.plugins.appsFlyer.initSdk({
      devKey: 'K2***************99', // your AppsFlyer devKey
      isDebug: false,
      appId: '41*****44', // your ios appID
      timeToWaitForAdvertiserID: 10, //time for the sdk to wait before launch
    },
      (result) => {
        console.log(result);
      },
      (error) => {
        console.error(error);
      }
    );
  
}, false);
```
---


## <a id="api"> 📑 API
  
See the full [API](/docs/API.md) available for this plugin.


## <a id="demo"> 📱 Demo
  
There is 1 demo project called ```demoC```.<br>run ```npm run setup_c``` in the appsflyer-cordova-plugin folder and then open the project ios in Xcode

## <a id="ionic"> 📍 Ionic

In case you are using Ionic framework, you have 2 options:
### 1 - Using Ionic native plugin
####  Ionic 4
run this commands:
**With Cordova**:
```
$ ionic cordova plugin add cordova-plugin-appsflyer-sdk
$ npm install @ionic-native/appsflyer
```
**With Capacitor**:
```
$ npm install cordova-plugin-appsflyer-sdk
$ npm install @ionic-native/appsflyer
ionic cap sync
```
Then add the following to `app.module.ts`
```
import { Appsflyer } from "@ionic-native/appsflyer/ngx";
...
providers: [
Appsflyer,
...,
]
```
and in your main ts file:
```
import { Appsflyer } from '@ionic-native/appsflyer/ngx';

constructor(private appsflyer: Appsflyer) { }
...
this.appsflyer.initSdk(options);
```
####  Ionic 2/3
If you're using Ionic 2/3, you'd need to install a previous version of the Ionic Native dependency (notice the **@4** at the end of the npm install command):
```
$ ionic cordova plugin add cordova-plugin-appsflyer-sdk
$ npm install @ionic-native/appsflyer@4
```
Then add the following to `app.module.ts`(with no **/ngx**)
```
import { Appsflyer } from "@ionic-native/appsflyer";
...
providers: [
Appsflyer,
...,
]
```
And finally in your main ts file:
```
import { Appsflyer } from '@ionic-native/appsflyer';
```
###  2. Using the `window` object directly
 You can use the plugin the same way like in Cordova with only one exception:
instead of `window.plugins...` use `window['plugins']...`
Check out the full [API](/docs/API.md) for more information
