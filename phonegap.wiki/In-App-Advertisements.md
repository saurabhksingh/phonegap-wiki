## Android

On Android, you can add adMob ads to your PhoneGap application.

If you are using localStorage within your PhoneGap / Cordova app, you will want to use Option 2 for the actual Java Code.  Loading Admob on demand will clear localStorage for some reason.  All the other steps are the same.
 
Follow these easy steps in your Admob Account:

- Sign up for an adMob account
- Create a site. (This needs to be an android application)
- Retrieve your Publisher ID
 
Now back to Eclipse or your IDE of choice:

- Download the adMob sdk and include it in your project.  [Follow the instructions here](https://developers.google.com/mobile-ads-sdk/docs/android/fundamentalsFollow%20the%20instructions%20here).
- Don't forget to add "Import com.google.ads.* " in your Main Java Activity
add the following to your AndroidManifest.xml
 
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
 
Add the following inside your application section of your AndroidManifest.xml:
 
    <activity android:name="com.google.ads.AdActivity" android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" /> 
 
The last thing to do (before adding the Java code below) is change your project.properties to "target=android-13" 
__Project > Properties > Android > Project Build Target = Android API 13 or higher__.
This means you will have to download sdk version 13. You can leave your <target-sdk> alone inside your manifest.xml
 
### Java Code - Option 1 - Show AdMob Instantly

Insert the following code in your MainActivity class.  This will load Admob on-demand. 
 
    super.onCreate(savedInstanceState);
    super.loadUrl("file:///android_asset/www/index.html");
    // the 2 lines above should already be in your Java activity if you setup Phonegap correctly.
    adView = new AdView(this, AdSize.BANNER, PUBLISHER_ID);      
    LinearLayout layout = super.root;
    layout.addView(adView);
    layout.setHorizontalGravity(android.view.Gravity.CENTER_HORIZONTAL);              //This centers the ads in landscape mode.
    adView.loadAd(new AdRequest());
 
If you want the ads at the top, put this before you load webview. If you want the ads at the bottom, put it after.
 
### Java Code - Option 2 - Delay AdMob Ads by X Seconds to prevent clearing your localStorage.....

There is a bug or glitch for localStorage with the Admob SDK and PhoneGap.   If you use the code in Option 1, your localStorage will clear when your application loads. Not good if you depend on that feature for storing user data.
 
add "import android.os.Handler;" to the top of your Main Java Activity
 
Below is the full Java code for delaying your AdMob ads by 5 seconds (in milliseconds)  Much thanks to this anonymous user at StackOverflow.
 
    public class MyAppActivity extends DroidGap {
        private Handler mHandler = new Handler();
        private AdView adView;
        /** Called when the activity is first created. */
        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            super.loadUrl("file:///android_asset/www/index.html");
       
            mHandler.postDelayed(new Runnable() {
                public void run() {
                    doAdMob();
                }
            }, 5000);         
        }
    
        private void doAdMob() {
            // Create the adView
            adView = new AdView(this, AdSize.BANNER, "YOUR PUB ID");
            // Lookup your LinearLayout - get the super.root
            LinearLayout layout = super.root;
            // Add the adView to it
            layout.addView(adView);
            // This centers the ads in landscape mode.        
            layout.setHorizontalGravity(android.view.Gravity.CENTER_HORIZONTAL);
            // Initiate a generic request to load it with an ad
            AdRequest request = new AdRequest();
            // and finally...     
            adView.loadAd(request);                    
        }
    }
 