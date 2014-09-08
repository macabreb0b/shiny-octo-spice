# jQuery Plugins

Let's use our knowledge of jQuery to make some plugins - or
modular bits of code that we can re-use to spiff up our websites!

## Tabs
For each of our plugins, create a folder and create three files for our html, JavaScript and CSS. Let's start with: 
* tabs.html
* tabs.js
* tabs.css

In tabs.html, include the following HTML boilerplate:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Cool Website</title>
  </head>
  <body>
    
  </body>
</html>
```
Between the head tags, include tags to require your js and css files, as well as jQuery.

You can download the jQuery source file from [jQuery.com](http://jquery.com/download/).

Or you can use Google's CDN to access the source code - include the script tag that they have on their site. (A quick search for Google jQuery CDN should get you there!)

You can also include a CSS-reset, to normalize the CSS that your browser comes pre-installed with.
`<link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/3.17.2/build/cssreset/cssreset-min.css">
`


## Carousel
### HTML
1. Make boilerplate HTML, JS, CSS
2. Set up carousel div, item-holder div inside
3. add links for left and right, give them appropriate, 
descriptive css classes
### CSS
1. on parent div
* fixed height and width, so that we can set the images' size
* margin: 0 auto; for centering
2. on image-holder
* position:relative;
* overflow: hidden;
* height / width 100%
### JavaScript

