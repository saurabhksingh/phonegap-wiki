# App Splash Screen Sizes

## Android

### Format

**9-Patch PNG** _(recommended)_

### Dimensions

- LDPI:
  - Portrait: **200x320px**
  - Landscape: **320x200px**
- MDPI:
  - Portrait: **320x480px**
  - Landscape: **480x320px**
- HDPI:
  - Portrait: **480x800px**
  - Landscape: **800x480px**
- XHDPI:
  - Portrait: **720px1280px**
  - Landscape: **1280x720px**

## Bada

### Format

**PNG** _(recommended)_

### Dimensions

- Portrait: **480x800px**
- Landscape: unsupported

## Bada-WAC

### Format

**PNG** _(recommended)_

### Dimensions

- Type 3: **320x480px**
- Type 4: **480x800px**
- Type 5: **240x400px**

## BlackBerry

### Format

**PNG** _(recommended)_

### Dimensions

- Recommended size: **250x250px**

### Notes

- The splash screen image is centered to the screen.
- The background colour of the splash screen can be defined in the `config.xml`.
- The image will rotate appropriately.
- Any image size can be used.
  - Ideally it should be smaller than your smallest screen size.

## iOS

### Format

**PNG** _(recommended)_

### Dimensions

- Tablet (iPad)
  - Non-Retina (1x)
    - Portrait: **768x1004px**
    - Landscape: **1024x748px**
  - Retina (2x)
    - Portrait: **1536x2008px**
    - Landscape: **2048x1496px**
- Handheld (iPhone, iPod)
  - Non-Retina (1x)
    - Portrait: **320x480px**
    - Landscape: **480x320px**
  - Retina (2x)
    - Portrait: **640x960px**
    - Landscape: **960x640px**
  - iPhone 5 Retina (2x)
    - Portrait: **640x1136px**
    - Landscape: **1136x640px**

### Notes

According to Apple's application guidelines, a tablet (iPad) application should not hide the status bar while a handheld (iPhone) application should hide status bar.

The above dimensions are assuming that you have chosen to follow this recommendation. If you choose a different path, then you should increase or decrease the image height based on the size of the status bar.

An iPhone app should include one launch image in portrait orientation; an iPad app should include one launch image in portrait orientation **and** one launch image in landscape orientation. This means that not all formats listed above are **required**.

## webOS

### Format

**PNG** _(recommended)_

### Dimensions

- Recommended size: **64x64px**

### Notes

- The splash screen image is centered to the screen.
- Any image size can be used.
  - Ideally it should be smaller than your smallest screen size.

## Windows Phone

### Format

**JPG** _(required)_

### Dimensions

- Portait: **480x800px**
- Landscape: unsupported

### Notes

- The splash screen is rendered as a 16-bit image.
  - A known side effect is banding on gradient images.
  - We recommend using a solid colour background to avoid the banding.