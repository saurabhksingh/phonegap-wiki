## Android
 
### PhoneGap 0.9.5 to Latest
 
    // This is your app's init method. Here's an example of how to use it
    function init() {
        document.addEventListener("deviceready", onDR, false);
    } 
    function onDR(){
        document.addEventListener("backbutton", backKeyDown, true);
        //boot your app...
    }
    function backKeyDown() { 
        // do something here if you wish
        // alert('go back!');
    }

### PhoneGap 0.9.4 and Earlier

    // This is your app's init method. Here's an example of how to use it
    function init() {
        document.addEventListener("deviceready", onDR, false);
    }
    function onDR(){
        BackButton.override(); 
        document.addEventListener("backKeyDown", backKeyDown, true);
        //boot your app...
    }
    function backKeyDown() { 
        // do something here if you wish
        // alert('go back!');
    }
 
### Note

If you have the problem, that back button always exits the app after firing the event, add the following to your `AndroidManifest.xml`:

    <uses-sdk android:minSdkVersion="7" android:targetSdkVersion="15"  />