# Debugging in PhoneGap

## Current State

Debugging support for your PhoneGap applications is not as well-developed as for native apps or for pure web apps. The main hurdle is that the browser to be debugged is on your mobile device or simulator. This makes it difficult to synchronize breakpoints or retrieve stack traces. Nonetheless, there is still a lot that you can do.
 
## Techniques

### Desktop

The desktop browser is a powerful tool for mobile web development. Surprisingly, the majority of your mobile development can be previewed and debugged in your desktop browser. The main pitfalls of using a desktop browser compared to mobile browser are rendering accuracy, JavaScript performance, and API availability. However, these pitfalls can be overcame with some [Additional Tools](#additional-tools)

#### Picking a Desktop Browser

When picking a desktop browser, you must consider your targeted mobile platform. Each mobile platform uses a different browser and while you cannot find exact same browser on the desktop, you can match the browser engines. Below is a table that lists desktops browsers for each platform:

<table>
  <tr>
    <th>Mobile Platform</th>
    <th>Mobile Browser Engine</th>
    <th>Compatible Desktop Browsers</th>
  </tr>
  <tr>
    <td>Android</td>
    <td>WebKit</td>
    <td>Apple Safari, Google Chrome</td>
  </tr>
  <tr>
    <td>Bada</td>
    <td>WebKit</td>
    <td>Apple Safari, Google Chrome</td>
  </tr>
  <tr>
    <td>BlackBerry 5.0</td>
    <td>Proprietary</td>
    <td>None</td>
  </tr>
  <tr>
    <td>BlackBerry 6.0+</td>
    <td>WebKit</td>
    <td>Apple Safari, Google Chrome</td>
  </tr>
  <tr>
    <td>iOS</td>
    <td>WebKit</td>
    <td>Apple Safari, Google Chrome</td>
  </tr>
  <tr>
    <td>webOS</td>
    <td>WebKit</td>
    <td>Apple Safari, Google Chrome</td>
  </tr>
  <tr>
    <td>Windows Phone</td>
    <td>Internet Explorer</td>
    <td>Internet Explorer</td>
  </tr>
</table>

#### Mimicking the Mobile Environment

##### Viewport

This is fairly straight-forward. Just resize your desktop browser window to be roughly the size of a mobile viewport.

##### Touch Events

In Google Chrome, you can open the WebInspector Settings (gear in the bottom right of WebInspector) to enable Touch Event emulation.

#### Debugging your Application

With the desktop browser, you can leverage the browser's debugging tools. In a WebKit browser, you can open WebInspector to inspect the DOM and debug JavaScript. Most other browsers have an equivalent debugging tool.

<a href="#" name="additional-tools"></a>
#### Additional Tools

- [PhoneGap Emulator](http://emulate.phonegap.com) uses Ripple to emulate the PhoneGap API.
- [Ripple Emulator](http://ripple.tinyhippos.com/) emulates the PhoneGap API.
- [ScreenQueri.es](http://screenqueri.es/) to preview exact device screen sizes.
- [thumbs.js](http://mwbrooks.github.com/thumbs.js/) is a TouchEvent polyfill.
- [PhoneGap Desktop](https://github.com/jxp/phonegap-desktop) is a mocking library for the PhoneGap API.

### Remote Web Inspector

After you've developed the first stage of your application with your desktop browser, you will want to test it on a mobile device. The main hurtle with testing on a mobile device is that you will not have access to WebInspector. This is where a remote web inspector steps in.

#### Weinre

Weinre is a remote WebInspector that will debug any browser remotely. It is not quite a full-fledged debugger, but gives you a live view of the DOM and access to the JavaScript console. Unfortunately, no breakpoints or stack traces are available, but the JavaScript console can lends clues to errors.

You can [run Weinre locally](http://people.apache.org/~pmuellr/weinre/docs/latest/) or [use debug.phonegap.com](http://debug.phonegap.com).

#### WebKit's Remote Web Inspector

WebKit has the ability to connect it's WebInspector to remote WebKit browsers, although few mobile platform support this feature.

- [BlackBerry supports Remote Web Inspector](http://docs.blackberry.com/en/developers/deliverables/38982/Getting_started_with_Web_Inspector_1695020_11.jsp)
- [iOS has unofficial support for Remote Web Inspector](http://www.mobilexweb.com/blog/debugging-web-safari-phonegap-iphone-ipad)

#### Additional Debugging Resources

- [SpotNeedle](http://www.spotneedle.com)
- [JSBin](http://jsbin.com)

### Log Messages

When all else fails, you can always use `console.log('...');` or `alert('...');` to mobile web application. I know it's not pretty, but it can help when you're in a jam.

Advanced log message handling can be found on [[Exception Log Handling]].

#### Android

On Android, all `console.log('...');` messages will appear as printouts in the command-line tool `logcat`, which is bundled with the Android SDK and integrated into the Android Eclipse plugin.

#### BlackBerry

On BlackBerry, all `console.log('...');`  are printed to the BlackBerry's Event Log. The Event Log can be accessed by pressing `ALT + LGLG`.

#### iOS

On iOS, all `console.log('...');` are output to the Xcode Debug Area console. 