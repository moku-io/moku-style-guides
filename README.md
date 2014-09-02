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

##Dichiarazioni:

###Variables
**Always use var.**
Globals pollute the global namespace and kill your cats while you sleep.  
Always declare them at the top of the scope.  
*Remember that cycles and conditionals are **not** scoped*.  
Group variable declarations together with commas.  
```javascript
var items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';
```
Always use meaningful names, you are not a manual minifier.

###Functions
 a meno che non sia necessario usare le espressioni, usare le dichiarazioni
 // dichiarazione
 function pippo(a, b) {
 	console.log("ciao pippo");
 }
 
 // espressione
 // GOOD, in caso usate questa, anche se viene valutata a runtime è tracciabile negli stacktrace e può chiamarsi ricorsivamente
 var factorial = function factorial(number) {
   if ( number < 2 ) {
     return 1;
   }
   return number * factorial(number - 1);
 };
 // BAD (non funziona neanche)
 var factorial = function(number) {
   if ( number < 2 ) {
     return 1;
   }
   return number * factorial(number - 1);
 }; 
 
- CODICE DEL GENERE E VI TAGLIO LE GOMME DELLA MACCHINA
function q(s) {
  return document.querySelectorAll(s);
}
var i,a=[],els=q("#foo");
for(i=0;i<els.length;i++){a.push(els[i]);}

 
* TRICKS
parameter defaults:
	
	function myFunction(x, y) {
   	 y = y || 0;
	}

* SUGGERIMENTI
-usare === e !== ogni volta in cui è possibile 
-gli early return spaccano
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

*JQUERY


