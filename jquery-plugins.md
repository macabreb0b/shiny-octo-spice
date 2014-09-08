# jQuery Plugins

Let's use our knowledge of jQuery to make some plugins - or
modular bits of code that we can re-use to spiff up our websites!

## Setup
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

# Tabs
It's pretty common to want to switch content out with the use of tabs. (Think of the last time you used a [shopping website](http://www.staples.com/Paper-Mate-Sharpwriter-Mechanical-Pencils-7mm-Yellow-Barrel-Dozen/product_107250).)
The site we're working on today will let us tab back and forth to view information on different types of dog breeds. Let's make a plugin that will help us accomplish this.  

Create your HTML content:
* If you haven't already, create a `ul` with the class `tabs`.
* Below this, create a `div`, give it the id `content-tabs`.
* Inside of our div#content-tabs, make three or more divs to hold our tabs' content. Give each of these the class `tab-pane`. 
* Add a `p` tag within each, and add some text about your favorite breeds of dog. (You might find some good [dog breed info here](http://www.justdogbreeds.com/all-dog-breeds.html)!)
* Give each of the `.tab-pane` divs a unique `id` describing its content. perhaps the breed of dog will do!
* Inside of our `ul.tabs`, add as many `li` tags as there are `tab-pane`s. Add an anchor tag (`a`) inside each one. Give each of these an href that points to its corresponding fragment. (These are the ids of our `.tab-pane` elements.) Your link should look something like: `<a href='#chihuahua'>Chihuahua</a>`


# Carousel
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

