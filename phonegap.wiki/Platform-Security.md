## Disclaimer

This document is a work in progress, please add information where applicable and even add information about platforms not listed here please!

## PhoneGap and Security

PhoneGap is generally limited to the security features of the platform on which it is running. This document is an attempt at exploring some of the various security features of iOS, Android and RIM OS. This document also discusses various attack vectors, specifically those that are considered most important by the Open Web Application Security Project (OWASP).

## Device Security

Most mobile operating systems now support hardware encryption. Hardware encryption gives a base level of protection to data on a mobile device when the device is locked. Some devices also support an encrypted data store here passwords and other sensitive data can be stored in an encrypted state.

However, there are two caveats here to keep in mind. First, data is not secure if the user of the device does not enable locking of the device and second some of these hardware encryption approaches have been compromised.

### iOS

####Short note on data security
Every iOS device has a built in AES 256 crypto engine which ensures highly efficient data encryption on device. Each device has a unique UID burned on the application processor during manufacturing. This helps in data encryption to be unique for different devices. No external software or firmware can crack this UID. However booting up the iOS decrypts the data automatically and this facility enables people to crack this encryption. So essentially having the access to device's UI allows people to read the encrypted data. Setting the device [passcode](http://support.apple.com/kb/HT4113) prevents access to the device UI and tangles with the UID. It also provides the facility of remote wipe-off of data. However till iOS 3.0 and before iPhone 3GS remote data deletion was a lengthier process as actual disk data used to be performed. Now from iOS 4 onwards a new feature called Data Protection has been introduced. This is feature is available on on generations of iPhone 3GS or later and iPad. Its active only when a device passcode is set. It encrypts the hardware keys used to encrypt the data on disk. So in order to decrypt data passcode must be provided first. This also facilitates the quick remote data removal by invalidating only the encryption key. So as such data remains on disk but it can not be decrypted. Mails, attachments, location data and application launch images are protected using Data Protection on Apple Devices (refer [this](http://images.apple.com/ipad/business/docs/iOS_Security_Oct12.pdf) for more info. 

####Data protection in PhoneGap applications
In PhoneGap encryption is not currently supported by default (till 2.1). This means that PhoneGap does not use these APIs while writing data on disk.
Applications can make use of this APIs to make sure that data saved on disk get protected by iOS Data Protection. To encrypt files that are written to the file system the NSData writeToFile:options:error method should be used with the NSDataWritingFileProtectionComplete option.For existing files, you can use the setAttributes:ofItemAtPath:error: method of NSFileManager to set or change the value of the NSFileProtectionKey as NSDataWritingFileProtectionComplete (refer [this](http://developer.apple.com/library/ios/#documentation/Cocoa/Reference/Foundation/Classes/NSData_Class/Reference/Reference.html#//apple_ref/c/econst/NSDataWritingOptions) for more options). 

The iOS keychain is another place that data can be stored securely. As with the general hardware encryption, this too has been cracked even more easily than the file system encryption.

In PhoneGap there is a plugin that allows access to the iOS keychain.

However as mentioned earlier the data written on disk by PhoneGap is still not protected. Also it may happen that you may not want to make changes in your code to make use of the APIs suggested above to protect data.
There is another lot simpler way to achieve the data protection for your application. Using [Entitlements](http://developer.apple.com/library/mac/#documentation/Miscellaneous/Reference/EntitlementKeyReference/Chapters/AboutEntitlements.html) Data Protection for the application data can be enabled without making any code change at all.
Following are the steps to achieve this :

1. On [provisioning portal](https://developer.apple.com/ios/manage/bundles/index.action) click on App Id tab.
2. Click on configure of App Id corresponding to bundle identifier for you iOS application.
3. On bottom of page check 'Enable for Data Protection' and select 'complete data protection' option. Click Done button
4. Now navigate to Provisioning->Distribution tab. 
5. Create a provisioning profile using the App Id configured in earlier steps.
6. Download this provisioning profile and add it to you XCode and device.
7. Open your project in XCode.
8. Select the project file in project navigator and select the target that will be used for distribution.
9. In the Summary tab of the target editor scroll down to bottom of page and click 'Entitlements'. Doing this will automatically creates a {App Name}.entitlements plist file.
10. Click on the .entitlements created in previous step.
11. Under 'XCode entitlements' add a key value pair. Chose 'Data Protection Class' as key and 'NSFileProtectionComplete' as value. Please note that this value has to be same as the one chosen in App Id configuration.
12. That's all !

So once these steps are performed all archived binaries will adhere to the Data Protection policy for all the data it writes on disk.

#### iOS App Decompilers

- http://www.google.ca/search?q=decompile+llvm
- http://cerezo.name/blog/2011/03/03/iphone-decompilation-obfuscation/

### Android

At this time Gingerbread does have an encrypted store on the SD card, and Honeycomb does support full-disk encryption. It is difficult to get much information about how this works it does seem that if enabled your WebSQL and localStorage in a PhoneGap application are encrypted when the device is locked.  This does not apply to PhoneGap developers as much as it applies to the user. 

The Android Account Manager is similar to the iOS keychain, but also has it's own security problems.

Files that are stored in the shared /sdcard directory are not secure.  Each Android application has access to its own filesystem directory that only it can access.  These are located in the /data/data/ directory and the directories are named after the application namespace.  This is based on the User Permissions system that Linux uses to make sure you can't read others directories.  Each application has its own UID and it can only read files that share this UID.  However, on rooted phones, this doesn't matter, since the user has root and can view ALL the files.  Incidentally, it's also why Widgets can't directly read data from this directory, since that code is running as a different process.

Android also has a robust permissions system.  Unfortunately, the current default for PhoneGap applications is to use the example AndroidManifest file which has everything turned on.  It is highly recommended that permissions be removed except for those that are required so that attackers only have access to the application features, and not the full functionality of the device.

There is some code implemented to encrypt files on Android, but these are deprecated, and shouldn't be relied upon for any form of serious security.  Android does have support for the Java BouncyCastle Cryptographic Functions, but there will always be the issue of the threat model, what you're protecting and who you're protecting it from.

#### Android App Decompilers

- Dex2jar http://android.amberfog.com/?p=582

### RIM OS

BlackBerry devices are likely the most secure discussed here.

http://docs.blackberry.com/en/smartphone_users/deliverables/14212/BlackBerry_Internet_Service-Security_Feature_Overview--787371-0205030634-001-3.0-US.pdf

password keeper - is there an api?

Any data you store in your webworks SQLite DB, localstorage is all encrypted.

If you store a file out to the file system it is not encrypted and other apps could access these files. You would have to write an encryption extension to encrypt a file for your app.

Files are only accessible with your device password when you connect your device to a computer via the USB port

## OWASP

https://www.owasp.org/index.php/Top_10_2010-Main

### Network Security

Network security is no different in a PhoneGap application from a normal web application. This is related to the OWASP guidlines around Broken Authentication and Session Management.

#### Insufficient Transport Layer Protection

Securing the network is primarily achieved through the use of SSL for any requests made to a remote server. In addition to ensure that any sensitive data sent over the network is secured using SSL authenticated sessions should have some timeout associated with them to prevent the use of an old authentication token. In addition to this when an application is paused or closed all session related information should be deleted from the application storage.
 
See OWASP Top 10: https://www.owasp.org/index.php/Top_10_2010-A9-Insufficient_Transport_Layer_Protection
 
#### Insecure Cryptographic Storage

The most common reason for this attack is that data that should be encrypted is stored in cleartext. The use of unsalted hashes to protect passwords is another common flaw that leads to this risk.

See OWASP Top 10: https://www.owasp.org/index.php/Top_10_2010-A7-Insecure_Cryptographic_Storage
 
### Application Security
 
Since PhoneGap applications use HTML and JavaScript, many of the security concerns around PhoneGap applications are similar to those concerns on the web at large. While the fact that cross domain network requests are possible from a PhoneGap application may seem like an additional security concern, there has always been a number of different ways to do cross domain requests from web applications running in browsers that respect the same origin policy (e.g. sending data in the querystring of a GET request as the result of loading an image, script etc).
 
#### Cross site scripting (XSS)
 
Like any web based application, a PhoneGap application is subject to Cross Site Scripting. To protect against this attack vector before rendering data in an application the data should be cleaned to ensure that HTML tags are not being rendered to the view that could initiate an XSS attack. As with any web application, data should also be cleaned on the server before it is inserted into the database.
 
Use a nonce. Use POST when changing data on the server.
 
In PhoneGap additional XSS prevention exists in the form of whitelisting domains from which the client can request resources from. This is a platform specific feature that exists on BlackBerry through the config.xml while on Android and iOS it is not currently supported as of PhoneGap 1.0.
 
#### Injection
 
We use JSON.parse to prevent malicious content from being executed in the context of your application using something like JavaScript eval(...). There is no built in prevention mechanism against JavaScript injection.
 
See OWASP Top 10: https://www.owasp.org/index.php/Top_10_2010-A1-Injection
 
## PhoneGap
 
Reverse engineering is a concern of many people that use PhoneGap since one can simply open an application binary and look at the JavaScript source code of the application. One could even go so far as to add malicious JavaScript code, re-package the application and re-submit it to app stores / markets in an attempt at app phishing. This practice could be undertaken with any application whether it is written with PhoneGap or otherwise since it is a similarly simple task to decompile either Java or Objective-C.

PhoneGap can actually get around this security concern since application developers can download JavaScript in their application at runtime, run that JavaScript, and delete it when the application closes. In that way, the source code is never on the device when the device is at rest. This is a much more difficult prospect with Java or Objective-C let alone the restrictions in the App Store around dynamically running Objective-C code.