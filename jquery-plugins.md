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
```html
<script src="./jquery-1.11.1.js"></script>
<script src="./tabs.js"></script>
<link href="./tabs.css" rel="stylesheet" type="text/css">
```

You can download the jQuery source file from [jQuery.com](http://jquery.com/download/).

Or you can use Google's CDN to access the source code - include the script tag that they have on their site. (A quick search for Google jQuery CDN should get you there!)

You can also include a CSS-reset, to normalize the CSS that your browser comes pre-installed with.
```html
<link rel="stylesheet" type="text/css" href="http://yui.yahooapis.com/3.17.2/build/cssreset/cssreset-min.css">
```

In tabs.js, include the following code to set up our plugin:
```
$.Tabs = function (el) { ... };

$.fn.tabs = function () {
  return this.each(function () {
    new $.Tabs(this);
  });
};
```

Back in tabs.html, let's add the element that we will be calling #tabs on:
`<ul class='tabs'></ul>`

And finally, add a script tag just before the `</body>` tag, where we will
run our code after the document loads:
```html
<script>
  $(function() {
    $('.tabs').tabs();
  })
</script>
```

Now we are ready to go!

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

