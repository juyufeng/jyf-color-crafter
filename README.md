# jyfColorCrafter

## 介绍
jyfColorCrafter 是一个快速的 JavaScript 库，用于颜色操作和转换。它允许多种输入形式，同时提供颜色转换和其他颜色实用函数。它没有依赖关系。
## Introduction
jyfColorCrafter is a fast JavaScript library for color manipulation and conversion. It allows multiple input formats and provides color conversion and other color utility functions. It has no dependencies.

## 在 node 中包含

`jyfColorCrafter` 可以从 npm 安装：

`jyfColorCrafter` can be installed from npm:

   -  npm install jyf-color-crafter

    然后可以在你的脚本中使用它：

```js
let jyfColorCrafter = require("jyf-color-crafter");
let color = jyfColorCrafter("red");
```
或者  or
```js
import jyfColorCrafter from "jyf-color-crafter";
let color = jyfColorCrafter("red");
```

### UMD

```html
<script type='text/javascript' src='./jyf-color-crafter.js'></script>
<script type='text/javascript'>
let color = jyfColorCrafter("red");
</script>
```

## 使用方法
## Usage

### Hex, 8-digit (RGBA) Hex
```js
jyfColorCrafter("#000");
jyfColorCrafter("000");
jyfColorCrafter("#369C");
jyfColorCrafter("369C");
jyfColorCrafter("#f0f0f6");
jyfColorCrafter("f0f0f6");
jyfColorCrafter("#f0f0f688");
jyfColorCrafter("f0f0f688");
```
### RGB, RGBA
```js
jyfColorCrafter("rgb (255, 0, 0)");
jyfColorCrafter("rgb 255 0 0");
jyfColorCrafter("rgba (255, 0, 0, .5)");
jyfColorCrafter({ r: 255, g: 0, b: 0 });
jyfColorCrafter.fromRatio({ r: 1, g: 0, b: 0 });
jyfColorCrafter.fromRatio({ r: .5, g: .5, b: .5 });
```
### HSL, HSLA
```js
jyfColorCrafter("hsl(0, 100%, 50%)");
jyfColorCrafter("hsla(0, 100%, 50%, .5)");
jyfColorCrafter("hsl(0, 100%, 50%)");
jyfColorCrafter("hsl 0 1.0 0.5");
jyfColorCrafter({ h: 0, s: 1, l: .5 });
jyfColorCrafter.fromRatio({ h: 1, s: 0, l: 0 });
jyfColorCrafter.fromRatio({ h: .5, s: .5, l: .5 });
```
### HSV, HSVA
```js
jyfColorCrafter("hsv(0, 100%, 100%)");
jyfColorCrafter("hsva(0, 100%, 100%, .5)");
jyfColorCrafter("hsv (0 100% 100%)");
jyfColorCrafter("hsv 0 1 1");
jyfColorCrafter({ h: 0, s: 100, v: 100 });
jyfColorCrafter.fromRatio({ h: 1, s: 0, v: 0 });
jyfColorCrafter.fromRatio({ h: .5, s: .5, v: .5 });
```

### Named
使用 [CSS 规范中的颜色列表](https://www.w3.org/TR/css-color-4/#named-colors)
 [list of colors in the CSS spec](https://www.w3.org/TR/css-color-4/#named-colors)

```js
jyfColorCrafter("RED");
jyfColorCrafter("blanchedalmond");
jyfColorCrafter("darkblue");
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

Returns the format used to create the jyfColorCrafter instance
```js
let color = jyfColorCrafter("red");
color.getFormat(); // "name"
color = jyfColorCrafter({r:255, g:255, b:255});
color.getFormat(); // "rgb"
```

### getOriginalInput

Returns the input passed into the constructor used to create the jyfColorCrafter instance
```js
let color = jyfColorCrafter("red");
color.getOriginalInput(); // "red"
color = jyfColorCrafter({r:255, g:255, b:255});
color.getOriginalInput(); // "{r: 255, g: 255, b: 255}"
```

### isValid

Return a boolean indicating whether the color was successfully parsed.  Note: if the color is not valid then it will act like `black` when being used with other methods.
```js
let color1 = jyfColorCrafter("red");
color1.isValid(); // true
color1.toHexString(); // "#ff0000"

let color2 = jyfColorCrafter("not a color");
color2.isValid(); // false
color2.toString(); // "#000000"
```
### getBrightness

Returns the perceived brightness of a color, from `0-255`, as defined by [Web Content Accessibility Guidelines (Version 1.0)](http://www.w3.org/TR/AERT#color-contrast).
```js
let color1 = jyfColorCrafter("#fff");
color1.getBrightness(); // 255

let color2 = jyfColorCrafter("#000");
color2.getBrightness(); // 0
```
### isLight

Return a boolean indicating whether the color's perceived brightness is light.
```js
let color1 = jyfColorCrafter("#fff");
color1.isLight(); // true

let color2 = jyfColorCrafter("#000");
color2.isLight(); // false
```
### isDark

Return a boolean indicating whether the color's perceived brightness is dark.
```js
let color1 = jyfColorCrafter("#fff");
color1.isDark(); // false

let color2 = jyfColorCrafter("#000");
color2.isDark(); // true
```
### getLuminance

Returns the perceived luminance of a color, from `0-1` as defined by [Web Content Accessibility Guidelines (Version 2.0).](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#contrast-ratiodef)
```js
let color1 = jyfColorCrafter("#fff");
color1.getLuminance(); // 1

let color2 = jyfColorCrafter("#000");
color2.getLuminance(); // 0
```
### getAlpha

Returns the alpha value of a color, from `0-1`.
```js
let color1 = jyfColorCrafter("rgba(255, 0, 0, .5)");
color1.getAlpha(); // 0.5

let color2 = jyfColorCrafter("rgb(255, 0, 0)");
color2.getAlpha(); // 1

let color3 = jyfColorCrafter("transparent");
color3.getAlpha(); // 0
```
### setAlpha

Sets the alpha value on a current color.  Accepted range is in between `0-1`.
```js
let color = jyfColorCrafter("red");
color.getAlpha(); // 1
color.setAlpha(.5);
color.getAlpha(); // .5
color.toRgbString(); // "rgba(255, 0, 0, .5)"
```
### String Representations

The following methods will return a property for the `alpha` value, which can be ignored: `toHsv`, `toHsl`, `toRgb`

### toHsv
```js
let color = jyfColorCrafter("red");
color.toHsv(); // { h: 0, s: 1, v: 1, a: 1 }
```
### toHsvString
```js
let color = jyfColorCrafter("red");
color.toHsvString(); // "hsv(0, 100%, 100%)"
color.setAlpha(0.5);
color.toHsvString(); // "hsva(0, 100%, 100%, 0.5)"
```
### toHsl
```js
let color = jyfColorCrafter("red");
color.toHsl(); // { h: 0, s: 1, l: 0.5, a: 1 }
```
### toHslString
```js
let color = jyfColorCrafter("red");
color.toHslString(); // "hsl(0, 100%, 50%)"
color.setAlpha(0.5);
color.toHslString(); // "hsla(0, 100%, 50%, 0.5)"
```
### toHex
```js
let color = jyfColorCrafter("red");
color.toHex(); // "ff0000"
```
### toHexString
```js
let color = jyfColorCrafter("red");
color.toHexString(); // "#ff0000"
```
### toHex8
```js
let color = jyfColorCrafter("red");
color.toHex8(); // "ff0000ff"
```
### toHex8String
```js
let color = jyfColorCrafter("red");
color.toHex8String(); // "#ff0000ff"
```
### toRgb
```js
let color = jyfColorCrafter("red");
color.toRgb(); // { r: 255, g: 0, b: 0, a: 1 }
```
### toRgbString
```js
let color = jyfColorCrafter("red");
color.toRgbString(); // "rgb(255, 0, 0)"
color.setAlpha(0.5);
color.toRgbString(); // "rgba(255, 0, 0, 0.5)"
```
### toPercentageRgb
```js
let color = jyfColorCrafter("red");
color.toPercentageRgb() // { r: "100%", g: "0%", b: "0%", a: 1 }
```
### toPercentageRgbString
```js
let color = jyfColorCrafter("red");
color.toPercentageRgbString(); // "rgb(100%, 0%, 0%)"
color.setAlpha(0.5);
color.toPercentageRgbString(); // "rgba(100%, 0%, 0%, 0.5)"
```
### toName
```js
let color = jyfColorCrafter("red");
color.toName(); // "red"
```
### toFilter
```
let color = jyfColorCrafter("red");
color.toFilter(); // "progid:DXImageTransform.Microsoft.gradient(startColorstr=#ffff0000,endColorstr=#ffff0000)"
```
### toString

Print to a string, depending on the input format.  You can also override this by passing one of `"rgb", "prgb", "hex6", "hex3", "hex8", "name", "hsl", "hsv"` into the function.
```js
let color1 = jyfColorCrafter("red");
color1.toString(); // "red"
color1.toString("hsv"); // "hsv(0, 100%, 100%)"

let color2 = jyfColorCrafter("rgb(255, 0, 0)");
color2.toString(); // "rgb(255, 0, 0)"
color2.setAlpha(.5);
color2.toString(); // "rgba(255, 0, 0, 0.5)"
```
### Color Modification

These methods manipulate the current color, and return it for chaining.  For instance:
```js
jyfColorCrafter("red").lighten().desaturate().toHexString() // "#f53d3d"
```
### lighten

`lighten: function(amount = 10) -> jyfColorCrafter`.  Lighten the color a given amount, from 0 to 100.  Providing 100 will always return white.
```js
jyfColorCrafter("#f00").lighten().toString(); // "#ff3333"
jyfColorCrafter("#f00").lighten(100).toString(); // "#ffffff"
```
### brighten

`brighten: function(amount = 10) -> jyfColorCrafter`.  Brighten the color a given amount, from 0 to 100.
```js
jyfColorCrafter("#f00").brighten().toString(); // "#ff1919"
```
### darken

`darken: function(amount = 10) -> jyfColorCrafter`.  Darken the color a given amount, from 0 to 100.  Providing 100 will always return black.
```js
jyfColorCrafter("#f00").darken().toString(); // "#cc0000"
jyfColorCrafter("#f00").darken(100).toString(); // "#000000"
```
### desaturate

`desaturate: function(amount = 10) -> jyfColorCrafter`.  Desaturate the color a given amount, from 0 to 100.  Providing 100 will is the same as calling `greyscale`.
```js
jyfColorCrafter("#f00").desaturate().toString(); // "#f20d0d"
jyfColorCrafter("#f00").desaturate(100).toString(); // "#808080"
```
### saturate

`saturate: function(amount = 10) -> jyfColorCrafter`.  Saturate the color a given amount, from 0 to 100.
```js
jyfColorCrafter("hsl(0, 10%, 50%)").saturate().toString(); // "hsl(0, 20%, 50%)"
```
### greyscale

`greyscale: function() -> jyfColorCrafter`.  Completely desaturates a color into greyscale.  Same as calling `desaturate(100)`.
```js
jyfColorCrafter("#f00").greyscale().toString(); // "#808080"
```
### spin

`spin: function(amount = 0) -> jyfColorCrafter`.  Spin the hue a given amount, from -360 to 360.  Calling with 0, 360, or -360 will do nothing (since it sets the hue back to what it was before).
```js
jyfColorCrafter("#f00").spin(180).toString(); // "#00ffff"
jyfColorCrafter("#f00").spin(-90).toString(); // "#7f00ff"
jyfColorCrafter("#f00").spin(90).toString(); // "#80ff00"

// spin(0) and spin(360) do nothing
jyfColorCrafter("#f00").spin(0).toString(); // "#ff0000"
jyfColorCrafter("#f00").spin(360).toString(); // "#ff0000"
```
### Color Combinations

Combination functions return an array of jyfColorCrafter objects unless otherwise noted.

### analogous

`analogous: function(, results = 6, slices = 30) -> array<jyfColorCrafter>`.
```js
let colors = jyfColorCrafter("#f00").analogous();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#ff0066", "#ff0033", "#ff0000", "#ff3300", "#ff6600" ]
```
### monochromatic

`monochromatic: function(, results = 6) -> array<jyfColorCrafter>`.
```js
let colors = jyfColorCrafter("#f00").monochromatic();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#2a0000", "#550000", "#800000", "#aa0000", "#d40000" ]
```
### splitcomplement

`splitcomplement: function() -> array<jyfColorCrafter>`.
```js
let colors = jyfColorCrafter("#f00").splitcomplement();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#ccff00", "#0066ff" ]
```
### triad

`triad: function() -> array<jyfColorCrafter>`.
```js
let colors = jyfColorCrafter("#f00").triad();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#00ff00", "#0000ff" ]
```
### tetrad

`tetrad: function() -> array<jyfColorCrafter>`.
```js
let colors = jyfColorCrafter("#f00").tetrad();

colors.map(function(t) { return t.toHexString(); }); // [ "#ff0000", "#80ff00", "#00ffff", "#7f00ff" ]

```
### complement

`complement: function() -> jyfColorCrafter`.
```js
jyfColorCrafter("#f00").complement().toHexString(); // "#00ffff"
```
## Color Utilities
```js
jyfColorCrafter.equals(color1, color2)
jyfColorCrafter.mix(color1, color2, amount = 50)
```
### random

Returns a random color.
```js
let color = jyfColorCrafter.random();
color.toRgb(); // "{r: 145, g: 40, b: 198, a: 1}"
```

### Readability

jyfColorCrafter assesses readability based on the [Web Content Accessibility Guidelines (Version 2.0)](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#contrast-ratiodef).

#### readability

`readability: function(jyfColorCrafter, jyfColorCrafter) -> Object`.
Returns the contrast ratio between two colors.
```js
jyfColorCrafter.readability("#000", "#000"); // 1
jyfColorCrafter.readability("#000", "#111"); // 1.1121078324840545
jyfColorCrafter.readability("#000", "#fff"); // 21
```
Use the values in your own calculations, or use one of the convenience functions below.

#### isReadable

`isReadable: function(jyfColorCrafter, jyfColorCrafter, Object) -> Boolean`.  Ensure that foreground and background color combinations meet WCAG guidelines. `Object` is optional, defaulting to `{level: "AA",size: "small"}`.  `level` can be `"AA"` or "AAA" and `size` can be `"small"` or `"large"`.

Here are links to read more about the [AA](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html) and [AAA](http://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast7.html) requirements.
```js
jyfColorCrafter.isReadable("#000", "#111", {}); // false
jyfColorCrafter.isReadable("#ff0088", "#5c1a72",{level:"AA",size:"small"}); //false
jyfColorCrafter.isReadable("#ff0088", "#5c1a72",{level:"AA",size:"large"}), //true
```
#### mostReadable

`mostReadable: function(jyfColorCrafter, [jyfColorCrafter, jyfColorCrafter ...], Object) -> Boolean`.
Given a base color and a list of possible foreground or background colors for that base, returns the most readable color.
If none of the colors in the list is readable, `mostReadable` will return the better of black or white if `includeFallbackColors:true`.
```js
jyfColorCrafter.mostReadable("#000", ["#f00", "#0f0", "#00f"]).toHexString(); // "#00ff00"
jyfColorCrafter.mostReadable("#123", ["#124", "#125"],{includeFallbackColors:false}).toHexString(); // "#112255"
jyfColorCrafter.mostReadable("#123", ["#124", "#125"],{includeFallbackColors:true}).toHexString();  // "#ffffff"
jyfColorCrafter.mostReadable("#ff0088", ["#2e0c3a"],{includeFallbackColors:true,level:"AAA",size:"large"}).toHexString()   // "#2e0c3a",
jyfColorCrafter.mostReadable("#ff0088", ["#2e0c3a"],{includeFallbackColors:true,level:"AAA",size:"small"}).toHexString()   // "#000000",
```

## Common operations

### clone

`clone: function() -> jyfColorCrafter`.
Instantiate a new jyfColorCrafter object with the same color.  Any changes to the new one won't affect the old one.
```js
let color1 = jyfColorCrafter("#F00");
let color2 = color1.clone();
color2.setAlpha(.5);

color1.toString(); // "#ff0000"
color2.toString(); // "rgba(255, 0, 0, 0.5)"
```
