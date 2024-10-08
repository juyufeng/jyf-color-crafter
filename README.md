# JyfColorCrafter

## 介绍
JyfColorCrafter 是一个高效快速的 JavaScript 库，用于颜色操作和转换。它允许多种输入形式，提供颜色转换和其他颜色实用函数。
它无需依赖任何其他库，具备跨平台及多浏览器兼容性，开箱即用，且未来将持续进行更新与优化。
## Introduction
JyfColorCrafter is a fast JavaScript library for color manipulation and conversion. It allows multiple input formats and provides color conversion and other color utility functions. 
It has no dependencies and is compatible with all browsers.

## 在 node 中包含

`JyfColorCrafter` 可以从 npm 安装：

`JyfColorCrafter` can be installed from npm:

   -  npm install jyf-color-crafter

    然后可以在你的脚本中使用它：

```js
let JyfColorCrafter = require("jyf-color-crafter");
let color = JyfColorCrafter("red");
```
或者  or
```js
import JyfColorCrafter from "jyf-color-crafter";
let color = JyfColorCrafter("red");
```

### UMD

```html
<script type='text/javascript' src='./jyf-color-crafter.js'></script>
<script type='text/javascript'>
let color = JyfColorCrafter("red");
</script>
```

## 使用方法
## Usage

### Hex, 8-digit (RGBA) Hex
```js
JyfColorCrafter("#000");
JyfColorCrafter("000");
JyfColorCrafter("#369C");
JyfColorCrafter("369C");
JyfColorCrafter("#f0f0f6");
JyfColorCrafter("f0f0f6");
JyfColorCrafter("#f0f0f688");
JyfColorCrafter("f0f0f688");
```
### RGB, RGBA
```js
JyfColorCrafter("rgb (255, 0, 0)");
JyfColorCrafter("rgb 255 0 0");
JyfColorCrafter("rgba (255, 0, 0, .5)");
JyfColorCrafter({ r: 255, g: 0, b: 0 });
JyfColorCrafter.fromRatio({ r: 1, g: 0, b: 0 });
JyfColorCrafter.fromRatio({ r: .5, g: .5, b: .5 });
```
### HSL, HSLA
```js
JyfColorCrafter("hsl(0, 100%, 50%)");
JyfColorCrafter("hsla(0, 100%, 50%, .5)");
JyfColorCrafter("hsl(0, 100%, 50%)");
JyfColorCrafter("hsl 0 1.0 0.5");
JyfColorCrafter({ h: 0, s: 1, l: .5 });
JyfColorCrafter.fromRatio({ h: 1, s: 0, l: 0 });
JyfColorCrafter.fromRatio({ h: .5, s: .5, l: .5 });
```
### HSV, HSVA
```js
JyfColorCrafter("hsv(0, 100%, 100%)");
JyfColorCrafter("hsva(0, 100%, 100%, .5)");
JyfColorCrafter("hsv (0 100% 100%)");
JyfColorCrafter("hsv 0 1 1");
JyfColorCrafter({ h: 0, s: 100, v: 100 });
JyfColorCrafter.fromRatio({ h: 1, s: 0, v: 0 });
JyfColorCrafter.fromRatio({ h: .5, s: .5, v: .5 });
```

### Named
使用 [CSS 规范中的颜色列表](https://www.w3.org/TR/css-color-4/#named-colors)
 [list of colors in the CSS spec](https://www.w3.org/TR/css-color-4/#named-colors)

```js
JyfColorCrafter("RED");
JyfColorCrafter("blanchedalmond");
JyfColorCrafter("darkblue");
```

### 接受的对象输入
### Accepted Object Input

```js
    { r: 255, g: 0, b: 0 }
    { r: 255, g: 0, b: 0, a: .5 }
    { h: 0, s: 100, l: 50 }
    { h: 0, s: 100, v: 100 }
```

## Methods

### getFormat

Returns the format used to create the JyfColorCrafter instance
```js
let color = JyfColorCrafter("red");
color.getFormat(); // "name"
color = JyfColorCrafter({r:255, g:255, b:255});
color.getFormat(); // "rgb"
```

### getOriginalInput

Returns the input passed into the constructor used to create the JyfColorCrafter instance
```js
let color = JyfColorCrafter("red");
color.getOriginalInput(); // "red"
color = JyfColorCrafter({r:255, g:255, b:255});
color.getOriginalInput(); // "{r: 255, g: 255, b: 255}"
```

### isValid

Return a boolean indicating whether the color was successfully parsed.  Note: if the color is not valid then it will act like `black` when being used with other methods.
```js
let color1 = JyfColorCrafter("red");
color1.isValid(); // true
color1.toHexString(); // "#ff0000"

let color2 = JyfColorCrafter("not a color");
color2.isValid(); // false
color2.toString(); // "#000000"
```
### getBrightness

Returns the perceived brightness of a color, from `0-255`, as defined by [Web Content Accessibility Guidelines (Version 1.0)](http://www.w3.org/TR/AERT#color-contrast).
```js
let color1 = JyfColorCrafter("#fff");
color1.getBrightness(); // 255

let color2 = JyfColorCrafter("#000");
color2.getBrightness(); // 0
```
### isLight

Return a boolean indicating whether the color's perceived brightness is light.
```js
let color1 = JyfColorCrafter("#fff");
color1.isLight(); // true

let color2 = JyfColorCrafter("#000");
color2.isLight(); // false
```
### isDark

Return a boolean indicating whether the color's perceived brightness is dark.
```js
let color1 = JyfColorCrafter("#fff");
color1.isDark(); // false

let color2 = JyfColorCrafter("#000");
color2.isDark(); // true
```
### getLuminance

Returns the perceived luminance of a color, from `0-1` as defined by [Web Content Accessibility Guidelines (Version 2.0).](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#contrast-ratiodef)
```js
let color1 = JyfColorCrafter("#fff");
color1.getLuminance(); // 1

let color2 = JyfColorCrafter("#000");
color2.getLuminance(); // 0
```
### getAlpha

Returns the alpha value of a color, from `0-1`.
```js
let color1 = JyfColorCrafter("rgba(255, 0, 0, .5)");
color1.getAlpha(); // 0.5

let color2 = JyfColorCrafter("rgb(255, 0, 0)");
color2.getAlpha(); // 1

let color3 = JyfColorCrafter("transparent");
color3.getAlpha(); // 0
```
### setAlpha

Sets the alpha value on a current color.  Accepted range is in between `0-1`.
```js
let color = JyfColorCrafter("red");
color.getAlpha(); // 1
color.setAlpha(.5);
color.getAlpha(); // .5
color.toRgbString(); // "rgba(255, 0, 0, .5)"
```
### String Representations

The following methods will return a property for the `alpha` value, which can be ignored: `toHsv`, `toHsl`, `toRgb`

### toHsv
```js
let color = JyfColorCrafter("red");
color.toHsv(); // { h: 0, s: 1, v: 1, a: 1 }
```
### toHsvString
```js
let color = JyfColorCrafter("red");
color.toHsvString(); // "hsv(0, 100%, 100%)"
color.setAlpha(0.5);
color.toHsvString(); // "hsva(0, 100%, 100%, 0.5)"
```
### toHsl
```js
let color = JyfColorCrafter("red");
color.toHsl(); // { h: 0, s: 1, l: 0.5, a: 1 }
```
### toHslString
```js
let color = JyfColorCrafter("red");
color.toHslString(); // "hsl(0, 100%, 50%)"
color.setAlpha(0.5);
color.toHslString(); // "hsla(0, 100%, 50%, 0.5)"
```
### toHex
```js
let color = JyfColorCrafter("red");
color.toHex(); // "ff0000"
```
### toHexString
```js
let color = JyfColorCrafter("red");
color.toHexString(); // "#ff0000"
```
### toHex8
```js
let color = JyfColorCrafter("red");
color.toHex8(); // "ff0000ff"
```
### toHex8String
```js
let color = JyfColorCrafter("red");
color.toHex8String(); // "#ff0000ff"
```
### toRgb
```js
let color = JyfColorCrafter("red");
color.toRgb(); // { r: 255, g: 0, b: 0, a: 1 }
```
### toRgbString
```js
let color = JyfColorCrafter("red");
color.toRgbString(); // "rgb(255, 0, 0)"
color.setAlpha(0.5);
color.toRgbString(); // "rgba(255, 0, 0, 0.5)"
```
### toPercentageRgb
```js
let color = JyfColorCrafter("red");
color.toPercentageRgb() // { r: "100%", g: "0%", b: "0%", a: 1 }
```
### toPercentageRgbString
```js
let color = JyfColorCrafter("red");
color.toPercentageRgbString(); // "rgb(100%, 0%, 0%)"
color.setAlpha(0.5);
color.toPercentageRgbString(); // "rgba(100%, 0%, 0%, 0.5)"
```
### toName
```js
let color = JyfColorCrafter("red");
color.toName(); // "red"
```
### toFilter
```
let color = JyfColorCrafter("red");
color.toFilter(); // "progid:DXImageTransform.Microsoft.gradient(startColorstr=#ffff0000,endColorstr=#ffff0000)"
```
### toString

Print to a string, depending on the input format.  You can also override this by passing one of `"rgb", "prgb", "hex6", "hex3", "hex8", "name", "hsl", "hsv"` into the function.
```js
let color1 = JyfColorCrafter("red");
color1.toString(); // "red"
color1.toString("hsv"); // "hsv(0, 100%, 100%)"

let color2 = JyfColorCrafter("rgb(255, 0, 0)");
color2.toString(); // "rgb(255, 0, 0)"
color2.setAlpha(.5);
color2.toString(); // "rgba(255, 0, 0, 0.5)"
```
### Color Modification

These methods manipulate the current color, and return it for chaining.  For instance:
```js
JyfColorCrafter("red").lighten().desaturate().toHexString() // "#f53d3d"
```
### lighten

`lighten: function(amount = 10) -> JyfColorCrafter`.  Lighten the color a given amount, from 0 to 100.  Providing 100 will always return white.
```js
JyfColorCrafter("#f00").lighten().toString(); // "#ff3333"
JyfColorCrafter("#f00").lighten(100).toString(); // "#ffffff"
```
### brighten

`brighten: function(amount = 10) -> JyfColorCrafter`.  Brighten the color a given amount, from 0 to 100.
```js
JyfColorCrafter("#f00").brighten().toString(); // "#ff1919"
```
### darken

`darken: function(amount = 10) -> JyfColorCrafter`.  Darken the color a given amount, from 0 to 100.  Providing 100 will always return black.
```js
JyfColorCrafter("#f00").darken().toString(); // "#cc0000"
JyfColorCrafter("#f00").darken(100).toString(); // "#000000"
```
### desaturate

`desaturate: function(amount = 10) -> JyfColorCrafter`.  Desaturate the color a given amount, from 0 to 100.  Providing 100 will is the same as calling `greyscale`.
```js
JyfColorCrafter("#f00").desaturate().toString(); // "#f20d0d"
JyfColorCrafter("#f00").desaturate(100).toString(); // "#808080"
```
### saturate

`saturate: function(amount = 10) -> JyfColorCrafter`.  Saturate the color a given amount, from 0 to 100.
```js
JyfColorCrafter("hsl(0, 10%, 50%)").saturate().toString(); // "hsl(0, 20%, 50%)"
```
### greyscale

`greyscale: function() -> JyfColorCrafter`.  Completely desaturates a color into greyscale.  Same as calling `desaturate(100)`.
```js
JyfColorCrafter("#f00").greyscale().toString(); // "#808080"
```
### spin

`spin: function(amount = 0) -> JyfColorCrafter`.  Spin the hue a given amount, from -360 to 360.  Calling with 0, 360, or -360 will do nothing (since it sets the hue back to what it was before).
```js
JyfColorCrafter("#f00").spin(180).toString(); // "#00ffff"
JyfColorCrafter("#f00").spin(-90).toString(); // "#7f00ff"
JyfColorCrafter("#f00").spin(90).toString(); // "#80ff00"

// spin(0) and spin(360) do nothing
JyfColorCrafter("#f00").spin(0).toString(); // "#ff0000"
JyfColorCrafter("#f00").spin(360).toString(); // "#ff0000"
```
### Color Combinations

Combination functions return an array of JyfColorCrafter objects unless otherwise noted.

### analogous

`analogous: function(, results = 6, slices = 30) -> array<JyfColorCrafter>`.
```js
let colors = JyfColorCrafter("#f00").analogous();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#ff0066", "#ff0033", "#ff0000", "#ff3300", "#ff6600" ]
```
### monochromatic

`monochromatic: function(, results = 6) -> array<JyfColorCrafter>`.
```js
let colors = JyfColorCrafter("#f00").monochromatic();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#2a0000", "#550000", "#800000", "#aa0000", "#d40000" ]
```
### splitcomplement

`splitcomplement: function() -> array<JyfColorCrafter>`.
```js
let colors = JyfColorCrafter("#f00").splitcomplement();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#ccff00", "#0066ff" ]
```
### triad

`triad: function() -> array<JyfColorCrafter>`.
```js
let colors = JyfColorCrafter("#f00").triad();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#00ff00", "#0000ff" ]
```
### tetrad

`tetrad: function() -> array<JyfColorCrafter>`.
```js
let colors = JyfColorCrafter("#f00").tetrad();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#80ff00", "#00ffff", "#7f00ff" ]

```
### complement

`complement: function() -> JyfColorCrafter`.
```js
JyfColorCrafter("#f00").complement().toHexString(); // "#00ffff"
```
## Color Utilities
```js
JyfColorCrafter.equals(color1, color2)
JyfColorCrafter.mix(color1, color2, amount = 50)
```
### random

Returns a random color.
```js
let color = JyfColorCrafter.random();
color.toRgb(); // "{r: 145, g: 40, b: 198, a: 1}"
```

### Readability

JyfColorCrafter assesses readability based on the [Web Content Accessibility Guidelines (Version 2.0)](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#contrast-ratiodef).

#### readability

`readability: function(JyfColorCrafter, JyfColorCrafter) -> Object`.
Returns the contrast ratio between two colors.
```js
JyfColorCrafter.readability("#000", "#000"); // 1
JyfColorCrafter.readability("#000", "#111"); // 1.1121078324840545
JyfColorCrafter.readability("#000", "#fff"); // 21
```
Use the values in your own calculations, or use one of the convenience functions below.

#### isReadable

`isReadable: function(JyfColorCrafter, JyfColorCrafter, Object) -> Boolean`.  Ensure that foreground and background color combinations meet WCAG guidelines. `Object` is optional, defaulting to `{level: "AA",size: "small"}`.  `level` can be `"AA"` or "AAA" and `size` can be `"small"` or `"large"`.

Here are links to read more about the [AA](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) and [AAA](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) requirements.
```js
JyfColorCrafter.isReadable("#000", "#111", {}); // false
JyfColorCrafter.isReadable("#ff0088", "#5c1a72",{level:"AA",size:"small"}); //false
JyfColorCrafter.isReadable("#ff0088", "#5c1a72",{level:"AA",size:"large"}), //true
```
#### mostReadable

`mostReadable: function(JyfColorCrafter, [JyfColorCrafter, JyfColorCrafter ...], Object) -> Boolean`.
Given a base color and a list of possible foreground or background colors for that base, returns the most readable color.
If none of the colors in the list is readable, `mostReadable` will return the better of black or white if `includeFallbackColors:true`.
```js
JyfColorCrafter.mostReadable("#000", ["#f00", "#0f0", "#00f"]).toHexString(); // "#00ff00"
JyfColorCrafter.mostReadable("#123", ["#124", "#125"],{includeFallbackColors:false}).toHexString(); // "#112255"
JyfColorCrafter.mostReadable("#123", ["#124", "#125"],{includeFallbackColors:true}).toHexString();  // "#ffffff"
JyfColorCrafter.mostReadable("#ff0088", ["#2e0c3a"],{includeFallbackColors:true,level:"AAA",size:"large"}).toHexString()   // "#2e0c3a",
JyfColorCrafter.mostReadable("#ff0088", ["#2e0c3a"],{includeFallbackColors:true,level:"AAA",size:"small"}).toHexString()   // "#000000",
```

## Common operations

### clone

`clone: function() -> JyfColorCrafter`.
Instantiate a new JyfColorCrafter object with the same color.  Any changes to the new one won't affect the old one.
```js
let color1 = JyfColorCrafter("#F00");
let color2 = color1.clone();
color2.setAlpha(.5);

color1.toString(); // "#ff0000"
color2.toString(); // "rgba(255, 0, 0, 0.5)"
```
