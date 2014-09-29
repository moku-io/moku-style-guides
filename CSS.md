#SCSS
##Categorizing SCSS Rules
There are three types of categories:
- Base
- Layout
- Module

### Base Rules
Base rules are the defaults. They are almost exclusively single element selectors but it could include attribute selectors, pseudo-class selectors, child selectors or sibling selectors. Essentially, a base style says that wherever this element is on the page, it should look like this.
```
html, body, form { margin: 0; padding: 0; }
input[type=text] { border: 1px solid #999; }
a { color: #039; }
a:hover { color: #03C; }
```
Queste regole dovranno contenere tutte le regole base che non sono state definite tra le impostazioni di Foundation e le strutture base del SASS (mixin,funzioni, variabili).

### Layout Rules
Layout rules divide the page into sections. Layouts hold one or more modules together.
Queste regole si comporranno di più file:
- **commons.scss** dove ci saranno tutte le regole per le parti in comune da tutto il sito, ovvero: header, footer e nav principale. A questi tre elementi è stato assegnato un id: header, footer e menu. Pertanto le regole dovranno essere di tipo id-rules. Per tutti gli elementi interni si dovranno utilizzare regole di tipo class-rules.
```
#header {
  .header__logo {
  }
  .header__title {
  }
}

#menu {
}

#footer {
}
```
-**custom-page.scss** ospiterà le regole di ogni pagina riguardanti layout e le id-rules dei moduli. Le regole di layout saranno del tipo id-rules dato che ad ogni elemento del layout (div, section) è stato dato un id. Per i moduli, invece, le regole saranno sia id-rules che class-rules.
```
#home-page__primary-content {
  
}

#slider-news--weekly {
  //modulo slider-news per le notizie weekly
  .slider-news__title {
    color: pink;
  }
}
```
### Module Rules
Module rules ospita le regole di stile dei vari moduli. In questo foglio di stile i moduli dovranno essere definiti per intero, le customizzazioni varie saranno affidate alle classi che riprendono il contenuto semantico del modulo riportate all’interno del custome-page.scss relativo. In questo foglio di stile ci saranno solamente regole di tipo class-rules.
```
// module: slider-news
.slider-news {
     .slider-news__title {
          color: red;
          font-size:  2rem;
     }
     .slider-news__content {
          color: black;
          font-size: 1.3 rem;
     }
}
```
##Font-size: px at the root, rem for components, em for text elements
You still keep px size adjustments at the document level so you can make easy/efficient sweeping size changes. But then each module on the page has a font-size set in rem. Actual text elements (h1, h2, p, li, whatever), if you size them at all, are sized in em, and thus become relative to the module.
This way you can adjust font-size at a module level, which is pretty easy. The chances the type within a single module have good proportions and can scale together nicely is high. 
```
/* Base Rules */
/* Document level adjustments */
html {
  font-size: 17px;
}
@media (max-width: 900px) {
  html { font-size: 15px; }
}
@media (max-width: 400px) {
  html { font-size: 13px; }
}


/* Layout Rules*/
/* Modules will scale with document */
.header {
  font-size: 1.5rem;
}
.footer {
  font-size: 0.75rem;
}
.sidebar {
  font-size: 0.85rem;
}

/* Module Rules */
/* Type will scale with modules */
h1 {
  font-size: 3em;
}
h2 {
  font-size: 2.5em;
}
h3 {
  font-size: 2em;
}
```
## Nested selectors: the inception rule
```
$border: 1px solid #EFC6F3;
.post {
  border-radius: 3px;
  background: #FFF8FF;
  border: 1px solid $border;
  padding: 15px;
  color: #333333;
  .title {
    color: #000000;
    font-size:20px;
  }
  .alt-title {
    @extend .title;
    border-bottom:1px solid $border;
  }
}
```
The above code will output the exact same code as the code you didn't like to write when you were writing CSS because of all repetition.

Here's the output of the above Sass just so you can see how this translates to CSS.
```
.post {
  border-radius: 3px;
  background: #FFF8FF;
  border: 1px solid 1px solid #efc6f3;
  padding: 15px;
  color: #333333;
}
.post .title, .post .alt-title {
  color: #000000;
  font-size: 20px;
}
.post .alt-title {
  border-bottom: 1px solid 1px solid #efc6f3;
}
```
And so, like a child with a new toy, we begin to use this feature in -what we think- is its "max potential". But actually what's taking happening is some may call, a "CSS Selector Nightmare."

Because Sass offers you the ability to nest your selectors, and you know that having your code encapsulated is the "good way to avoid collisions with other styles", you might find yourself mimicking the DOM in your Sass (bad idea).

To prevent you from falling into this nightmare, the inception rule is **don’t go more than four levels deep.**

## Efficient CSS
- http://css-tricks.com/efficiently-rendering-css/
- https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS

## SASS
- http://sass-lang.com/guide
- http://thesassway.com/
