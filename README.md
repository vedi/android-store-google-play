*This project is a billing provider plugin to [android-store](https://github.com/soomla/android-store).*


## android-store-google-play

android-store-google-play is the default billing service plugin for android-store. It uses the default code given by Google which was adapted to IabHelper and IIabService interface so it'll be useful to SOOMLA's android-store.


## Getting Started

In order to work with this plugin you first need to go over android-store's [Getting Started](https://github.com/soomla/android-store#getting-started).

The steps to integrate this billing service are also in android-store's [Selecting Billing Service](https://github.com/soomla/android-store#google-play) but we will also write them here for convenience:

Once you complete the following steps, see the [Google Play IAB](http://know.soom.la/android/store/Store_GooglePlayIAB)
tutorial in our _Knowledge Base_ for information about in-app-purchase setup, integration with SOOMLA, and how to define
your in-app purchase items.

1. Add `AndroidStoreGooglePlay.jar` from the folder `billing-services/google-play` to your project.

2. Make the following changes in `AndroidManifest.xml`:

  Add the following permission (for Google Play):

  ``` xml
  <uses-permission android:name="com.android.vending.BILLING" />
  ```

  Add the `IabActivity` to your `application` element, the plugin will spawn a transparent activity to make purchases. Also, you need to tell us what plugin you're using so add a meta-data tag for that:

  ``` xml
  <activity android:name="com.soomla.store.billing.google.GooglePlayIabService$IabActivity"
            android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen"/>
  <meta-data android:name="billing.service" android:value="google.GooglePlayIabService" />
  ```

3. After you initialize `SoomlaStore`, let the plugin know your public key from [Google play Developer Console](https://play.google.com/apps/publish/):

  ``` java
  public class StoreExampleActivity extends Activity {
      ...
      protected void onCreate(Bundle savedInstanceState) {
          ...
          GooglePlayIabService.getInstance().setPublicKey("[YOUR PUBLIC KEY FROM GOOGLE PLAY]");
      }
  }
  ```

4. If you want to allow Android's test purchases, all you need to do is tell that to the plugin:

  ``` java
  public class StoreExampleActivity extends Activity {
      ...
      protected void onCreate(Bundle savedInstanceState) {
          ...
          GooglePlayIabService.AllowAndroidTestPurchases = true;
      }
  }
  ```

5. In case you want to turn on _Fraud Protection_ you need to get clientId, clientSecret and refreshToken as
explained in [Google Play Purchase Verification](http://know.soom.la/android/store/Store_GooglePlayVerification) in
our _Knowledge Base_ and use them like this:

  ``` java
      GooglePlayIabService.getInstance().configVerifyPurchases(new HashMap<String, Object>() {{
          put("clientId", <YOU_CLIENT_ID>);
          put("clientSecret", <YOUR_CLIENT_SECRET>);
          put("refreshToken", <YOUR_REFRESH_TOKEN>);
      }});
  ```

  >  Optionally you can turn on `verifyOnServerFailure` if you want to get purchases automatically verified in case of network failures during the verification process:
  >
  > ``` java
  > GooglePlayIabService.getInstance().verifyOnServerFailure = true;
  > ```

####**If you have an in-game storefront**

We recommend that you open the IAB Service and keep it open in the background. This how to do that:

When you open the store, call:  
``` java
SoomlaStore.getInstance().startIabServiceInBg();
```

When the store is closed, call:  
``` java
SoomlaStore.getInstance().stopIabServiceInBg();
```


Contribution
---
SOOMLA appreciates code contributions! You are more than welcome to extend the capabilities of SOOMLA.

Fork -> Clone -> Implement -> Add documentation -> Test -> Pull-Request.

IMPORTANT: If you would like to contribute, please follow our [Documentation Guidelines](https://github.com/soomla/android-store/blob/master/documentation.md). Clear, consistent comments will make our code easy to understand.

## SOOMLA, Elsewhere ...

+ [Framework Website](http://www.soom.la/)
+ [Knowledge Base](http://know.soom.la/)


<a href="https://www.facebook.com/pages/The-SOOMLA-Project/389643294427376"><img src="http://know.soom.la/img/tutorial_img/social/Facebook.png"></a><a href="https://twitter.com/Soomla"><img src="http://know.soom.la/img/tutorial_img/social/Twitter.png"></a><a href="https://plus.google.com/+SoomLa/posts"><img src="http://know.soom.la/img/tutorial_img/social/GoogleP.png"></a><a href ="https://www.youtube.com/channel/UCR1-D9GdSRRLD0fiEDkpeyg"><img src="http://know.soom.la/img/tutorial_img/social/Youtube.png"></a>

## License

Apache License. Copyright (c) 2012-2014 SOOMLA. http://soom.la
+ http://opensource.org/licenses/Apache-2.0
