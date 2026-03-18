
# CSS — Learning Objectives
## Selectors, properties, and values

CSS is made of **rules** that follow this structure:

```css
selector {
  property: value;
}
```

### Selectors — target HTML elements
```css
/* Element selector */
p { color: red; }

/* Class selector */
.card { background: white; }

/* ID selector */
#header { height: 80px; }

/* Attribute selector */
input[type="text"] { border: 1px solid gray; }

/* Descendant selector */
nav a { text-decoration: none; }

/* Child selector */
ul > li { list-style: none; }

/* Pseudo-class */
a:hover { color: blue; }

/* Pseudo-element */
p::first-line { font-weight: bold; }
```

### Properties and values
```css
/* Typography */
font-size: 16px;
font-family: Arial, sans-serif;
font-weight: bold;
color: #333333;

/* Box model */
margin: 10px;
padding: 20px;
border: 1px solid black;
width: 100%;
height: auto;

/* Display */
display: flex;
position: relative;
```

---

## The difference between block and inline styling

| | Block | Inline |
|---|-------|--------|
| Takes up | Full width of parent | Only as wide as content |
| Starts on | New line | Same line as other elements |
| Respects width/height | ✅ Yes | ❌ No |
| Examples | `<div>`, `<p>`, `<h1>`, `<section>` | `<span>`, `<a>`, `<strong>`, `<em>` |

```css
/* Force an element to be block */
span { display: block; }

/* Force an element to be inline */
div { display: inline; }

/* Block + inline hybrid */
span { display: inline-block; } /* respects width/height but stays inline */
```

---

## How to ensure consistency across all browsers (CSS reset)

Different browsers apply their own default styles — CSS reset removes them so you start from a clean base.

### Option 1 — Simple reset
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

### Option 2 — Normalize.css
Instead of removing all styles, **normalize.css** makes default styles consistent across browsers without removing useful defaults. Import it before your own CSS:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.min.css" />
<link rel="stylesheet" href="styles.css" />
```

> Always apply the reset/normalize **before** your own styles.

---

## How to setup CSS variables

CSS variables (custom properties) allow you to store values and reuse them throughout your stylesheet.

```css
/* Define variables in :root (global scope) */
:root {
  --color-primary: #d73953;
  --color-secondary: #0096a2;
  --color-text: #333333;
  --font-size-base: 16px;
  --spacing-small: 8px;
  --spacing-medium: 16px;
  --spacing-large: 32px;
}

/* Use variables with var() */
body {
  color: var(--color-text);
  font-size: var(--font-size-base);
}

h1 {
  color: var(--color-primary);
  margin-bottom: var(--spacing-large);
}

/* Fallback value if variable is not defined */
p {
  color: var(--color-text, black);
}
```

---

## The differences between inline, embedded and external CSS

### 1. Inline CSS
Applied directly to a single HTML element using the `style` attribute.
```html
<p style="color: red; font-size: 18px;">This is red text.</p>
```
- ✅ Quick for one-off overrides
- ❌ Not reusable, hard to maintain, highest specificity

### 2. Embedded CSS (Internal)
Written inside a `<style>` tag in the `<head>` of the HTML file.
```html
<head>
  <style>
    p {
      color: red;
      font-size: 18px;
    }
  </style>
</head>
```
- ✅ Good for single-page styling
- ❌ Not reusable across multiple pages

### 3. External CSS
Written in a separate `.css` file and linked with `<link>`.
```html
<head>
  <link rel="stylesheet" href="styles.css" />
</head>
```
- ✅ Reusable across all pages
- ✅ Browser can cache the file
- ✅ Best practice for any real project

| | Inline | Embedded | External |
|---|--------|----------|---------|
| Location | Inside HTML tag | `<style>` in `<head>` | Separate `.css` file |
| Reusable | ❌ No | ❌ One page only | ✅ All pages |
| Maintainability | ❌ Poor | 🟡 Medium | ✅ Best |
| Performance | ❌ Poor | 🟡 Medium | ✅ Best (cached) |

---

## How grid systems work (with floats)

Before Flexbox and Grid, layouts were built using **floats**. The idea is to float columns side by side.

```css
/* Container clears the floats */
.row::after {
  content: "";
  display: table;
  clear: both;
}

/* Columns float side by side */
.col-1-2 {
  float: left;
  width: 50%;
}

.col-1-3 {
  float: left;
  width: 33.33%;
}

.col-1-4 {
  float: left;
  width: 25%;
}
```

```html
<div class="row">
  <div class="col-1-2">Left column</div>
  <div class="col-1-2">Right column</div>
</div>
```

> ⚠️ Float-based grids are legacy. Modern layouts use **Flexbox** or **CSS Grid**. But you need to understand floats for older codebases.

---

## The difference between icon webfonts and SVG icons

### Icon Webfonts (e.g. Font Awesome)
Icons are treated as **font characters** — they scale with font-size and are styled with CSS text properties.

```html
<i class="fa fa-home"></i>
```

```css
.fa-home {
  color: red;
  font-size: 24px;
}
```

### SVG Icons
Icons are actual **vector graphics** embedded in HTML or linked as image files.

```html
<!-- Inline SVG -->
<svg width="24" height="24" viewBox="0 0 24 24">
  <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/>
</svg>
```

| | Icon Webfonts | SVG Icons |
|---|--------------|-----------|
| Format | Font/text | Vector graphic |
| Styling | CSS text properties | CSS + SVG attributes |
| Accessibility | ❌ Poor (screen readers skip) | ✅ Better (can add `aria-label`) |
| Performance | 🟡 Loads entire font file | ✅ Only loads what you use |
| Multi-color | ❌ One color only | ✅ Multiple colors possible |
| Recommendation | Legacy | ✅ Preferred today |

---

## The difference between pseudo-classes and pseudo-elements

### Pseudo-classes — target an element's **state**
Use a single colon `:`.

```css
a:hover        { color: blue; }       /* mouse over */
a:visited      { color: purple; }     /* already visited */
input:focus    { border: 2px solid blue; } /* focused input */
li:first-child { font-weight: bold; } /* first item in list */
li:last-child  { margin: 0; }         /* last item in list */
li:nth-child(2){ color: red; }        /* second item */
p:not(.intro)  { font-size: 14px; }   /* all p except .intro */
```

### Pseudo-elements — target a **part** of an element
Use double colon `::`.

```css
p::first-line   { font-weight: bold; }   /* first line of text */
p::first-letter { font-size: 2em; }      /* first letter (drop cap) */
div::before     { content: "→ "; }       /* insert content before */
div::after      { content: " ←"; }       /* insert content after */
::selection     { background: yellow; }  /* highlighted text */
```

| | Pseudo-class | Pseudo-element |
|---|-------------|----------------|
| Syntax | `:hover`, `:focus` | `::before`, `::after` |
| Targets | State of an element | A part of an element |
| Example | Button when hovered | First letter of a paragraph |

---

## How to make background gradients

### Linear gradient
```css
/* Direction + colors */
background: linear-gradient(to right, #d73953, #0096a2);

/* With angle */
background: linear-gradient(45deg, #d73953, #0096a2);

/* Multiple color stops */
background: linear-gradient(to bottom, #d73953 0%, #ffffff 50%, #0096a2 100%);
```

### Radial gradient
```css
/* Circle from center */
background: radial-gradient(circle, #d73953, #0096a2);

/* Ellipse with stops */
background: radial-gradient(ellipse at center, #d73953 0%, #0096a2 100%);
```

### Conic gradient
```css
background: conic-gradient(#d73953, #0096a2, #d73953);
```

---

## How to animate elements in CSS

### Transitions — smooth change between states
```css
.button {
  background-color: #d73953;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: #0096a2;
}
```

Transition syntax: `property duration timing-function delay`

```css
transition: all 0.3s ease-in-out;
transition: background-color 0.5s linear 0.2s;
```

### Animations with `@keyframes`
```css
/* Define the animation */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Apply the animation */
.card {
  animation: fadeIn 0.5s ease forwards;
}
```

Animation properties:
```css
animation-name: fadeIn;
animation-duration: 0.5s;
animation-timing-function: ease;
animation-delay: 0.2s;
animation-iteration-count: infinite; /* or a number */
animation-direction: alternate;
animation-fill-mode: forwards;

/* Shorthand */
animation: fadeIn 0.5s ease 0.2s infinite alternate forwards;
```

---

## How to transform (2D, 3D) elements

### 2D Transforms
```css
/* Move element */
transform: translate(50px, 20px);
transform: translateX(50px);
transform: translateY(20px);

/* Scale element */
transform: scale(1.5);        /* 150% size */
transform: scaleX(2);         /* double width */

/* Rotate element */
transform: rotate(45deg);

/* Skew element */
transform: skew(10deg, 5deg);

/* Combine multiple transforms */
transform: translate(50px, 0) rotate(45deg) scale(1.2);
```

### 3D Transforms
```css
/* Enable 3D space on the parent */
.container {
  perspective: 1000px;
}

/* 3D rotation */
.card {
  transform: rotateX(45deg);  /* flip on X axis */
  transform: rotateY(45deg);  /* flip on Y axis */
  transform: rotateZ(45deg);  /* same as 2D rotate */
}

/* Move on Z axis (closer/farther) */
.card {
  transform: translateZ(100px);
}

/* Full 3D card flip effect */
.card {
  transform-style: preserve-3d;
  transition: transform 0.6s;
}
.card:hover {
  transform: rotateY(180deg);
}
```

---

## What vendor prefixes are

Vendor prefixes are browser-specific prefixes added to CSS properties that are experimental or not yet standardized. They allow browsers to implement new features before they become official standards.

```css
/* Vendor prefixes for a CSS property */
-webkit-transform: rotate(45deg);  /* Chrome, Safari, newer Opera */
-moz-transform: rotate(45deg);     /* Firefox */
-ms-transform: rotate(45deg);      /* Internet Explorer */
-o-transform: rotate(45deg);       /* Older Opera */
transform: rotate(45deg);          /* Standard — always add last */
```

| Prefix | Browser |
|--------|---------|
| `-webkit-` | Chrome, Safari, newer Opera, Edge |
| `-moz-` | Firefox |
| `-ms-` | Internet Explorer / Edge (old) |
| `-o-` | Old Opera |

```css
/* Example: gradient with prefixes */
background: -webkit-linear-gradient(to right, #d73953, #0096a2);
background: -moz-linear-gradient(to right, #d73953, #0096a2);
background: -ms-linear-gradient(to right, #d73953, #0096a2);
background: linear-gradient(to right, #d73953, #0096a2); /* always last */
```

> Today, most modern CSS properties don't need vendor prefixes anymore. Tools like **Autoprefixer** can add them automatically when needed.


---
---

## CSS Quiz Answers
### Question #0
- [ ] Black (default value)  
- [x] #FF0000  
- [ ] #00FF00  
- [ ] #0000FF  

**Explanation:**  
A direct selector `h1` applies explicitly to the `<h1>` element. No competing rule → color is `#FF0000`.

---

### Question #1
- [ ] Black (default value)  
- [x] #FF0000  
- [ ] #00FF00  
- [ ] #0000FF  

**Explanation:**  
The grouped selector `h1, h2` includes `<h1>`, so the rule applies directly → `#FF0000`.

---

### Question #2
- [x] Black (default value)  
- [ ] #FF0000  
- [ ] #00FF00  
- [ ] #0000FF  

**Explanation:**  
Selector `h1.title` targets `<h1 class="title">`. The `<h1>` has no class → rule does not apply → default black.

---

### Question #3
- [ ] Black (default value)  
- [ ] #FF0000  
- [x] #00FF00  
- [ ] #0000FF  

**Explanation:**  
`color` is inherited. `body { color: #00FF00; }` propagates to `<h1>` → green.

---

### Question #4
- [ ] Black (default value)  
- [x] #FF0000  
- [ ] #00FF00  
- [ ] #0000FF  

**Explanation:**  
Both rules apply, but `h1` is more specific than inherited `body` → `#FF0000`.

---

### Question #5
- [ ] Black (default value)  
- [ ] #FF0000  
- [x] #00FF00  
- [ ] #0000FF  

**Explanation:**  
`body h1` has higher specificity than `h1` → overrides → `#00FF00`.

---

### Question #6
What’s the final color text of <h1> in this code?
```css
h1 {
    color: #FF0000;
}
h1.title {
    color: #00FF00;
}
body h1 {
    color: #0000FF;
}


Hello
```

**Algun error**
Holberton marca que es #00FF00
- [ ] Black (default value)  
- [ ] #FF0000  
- [ ] #00FF00  
- [x] #0000FF  

**Explanation:**  
Matching selectors:
- `h1` → low specificity  
- `body h1` → higher specificity  
- `h1.title` → not applied  

Highest valid specificity → `body h1` → `#0000FF`.

---

### Question #7
- [ ] Black (default value)  
- [x] #FF0000  
- [ ] #00FF00  
- [ ] #0000FF  

**Explanation:**  
Selectors:
- `body > h1.title` → most specific (class + direct child)
- `h1.title`
- `body h1`

Assuming the `<h1>` has class `title`, the most specific selector wins → `#FF0000`.
-   El operador > en CSS es un combinador de hijo directo (child combinator).
    +   Selecciona solo los elementos que son hijos directos de otro elemento, no descendientes más profundos.
Esto aplica estilos únicamente a los <p> que están directamente dentro de un <div>:
```css
div > p {
  color: red;
}
```


---

### Question #8
- [x] Between the inside content and the border of the element  
- [ ] Between the border of the element and external elements  

**Explanation:**  
`padding` = inner spacing (content → border).

---

### Question #9
- [ ] Between the inside content and the border  
- [x] Between the border and external elements  

**Explanation:**  
`margin` = outer spacing (element → others).

---

### Question #10
- [ ] the element position will be relative to its normal position  
- [ ] the element position will be relative to the nearest positioned ancestor element  
- [ ] the element position will be based on the user’s scroll position  
- [x] the element position will be relative to the viewport  

**Explanation:**  
`position: fixed` anchors the element to the viewport.

---

### Question #11
- [ ] the element position will be relative to its normal position  
- [x] the element position will be relative to the nearest positioned ancestor element  
- [ ] the element position will be based on the user’s scroll position  
- [ ] the element position will be relative to the viewport  

**Explanation:**  
`position: absolute` uses the closest ancestor with `position` defined.

---

### Question #12
- [ ] z-index is defining the left position of an element  
- [x] z-index is defining the stack position of an element (from front to background)  
- [ ] z-index is defining the SEO indexing position  

**Explanation:**  
Controls stacking order (z-axis).

---

### Question #13
What’s the impact of overflow-y: auto on an element?  
- [ ] the element allows horizontal scrolling if the content is too large  
- [x] the element allows vertical scrolling if the content is too long  
- [ ] the element allows vertical and horizontal scrolling if the content is too long/large  
- [ ] the element doesn’t allow vertical and horizontal scrolling if the content is too long/large  
- [ ] no impact on the element  

**Explanation:**  
`overflow-y: auto` enables vertical scrolling only when needed.

---

### Question #14
What’s the `font-size` in pixel of an element `p.my_class`?
```css
p {
    font-size: 12px;
}
p.my_class {
    color: #FF0000;
}
```
- [ ] 10px  
- [x] 12px  
- [ ] 16px  
- [ ] 20px  

**Explanation:**  
No override of `font-size` → stays `12px`.

---

### Question #15
What’s the `font-size` in pixel of an element `p.my_class`?
```css
p {
    font-size: 12px;
}
p.my_class {
    font-size: 1em;
}
```
- [ ] 10px  
- [x] 12px  
- [ ] 14px  
- [ ] 16px  

**Explanation:**  
`1em = parent size` → 12px.

---

### Question #16
What’s the font-size in pixel of an element p.my_class?
```css
p {
    font-size: 12px;
}
p.my_class {
    font-size: 1.5em;
}
```
- [ ] 10px  
- [ ] 12px  
- [ ] 16px  
- [x] 18px  
- [ ] 20px  
- [ ] 24px  

**Explanation:**  
`1.5 × 12px = 18px`.

---

### Question #17
What’s the `font-size` in pixel of an element `p.my_class`?
```css
p {
    font-size: 12px;
}
p.my_class {
    font-size: 0.25em;
}
```
- [x] 3px  
- [ ] 4px  
- [ ] 6px  
- [ ] 10px  

**Explanation:**  
`0.25 × 12px = 3px`.

---

### Question #18
What’s the `font-size` in pixel of an element `p.my_class` if the default `p font-size` is 16px?
```css
p {
    font-size: 12px;
}
p.my_class {
    font-size: 0.25rem;
}
```
- [ ] 3px  
- [x] 4px  
- [ ] 6px  
- [ ] 10px  

**Explanation:**  
`0.25 × 16px (root) = 4px`.

---

### Question #19
What’s the font-size in pixel of an element p.my_class if the default p font-size is 16px?
```css
p {
    font-size: 12px;
}
p.my_class {
    font-size: 2.25rem;
}
```
- [ ] 12px  
- [ ] 16px  
- [ ] 20px  
- [ ] 27px  
- [x] 36px  
- [ ] 43px  
- [ ] 64px  

**Explanation:**  
`2.25 × 16px = 36px`.

---

### Question #20
What’s the font-size in pixel of an element p.my_class if the default p font-size is 16px?
```css
p {
    font-size: 75%;
}
p.my_class {
    font-size: 2.25em;
}
```
- [ ] 12px  
- [ ] 16px  
- [ ] 20px  
- [ ] 25px  
- [x] 27px  
- [ ] 30px  
- [ ] 36px  

**Explanation:**  
- `75% of 16px = 12px`  
- `2.25 × 12px = 27px`

---
---

# Exercises

---

##  1. Effortless transitions when scrolling

`styles/1-style.css`
```css
/* Smooth scrolling on the whole document */
html {
    scroll-behavior: smooth;
}
```

---

##  2. Do you know your color values?

`styles/2-style.css`
```css
/* Customizations for the whole document */
html {
  scroll-behavior: smooth;
}

/* Base styles for body and anchors */
body {
  color: #161616;
}

a {
  color: #161616;
}

/* Utility class to hide elements */
.visually-hidden {
  display: none;
}

/* Color accents for specific categories and taglines */
.card-category {
  color: #D73953;
}

.section-tagline {
  color: #D73953;
}

```

---

##  3. Reuse and repeat. A programmer's life should be simple with variables

`styles/3-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
}

/* Global styles */
html {
  scroll-behavior: smooth;
}

body {
  color: var(--text-color);
}

a {
  color: var(--text-color);
}

.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-tagline {
  color: var(--color-primary);
}
```
**Logica**
1. **El selector `:root`:** 
Representa la etiqueta <html>, pero tiene mayor especificidad. Es el lugar estándar para declarar variables globales porque garantiza que cualquier elemento del documento pueda acceder a ellas.

2. **Sintaxis de variables:**
- Se declaran con dos guiones: `--nombre-variable`.
- Se usan con la función: var(`--nombre-variable`).

3. **Variables anidadas:** 
Fíjate en `--text-color: var(--color-black);`. Esto es muy útil porque si mañana decides que el texto debe ser un gris oscuro en lugar de negro puro, solo cambias la referencia ahí.

4. **Mantenimiento:** 
Ahora, si el cliente de Techium te pide cambiar el rojo por azul, solo cambias el valor de `--color-primary` una vez, en lugar de buscar en 50 archivos.

---

##  4. Variables for storing certain font types

`styles/4-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Helvetica Neue", Helvetica, Arial, sans-serif;
}

/* Global styles */
html {
  scroll-behavior: smooth;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
}

a {
  color: var(--text-color);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-tagline {
  color: var(--color-primary);
}
```
**logica**
1. **Font Stack (Pila de fuentes)**: Siempre terminamos con una fuente genérica como `sans-serif`.  
Esto es un "seguro de vida": si el navegador del usuario no tiene Helvetica, usará Arial, y si no tiene ninguna, usará la fuente de palo seco que tenga por defecto.

2. **Comillas en las fuentes**: Las fuentes que tienen espacios en su nombre, como `"Helvetica Neue"`, deben ir obligatoriamente entre comillas para que el navegador las reconozca correctamente.

3. **Selector de encabezados**: Al usar `h1, h2, h3, h4, h5, h6`, aplicamos el estilo a todos los niveles de una sola vez, manteniendo la consistencia visual en todo el documento.

---

##  5. Variables for the font size

`styles/5-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%; /* Reset to 10px */
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
}

a {
  color: var(--text-color);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-tagline {
  color: var(--color-primary);
}
```
**Logica**
Por defecto, la mayoría de los navegadores tienen un tamaño de fuente de 16px.
- Si calculas 16 * 0.625, el resultado es **10px**.
- Al establecer el `html` a 62.5%, ahora `1rem` equivale exactamente a **10px**.
Esto hace que tus variables sean muy fáciles de leer:
- `1.2rem` = 12px
- `1.6rem` = 16px (el tamaño estándar que tendrá el body)
- `4.8rem` = 48px
---

##  6. Variables for the font-weight

`styles/6-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
}

a {
  color: var(--text-color);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-tagline {
  color: var(--color-primary);
}
```
**Logica**
1.  Valores Numéricos: En CSS, el font-weight suele usar valores de 100 a 900.
- 400 equivale a `normal` o `regular`.
- 700 equivale a `bold`.

2.  Jerarquía Visual: Al aplicar el peso 700 a todos los encabezados (`h1-h6`), nos aseguramos de que la estructura del documento sea clara para el usuario, diferenciando los títulos del texto corrido del `body`.

3.  Herencia: Al definir el peso en el `body`, todos los elementos (párrafos, listas, etc.) heredarán el peso 400 automáticamente, a menos que especifiquemos lo contrario.

---

##  7. Integrating Google Fonts into the CSS file

`styles/7-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  
  /* Typography Update */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
}

a {
  color: var(--text-color);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-tagline {
  color: var(--color-primary);
}
```

---

##  8. Defining line heights

`styles/8-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  /* heights */
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  /* minimum heights */
  line-height: var(--line-height-base);
}

a {
  color: var(--text-color);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-tagline {
  color: var(--color-primary);
}

```
### ¿Por qué no usamos unidades (px/rem) en line-height?
Fíjate que los valores son números puros (1.2, 1.5, 1.8) sin `px` ni `rem`.

- Valores sin unidad: 
  + Son multiplicadores del font-size actual. 
  + Si un párrafo tiene 16px y `line-height: 1.5`, el espacio total de la línea será de 24px.

- Ventaja: 
  + Si cambias el tamaño de la fuente en un elemento hijo, la altura de línea se ajusta automáticamente de forma proporcional. 
  + Es la mejor práctica en CSS moderno.

---

##  9. Links are decorated by default, time to remove them

`styles/9-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Style */
a {
  color: var(--text-color);
  text-decoration: none;
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-tagline {
  color: var(--color-primary);
}
```
### ¿Qué hace `text-decoration: none`?
La propiedad `text-decoration` controla líneas decorativas como el subrayado (`underline`), tachado (`line-through`) o líneas superiores (`overline`).

- Comportamiento por defecto: Los enlaces vienen con `underline`.

- Resultado: Al ponerlo en `none`, el texto del enlace se ve limpio, como un texto normal, pero manteniendo su funcionalidad de clic. Esto es vital para que los botones y el menú de Techium se vean profesionales.
---

##  10. Centering the section titles

`styles/10-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

a {
  color: var(--text-color);
  text-decoration: none;
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* New declaration placed exactly above section-tagline */
.section-header {
  text-align: var(--section-header-align);
}

.section-tagline {
  color: var(--color-primary);
}
```
**Logica**
1. Alineación de texto: 
- La propiedad `text-align` se aplica al contenedor (`.section-header`) para alinear todos los elementos de texto que tenga dentro (como el `h2` del título y la `p` de la descripción o tagline).

2. Uso de Variables: 
- Nuevamente, en lugar de escribir `center` directamente, usamos `var(--section-header-align)`. 
- Esto permite que si más adelante decides que todo el sitio debe estar alineado a la izquierda, solo cambias una palabra en el `:root`.

3. Orden del código: 
- La tarea pide específicamente colocar la declaración de `.section-header` justo arriba de `.section-tagline`. 
- Mantener este orden ayuda a que el CSS sea más fácil de leer, ya que agrupas los estilos de las secciones en un mismo bloque.

---

##  11. Add more styles to the section tagline

`styles/11-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

a {
  color: var(--text-color);
  text-decoration: none;
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-header {
  text-align: var(--section-header-align);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}
```
**Logica**
1. **Jerarquía Visual**: Al usar la fuente de títulos (`Raleway`) y el peso bold (700) en el tagline, logramos que, aunque sea un texto pequeño, tenga la fuerza visual de un encabezado.

2. **`text-transform: uppercase`**: Esta es una técnica muy usada en diseño "branding" para que las etiquetas o subtítulos se vean más ordenados y profesionales.

3. **Consistencia**: Al seguir usando variables, si el diseño de Techium cambia a minúsculas en el futuro, solo tendrías que tocar una línea en el `:root`.
---

##  12. Adding more styling to the section title

`styles/12-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

a {
  color: var(--text-color);
  text-decoration: none;
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-header {
  text-align: var(--section-header-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}
```
**Logica**
1.  **Manejo de Márgenes**: Al establecer el `margin` en 0, eliminamos el espacio que los navegadores ponen por defecto a los encabezados (`h2`). Esto nos permite controlar el espaciado de forma manual y precisa más adelante.

2.  **Impacto del Tamaño**: Usar `4.8rem` es un cambio drástico que asegura que el usuario sepa exactamente en qué sección se encuentra.

3.  **Orden de Declaración**: Fíjate que ahora tenemos un bloque lógico de secciones:
- `.section-header` (Alineación)
- `.section-title` (El título grande)
- `.section-tagline` (El subtítulo en rojo/mayúsculas)
---

##  13. Pseudo Classes

`styles/13-style.css`
```css
/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-header {
  text-align: var(--section-header-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}
```
**Logica**
1.  **Selector de atributo `a[href]`**: Al usar los corchetes, nos aseguramos de que el estilo solo se aplique a los enlaces que realmente tienen una dirección (`href`). Si usas una etiqueta <a> como un ancla vacía, no se verá afectada.

2.  **Estado `:visited`**: Ayuda al usuario a saber qué páginas ya ha consultado. Aquí usamos `font-style: italic`.

3.  **Estado `:hover`**: Cuando el usuario pasa el cursor, el subrayado vuelve a aparecer (`text-decoration: underline`).

4.  **Estado `:active`**: Se activa en el milisegundo en que el usuario hace clic. El fondo gris claro (`--color-light-grey`) da una sensación de "botón presionado".
---

##  14. Resetting the CSS stylesheet for browser consistency

`styles/14-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-header {
  text-align: var(--section-header-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}

```

---
**Logica**
### ¿Por qué Normalize debe ir arriba del todo?
El CSS se lee en "cascada" (de arriba hacia abajo). Al poner Normalize al principio:
1.  Reseteas los errores y diferencias de los navegadores primero.
2.  Tus estilos personalizados (como font-size: 62.5%) se aplican después, sobrescribiendo cualquier valor de Normalize que necesites ajustar. Si lo pusieras al revés, Normalize podría "borrar" tus estilos personalizados.

##  15. Add universal box-sizing

`styles/15-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* Task 15: Universal Box Sizing */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-header {
  text-align: var(--section-header-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}

```
**Logica**
1.  El selector universal (*): Esta regla le dice al navegador: "Aplica esto a absolutamente todas las etiquetas HTML del sitio".

2.  Pseudo-elementos (:before, :after): También incluimos a los elementos generados por CSS, para que nada se escape de esta lógica.

3.  border-box: Cambiamos el modelo de caja de content-box (el estándar antiguo) a border-box.

### ¿Por qué es esto vital para Techium?
Como vas a trabajar con columnas (clases como col-1-3), necesitas que si una columna ocupa el 33%, siga ocupando el 33% aunque le pongas un margen interno o un borde. Sin esta regla, las columnas se "romperían" y se irían hacia abajo.

---

##  16. Styling the container

`styles/16-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

.section-header {
  text-align: var(--section-header-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}

/* Task 16: Styling the container */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

```
**Logica**
1.  **`width: 960px`:** 
- Establece un ancho fijo. 
- 960px es un estándar clásico en diseño web porque es divisible por muchas columnas (12, 16, etc.), lo que facilita la maquetación.

2.  **`margin-left: auto` y `margin-right: auto`:** 
- Esta es la "fórmula mágica" en CSS para centrar un elemento de bloque. 
-Al decirle al navegador que calcule automáticamente el espacio a ambos lados, el contenedor se queda perfectamente en medio de la pantalla.
---

##  17. Adding padding to sections

`styles/17-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-padding: 5rem 0;
  --section-header-padding: 0 0 3rem;
  --section-body-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --footer-padding: 5rem 0 1rem;
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* New section declaration before section-header */
.section {
  padding: var(--section-padding);
}

.section-header {
  text-align: var(--section-header-align);
  padding: var(--section-header-padding); /* Added padding */
}

/* New declarations following section-header */
.section-body {
  padding: var(--section-body-padding);
}

.section-footer {
  padding: var(--section-footer-padding);
  text-align: var(--section-footer-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}

.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

/* New footer declaration at the end */
.footer {
  padding: var(--footer-padding);
}

```
**Logica**
1.  Shorthand de Padding: Cuando usamos `5rem 0`, estamos diciendo: `5rem` arriba y abajo, y `0` a los lados. Esto crea ese espacio elegante entre secciones sin afectar el ancho del contenido.

2.  Estructura de la Sección: Ahora cada sección de Techium tiene una anatomía clara:
- `.section`: El contenedor general con espacio arriba/abajo.
- `.section-header`: Espacio para el título y tagline.
- `.section-body`: Donde irá el contenido principal.
- `.section-footer`: Para botones de "Ver más" o enlaces finales, centrados gracias a `section-footer-align`.

3.  Orden de las reglas: He movido `.section` justo arriba de `.section-header` y he añadido `.section-body` y `.section-footer `inmediatamente después, tal como dictan las instrucciones.

---

##  18. Customizing the navbar

`styles/18-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-padding: 5rem 0;
  --section-header-padding: 0 0 3rem;
  --section-body-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --footer-padding: 5rem 0 1rem;
  /* Task 18: Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);
}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Navbar Styles */
.navbar-menu {
  float: right;
}

.nav {
  margin: 0;
  padding: 0;
  list-style: none;
  text-align: center;
}

.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}

.nav .nav-link {
  display: block;
  padding: 0.5rem 1rem; /* Half of root (0.5rem) and equal to root (1rem) */
}

.nav .nav-link:hover {
  color: var(--nav-item-link-hover);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* New section declaration before section-header */
.section {
  padding: var(--section-padding);
}

.section-header {
  text-align: var(--section-header-align);
  padding: var(--section-header-padding); /* Added padding */
}

/* New declarations following section-header */
.section-body {
  padding: var(--section-body-padding);
}

.section-footer {
  padding: var(--section-footer-padding);
  text-align: var(--section-footer-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
}

.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

/* New footer declaration at the end */
.footer {
  padding: var(--footer-padding);
}

```
**Logica**
1.  Cálculo de Unidades (rem):
- El "root element" es de 10px (gracias a nuestro 62.5%).
- letter-spacing: 4% de 10px = 0.4px o 0.04rem.
- padding: 0.5rem 1rem: Esto crea un área de clic cómoda. Arriba y abajo (5px) y a los lados (10px).

2.  display: inline-block: Es lo que permite que los ítems del menú (li) se pongan en fila en lugar de uno debajo del otro, pero que sigan respetando márgenes y paddings.

3.  float: right: Empuja todo el menú a la derecha de la navbar, dejando espacio (probablemente) para un logo a la izquierda.

4.  list-style: none: Vital para quitar los "puntos" (bullets) de la lista desordenada del menú.

---

##  19. Grid styling and custom variables

`styles/19-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-padding: 5rem 0;
  --section-header-padding: 0 0 3rem;
  --section-body-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-tagline-margin: 0;
  --footer-padding: 5rem 0 1rem;
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);

}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Navbar Styles */
.navbar-menu {
  float: right;
}

.nav {
  margin: 0;
  padding: 0;
  list-style: none;
  text-align: center;
}

.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}

.nav .nav-link {
  display: block;
  padding: 0.5rem 1rem; /* Half of root (0.5rem) and equal to root (1rem) */
}

.nav .nav-link:hover {
  color: var(--nav-item-link-hover);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* New section declaration before section-header */
.section {
  padding: var(--section-padding);
}

.section-header {
  text-align: var(--section-header-align);
  padding: var(--section-header-padding); /* Added padding */
}

/* New declarations following section-header */
.section-body {
  padding: var(--section-body-padding);
}

.section-footer {
  padding: var(--section-footer-padding);
  text-align: var(--section-footer-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Row class for ul tags */
ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

/* Columns */
.col-1-3 {
  width: 33.33%;
  float: left;
  padding: 0.5rem;
}

.col-1-2 {
  width: 50%;
  float: left;
  padding: 0.5rem;
}

/* Footer Copyright */
.footer-copyright {
  margin: 0;
  font-size: var(--font-size-small);
  color: var(--text-color);
}

/* Footer lists alignment */
.footer ul {
  text-align: right;
}

.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

/* New footer declaration at the end */
.footer {
  padding: var(--footer-padding);
}

```
**Logica**
1.  ul.row: Al quitarle los márgenes, paddings y los puntos (list-style: none), convertimos la lista en un contenedor neutral para nuestras columnas.

2.  Columnas (col-1-3 y col-1-2):
- float: left: Es lo que permite que se pongan una al lado de la otra.
- padding: 0.5rem: Crea un espacio ("gutter") entre las columnas para que el contenido no se toque. Gracias al box-sizing: border-box que pusimos en la Task 15, este padding no romperá el ancho de la columna.

3.  Alineación del Footer: Al poner text-align: right en las listas dentro del footer, movemos los enlaces sociales o de navegación hacia el extremo derecho, creando un equilibrio visual con el copyright que suele ir a la izquierda.
---

##  20. Clear the context of the grid

`styles/20-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-padding: 5rem 0;
  --section-header-padding: 0 0 3rem;
  --section-body-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-tagline-margin: 0;
  --footer-padding: 5rem 0 1rem;
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);

}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Navbar Styles */
.navbar-menu {
  float: right;
}

.nav {
  margin: 0;
  padding: 0;
  list-style: none;
  text-align: center;
}

.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}

.nav .nav-link {
  display: block;
  padding: 0.5rem 1rem; /* Half of root (0.5rem) and equal to root (1rem) */
}

.nav .nav-link:hover {
  color: var(--nav-item-link-hover);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* New section declaration before section-header */
.section {
  padding: var(--section-padding);
}

.section-header {
  text-align: var(--section-header-align);
  padding: var(--section-header-padding); /* Added padding */
}

/* New declarations following section-header */
.section-body {
  padding: var(--section-body-padding);
}

.section-footer {
  padding: var(--section-footer-padding);
  text-align: var(--section-footer-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Row class for ul tags */
ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

/* Task 20: Clear the context of the grid (Clearfix) */
.row::after {
  content: "";
  display: table;
  clear: both;
}

/* Columns */
.col-1-3 {
  width: 33.33%;
  float: left;
  padding: 0.5rem;
}

.col-1-2 {
  width: 50%;
  float: left;
  padding: 0.5rem;
}

/* Footer Copyright */
.footer-copyright {
  margin: 0;
  font-size: var(--font-size-small);
  color: var(--text-color);
}

/* Footer lists alignment */
.footer ul {
  text-align: right;
}

.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

/* New footer declaration at the end */
.footer {
  padding: var(--footer-padding);
}

```
### ¿Cómo funciona técnicamente este "Clearfix"?
1. **`content: ""`**: Crea un elemento invisible al final de la fila. Sin contenido, no ocupa espacio visual.

2.  **`display: table`**: Le da al pseudo-elemento un comportamiento de bloque que ayuda a contener los márgenes.

3.  **`clear: both`**: 
- Le dice al navegador: "No permitas elementos flotantes (`float: left` o `right`) a mi lado". 
- Esto empuja al pseudo-elemento al final de la fila, forzando al contenedor padre a estirarse para alcanzarlo.
---

## 21. Simplify the col- selector

`styles/21-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-padding: 5rem 0;
  --section-header-padding: 0 0 3rem;
  --section-body-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-tagline-margin: 0;
  --footer-padding: 5rem 0 1rem;
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);

}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Navbar Styles */
.navbar-menu {
  float: right;
}

.nav {
  margin: 0;
  padding: 0;
  list-style: none;
  text-align: center;
}

.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}

.nav .nav-link {
  display: block;
  padding: 0.5rem 1rem; /* Half of root (0.5rem) and equal to root (1rem) */
}

.nav .nav-link:hover {
  color: var(--nav-item-link-hover);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* New section declaration before section-header */
.section {
  padding: var(--section-padding);
}

.section-header {
  text-align: var(--section-header-align);
  padding: var(--section-header-padding); /* Added padding */
}

/* New declarations following section-header */
.section-body {
  padding: var(--section-body-padding);
}

.section-footer {
  padding: var(--section-footer-padding);
  text-align: var(--section-footer-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Row class for ul tags */
ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

/* Selects any class that starts with "col-" */
[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

/* Columns */
.col-1-3 {
  width: 33.33%;
}

.col-1-2 {
  width: 50%;
}

/* Footer Copyright */
.footer-copyright {
  margin: 0;
  font-size: var(--font-size-small);
  color: var(--text-color);
}

/* Footer lists alignment */
.footer ul {
  text-align: right;
}

.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

/* New footer declaration at the end */
.footer {
  padding: var(--footer-padding);
}

```
### ¿Cómo funciona el selector [class^="col-"]?
- **`^=`**: 
  + Este símbolo significa "comienza con".

- **`class^="col-"`**: 
  + Le dice al navegador: "Busca cualquier elemento que tenga una clase cuyo nombre empiece por 'col-' y aplícale estos estilos".

- **Especificidad**: 
  + Al hacer esto, ya no necesitas escribir `float: left` y `padding: 0.5rem` dentro de `.col-1-3` o `.col-1-2`. 
  + Si en el futuro decides crear una columna `.col-1-4`, solo tendrás que definir su `width`, porque el float y el padding ya los tendrá por defecto.
---

##  22. Add a dark theme to sections

`styles/22-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-padding: 5rem 0;
  --section-header-padding: 0 0 3rem;
  --section-body-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-tagline-margin: 0;
  --footer-padding: 5rem 0 1rem;
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);

}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Navbar Styles */
.navbar-menu {
  float: right;
}

.nav {
  margin: 0;
  padding: 0;
  list-style: none;
  text-align: center;
}

.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}

.nav .nav-link {
  display: block;
  padding: 0.5rem 1rem; /* Half of root (0.5rem) and equal to root (1rem) */
}

.nav .nav-link:hover {
  color: var(--nav-item-link-hover);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* Task 22: Dark theme for sections */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
}

/* New section declaration before section-header */
.section {
  padding: var(--section-padding);
}

.section-header {
  text-align: var(--section-header-align);
  padding: var(--section-header-padding); /* Added padding */
}

/* New declarations following section-header */
.section-body {
  padding: var(--section-body-padding);
}

.section-footer {
  padding: var(--section-footer-padding);
  text-align: var(--section-footer-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Row class for ul tags */
ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

/* Selects any class that starts with "col-" */
[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

/* Columns */
.col-1-3 {
  width: 33.33%;
}

.col-1-2 {
  width: 50%;
}

/* Footer Copyright */
.footer-copyright {
  margin: 0;
  font-size: var(--font-size-small);
  color: var(--text-color);
}

/* Footer lists alignment */
.footer ul {
  text-align: right;
}

.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

/* New footer declaration at the end */
.footer {
  padding: var(--footer-padding);
}

```
### ¿Por qué usamos [data-section-theme="dark"]?
1.  **Scope (Alcance)**: 
- Al redefinir `--text-color` dentro de este selector, el cambio solo afecta a los elementos que estén dentro de esa sección.
- El resto de la página seguirá usando el color negro por defecto.

2. **Mantenibilidad**: 
- Si mañana decides que el "tema oscuro" debe ser un gris muy oscuro en lugar de negro puro, solo cambias el `background-color` en este bloque y listo.

3.  **Herencia**: 
- Todos los componentes que ya creamos (como `.section-title` o `.footer-copyright`) que usan `var(--text-color)` se actualizarán automáticamente al blanco cuando detecten que su padre tiene el atributo `data-section-theme="dark"`.

---

##  23. Fix issues for dark theme

``
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* Custom properties (Variables) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  --section-header-align: center;
  --section-tagline-transform: uppercase;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-padding: 5rem 0;
  --section-header-padding: 0 0 3rem;
  --section-body-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-tagline-margin: 0;
  --footer-padding: 5rem 0 1rem;
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);

}

body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

/* Updated Anchor Styles with Pseudo-classes */
a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited {
  font-style: italic;
}

a:hover {
  text-decoration: underline;
}

a:active {
  background-color: var(--color-light-grey);
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

/* Navbar Styles */
.navbar-menu {
  float: right;
}

.nav {
  margin: 0;
  padding: 0;
  list-style: none;
  text-align: center;
}

.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}

.nav .nav-link {
  display: block;
  padding: 0.5rem 1rem; /* Half of root (0.5rem) and equal to root (1rem) */
}

.nav .nav-link:hover {
  color: var(--nav-item-link-hover);
}

/* Utility classes */
.visually-hidden {
  display: none;
}

.card-category {
  color: var(--color-primary);
}

/* Task 22: Dark theme for sections */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
}

/* New section declaration before section-header */
.section {
  padding: var(--section-padding);
}

.section-header {
  text-align: var(--section-header-align);
  padding: var(--section-header-padding); /* Added padding */
}

/* New declarations following section-header */
.section-body {
  padding: var(--section-body-padding);
}

.section-footer {
  padding: var(--section-footer-padding);
  text-align: var(--section-footer-align);
}

.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}

.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Row class for ul tags */
ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

/* Selects any class that starts with "col-" */
[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

/* Columns */
.col-1-3 {
  width: 33.33%;
}

.col-1-2 {
  width: 50%;
}

.footer-address {
  color: var(--text-color);
}

.social-link {
  display: block;
}

.social-link svg {
  fill: var(--text-color);
}

/* Footer Copyright */
.footer-copyright {
  margin: 0;
  font-size: var(--font-size-small);
  color: var(--text-color);
}

/* Footer lists alignment */
.footer ul {
  text-align: right;
}

.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

/* New footer declaration at the end */
.footer {
  padding: var(--footer-padding);
}

```
**Logica**
1.  **`.footer-address`**: 
- Al usar `var(--text-color)`, garantizamos que si la sección es clara, el texto sea negro, y si es oscura (gracias al atributo `data-section-theme="dark"`), el texto cambie automáticamente a blanco.

2. **`.social-link` como `block`**: 
- Esto permite que el enlace ocupe todo el ancho disponible o que se comporte como un contenedor sólido para el icono, facilitando el control de márgenes y paddings.

3.  **El selector `.social-link svg`**:
- Los archivos SVG no usan la propiedad `color` para su relleno, sino la propiedad `fill`.
- Al heredar `var(--text-color)`, los iconos sociales (Twitter, Facebook, etc.) siempre harán contraste con el fondo de la sección, ya sea blanca o negra.
---

##  24. Add background and hover state to services

`styles/24-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; }
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Servicios) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
**Logica**
1.  **Selectores Descendientes**: 
- Al usar `.card-services .card-title`, nos aseguramos de que el margen 0 solo se aplique a los títulos dentro de servicios, sin afectar otros títulos del sitio.

2.  **El "Efecto Botón"**: 
- Al poner `display: block` en el <a>, el enlace deja de ocupar solo el ancho del texto y pasa a ocupar todo el ancho de la tarjeta. 
- Esto, sumado al `padding: 2rem`, crea una superficie de clic muy amplia.

3.  **Feedback Visual (Hover)**: 
- Cambiar el fondo a `color-primary` (#d73953) y el texto a blanco es una forma clásica y efectiva de decirle al usuario: "Este elemento es interactivo".
 
---

##  25. Add border to the button

`styles/25-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; }
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Servicios) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Logica**
1.  **Flexibilidad del Botón**: 
- Al usar `display: inline-block`, el botón respetará el padding y los márgenes, pero se mantendrá en línea con el texto si es necesario.

2.  **El "Truco" del Tema Oscuro**: 
- Fíjate que en [data-section-theme="dark"] solo redefinimos `--button-color`. 
- No tuvimos que reescribir toda la clase `.button`. 
- El navegador detecta que el valor de la variable cambió a blanco y actualiza el botón automáticamente.

3.  **Jerarquía Visual**: 
- El borde de `0.2rem` con el color primario le da una identidad fuerte al "Call to Action" de la página.
---

##  26. Add border radius to images

`styles/26-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; }
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Services) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Card (Testimonial) - Task 26 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;  /* 10x root element (10px * 10) */
  height: 10rem; /* 10x root element (10px * 10) */
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem; /* 1x root element (10px) */
  color: var(--color-primary);
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Logica**
1.  **Círculos perfectos**: 
- Para que `border-radius: 50%` funcione y cree un círculo, el elemento debe tener el mismo ancho que alto (en este caso, `10rem`). - Si fueran diferentes, obtendrías un óvalo.

2.  **Etiqueta <cite>**: 
- Por defecto, los navegadores suelen mostrar <cite> en cursiva. 
- Al ponerle `display: block`, hacemos que salte a una nueva línea (debajo de la cita), y con el `padding-top` le damos aire respecto al texto superior.

3.  **Color Primario**: 
- Usar `var(--color-primary)` para el nombre del autor del testimonio ayuda a resaltar quién está hablando, manteniendo la paleta de colores de Techium.

---

##  27. Styling the section hero

`styles/27-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; }
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Task 27: Section Hero Styling */
.section-hero {
  background-size: 90rem auto; /* 2-value syntax: width height */
}

.section-hero .section-title {
  margin-bottom: 5rem;
}

.section-hero .section-inner {
  padding: 10rem 40rem 2rem 0; /* top right bottom left */
}

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Services) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Card (Testimonial) - Task 26 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;  /* 10x root element (10px * 10) */
  height: 10rem; /* 10x root element (10px * 10) */
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem; /* 1x root element (10px) */
  color: var(--color-primary);
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Logica**
1.  **`background-size: 90rem auto`**: 
- Le estamos diciendo al navegador que queremos que la imagen de fondo mida exactamente `90rem` de ancho y que la altura se ajuste automáticamente para mantener la proporción original.

2.  **Padding Asimétrico en `.section-inner`**: 
- Al poner un padding de `40rem` a la derecha, estamos "empujando" el contenido de texto hacia la izquierda. 
- Esto es un truco clásico de diseño para dejar espacio visual a una imagen que se posicionará en el lado derecho de la sección.

3.  **Margen del Título**: 
- Los `5rem` de margen inferior en el título ayudan a separar el encabezado principal de los párrafos o botones que sigan, dándole más "aire" y elegancia al banner.
---

##  28. Fixing the header and menu navigation bar

`styles/28-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
    /* Header Variables - Task 28 */
  --header-padding: 4rem 0 0;
  --header-logo-position: relative;
  --header-logo-link-display: inline-block;
  --header-logo-link-position: absolute;
  --header-logo-link-top: -1rem;
  --header-logo-link-left: 0;
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  --nav-item-link-hover: var(--color-primary);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Header Styles - Task 28 */
.header {
  padding: var(--header-padding);
}

.header-logo {
  position: var(--header-logo-position);
}

.header-logo a {
  display: var(--header-logo-link-display);
  position: var(--header-logo-link-position);
  top: var(--header-logo-link-top);
  left: var(--header-logo-link-left);
}

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; }
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Task 27: Section Hero Styling */
.section-hero {
  background-size: 90rem auto; /* 2-value syntax: width height */
}

.section-hero .section-title {
  margin-bottom: 5rem;
}

.section-hero .section-inner {
  padding: 10rem 40rem 2rem 0; /* top right bottom left */
}

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Services) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Card (Testimonial) - Task 26 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;  /* 10x root element (10px * 10) */
  height: 10rem; /* 10x root element (10px * 10) */
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem; /* 1x root element (10px) */
  color: var(--color-primary);
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Cambios**
```css
/* ... (Todo el código anterior de 27-style.css se mantiene igual) ... */

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  /* ... (Variables de colores, fuentes, botones, etc.) ... */

  /* Header Variables - Task 28 */
  --header-padding: 4rem 0 0;
  --header-logo-position: relative;
  --header-logo-link-display: inline-block;
  --header-logo-link-position: absolute;
  --header-logo-link-top: -1rem;
  --header-logo-link-left: 0;

  /* ... (Resto de variables de section, nav, etc.) ... */
}

/* ... (Base Styles y Layout se mantienen igual) ... */

/* 6. COMPONENTS */

/* Header Styles - Task 28 */
.header {
  padding: var(--header-padding);
}

.header-logo {
  position: var(--header-logo-position);
}

.header-logo a {
  display: var(--header-logo-link-display);
  position: var(--header-logo-link-position);
  top: var(--header-logo-link-top);
  left: var(--header-logo-link-left);
}

/* Navbar Styles (Siguen aquí abajo) */
.navbar-menu { float: right; }
/* ... */
```
### **Logica**
1.  **Posicionamiento Absoluto vs Relativo**: 
- Al definir `.header-logo` como `relative`, este se convierte en el "ancla" o punto de referencia. 
- Cuando el enlace dentro (<a>) se pone en `absolute`, sus coordenadas `top` y `left` se calculan basándose en los límites de `.header-logo`, no de toda la página.

2. **Top Negativo (-1rem)**: 
- Al usar un valor negativo, estamos desplazando el logo hacia arriba, fuera de su posición natural. 
- Esto es muy común para logos que "flotan" sobre el borde del encabezado.

3. **Inline-block en el enlace**: 
- Es fundamental que el <a> tenga un tipo de display que permita aplicar dimensiones y posicionamiento correctamente mientras se mantiene en línea.
---

##  29. Styling and custom properties for the nav

`styles/29-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
    /* Header Variables - Task 28 */
  --header-padding: 4rem 0 0;
  --header-logo-position: relative;
  --header-logo-link-display: inline-block;
  --header-logo-link-position: absolute;
  --header-logo-link-top: -1rem;
  --header-logo-link-left: 0;
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  /* Task 29: Edit nav-item-link-hover */
  --nav-item-link-hover: var(--color-white);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Header Styles - Task 28 */
.header {
  padding: var(--header-padding);
}

.header-logo {
  position: var(--header-logo-position);
}

.header-logo a {
  display: var(--header-logo-link-display);
  position: var(--header-logo-link-position);
  top: var(--header-logo-link-top);
  left: var(--header-logo-link-left);
}

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; position: relative;}
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Task 29: Nav-link before pseudo-element */
.nav .nav-link::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--color-white);
  width: 0;
  height: 0.2rem; /* 20% of 10px root element */
}

/* Task 29: Hover state for before pseudo-element */
.nav .nav-item:hover .nav-link::before {
  background-color: var(--color-primary);
  width: 100%;
}

/* Task 27: Section Hero Styling */
.section-hero {
  background-size: 90rem auto; /* 2-value syntax: width height */
}

.section-hero .section-title {
  margin-bottom: 5rem;
}

.section-hero .section-inner {
  padding: 10rem 40rem 2rem 0; /* top right bottom left */
}

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Services) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Card (Testimonial) - Task 26 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;  /* 10x root element (10px * 10) */
  height: 10rem; /* 10x root element (10px * 10) */
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem; /* 1x root element (10px) */
  color: var(--color-primary);
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Cambios**
```css
/* ... (Todo el código anterior de 28-style.css se mantiene igual) ... */

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  /* ... (Otras variables) ... */

  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem;
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0;
  /* Task 29: Edit nav-item-link-hover */
  --nav-item-link-hover: var(--color-white);

  /* ... */
}

/* ... (Base Styles y Layout) ... */

/* 6. COMPONENTS */

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; position: relative; } /* Added relative for absolute pseudo-element */
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Task 29: Nav-link before pseudo-element */
.nav .nav-link::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--color-white);
  width: 0;
  height: 0.2rem; /* 20% of 10px root element */
}

/* Task 29: Hover state for before pseudo-element */
.nav .nav-item:hover .nav-link::before {
  background-color: var(--color-primary);
  width: 100%;
}

/* ... (Resto del código: Sections, Hero, Cards, Footer, Themes) ... */
```
### **Logica**
1.  **Pseudoelementos `(::before)`**: 
- Al usar `content: ""`, creas un elemento "invisible" que puedes estilizar. 
- Al darle `position: absolute`, lo sacas del flujo normal para colocarlo exactamente donde quieras (en este caso, en el `top: 0` del enlace).

2.  **Transición de Ancho**: 
- El requerimiento pide que el ancho inicial sea `0` y en hover pase a 100%. 
- Esto prepara el camino para que, si luego agregas `transition: width 0.3s`, la línea se deslice suavemente.

3.  **Jerarquía de Selectores**: 
- Fíjate en el selector `.nav .nav-item:hover .nav-link::before`. 
- Esto significa: "Cuando el mouse esté sobre el item de la lista, modifica el pseudoelemento del enlace que está adentro". 
- Es la forma más estable de disparar efectos complejos en menús.

---

##  30. Fix the works section
En la Task 30 estamos creando un efecto de "Overlay" interactivo para las tarjetas de la sección de trabajos.

Lo que estamos haciendo técnicamente es ocultar el título y un fondo oscuro, para luego revelarlos suavemente cuando el usuario pasa el mouse sobre la tarjeta. El uso de object-fit: cover es la clave para que todas tus imágenes tengan el mismo tamaño (30rem) sin que se vean estiradas.
`styles/30-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
    /* Header Variables - Task 28 */
  --header-padding: 4rem 0 0;
  --header-logo-position: relative;
  --header-logo-link-display: inline-block;
  --header-logo-link-position: absolute;
  --header-logo-link-top: -1rem;
  --header-logo-link-left: 0;
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  /* Task 29: Edit nav-item-link-hover */
  --nav-item-link-hover: var(--color-white);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Header Styles - Task 28 */
.header {
  padding: var(--header-padding);
}

.header-logo {
  position: var(--header-logo-position);
}

.header-logo a {
  display: var(--header-logo-link-display);
  position: var(--header-logo-link-position);
  top: var(--header-logo-link-top);
  left: var(--header-logo-link-left);
}

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; position: relative;}
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Task 29: Nav-link before pseudo-element */
.nav .nav-link::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--color-white);
  width: 0;
  height: 0.2rem; /* 20% of 10px root element */
}

/* Task 29: Hover state for before pseudo-element */
.nav .nav-item:hover .nav-link::before {
  background-color: var(--color-primary);
  width: 100%;
}

/* Task 27: Section Hero Styling */
.section-hero {
  background-size: 90rem auto; /* 2-value syntax: width height */
}

.section-hero .section-title {
  margin-bottom: 5rem;
}

.section-hero .section-inner {
  padding: 10rem 40rem 2rem 0; /* top right bottom left */
}

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Services) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Card (Testimonial) - Task 26 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;  /* 10x root element (10px * 10) */
  height: 10rem; /* 10x root element (10px * 10) */
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem; /* 1x root element (10px) */
  color: var(--color-primary);
}

/* Task 30: Card Work Styling */
.card-work .card-outer {
  position: relative;
  overflow: hidden;
}

.card-work .card-image img {
  height: 30rem;
  width: 100%;
  object-fit: cover;
  vertical-align: bottom;
}

.card-work .card-inner {
  position: absolute;
  top: -0.1rem;
  left: -0.1rem;
  right: -0.1rem;
  z-index: 1;
}

.card-work:hover .card-inner {
  background-color: rgba(0, 0, 0, 0.7);
}

.card-work .card-title {
  text-align: center;
  margin: 0;
  opacity: 0;
  height: 100%;
  position: relative;
}

.card-work .card-title a {
  display: block;
  text-decoration: none;
  padding-top: 45%;
}

.card-work .card-title a::after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}

.card-work:hover .card-title {
  opacity: 1;
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Cambios**
```css
/* ... (Todo el código anterior de 29-style.css se mantiene igual) ... */

/* 6. COMPONENTS */

/* ... (Navbar, Hero, Testimonials) ... */

/* Task 30: Card Work Styling */
.card-work .card-outer {
  position: relative;
  overflow: hidden;
}

.card-work .card-image img {
  height: 30rem;
  width: 100%;
  object-fit: cover;
  vertical-align: bottom;
}

.card-work .card-inner {
  position: absolute;
  top: -0.1rem;
  left: -0.1rem;
  right: -0.1rem;
  z-index: 1;
}

.card-work:hover .card-inner {
  background-color: rgba(0, 0, 0, 0.7);
}

.card-work .card-title {
  text-align: center;
  margin: 0;
  opacity: 0;
  height: 100%;
  position: relative;
}

.card-work .card-title a {
  display: block;
  text-decoration: none;
  padding-top: 45%;
}

.card-work .card-title a::after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}

.card-work:hover .card-title {
  opacity: 1;
}

/* ... (Resto del código: Footer, Themes, Utilities) ... */
```
### **Logica**
1.  `object-fit: cover`: 
- Le dice a la imagen: "Llena el espacio de 30rem de alto, recorta lo que sobre, pero mantén la proporción". 
- Así evitas que las fotos se vean aplastadas.

2.  **El Overlay (`card-inner`)**: 
- Al posicionarlo de forma absoluta con valores negativos (`-0.1rem`), nos aseguramos de que cubra perfectamente cualquier borde o imperfección del contenedor. 
- El `rgba(0, 0, 0, 0.7)` crea ese efecto de vidrio ahumado negro cuando hacemos hover.

3. **El Truco del Enlace `(::after)`**: 
- Al ponerle un `::after` absoluto que cubra todo el espacio (0 en todos los lados), convertimos toda la tarjeta en un link cliqueable, no solo el texto del título.

4.  **Opacidad**: 
- Al empezar con `opacity: 0` en el título, lo mantenemos oculto hasta que el hover en el padre (`.card-work:hover`) lo cambia a 1.

---

##  31. Add quotes decoration on testimonials
Vamos a actualizar la sección de Card Testimonial dentro de tus componentes. Usaremos el código hexadecimal `\201C`, que corresponde a las comillas de apertura dobles (“).
`styles/31-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
    /* Header Variables - Task 28 */
  --header-padding: 4rem 0 0;
  --header-logo-position: relative;
  --header-logo-link-display: inline-block;
  --header-logo-link-position: absolute;
  --header-logo-link-top: -1rem;
  --header-logo-link-left: 0;
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  /* Task 29: Edit nav-item-link-hover */
  --nav-item-link-hover: var(--color-white);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Header Styles - Task 28 */
.header {
  padding: var(--header-padding);
}

.header-logo {
  position: var(--header-logo-position);
}

.header-logo a {
  display: var(--header-logo-link-display);
  position: var(--header-logo-link-position);
  top: var(--header-logo-link-top);
  left: var(--header-logo-link-left);
}

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; position: relative;}
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Task 29: Nav-link before pseudo-element */
.nav .nav-link::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--color-white);
  width: 0;
  height: 0.2rem; /* 20% of 10px root element */
}

/* Task 29: Hover state for before pseudo-element */
.nav .nav-item:hover .nav-link::before {
  background-color: var(--color-primary);
  width: 100%;
}

/* Task 27: Section Hero Styling */
.section-hero {
  background-size: 90rem auto; /* 2-value syntax: width height */
}

.section-hero .section-title {
  margin-bottom: 5rem;
}

.section-hero .section-inner {
  padding: 10rem 40rem 2rem 0; /* top right bottom left */
}

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Services) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Card (Testimonial) - Task 26 & 31 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;  /* 10x root element (10px * 10) */
  height: 10rem; /* 10x root element (10px * 10) */
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem; /* 1x root element (10px) */
  color: var(--color-primary);
}

/* Task 31: Quote decoration */
.card-testimonial .card-quote {
  position: relative;
}

.card-testimonial .card-quote::before {
  content: "\201C";
  position: absolute;
  top: -4.5rem;
  left: -1rem;
  color: #efeded;
  font-size: 10rem;
  z-index: -1;
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem;
  color: var(--color-primary);
}

/* Task 30: Card Work Styling */
.card-work .card-outer {
  position: relative;
  overflow: hidden;
}

.card-work .card-image img {
  height: 30rem;
  width: 100%;
  object-fit: cover;
  vertical-align: bottom;
}

.card-work .card-inner {
  position: absolute;
  top: -0.1rem;
  left: -0.1rem;
  right: -0.1rem;
  z-index: 1;
}

.card-work:hover .card-inner {
  background-color: rgba(0, 0, 0, 0.7);
}

.card-work .card-title {
  text-align: center;
  margin: 0;
  opacity: 0;
  height: 100%;
  position: relative;
}

.card-work .card-title a {
  display: block;
  text-decoration: none;
  padding-top: 45%;
}

.card-work .card-title a::after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}

.card-work:hover .card-title {
  opacity: 1;
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Cmbios**
```css
/* ... (Todo el código anterior de 30-style.css se mantiene igual) ... */

/* 6. COMPONENTS */

/* ... (Navbar, Hero, Services, Work) ... */

/* Card (Testimonial) - Task 26 & 31 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;
  height: 10rem;
}

/* Task 31: Quote decoration */
.card-testimonial .card-quote {
  position: relative;
}

.card-testimonial .card-quote::before {
  content: "\201C";
  position: absolute;
  top: -4.5rem;
  left: -1rem;
  color: #efeded;
  font-size: 10rem;
  z-index: -1;
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem;
  color: var(--color-primary);
}

/* ... (Footer, Themes, Utilities) ... */
```
### **Logica**
1.  **Posicionamiento Relativo**: 
- Al poner `position: relative` en `.card-quote`, establecemos el marco de referencia. 
- Sin esto, las comillas se posicionarían respecto a la tarjeta entera o incluso al cuerpo de la página.

2.  **El valor `\201C`**: 
- Es el escape CSS para el carácter Unicode de las comillas tipográficas. 
- Es la forma correcta de insertar símbolos especiales directamente desde el CSS.

3.  **Z-index negativo**: 
- Al usar `z-index: -1`, nos aseguramos de que la comilla gigante quede detrás del texto del testimonio. 
- Esto permite que el texto sea legible aunque la comilla sea enorme (`10rem`).

4.  **Color Suave**: 
- El color `#efeded` es un gris muy claro. 
- Esto crea un contraste sutil con el fondo blanco, logrando que la decoración sea elegante y no distraiga demasiado.
---

##  32. Incorporating transitions
El efecto que estamos construyendo en la sección de "Work" es muy elegante: cuando el usuario pasa el mouse, el contenedor se encoge ligeramente (scale 0.95) mientras que la imagen dentro se agranda (scale 1.2), creando una sensación de "ventana" muy profesional.
`styles/32-style.css`
```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Render the `main` element consistently in IE.
 */

main {
  display: block;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

/* 2. BOX SIZING & GLOBAL CONFIG */
*, *:before, *:after {
  box-sizing: border-box;
}

/* Global styles */
html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  --color-primary: #d73953;
  --color-black: #090909;
  --color-white: #ffffff;
  --color-light-grey: #f3f3f3;
  --color-dark-grey: #353535;
  --text-color: var(--color-black);
  /* Fonts */
  --font-family-base: "Open Sans", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-family-title: "Raleway", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --font-size-small: 1.2rem;
  --font-size-medium: 1.6rem;
  --font-size-large: 1.8rem;
  --font-size-x-large: 2.3rem;
  --font-size-xx-large: 4.8rem;
  --font-weight-regular: 400;
  --font-weight-bold: 700;
  --line-height-small: 1.2;
  --line-height-base: 1.5;
  --line-height-big: 1.8;
  /* Button Variables - Task 25 */
  --button-display: inline-block;
  --button-padding: 1.5rem 3rem;
  --button-border: 0.2rem solid var(--color-primary);
  --button-color: var(--color-black);
  --button-text-decoration: none;
  --button-font-size: var(--font-size-large);
  --button-hover-color: var(--color-white);
  --button-hover-text-decoration: none;
  --button-hover-background: var(--color-primary);
    /* Header Variables - Task 28 */
  --header-padding: 4rem 0 0;
  --header-logo-position: relative;
  --header-logo-link-display: inline-block;
  --header-logo-link-position: absolute;
  --header-logo-link-top: -1rem;
  --header-logo-link-left: 0;
  /* Section Variables */
  --section-padding: 5rem 0;
  --section-header-align: center;
  --section-body-padding: 0 0 3rem;
  --section-header-padding: 0 0 3rem;
  --section-footer-padding: 3rem 0 0;
  --section-footer-align: center;
  --section-title-margin: 0;
  --section-title-color: var(--color-black);
  --section-tagline-transform: uppercase;
  --section-tagline-margin: 0;
  /* Navbar Variables */
  --nav-item-font-family: var(--font-family-title);
  --nav-item-font-weight: var(--font-weight-bold);
  --nav-item-font-size: var(--font-size-medium);
  --nav-item-letter-spacing: 0.04rem; /* 4% of 10px (root) */
  --nav-item-display: inline-block;
  --nav-item-margin: 0 0 3rem 0; /* 3 times root element on bottom */
  /* Task 29: Edit nav-item-link-hover */
  --nav-item-link-hover: var(--color-white);
  /* Footer Variables */
  --footer-padding: 5rem 0 1rem;
  /* Task 32: Transition Variables */
  --transition-duration: .3s;
  --transition-cubic-bezier: cubic-bezier(0.17, 0.67, 0, 1.01);
}

/* 4. BASE STYLES */
body {
  color: var(--text-color);
  font-family: var(--font-family-base);
  font-size: var(--font-size-medium);
  font-weight: var(--font-weight-regular);
  line-height: var(--line-height-base);
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-family-title);
  font-weight: var(--font-weight-bold);
}

a[href] {
  color: var(--text-color);
  text-decoration: none;
}

a:visited { font-style: italic; }
a:hover { text-decoration: underline; }
a:active { background-color: var(--color-light-grey); }

/* Task 25: Button Component */
.button {
  display: var(--button-display);
  padding: var(--button-padding);
  border: var(--button-border);
  font-size: var(--button-font-size);
  color: var(--button-color);
  text-decoration: var(--button-text-decoration);
}

.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
}

/* 5. LAYOUT (CONTAINER & GRID) */
.container {
  width: 960px;
  margin-left: auto;
  margin-right: auto;
}

ul.row {
  margin: 0;
  padding: 0;
  list-style: none;
}

.row::after {
  content: "";
  display: table;
  clear: both;
}

[class^="col-"] {
  float: left;
  padding: 0.5rem;
}

.col-1-3 { width: 33.33%; }
.col-1-2 { width: 50%; }

/* 6. COMPONENTS */

/* Header Styles - Task 28 */
.header {
  padding: var(--header-padding);
}

.header-logo {
  position: var(--header-logo-position);
}

.header-logo a {
  display: var(--header-logo-link-display);
  position: var(--header-logo-link-position);
  top: var(--header-logo-link-top);
  left: var(--header-logo-link-left);
}

/* Task 25 & 32: Button Hover Animation */
.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
  /* Task 32 additions */
  transition-duration: var(--transition-duration);
  transition-property: color, background-color;
}

/* Navbar */
.navbar-menu { float: right; }
.nav { margin: 0; padding: 0; list-style: none; text-align: center; }
.nav .nav-item {
  font-family: var(--nav-item-font-family);
  font-weight: var(--nav-item-font-weight);
  font-size: var(--nav-item-font-size);
  letter-spacing: var(--nav-item-letter-spacing);
  display: var(--nav-item-display);
  margin: var(--nav-item-margin);
}
.nav .nav-link { display: block; padding: 0.5rem 1rem; position: relative;}
.nav .nav-link:hover { color: var(--nav-item-link-hover); }

/* Task 29: Nav-link before pseudo-element */
.nav .nav-link::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--color-white);
  width: 0;
  height: 0.2rem; /* 20% of 10px root element */
  /* Task 32: Animation on nav items */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

/* Task 29: Hover state for before pseudo-element */
.nav .nav-item:hover .nav-link::before {
  background-color: var(--color-primary);
  width: 100%;
}

/* Task 27: Section Hero Styling */
.section-hero {
  background-size: 90rem auto; /* 2-value syntax: width height */
}

.section-hero .section-title {
  margin-bottom: 5rem;
}

.section-hero .section-inner {
  padding: 10rem 40rem 2rem 0; /* top right bottom left */
}

/* Sections */
.section { padding: var(--section-padding); }
.section-header { text-align: var(--section-header-align); padding: var(--section-header-padding); }
.section-body { padding: var(--section-body-padding); }
.section-footer { padding: var(--section-footer-padding); text-align: var(--section-footer-align); }
.section-title {
  font-family: var(--font-family-title);
  font-size: var(--font-size-xx-large);
  font-weight: var(--font-weight-bold);
  margin: var(--section-title-margin);
  color: var(--section-title-color);
}
.section-tagline {
  color: var(--color-primary);
  font-family: var(--font-family-title);
  text-transform: var(--section-tagline-transform);
  font-weight: var(--font-weight-bold);
  margin: var(--section-tagline-margin);
}

/* Cards (Services) - Task 24 */
.card-services .card-title {
  margin: 0;
}
.card-services a {
  display: block;
  padding: 2rem;
  background-color: var(--color-light-grey);
}
.card-services a:hover {
  color: var(--color-white);
  background-color: var(--color-primary);
  text-decoration: none;
}

/* Card (Testimonial) - Task 26 & 31 */
.card-testimonial {
  text-align: center;
}

.card-testimonial .card-avatar {
  border-radius: 50%;
  width: 10rem;  /* 10x root element (10px * 10) */
  height: 10rem; /* 10x root element (10px * 10) */
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem; /* 1x root element (10px) */
  color: var(--color-primary);
}

/* Task 31: Quote decoration */
.card-testimonial .card-quote {
  position: relative;
}

.card-testimonial .card-quote::before {
  content: "\201C";
  position: absolute;
  top: -4.5rem;
  left: -1rem;
  color: #efeded;
  font-size: 10rem;
  z-index: -1;
}

.card-testimonial .card-quote cite {
  display: block;
  padding-top: 1rem;
  color: var(--color-primary);
}

/* Task 30 & 32: Card Work Styling */
.card-work .card-outer {
  position: relative;
  overflow: hidden;
  /* Task 32: Transition for the shrink effect */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

.card-work:hover .card-outer {
  transform: scale(0.95);
}

.card-work .card-image img {
    height: 30rem;
  width: 100%;
  object-fit: cover;
  vertical-align: bottom;
  /* Task 32: Transition for the zoom effect */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

.card-work:hover .card-image img {
  transform: scale(1.2);
}

.card-work .card-inner {
  position: absolute;
  top: -0.1rem;
  left: -0.1rem;
  right: -0.1rem;
  z-index: 1;
  /* Task 32: Transition for overlay */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

.card-work:hover .card-inner {
  background-color: rgba(0, 0, 0, 0.7);
}

.card-work .card-title {
  text-align: center;
  margin: 0;
  opacity: 0;
  height: 100%;
  position: relative;
}

.card-work .card-title a {
  display: block;
  text-decoration: none;
  padding-top: 45%;
}

.card-work .card-title a::after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}

.card-work:hover .card-title {
  opacity: 1;
}

/* Footer */
.footer { padding: var(--footer-padding); }
.footer-copyright { margin: 0; font-size: var(--font-size-small); color: var(--text-color); }
.footer-address { color: var(--text-color); }
.footer ul { text-align: right; }
.social-link { display: block; }
.social-link svg { fill: var(--text-color); }

/* 7. THEMES */
[data-section-theme="dark"] {
  --text-color: var(--color-white);
  --section-title-color: var(--color-white);
  background-color: var(--color-black);
  /* Task 25: Button color for dark theme */
  --button-color: var(--color-white);
}

/* 8. UTILITIES */
.visually-hidden { display: none; }
.card-category { color: var(--color-primary); }

```
### **Cmbios**
```css
/* ... (Todo el código anterior de 31-style.css se mantiene igual) ... */

/* 3. VARIABLES (CUSTOM PROPERTIES) */
:root {
  /* ... (Otras variables) ... */

  /* Task 32: Transition Variables */
  --transition-duration: .3s;
  --transition-cubic-bezier: cubic-bezier(0.17, 0.67, 0, 1.01);

  /* ... */
}

/* ... (Base Styles y Layout) ... */

/* 6. COMPONENTS */

/* Task 25 & 32: Button Hover Animation */
.button:hover {
  color: var(--button-hover-color);
  text-decoration: var(--button-hover-text-decoration);
  background-color: var(--button-hover-background);
  /* Task 32 additions */
  transition-duration: var(--transition-duration);
  transition-property: color, background-color;
}

/* Navbar */
/* ... */
.nav .nav-link::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--color-white);
  width: 0;
  height: 0.2rem;
  /* Task 32: Animation on nav items */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

/* Task 30 & 32: Card Work Styling */
.card-work .card-outer {
  position: relative;
  overflow: hidden;
  /* Task 32: Transition for the shrink effect */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

.card-work:hover .card-outer {
  transform: scale(0.95);
}

.card-work .card-image img {
  height: 30rem;
  width: 100%;
  object-fit: cover;
  vertical-align: bottom;
  /* Task 32: Transition for the zoom effect */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

.card-work:hover .card-image img {
  transform: scale(1.2);
}

.card-work .card-inner {
  position: absolute;
  top: -0.1rem;
  left: -0.1rem;
  right: -0.1rem;
  z-index: 1;
  /* Task 32: Transition for overlay */
  transition: var(--transition-duration) var(--transition-cubic-bezier);
}

/* ... (Resto del código igual) ... */
```
### **Logica**
1.  **Cubic Bezier**: 
- A diferencia de un simple `ease`, esta curva `cubic-bezier(0.17, 0.67, 0, 1.01)` crea un movimiento más natural y "elástico", lo que da una sensación de mayor calidad al sitio.
2.  **Efecto de Zoom Inverso**:
- El contenedor (`.card-outer`) hace un **scale(0.95)** (se encoge un 5%).
- La imagen (`img`) hace un **scale(1.2)** (crece un 20%).
- Al estar el contenedor con `overflow: hidden`, la imagen parece que se expande dentro de un marco que se aprieta. Es un efecto visualmente impactante.

3.  **Transition-property en Botones**: 
- Al especificar `color`, `background-color`, le decimos al navegador que solo anime esas dos propiedades, optimizando el rendimiento.

---

