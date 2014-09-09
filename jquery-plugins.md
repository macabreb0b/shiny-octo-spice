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

# Corgi Tabs :dog:
It's pretty common to want to switch content out with the use of tabs. (Think of the last time you used a [shopping website](http://www.staples.com/Paper-Mate-Sharpwriter-Mechanical-Pencils-7mm-Yellow-Barrel-Dozen/product_107250).)
The site we're working on today will let us tab back and forth to view information on different types of dog breeds. Let's make a plugin that will help us accomplish this.  

Create your HTML content:

* If you haven't already, create a `ul` with the class `tabs`.
* Below this, create a `div`, give it the id `content-tabs`.
* Inside of our `div#content-tabs`, make three or more `div`s to hold our tabs' content. Give each of these the class `tab-pane`. 
* Add a `p` tag within each, and add some text about your favorite breeds of dog. (You might find some good [dog breed info here](http://www.justdogbreeds.com/all-dog-breeds.html)!)
* Give each of the `.tab-pane`s a unique `id` describing its content. perhaps the breed of dog will do!
* Inside of our `ul.tabs`, add as many `li` tags as there are `tab-pane`s. Add an anchor tag (`a`) inside each one. Give each of these an href that points to its corresponding fragment. (These are the ids of our `.tab-pane` elements.) Your link should look something like: `<a href='#chihuahua'>Chihuahua</a>`

Now open your HTML file in the browser - you should see all of your links, and all of your content! 

Let's make some decisions about how we're going to signal which tabs should be displayed. We will use jQuery to give the class 'active' to the tab that we want to see. To initialize our app so that it starts on the first tab, give the first `div.tab-pane` the class 'active.' Also give the corresponding `a` tag the class 'active.'

To display only the active content, lets add some CSS rules. In tabs.css, use selectors to add the following properties appropriately.

* All links with the class 'active' inside of something with the class 'tabs' should have `font-weight: bold;`.
* All `div`s with the class 'tab-pane' should have `display:none;`.
* All `div`s with both class 'tab-pane' and class 'active' should have `display: block;`.

Now refresh the page - you should see _only_ the information about your first dog breed, and its corresponding link should be bold. Let's set up our JavaScript file so that we can see information on other breeds!

Go to tabs.js, and let's set up the constructor function for our plugin.

* Our constructor function is `$.Tabs = function(el) {}`. In it, lets create some instance variables.
* The constructor will be passed a plain HTML element (el). Make this into a jQuery object and save it as `this.$el`.
* Get the location where our content is - pull the value of data-content-tabs from `this.$el`, make it into a jQuery object, and save it as `this.$contentTabs`.
* Get the active tab from our content tabs - save this as an ivar, making sure it's a jQuery object.

Write the prototype method that we will call when our tab links get clicked, `Tabs#clickTab`.

* Use instance variables to access the content tabs and list of links. Remove the class 'active' from all of these.
* Use `$(event.currentTarget)` to get the tab that we want to make active. Add the 'active' class to the proper `div.tab-pane` and `a` tags.
* Don't forget to prevent the link's default action, which is a page refresh.
* In the contructor, set up our click event handler by calling `this.$el.on('click', 'a', ...)`.

Refresh the page - you should have a working tab-browser!   

Those transitions are a bit harsh though - let's make it feel a little smoother.

Add some new CSS rules to `tabs.css`:

* All `div`s with both class 'tab-pane' _and_ class 'active' should have `opacity: 1;`, and a transition property for opacity.
* All `div`s with both class 'tab-pane' _and_ class 'transitioning' should have `display: block;`, `opacity: 0;`, and also a transition property for opacity.

Now let's modify our `Tabs#clickTab` method. It will handle the link classes the same way, but now on our tabs we will use the 'transitioning' class as an interim. 

* Remove class 'active' from our `$activeTab` ivar and add the class 'transitioning.'
* Set up a one-time event (you might want to lookup jQuery's #one method) that listens for the event 'transitionend.' Give this a callback that will:
    * Remove class 'transitioning' from the old active tab.
    * Add class 'transitioning' to our new active tab.
    * Use setTimeout to remove class 'transitioning' and add class 'active' to our new active tab.
    * NB: It may be helpful to keep track of whether or not the transition is currently happening, and use this to make sure that we don't call the method again mid-transition.

Good work! Call your TA over to check your work once you've got your tabs transitioning.

# Kitten Carousel :cat:
Now we will make a plugin that, when called on a list of images, will let you scroll through them carousel-style. Setup your three files in the same fashion as before, but instead of a `ul` tag, add a `div` between our `body` tags, and give it the class 'carousel.'

* Give your carousel `div` a fixed height and width, and center it in the page using `margin: 0 auto;`.
* Put another `div` inside of the carousel div. This will contain our images - give it class 'items.'
* Grab a handful of image urls from [placekitten](http://www.placekitten.com) or [placecorgi](http://placecorgi.com/). Make sure they are all large enough to fill your carousel. Put them all in `img` tags within `div.items`.
* Add two links to 'Previous' and 'Next' after `div.items`, and give them classes 'slide-right' and 'slide-left', respectively. You can add a '#' as the href attribute, or `javascript:void(0)`. ([More on this here](http://stackoverflow.com/questions/1291942/what-does-javascriptvoid0-mean)).

Now that we have our content, open your webpage. You should see all of the images stacked on top of one another.

Let's add some CSS rules to make sure we can only see one image at a time. We will follow a similar pattern to when we were making Tabs, adding and removing the class 'active' to our images.

In our CSS file:

* Give all `div`s with class 'items' that are direct children of `div`s with class 'carousel' the following properties: `overflow:hidden;`, `height: 100%;`, `width: 100%;`. Also give it `position: absolute;`. We will come back to why.
* All `img`s that are a direct child of `div`s with class 'items' that are direct descendants of `div`s with class 'carousel' should have `position:absolute;`, as well as 100% width and `top: 0;`.
    * When these images have the class 'active,' they should have the property `left: 0;`. Also give it a linear `transition` property on 'left'.
    * Give all of these images that are _not_ 'active' `display: none;`.
    * When these images have the class 'active' _and_ 'left,' they should have `left: -100%;`. Do the opposite for 'right.'
    
That should do it for now. Refresh the page - you should not see any cats, although you should see your 'Previous' and 'Next' links. Let's go to carousel.js to start writing our plugin. 

* In the constructor, take in an `el` and save it as a jQuery object.
    * Store ivars for your images and the active index.
    * Add class 'active' to the first image.
* Write a `#slide` method, that will take an integer (1 or -1) to determine the direction to slide in. This method should:
    * Update the active index.
    * Find the current active image (old item) and the one to become active (new item).
    * Give the new item classes 'active' and the direction it's sliding in ('right' or 'left').
    * Give the old item the class for the opposite direction.
    * Set an event listener on the old item for 'transitioned.' The completion callback should:
        * Remove classes 'active' and opposite direction from the old item.
* Write `#slideLeft` and `#slideRight` methods. These should just call `#slide`.

Test out your Carousel in the browser. You may have transitioning kittens! If you don't (or if they only transition half the time), you may want to look into the [setTimeout trick](http://stackoverflow.com/questions/779379/why-is-settimeoutfn-0-sometimes-useful). (Use this to group everything that comes after adding the 'active' class to the new item in #slide.)

NB: You also may want to add a 'transitioning' property on your model, to make sure that the #slide method does not fire during a transition.
