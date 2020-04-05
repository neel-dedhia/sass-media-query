# Sass Media Query (v-1.0)
*-A new approach to write media queries in sass.*

##Introduction

Hey Folks, I recently begin learning sass. It makes css writing easy, logical & hasell free. Sass helps in writing css programtically which helps to write reusable classes alongwith logical properties. While go through this journey one difficulty i found is regarding media queries.

Sass documentation has given a way of writing media-queryies but with that approach your css might contain multiple media-queries for same media type which in turn increase css file size. 

This happens because sass doesnt stores any complied css. It complies and writes directly to css file.

So I have developed a small plugin kind of for this media query where you can write media queries similar to the way you used to in sass but in this scenario there will be no duplication of similar media types and also all the media queries will be present at a single location.

##How Does it Work??
* My plugin contains a config file where the standard media-queries like sm, lg, md, xs have some value and you can change as per your need.
* Calling the respective mixins you can pass css for the class you want. 
* This will create a sass-map for each breakpoints which will act like buffer. 
* Everytime you call a mixin of specific breakpoint (eg: for-sm(...)) the css you specify will be stored in the respective buffer map for the respective class. 
* When you will call apply-media-css() mixin all this buffer maps will be released and printed.

**Summary**: So all media query css is stored in s buffer and dumped when you call apply-media-css() mixin.

##Lets use it

####*For the standard breakpoints:*

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
####*For other screen widths:*
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

##ChangeLog:
1. v-1.0: Introduced.
