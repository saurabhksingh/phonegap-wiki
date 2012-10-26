## Cross-Platform

- Rendering performance of an iFrame is up for grabs on each platform. Expect things such as CSS transitions to not perform as well.
- Interaction with the iFrame is up for grabs on each platform. There is sometimes a delay in touch events and touchmove may conflict with one of the parent windows' scroll panes.  
 
## Android
 
- History does not work the way it should. history.back() and history.forward() don't work and we have to hack it (with history states) to make it work (sorta). We were able to get around it by setting the usePolling property to true.
- Conflicts between the main window and the iframe window for everything (URLs, events, etc) 
- There were an issue regarding the ability to select text in the iframe content; I believe Anis found a solution / workaround for it.
- Can't use XmlHttpRequests to set document data (it messes up with CSS/js etc). 
 
## iOS
 
- Enabling iFrames on PhoneGap-iOS requires that you whitelist the iframe domains and enable "OpenAllWhitelistURLsInWebView". While this doesn't sound like a problem, many applications want to open specific sites in MobileSafari (not a ChildBrowser), which cannot be accomplished easily when "OpenAllWhitelistURLsInWebView" is enabled.
- To change OpenAllWhitelistURLsInWebView open the Cordova.plist file in Xcode. 
- To whitelist a domain. Add it to the ExternalHosts array in the Cordova.plist file. Simply press the + next to the ExternalHosts title and when the item0 appears bellow add your domain to the value section (in the format example.com).