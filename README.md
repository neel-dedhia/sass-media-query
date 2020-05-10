# Sass Media Query (v-1.0)
*-A new approach to write media queries in sass.*

## Introduction

Hey Folks, I recently begin learning sass. Sass helps in writing CSS programmatically which helps to write reusable classes along with logical properties.

Sass documentation has given a pleasant way of writing media-queries where you can write your media queries while defining your class itself, but with this approach your CSS file might contain multiple media-queries for the same media type which in turn increase CSS code length in the file. 

This happens because sass doesn't store any complied CSS. It compiles and writes directly to the CSS file.

So I have developed a small plugin wherein you can write media queries similar to the way you used to in sass but in this scenario there will be no duplication of similar media types and also all the media queries will be present at a single location.

This helps to keep CSS code length minimal and up to the mark and also it becomes easy for non-sass CSS developers to debug the CSS.

## How Does it Work??
* The plugin contains a _media-query-config.sCSS file where the standard media-queries like sm, lg, md, xs have some fixed value, you can change as per your need.
* Calling the respective mixins you can pass CSS for the class you want. 
* This will create a sass-map for each breakpoints which will act like buffer. 
* Everytime you call a mixin of specific breakpoint (eg: for-sm(...)) the CSS you specify will be stored in the respective buffer map for the respective class. 
* When you will call apply-media-CSS() mixin all this buffer maps will be released and printed.

**Summary**: So all media query CSS is stored in s buffer and dumped when you call apply-media-CSS() mixin.


#### ADD a new breakpoint constant
1. In **_media-query-config.scss**
	* Create a variable with the constant name you want. (EG: $ipad: 768px; )
	* Create a empty list like this: $media-ipad: ();
	* Save the file.
2. In **_media-query-mixins.scss**
	* There is code snippet documented in that file for adding your new breakpoint into required mixins follow those properly and save the file.

## ChangeLog:
1. v-1.0: Introduced.
2. v-1.5: One mixin for all breakpoints constant.
