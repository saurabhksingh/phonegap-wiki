## Disclaimer

This document is a work in progress, please add information where applicable and even add information about platforms not listed here please!

## PhoneGap and Security

PhoneGap is generally limited to the security features of the platform on which it is running. This document is an attempt at exploring some of the various security features of iOS, Android and RIM OS. This document also discusses various attack vectors, specifically those that are considered most important by the Open Web Application Security Project (OWASP).

## Device Security

Most mobile operating systems now support hardware encryption. Hardware encryption gives a base level of protection to data on a mobile device when the device is locked. Some devices also support an encrypted data store here passwords and other sensitive data can be stored in an encrypted state.

However, there are two caveats here to keep in mind. First, data is not secure if the user of the device does not enable locking of the device and second some of these hardware encryption approaches have been compromised.

### iOS

Hardware encryption is available on the iOS devices listed above. When the device is locked using a PIN on iOS, by default only emails on the device are encrypted (reference needed). However, the key that is used to do the encryption is stored on the device, which has enabled people to crack this encryption.

In PhoneGap encryption is not currently supported by default. To encrypt files that are written to the file system the NSData writeToFile:options:error method should be used with the NSDataWritingFileProtectionComplete option -- this is not done as of PhoneGap 1.0. One could also use the built in crypto APIs to do custom software encryption.

The iOS keychain is another place that data can be stored securely. As with the general hardware encryption, this too has been cracked even more easily than the file system encryption.

In PhoneGap there is a plugin that allows access to the iOS keychain.

On devices that are encrypted, other security options like remote wipe are also then enabled.

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