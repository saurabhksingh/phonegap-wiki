## About

In some cases, you will want to have different CSS depending on the screen size of the phone, this is especially important for Android phones of different screen sizes.

## How it works

The simplest way is to build one CSS file and have the media queries within the CSS, with replacement Class & ID entries (complete replacement rather than additions), rather than having multiple CSS files - the reason for this is that it is easier to manage a the CSS queries rather than having to include a multitude of CSS files.

## Example

.myClass {
    top: 50px;
    left: 25px;
}
@media only screen and (max-device-height: 460px) {
    .myClass {
        top: 30px;
        left: 25px;
    }
}

## Important considerations

Different devices have different screen sizes for PhoneGap's use in px, examples are:
* iPhone 3G/3GS/4/4S = 320 wide x 480 high
* Android HD = 360 wide x 567 high

Note that PhoneGap seems to "ignore" the pixel density and average it down to half of the higher resolution screens, thus nullifying the iPhone "Retina Display".

The easy way to find out your screen's dimensions within PhoneGap are to use some JavaScript (example uses JQuery):
consoleLog( "window=" + $(document).width() + "x" + $(document).height() );

For the "height" variations of the Media Queries you must use the height returned by the JavaScript, **BUT**, the "width" parameters use the actual pixel width of the screen:
@media only screen and (min-device-width: 700px) {
}

## Tablets

If you wish to include CSS for tablets (iPad, Android 7"+ or PlayBook) you will have to include more CSS Media Queries as there can be a dramatic difference in the sizes of the screen, and only outputting the sizes returned by the above JavaScript will give you some indication on what your heights and widths will be.