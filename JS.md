# JavaScript
## Style
### Names
```javascript
functionNamesLikeThis;
variableNamesLikeThis;
ConstructorNamesLikeThis;
EnumNamesLikeThis;
methodNamesLikeThis;
SYMBOLIC_CONSTANTS_LIKE_THIS;
$jQueryObject;
```

###Spaces

```javascript
x = 5 + 6;        // Good
x=5+6             // Bad
```
Exception: Parentheses
```javascript
[40, 100, 1, 5]   // Good
[40,100,1,5]      // Bad
[ 40, 100, 1, 5 ]   // Bad
function myStuff(socks, pajamas) { // good

}
myStuff("striped", "lovely pajamas with bears"); // good
```

### Conditionals & Loops
Always use {} and a new line
```javascript
if (pippo) pluto(); // makes baby jesus cry

if (pippo) {
	pluto(); 		// much better
}
```
### Misc
Never end lists with commas.  
Always use double quotes: ""  
Always put ; after each row  
Use English for names and meaningful comments. (Joke comments are allowed)

##Declarations

###Variables
**Always use var.**
Globals pollute the global namespace and kill your cats while you sleep.  
Always declare them at the top of the scope.  
Remember that cycles and conditionals are **not** scoped.  
Group variable declarations together with commas.  
```javascript
var items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';
```
Always use literal syntax.
```javascript
// GOOD
var array = [],
    object = {};
// BAD
var array = new Array(),
    object = new Object();
```
Always use meaningful names, you are not a human minifier.

###Functions
If possible use standard declarations:
```javascript
function pippo(a, b) { //standard declaration
	console.log("ciao pippo");
}
```
If expressions are necessary, prefer the named version. Named function expressions are evaluated at runtime, but are tracked in stacktraces and can call themselves recursively if needed.
```javascript
// GOOD
var factorial = function factorial(number) {
	if ( number < 2 ) {
		return 1;
	}
	return number * factorial(number - 1);
};

// BAD (doesn't even work)
var factorial = function(number) {
	if ( number < 2 ) {
    	return 1;
	}
	return number * factorial(number - 1);
}; 
```

##Suggestions
###Comparisons
== and != are a mess. Use === and !== every time it's possible.

###Early returns
Early returns rule. They're efficient and easily understandable.

```javascript
// Bad:
function returnLate(foo) {
  var ret;
  if (foo) {
    ret = "foo";
  } else {
    ret = "quux";
  }
  return ret;
}

// Good:

function returnEarly(foo) {
  if (foo) {
    return "foo";
  }
  return "quux";
}
```
###Sections
Separate your code in sections.  
Add a comment to prefix each section.
```javascript
/***********
** SECTION: TOP BAR
***********/
```
Stick to it. Please.

##Good Tricks
###Parameter defaults
Always try and include parameter defaults.
This trick works nicely:
```javascript
	function myFunction(x, y) {
   	 y = y || 0;
	}
```

## Summing it up
Don't do anything stupid.
Write code like this and i'll cut your tyres:
```javascript
function q(s) {
  return document.querySelectorAll(s);
}
var i,a=[],els=q("#foo");
for(i=0;i<els.length;i++){a.push(els[i]);}
```

#jQuery
##Variables
Use $camelCase names.  
Cache them!
```javascript
var $myDiv = $("#myDiv");
```
##Selectors
As a general rule, use as few selectors as possible.  
Use ID when possible. Use a single ID selector, multiple are useless.  
When using class selectors, don't use the element type in your selector.  
```javascript
var $products = $("div.products"); // SLOW
var $products = $(".products"); // FAST
```
Avoid Excessive Specificity.  
```javascript
$(".data table.attendees td.gonzalez");
 
// Better: Drop the middle if possible.
$(".data td.gonzalez");
```
Give your Selectors a Context.
```javascript
// SLOWER because it has to traverse the whole DOM for .class
$('.class');

// FASTER because now it only looks under class-container.
$('.class', '#class-container');
```
##Events
Use only one Document Ready handler per page. It makes it easier to debug and keep track of the behavior flow. Always put it on top of the js file.  
DO NOT use anonymous functions to attach events. Anonymous functions are difficult to debug, maintain, test, or reuse.  
ALWAYS put them outside the document ready handler. I'm serious. Putting them inside it makes no fricking sense.
```javascript
$("#myLink").on("click", function(){...}); // BAD

// GOOD
function myLinkClickHandler(){...}
$("#myLink").on("click", myLinkClickHandler);
```
DO NOT use behavioral markup in HTML (JavaScript inlining). Always bind events with jQuery to be consistent so it's easier to attach and remove events dynamically.  
Use onclick and i'll punch you when you least expect it.  
```javascript
<a id="myLink" href="#" onclick="myEventHandler();">my link</a> <!-- BAD -->
$("#myLink").on("click", myEventHandler); // GOOD
```
##Chaining
Use Chaining whenever possible. If the chain grows over 3 links or gets complicated because of event assignment, use appropriate line breaks and indentation to make the code readable.
```javascript
$("#myLink")
    .addClass("bold")
    .on("click", myClickHandler)
    .on("mouseover", myMouseOverHandler)
    .show();
```
##Misc
Do not mix CSS and jQuery, always use classes, defined in your CSS and apply them using jQuery.
```javascript
$("#mydiv").css({'color':red, 'font-weight':'bold'}); // BAD
.error { 
	color: red; 
	font-weight: bold; 
} /* GOOD */
$("#mydiv").addClass("error"); // GOOD
```
Same goes for animation and transitions. Always prefer CSS if possible, resort to a polyfill if necessary.
