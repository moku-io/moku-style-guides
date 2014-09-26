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
Queste regole dovranno contenere tutte le regole base che non sono state definite tra le impostazioni di Foundation.

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
-**custom-page.scss** ospiterà le regole di ogni pagina riguardanti layout e le id-rules dei moduli. 
