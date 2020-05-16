# Sass Media Query (v-2.0)
*-A new approach to write media queries in sass.*

*-v2.0 Support for custom media queries*

## Introduction

Hey Folks, I recently begin learning sass. Sass helps in writing CSS programmatically which helps to write reusable classes along with logical properties.

Sass documentation has given a pleasant way of writing media-queries where you can write your media queries while defining your class itself, but with this approach your CSS file might contain multiple media-queries for the same media type which in turn increase CSS code length in the file. 

This happens because sass doesn't store any complied CSS. It compiles and writes directly to the CSS file.

So I have developed a small plugin wherein you can write media queries similar to the way you used to in sass but in this scenario there will be no duplication of similar media types and also all the media queries will be present at a single location.

This helps to keep CSS code length minimal and up to the mark and also it becomes easy for non-sass CSS developers to debug the CSS.

## How Does it Work??
* The plugin contains a _media-query-config.scss_ file where the standard media-queries like sm, lg, md, xs have some fixed value, you can change as per your need.
* Using mixin `for-media()` you can pass your css for specific screen width. 
* This will create a sass-map for each breakpoints which will act like buffer. 
* Everytime you call a mixin of specific breakpoint (eg: for-sm(...)) the CSS you specify will be stored in the respective buffer map for the respective class. 
* When you will call `apply-media-css()` mixin all this buffer maps will be released and printed.

**Summary**: So all media query CSS is stored in a buffer and dumped when you call _apply-media-css()_ mixin.

## Lets use it

1. Include this line in your style.sCSS<br> 
``` @import "media-query/_media-query-config"; ```
2. Include this line in our sCSS file where you want to generate media query CSS<br> 
``` @include apply-media-CSS(); ```

#### *For the standard breakpoints:*

```
@include for-media('breakpoint_name', selector_name, (
	CSS-property1: value1,
	CSS-property2: value2,
	...
	CSS-propertyN: valueN
));
```

**Example**:
```
@include for-media('md', '.some-class', (
	display: block,
	width: 60%,
	border: 1px solid #222,
	padding: 30px,
	margin: 0 auto
));
```
#### *For screen widths other than standard breakpoints:*
```
@include for-media(screen_width, selector_name, (
	CSS-property1: value1,
	CSS-property2: value2,
	...
	CSS-propertyN: valueN
));
```

**Example**:
```
@include for-media(991px, '.some-class', (
	display: block,
	width: 60%,
	border: 1px solid #222,
	padding: 30px,
	margin: 0 auto
));
```

> This will generate media query of (max-width: 991px), for (min-width: 991px) give screen with - as prefix. (Example: for-screen(-991px, ..., (...));)

_You can refer style.scss for demo_.


#### ADD a new breakpoint constant
1. In **_media-query-config.scss**
	* Create a variable with the constant name you want. (EG: $ipad: 768px; )
	* Create a empty list like this: $media-ipad: ();
	* Save the file.
2. In **_media-query-mixins.scss**
	* There is code snippet documented in that file for adding your new breakpoint into required mixins follow those properly and save the file.

## Introducing Custom Media Query

* To use register custom media query use `add-media-custom()`.

**Syntax:**
```
	@inlcude add-media-custom('media-name', 'media-parameter');
```
**Example:**
```
	@include add-custom-media('speech', 'speech and (aspect-ratio: 11/5)');
```

* To apply css for custom media use `for-media-custom()`.
**Syntax:**
```
	@inlcude for-media-custom('media-name', selector, (
	CSS-property1: value1,
	CSS-property2: value2,
	...
	CSS-propertyN: valueN
));
```
**Example:**
```
	@include for-custom-media('speech', '.test-clas', (background: black));
```

* To print custom media query use `apply-media-custom-css()`.
* To print custom media query of specific media type use `print-custom-media-for().`
**Syntax:**
```
	@inlcude print-custom-media-for('media-name', $preserve: false);
```
**Example:**
```
	@include print-custom-media-for('speech', true);
```

> In *print-custom-media-for()*, if parameter preserve (default false) is set to true than the media type specified will be preserved and will get print when *apply-media-custom-css()* is called. 

## ChangeLog:
1. v-1.0: Introduced.
2. v-1.5: One mixin for all breakpoints constant.
3. v-1.6: Combined for-media() and for-screen() mixin & examples updated.
4. v-2.0: Support for Custom Media Query & Code Optimization.
