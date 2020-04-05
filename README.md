# Sass Media Query (v-1.0)
*-A new approach to write media queries in sass.*

## Introduction

Hey Folks, I recently begin learning sass. It makes css writing easy, logical & hasell free. Sass helps in writing css programtically which helps to write reusable classes alongwith logical properties.

Sass documentation has given a pleasant way of writing media-queryies where you can write your media queries while defining you class itself, but with this approach your css file might contain multiple media-queries for same media type which in turn increase css code length in the file. 

This happens because sass doesnt stores any complied css. It complies and writes directly to css file.

So I have developed a small plugin wherein you can write media queries similar to the way you used to in sass but in this scenario there will be no duplication of similar media types and also all the media queries will be present at a single location.

This helps to keep css code length minimal and upto the mark and also it becomes easy for non-sass css developers to debug the css.

## How Does it Work??
* The plugin contains a _media-query-config.scss file where the standard media-queries like sm, lg, md, xs have some fixed value, you can change as per your need.
* Calling the respective mixins you can pass css for the class you want. 
* This will create a sass-map for each breakpoints which will act like buffer. 
* Everytime you call a mixin of specific breakpoint (eg: for-sm(...)) the css you specify will be stored in the respective buffer map for the respective class. 
* When you will call apply-media-css() mixin all this buffer maps will be released and printed.

**Summary**: So all media query css is stored in s buffer and dumped when you call apply-media-css() mixin.

## Lets use it

1. Include this line in your style.scss<br> 
``` @import "media-query/_media-query-config"; ```
2. Include this line in our scss file where you want to generate media query css<br> 
``` @include apply-media-css(); ```

#### *For the standard breakpoints:*

```
@include for-{breakpoint_name}(selector_name, (
	css-property1: value1,
	css-property2: value2,
	...
	css-propertyN: valueN
));
```

**Example**:
```
@include for-md('.some-class', (
	display: block,
	width: 60%,
	border: 1px solid #222,
	padding: 30px,
	margin: 0 auto
));
```
#### *For other screen widths:*
```
@include for-screen(screen_width, selector_name, (
	css-property1: value1,
	css-property2: value2,
	...
	css-propertyN: valueN
));
```

**Example**:
```
@include for-screen(991px, '.some-class', (
	display: block,
	width: 60%,
	border: 1px solid #222,
	padding: 30px,
	margin: 0 auto
));
```

> This will generate media query of (max-width: 991px), for (min-width: 991px) give screen with - as prefix. (Example: for-screen(-991px, ..., (...));)

_You can refer style.scss for demo_.

## ChangeLog:
1. v-1.0: Introduced.
