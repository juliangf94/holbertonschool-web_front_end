# HTML — Learning Objectives

## Which guidelines to follow for HTML

- Always use **lowercase** for HTML tags and attributes
- Always **quote attribute values** with double quotes: `class="container"`
- Always declare the **doctype** at the top: `<!DOCTYPE html>`
- Always define **lang** attribute on the `<html>` tag: `<html lang="en">`
- Always define **charset** in the `<head>`: `<meta charset="UTF-8">`
- Always include **alt** attribute on images
- Validate your code with the **W3C Validator**
- Close all tags properly
- Use **semantic tags** over generic `div` whenever possible

---

## How to create the skeleton of an HTML5 page

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Page Title</title>
  </head>
  <body>
    <!-- content here -->
  </body>
</html>
```

| Part | Description |
|------|-------------|
| `<!DOCTYPE html>` | Tells the browser this is an HTML5 document |
| `<html lang="en">` | Root element, `lang` helps screen readers and SEO |
| `<head>` | Contains metadata — not visible to the user |
| `<meta charset="UTF-8">` | Defines character encoding |
| `<meta name="viewport">` | Makes the page responsive on mobile |
| `<title>` | Text shown in the browser tab |
| `<body>` | All visible content goes here |

---

## How to use semantic HTML tags to structure a web page

Semantic tags describe the **meaning** of the content, not just its appearance.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Techium</title>
  </head>
  <body>
    <header>
      <nav>...</nav>
    </header>
    <main>
      <section>
        <article>...</article>
      </section>
      <aside>...</aside>
    </main>
    <footer>...</footer>
  </body>
</html>
```
-   **`main` tag**
    +   The <main> HTML tag is a structural element located generally between the <header> and the <footer> and contains the content of your web page.
-   **`footer` tag**
    +   The <footer> HTML tag is a structural element used to identify the footer of a page, article, or section.
    +   Usage
        *   copyright information
        *   authorship information
        *   navigation elements
        *   social icons or links
-   **`aside` tag**
    +   The <aside> HTML tag contains additional information related to the `main` content.
    +   Usage
        *   monthly archives
        *   list of categories
-   **`section` tag**
    +   The <section> tag element allows the grouping of related elements. You can usually find a <header> and <footer> attached to a section.
-   **`article` tag**
    +   An <article> HTML tag represent a self-contained piece of content which could theoretically be distributed to other websites and platforms as a stand-alone unit.
    +   Usage
        *   blog posts
        *   news articles
        *   product cards
        *   forum posts
-   **`nav` tag**
    +   The <nav> HTML tag is a structural element with navigation links.
---

## Which use cases to use `div` vs `span`
-   A `div` (stands for “document division”) is a generic block of content used to structure elements in your layout.
```html
<!-- div: wraps a block of content -->
<div class="card">
  <h2>Title</h2>
  <p>Some text here.</p>
</div>
```

-   A `span` is a generic inline of content used usually for text that are not inside a `paragraph`. 
    +   `span` should be used as little as possible.
```html
<!-- span: wraps inline content inside text -->
<p>The price is <span class="highlight">$99</span> today.</p>

> Use `div` and `span` only when **no semantic tag fits**. Always prefer semantic tags first.
```

| Tag | Type | Use case |
|-----|------|----------|
| `<div>` | Block-level | Groups **block** elements (sections, layouts) |
| `<span>` | Inline | Groups **inline** content (words, characters inside text) |


---

## The semantic value of `header`, `main`, `footer`, `article`, `nav`, `section`, `aside`

| Tag | Semantic value |
|-----|---------------|
| `<header>` | Introductory content — logo, site title, top navigation |
| `<nav>` | Block of navigation links |
| `<main>` | The dominant, unique content of the page. Only **one per page** |
| `<section>` | A thematic grouping of content, usually with a heading |
| `<article>` | Independent, self-contained content (blog post, news article, card) |
| `<aside>` | Secondary content related to the main content (sidebar, related links) |
| `<footer>` | Footer of the page or section — copyright, contact info, links |

```html
<header>
  <nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
  </nav>
</header>

<main>
  <section>
    <h2>Latest News</h2>
    <article>
      <h3>Article Title</h3>
      <p>Article content...</p>
    </article>
  </section>
  <aside>
    <p>Related links...</p>
  </aside>
</main>

<footer>
  <p>&copy; 2024 Techium</p>
</footer>
```

---

## How to use headings and why it's important to follow the hierarchical order

HTML has 6 levels of headings: `<h1>` to `<h6>`.

```html
<h1>Page Title</h1>         <!-- Only ONE per page -->
  <h2>Main Section</h2>
    <h3>Subsection</h3>
      <h4>Sub-subsection</h4>
        <h5>...</h5>
          <h6>...</h6>
```

**Rules:**
- There should be **only one `<h1>`** per page — it's the main title
- Never **skip levels** — don't go from `<h2>` to `<h4>`
- Headings are used by **screen readers** and **SEO** to understand the page structure
- Don't use headings just to make text bigger — use CSS for styling

---

## How to make lists in HTML

### Unordered list (bullet points)
```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```

### Ordered list (numbered)
```html
<ol>
  <li>First step</li>
  <li>Second step</li>
  <li>Third step</li>
</ol>
```

### Description list (term + definition)
```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```

---

## The differences between media types (SVG, GIF, PNG, JPG)

| Format | Type | Transparency | Animation | Best for |
|--------|------|-------------|-----------|----------|
| **JPG/JPEG** | Raster | ❌ No | ❌ No | Photos, complex images with many colors |
| **PNG** | Raster | ✅ Yes | ❌ No | Images that need transparency, logos, icons |
| **GIF** | Raster | ✅ Yes (1-bit) | ✅ Yes | Simple animations, low-color images |
| **SVG** | Vector | ✅ Yes | ✅ Yes | Icons, logos, illustrations — scales infinitely without quality loss |

> - **Raster** = made of pixels, loses quality when scaled up
> - **Vector** = made of math formulas, scales to any size without quality loss
> - Use **JPG** for photos, **PNG** for images with transparency, **SVG** for icons and logos

---

## How to structure data in a table

```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>25</td>
      <td>Paris</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>30</td>
      <td>Lyon</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="3">Total: 2 users</td>
    </tr>
  </tfoot>
</table>
```

| Tag | Description |
|-----|-------------|
| `<table>` | Container for the entire table |
| `<thead>` | Header section of the table |
| `<tbody>` | Body section with the data rows |
| `<tfoot>` | Footer section (totals, summaries) |
| `<tr>` | Table row |
| `<th>` | Header cell (bold and centered by default) |
| `<td>` | Data cell |
| `colspan` | Makes a cell span multiple columns |
| `rowspan` | Makes a cell span multiple rows |

---

## How to integrate a video in a webpage

```html
<video width="640" height="360" controls>
  <source src="video.mp4" type="video/mp4" />
  <source src="video.webm" type="video/webm" />
  Your browser does not support the video tag.
</video>
```

| Attribute | Description |
|-----------|-------------|
| `controls` | Shows play, pause, volume controls |
| `autoplay` | Starts playing automatically |
| `muted` | Mutes the video (required for autoplay in most browsers) |
| `loop` | Repeats the video when it ends |
| `poster` | Image shown before the video plays |
| `width` / `height` | Dimensions of the video player |

> The text inside `<video>` is shown only if the browser doesn't support the tag (fallback).

---

## How to integrate an audio file in a webpage

```html
<audio controls>
  <source src="audio.mp3" type="audio/mp3" />
  <source src="audio.ogg" type="audio/ogg" />
  Your browser does not support the audio tag.
</audio>
```

| Attribute | Description |
|-----------|-------------|
| `controls` | Shows play, pause, volume controls |
| `autoplay` | Starts playing automatically |
| `loop` | Repeats when it ends |
| `muted` | Starts muted |

---

## How to embed external content

### iframe (external webpage or map)
```html
<iframe
  src="https://www.google.com/maps/embed?..."
  width="600"
  height="450"
  allowfullscreen
  loading="lazy">
</iframe>
```

### YouTube video embed
```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="YouTube video player"
  allowfullscreen>
</iframe>
```

### Object (PDFs, Flash)
```html
<object data="file.pdf" type="application/pdf" width="600" height="400">
  <p>Your browser does not support PDFs.</p>
</object>
```

---

## How to correctly structure an HTML page

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content="Techium - A web company" />
    <title>Techium</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <header>
      <nav>
        <a href="/">Home</a>
        <a href="/about">About</a>
        <a href="/contact">Contact</a>
      </nav>
    </header>

    <main>
      <section>
        <h1>Welcome to Techium</h1>
        <p>We are a web company.</p>
      </section>

      <section>
        <h2>Our Services</h2>
        <article>
          <h3>Web Design</h3>
          <p>We create beautiful websites.</p>
        </article>
        <article>
          <h3>Development</h3>
          <p>We build robust applications.</p>
        </article>
      </section>

      <aside>
        <h2>Latest News</h2>
        <p>Check our blog for updates.</p>
      </aside>
    </main>

    <footer>
      <p>&copy; 2024 Techium. All rights reserved.</p>
    </footer>
  </body>
</html>
```

**Checklist for a correct HTML page:**
- [ ] `<!DOCTYPE html>` at the very top
- [ ] `<html lang="...">` with language attribute
- [ ] `<meta charset="UTF-8">` in `<head>`
- [ ] `<meta name="viewport">` in `<head>`
- [ ] One `<title>` in `<head>`
- [ ] Only one `<h1>` per page
- [ ] Headings follow hierarchical order (h1 → h2 → h3)
- [ ] Semantic tags used (`header`, `main`, `footer`, etc.)
- [ ] All tags properly closed
- [ ] All images have `alt` attribute
- [ ] Code validated with W3C Validator


---
---

# HTML — Quiz Answers
---
## Question #0 — Which information can we find in the tag `<head>`?

- [x] metadata
- [ ] navigation
- [ ] link to Twitter
- [x] link to stylesheets

> El `<head>` contiene información **no visible** para el usuario. Ahí van los metadatos (`<meta charset>`, `<meta name="description">`), el título de la pestaña (`<title>`), y los links a recursos externos como hojas de estilo CSS (`<link rel="stylesheet">`). La navegación va en `<nav>` dentro del `<body>`, no en el `<head>`.

---

## Question #1 — Which tag should we use to change the browser tab text?

- [ ] `<head>`
- [x] `<title>`
- [ ] `<tab>`
- [ ] `<browser>`

> `<title>` es el único tag que controla el texto que aparece en la pestaña del navegador. Va dentro del `<head>`. `<head>` es el contenedor general, no el que define el texto. `<tab>` y `<browser>` no existen en HTML.

---

## Question #2 — How many levels are available in HTML5 for section headings?

- [ ] 1
- [ ] 2
- [ ] 4
- [x] 6
- [ ] 8
- [ ] 10

> HTML5 tiene exactamente **6 niveles** de headings: `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` y `<h6>`. `<h1>` es el más importante (título principal) y `<h6>` el menos importante. Siempre deben usarse en orden jerárquico sin saltear niveles.

---

## Question #3 — Which tag should we use to draw a horizontal line?

- [ ] `<line>`
- [ ] `<br>`
- [ ] `<break>`
- [x] `<hr>`

> `<hr>` (Horizontal Rule) dibuja una línea horizontal y se usa para separar secciones o temas en una página. Es un tag vacío — no necesita cierre. `<br>` hace un salto de línea dentro de un texto, no dibuja una línea. `<line>` y `<break>` no existen en HTML.

---

## Question #4 — Which tag should we use to group elements in an unordered list?

- [ ] `<li>`
- [x] `<ul>`
- [ ] `<ol>`
- [ ] `<table>`
- [ ] `<unordered list>`
- [ ] `<list>`

> `<ul>` (Unordered List) es el contenedor de una lista sin orden (con bullets). Cada elemento de la lista va dentro de `<li>`. `<ol>` es para listas **ordenadas** (numeradas). `<unordered list>` y `<list>` no existen en HTML.
> ```html
> <ul>
>   <li>Item 1</li>
>   <li>Item 2</li>
> </ul>
> ```

---

## Question #5 — Which tag should we use to create a hyperlink?

- [ ] `<link>`
- [ ] `<to>`
- [ ] `<p>`
- [ ] `<div>`
- [x] `<a>`

> `<a>` (Anchor) es el tag para crear hipervínculos. El atributo `href` define la URL de destino.
> ```html
> <a href="https://techium.com">Visit Techium</a>
> ```
> `<link>` existe pero se usa en el `<head>` para vincular recursos externos como CSS, no para crear links clickeables en el contenido.

---

## Question #6 — Which tag should we use to change the font weight of a text?

- [ ] `<h1>`
- [x] `<b>`
- [ ] `<i>`
- [ ] `<em>`
- [x] `<strong>`
- [ ] `<bold>`

> - ✅ `<b>` — pone el texto en **negrita** de forma puramente visual (sin valor semántico).
> - ✅ `<strong>` — pone el texto en **negrita** CON valor semántico — indica que el contenido es importante. Screen readers lo leen con énfasis.
> - ❌ `<i>` — pone el texto en *cursiva*, no en negrita.
> - ❌ `<em>` — también cursiva pero con valor semántico de énfasis.
> - ❌ `<h1>` — es un heading, aunque se ve en negrita su propósito es otro.
> - ❌ `<bold>` — no existe en HTML.

---

## Question #7 — Which tag should we use to embed an image?

- [x] `<img>`
- [ ] `<iframe>`
- [ ] `<div>`
- [ ] `<caption>`

> `<img>` es el tag específico para insertar imágenes. Es un tag vacío (no necesita cierre) y siempre debe tener el atributo `alt` para accesibilidad.
> ```html
> <img src="logo.png" alt="Techium logo" />
> ```
> `<iframe>` se usa para embeber páginas web externas, no imágenes. `<caption>` es para agregar un título a una tabla.

---

## Question #8 — Which tag should we use to embed another website?

- [ ] `<div>`
- [ ] `<a>`
- [x] `<iframe>`
- [ ] `<p>`
- [ ] `<code>`

> `<iframe>` (Inline Frame) permite embeber otra página web dentro de la actual. Se usa mucho para integrar mapas de Google, videos de YouTube, etc.
> ```html
> <iframe
>   src="https://www.google.com/maps/embed?..."
>   width="600"
>   height="450"
>   allowfullscreen>
> </iframe>
> ```
> `<a>` crea un link para navegar a otra página, pero no la embebe dentro de la actual.

---
---

#   Exercises

---
##  0. Create your first webpage
Create your first HTML file 0-index.html with:
-   Add the doctype on the first line (without any comment)
-   After the doctype, open and close a html tag
-   Add the language tag, specify English for ISO language code and add the direction tag (ltr or rtl) on the html tag.
-   Open your file in your browser (the page should be blank)

`0-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
</html>

```

---

##  1. Structure your webpage
Copy the content of 0-index.html into 1-index.html
Create the head and body sections
-   inside the html tag, create the head and body tags (empty) in this order
W3C won't pass - you can ignore it
`1-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
    </head>
    <body>
    </body>
</html>

```

---
##  2. The head - meta charset, viewport, title, description, favicons

`2-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
        <title>Homepage - Techium</title>
        <meta name="description" content="Techium is a digital agency">
        <link rel="icon" type="image/x-icon" href="./favicon.ico">
        <link rel="icon" type="image/png" href="./favicon.png">
    </head>
    <body>
    </body>
</html>

```

---
##  3. Simple header, main, footer

`3-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
        <title>Homepage - Techium</title>
        <meta name="description" content="Techium is a digital agency">
        <link rel="icon" type="image/x-icon" href="./favicon.ico">
        <link rel="icon" type="image/png" href="./favicon.png">
    </head>
    <body>
        <header>
            Header
        </header>
        <main>
            Main content
        </main>
        <footer>
            Footer
        </footer>
    </body>
</html>

```

---
##  4. Aside

`article.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
        <title>Article - Techium</title>
        <meta name="description" content="Techium is a digital agency">
        <link rel="icon" type="image/x-icon" href="./favicon.ico">
        <link rel="icon" type="image/png" href="./favicon.png">
    </head>
    <body>
        <header>
            Header
        </header>
        <main>
            Main content
            <aside>
                Aside
            </aside>
        </main>
        <footer>
            Footer
        </footer>
    </body>
</html>

```

---
##  5. Section

`5-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
        <title>Homepage - Techium</title>
        <meta name="description" content="Techium is a digital agency">
        <link rel="icon" type="image/x-icon" href="./favicon.ico">
        <link rel="icon" type="image/png" href="./favicon.png">
    </head>
    <body>
        <header>
            Header
        </header>
        <main>
            <section>Hero section</section>
            <section>Services section</section>
            <section>Works section</section>
            <section>About section</section>
            <section>Latest news section</section>
            <section>Testimonials section</section>
            <section>Contact section</section>
        </main>
        <footer>
            Footer
        </footer>
    </body>
</html>

```

---
##  6. Work, News, Testimonial articles

`6-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
        <title>Homepage - Techium</title>
        <meta name="description" content="Techium is a digital agency">
        <link rel="icon" type="image/x-icon" href="./favicon.ico">
        <link rel="icon" type="image/png" href="./favicon.png">
    </head>
    <body>
        <header>
            Header
        </header>
        <main>
            <section>Hero section</section>
            <section>Services section</section>
            <section>
                Works section
                <article>Work 1</article>
                <article>Work 2</article>
                <article>Work 3</article>
            </section>
            <section>About section</section>
            <section>
                Latest news section
                <article>Article 1</article>
                <article>Article 2</article>
                <article>Article 3</article>
            </section>
            <section>
                Testimonials section
                <article>Testimonial 1</article>
                <article>Testimonial 2</article>
                <article>Testimonial 3</article>
            </section>
            <section>Contact section</section>
        </main>
        <footer>
            Footer
        </footer>
    </body>
</html>


```

---
##  7. Navigation

`7-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
        <title>Homepage - Techium</title>
        <meta name="description" content="Techium is a digital agency">
        <link rel="icon" type="image/x-icon" href="./favicon.ico">
        <link rel="icon" type="image/png" href="./favicon.png">
    </head>
    <body>
        <header>
            <nav></nav>
        </header>
        <main>
            <section>Hero section</section>
            <section>Services section</section>
            <section>
                Works section
                <article>Work 1</article>
                <article>Work 2</article>
                <article>Work 3</article>
            </section>
            <section>About section</section>
            <section>
                Latest news section
                <article>Article 1</article>
                <article>Article 2</article>
                <article>Article 3</article>
            </section>
            <section>
                Testimonials section
                <article>Testimonial 1</article>
                <article>Testimonial 2</article>
                <article>Testimonial 3</article>
            </section>
            <section>Contact section</section>
        </main>
        <footer>
            Footer
        </footer>
    </body>
</html>


```

---
##  8. Level 1 headings

`8-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
        <title>Homepage - Techium</title>
        <meta name="description" content="Techium is a digital agency">
        <link rel="icon" type="image/x-icon" href="./favicon.ico">
        <link rel="icon" type="image/png" href="./favicon.png">
    </head>
    <body>
        <header>
            <nav></nav>
        </header>
        <main>
            <h1>Homepage</h1>
            <section>Hero section</section>
            <section>Services section</section>
            <section>
                Works section
                <article>Work 1</article>
                <article>Work 2</article>
                <article>Work 3</article>
            </section>
            <section>About section</section>
            <section>
                Latest news section
                <article>Article 1</article>
                <article>Article 2</article>
                <article>Article 3</article>
            </section>
            <section>
                Testimonials section
                <article>Testimonial 1</article>
                <article>Testimonial 2</article>
                <article>Testimonial 3</article>
            </section>
            <section>Contact section</section>
        </main>
        <footer>
            Footer
        </footer>
    </body>
</html>

```

---
##  9. Level 2 headings

`9-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header>
      <nav></nav>
    </header>
    <main>
      <h1>Homepage</h1>
      <section>
        <h2>We help you build your brand!</h2>
      </section>
      <section>
        <h2>Services</h2>
      </section>
      <section>
        <h2>Works</h2>
        <article>Work 1</article>
        <article>Work 2</article>
        <article>Work 3</article>
      </section>
      <section>
        <h2>About Us</h2>
      </section>
      <section>
        <h2>Latest news</h2>
        <article>Article 1</article>
        <article>Article 2</article>
        <article>Article 3</article>
      </section>
      <section>
        <h2>Testimonials</h2>
        <article>Testimonial 1</article>
        <article>Testimonial 2</article>
        <article>Testimonial 3</article>
      </section>
      <section>
        <h2>Contact</h2>
      </section>
    </main>
    <footer>
      Footer
    </footer>
  </body>
</html>

```

---
##  10. Level 3 headings

`10-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header>
      <nav></nav>
    </header>
    <main>
      <h1>Homepage</h1>
      <section>
        <h2>We help you build your brand!</h2>
      </section>
      <section>
        <h2>Services</h2>
        <h3>Design &amp; Concept</h3>
        <h3>Digital Strategy</h3>
        <h3>Content Strategy</h3>
        <h3>UX Design</h3>
        <h3>Web Development</h3>
        <h3>Social Media</h3>
      </section>
      <section>
        <h2>Works</h2>
        <article>
          <h3>Interior Design</h3>
        </article>
        <article>
          <h3>Web Development</h3>
        </article>
        <article>
          <h3>Personal Brand</h3>
        </article>
      </section>
      <section>
        <h2>About Us</h2>
        <h3>Who are we</h3>
        <h3>Our culture</h3>
        <h3>How we work</h3>
      </section>
      <section>
        <h2>Latest news</h2>
        <article>
          <h3>Hoc loco tenere se Triarius non potuit.</h3>
        </article>
        <article>
          <h3>Ut alios omittam, hunc appello, quem ille unum secutus est.</h3>
        </article>
        <article>
          <h3>Bestiarum vero nullum iudicium puto.</h3>
        </article>
      </section>
      <section>
        <h2>Testimonials</h2>
        <article>Testimonial 1</article>
        <article>Testimonial 2</article>
        <article>Testimonial 3</article>
      </section>
      <section>
        <h2>Contact</h2>
      </section>
    </main>
    <footer>
      Footer
    </footer>
  </body>
</html>
```
### **Explicacion**
-   Entidades HTML (&amp;): 
    +   En la sección de servicios, para el texto "Design & Concept", es una buena práctica usar &amp; para representar el símbolo `&`. 

---

##  11. styleguide

`11-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>
    </main>
    <footer></footer>
  </body>
</html>
```

---
##  12. Paragraphs

`12-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header>
      <nav></nav>
    </header>
    <main>
      <h1>Homepage</h1>
      <section>
        <h2>We help you build your brand!</h2>
      </section>
      <section>
        <h2>Services</h2>
        <p>We work with you</p>
        <h3>Design &amp; Concept</h3>
        <h3>Digital Strategy</h3>
        <h3>Content Strategy</h3>
        <h3>UX Design</h3>
        <h3>Web Development</h3>
        <h3>Social Media</h3>
      </section>
      <section>
        <h2>Works</h2>
        <p>Take a look in our portfolio</p>
        <article>
          <h3>Interior Design</h3>
        </article>
        <article>
          <h3>Web Development</h3>
        </article>
        <article>
          <h3>Personal Brand</h3>
        </article>
      </section>
      <section>
        <h2>About Us</h2>
        <p>Everything about us</p>
        <h3>Who are we</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
        <h3>Our culture</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
        <h3>How we work</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
      </section>
      <section>
        <h2>Latest news</h2>
        <article>
          <p>Career</p>
          <h3>Hoc loco tenere se Triarius non potuit.</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
        </article>
        <article>
          <p>Digital Life</p>
          <h3>Ut alios omittam, hunc appello, quem ille unum secutus est.</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
        </article>
        <article>
          <p>Social</p>
          <h3>Bestiarum vero nullum iudicium puto.</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
        </article>
      </section>
      <section>
        <h2>Testimonials</h2>
        <p>We are more than a digital company</p>
        <article>Testimonial 1</article>
        <article>Testimonial 2</article>
        <article>Testimonial 3</article>
      </section>
      <section>
        <h2>Contact</h2>
        <p>We like to know new people</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
      </section>
    </main>
    <footer>
      Footer
    </footer>
  </body>
</html>
```

---
##  13. styleguide paragraphs

`13-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>

      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>
    </main>
    <footer></footer>
  </body>
</html>
```

---
##  14. Span

`14-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header>
      <span>Techium</span>
      <nav></nav>
    </header>
    <main>
      <h1>Homepage</h1>
      <section>
        <h2>We help you build your brand!</h2>
      </section>
      <section>
        <h2>Services</h2>
        <p>We work with you</p>
        <h3>Design &amp; Concept</h3>
        <h3>Digital Strategy</h3>
        <h3>Content Strategy</h3>
        <h3>UX Design</h3>
        <h3>Web Development</h3>
        <h3>Social Media</h3>
      </section>
      <section>
        <h2>Works</h2>
        <p>Take a look in our portfolio</p>
        <article>
          <h3>Interior Design</h3>
        </article>
        <article>
          <h3>Web Development</h3>
        </article>
        <article>
          <h3>Personal Brand</h3>
        </article>
      </section>
      <section>
        <h2>About Us</h2>
        <p>Everything about us</p>
        <h3>Who are we</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
        <h3>Our culture</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
        <h3>How we work</h3>
        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
      </section>
      <section>
        <h2>Latest news</h2>
        <article>
          <p>Career</p>
          <h3>Hoc loco tenere se Triarius non potuit.</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
        </article>
        <article>
          <p>Digital Life</p>
          <h3>Ut alios omittam, hunc appello, quem ille unum secutus est.</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
        </article>
        <article>
          <p>Social</p>
          <h3>Bestiarum vero nullum iudicium puto.</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
        </article>
      </section>
      <section>
        <h2>Testimonials</h2>
        <p>We are more than a digital company</p>
        <article>Testimonial 1</article>
        <article>Testimonial 2</article>
        <article>Testimonial 3</article>
      </section>
      <section>
        <h2>Contact</h2>
        <p>We like to know new people</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
      </section>
    </main>
    <footer>
      Footer
    </footer>
  </body>
</html>

```

---
##  15. Div 

`15-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header>
      <div>
        <nav></nav>
      </div>
    </header>
    <main>
      <h1>Homepage</h1>
      <section>
        <div>
          <h2>We help you build your brand!</h2>
        </div>
      </section>
      <section>
        <div>
          <h2>Services</h2>
          <p>We work with you</p>
          <h3>Design &amp; Concept</h3>
          <h3>Digital Strategy</h3>
          <h3>Content Strategy</h3>
          <h3>UX Design</h3>
          <h3>Web Development</h3>
          <h3>Social Media</h3>
        </div>
      </section>
      <section>
        <div>
          <h2>Works</h2>
          <p>Take a look in our portfolio</p>
          <article>
            <h3>Interior Design</h3>
          </article>
          <article>
            <h3>Web Development</h3>
          </article>
          <article>
            <h3>Personal Brand</h3>
          </article>
        </div>
      </section>
      <section>
        <div>
          <h2>About Us</h2>
          <p>Everything about us</p>
          <h3>Who are we</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          <h3>Our culture</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          <h3>How we work</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
        </div>
      </section>
      <section>
        <div>
          <h2>Latest news</h2>
          <article>
            <p>Career</p>
            <h3>Hoc loco tenere se Triarius non potuit.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
          </article>
          <article>
            <p>Digital Life</p>
            <h3>Ut alios omittam, hunc appello, quem ille unum secutus est.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
          </article>
          <article>
            <p>Social</p>
            <h3>Bestiarum vero nullum iudicium puto.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
          </article>
        </div>
      </section>
      <section>
        <div>
          <h2>Testimonials</h2>
          <p>We are more than a digital company</p>
          <article>Testimonial 1</article>
          <article>Testimonial 2</article>
          <article>Testimonial 3</article>
        </div>
      </section>
      <section>
        <div>
          <h2>Contact</h2>
          <p>We like to know new people</p>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
        </div>
      </section>
    </main>
    <footer>
      <div>
        Footer
      </div>
    </footer>
  </body>
</html>
```

---
##  16. Structure your sections

`16-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <title>Homepage - Techium</title>
  <meta name="description" content="Techium is a digital agency">
  <link rel="icon" type="image/x-icon" href="./favicon.ico">
  <link rel="icon" type="image/png" href="./favicon.png">
</head>
<body>
  <header>
    <div>
      <nav></nav>
    </div>
  </header>
  <main>
    <h1>Homepage</h1>
    <section>
      <div>
        <h2>We help you build your brand!</h2>
      </div>
    </section>

    <section>
      <div>
        <header>
          <h2>Services</h2>
          <p>We work with you</p>
        </header>
        <div>
          <h3>Design &amp; Concept</h3>
          <h3>Digital Strategy</h3>
          <h3>Content Strategy</h3>
          <h3>UX Design</h3>
          <h3>Web Development</h3>
          <h3>Social Media</h3>
        </div>
      </div>
    </section>

    <section>
      <div>
        <header>
          <h2>Works</h2>
          <p>Take a look in our portfolio</p>
        </header>
        <div>
          <article>
            <h3>Interior Design</h3>
          </article>
          <article>
            <h3>Web Development</h3>
          </article>
          <article>
            <h3>Personal Brand</h3>
          </article>
        </div>
      </div>
    </section>

    <section>
      <div>
        <header>
          <h2>About Us</h2>
          <p>Everything about us</p>
        </header>
        <div>
          <h3>Who are we</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          <h3>Our culture</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          <h3>How we work</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
        </div>
      </div>
    </section>

    <section>
      <div>
        <header>
          <h2>Latest news</h2>
        </header>
        <div>
          <article>
            <p>Career</p>
            <h3>Hoc loco tenere se Triarius non potuit.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
          </article>
          <article>
            <p>Digital Life</p>
            <h3>Ut alios omittam, hunc appello, quem ille unum secutus est.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
          </article>
          <article>
            <p>Social</p>
            <h3>Bestiarum vero nullum iudicium puto.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
          </article>
        </div>
      </div>
    </section>

    <section>
      <div>
        <header>
          <h2>Testimonials</h2>
          <p>We are more than a digital company</p>
        </header>
        <div>
          <article>Testimonial 1</article>
          <article>Testimonial 2</article>
          <article>Testimonial 3</article>
        </div>
      </div>
    </section>

    <section>
      <div>
        <header>
          <h2>Contact</h2>
          <p>We like to know new people</p>
        </header>
        <div>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
        </div>
      </div>
    </section>
  </main>
  <footer>
    <div>
      Footer
    </div>
  </footer>
</body>
</html>

```

---
##  17. Comments

`17-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
  <title>Homepage - Techium</title>
  <meta name="description" content="Techium is a digital agency">
  <link rel="icon" type="image/x-icon" href="./favicon.ico">
  <link rel="icon" type="image/png" href="./favicon.png">
</head>
<body>

  <!-- Header -->
  <header>
    <div>
      <nav></nav>
    </div>
  </header>

  <!-- Main -->
  <main>
    <h1>Homepage</h1>

    <!-- Hero section -->
    <section>
      <div>
        <h2>We help you build your brand!</h2>
      </div>
    </section>

    <!-- Services section -->
    <section>
      <div>
        <header>
          <h2>Services</h2>
          <p>We work with you</p>
        </header>
        <div>
          <h3>Design &amp; Concept</h3>
          <h3>Digital Strategy</h3>
          <h3>Content Strategy</h3>
          <h3>UX Design</h3>
          <h3>Web Development</h3>
          <h3>Social Media</h3>
        </div>
      </div>
    </section>

    <!-- Works section -->
    <section>
      <div>
        <header>
          <h2>Works</h2>
          <p>Take a look in our portfolio</p>
        </header>
        <div>
          <article>
            <h3>Interior Design</h3>
          </article>
          <article>
            <h3>Web Development</h3>
          </article>
          <article>
            <h3>Personal Brand</h3>
          </article>
        </div>
      </div>
    </section>

    <!-- About Us section -->
    <section>
      <div>
        <header>
          <h2>About Us</h2>
          <p>Everything about us</p>
        </header>
        <div>
          <h3>Who are we</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          <h3>Our culture</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          <h3>How we work</h3>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
        </div>
      </div>
    </section>

    <!-- Latest news section -->
    <section>
      <div>
        <header>
          <h2>Latest news</h2>
        </header>
        <div>
          <article>
            <p>Career</p>
            <h3>Hoc loco tenere se Triarius non potuit.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
          </article>
          <article>
            <p>Digital Life</p>
            <h3>Ut alios omittam, hunc appello, quem ille unum secutus est.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
          </article>
          <article>
            <p>Social</p>
            <h3>Bestiarum vero nullum iudicium puto.</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
          </article>
        </div>
      </div>
    </section>

    <!-- Testimonials section -->
    <section>
      <div>
        <header>
          <h2>Testimonials</h2>
          <p>We are more than a digital company</p>
        </header>
        <div>
          <article>Testimonial 1</article>
          <article>Testimonial 2</article>
          <article>Testimonial 3</article>
        </div>
      </div>
    </section>

    <!-- Contact section -->
    <section>
      <div>
        <header>
          <h2>Contact</h2>
          <p>We like to know new people</p>
        </header>
        <div>
          <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
        </div>
      </div>
    </section>

  </main>

  <!-- Footer -->
  <footer>
    <div>
      Footer
    </div>
  </footer>
</body>
</html>

```

---
##  18. link your logo

`18-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav></nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3>Design &amp; Concept</h3>
            <h3>Digital Strategy</h3>
            <h3>Content Strategy</h3>
            <h3>UX Design</h3>
            <h3>Web Development</h3>
            <h3>Social Media</h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article><h3>Interior Design</h3></article>
            <article><h3>Web Development</h3></article>
            <article><h3>Personal Brand</h3></article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum...</p>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3>Hoc loco...</h3>
              <p>Lorem ipsum...</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum...</p>
          </div>
        </div>
      </section>

    </main>

    <footer>
      <div>Footer</div>
    </footer>
  </body>
</html>

```

---
##  19. Create new pages

`about.html`
```html

```
`latest_news.html`
```html

```
`contact.html`
```html
```
---
##  20. Add links

`20-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
          <div>
          <a href="/">
              <span>Techium</span>
          </a>
          </div>
          <nav>
          <a href="/">Home</a>
          <a href="#services">Services</a>
          <a href="#works">Works</a>
          <a href="#about">About</a>
          <a href="#latest_news">Latest news</a>
          <a href="#testimonials">Testimonials</a>
          <a href="#contact">Contact</a>
          </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3>Design &amp; Concept</h3>
            <h3>Digital Strategy</h3>
            <h3>Content Strategy</h3>
            <h3>UX Design</h3>
            <h3>Web Development</h3>
            <h3>Social Media</h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article><h3>Interior Design</h3></article>
            <article><h3>Web Development</h3></article>
            <article><h3>Personal Brand</h3></article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum...</p>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3>Hoc loco...</h3>
              <p>Lorem ipsum...</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum...</p>
          </div>
        </div>
      </section>

    </main>

    <footer>
      <div>Footer</div>
    </footer>
  </body>
</html>

```

---
##  21. Add social media links

`21-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
          <div>
          <a href="/">
              <span>Techium</span>
          </a>
          </div>
          <nav>
          <a href="/">Home</a>
          <a href="#services">Services</a>
          <a href="#works">Works</a>
          <a href="#about">About</a>
          <a href="#latest_news">Latest news</a>
          <a href="#testimonials">Testimonials</a>
          <a href="#contact">Contact</a>
          </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3>Design &amp; Concept</h3>
            <h3>Digital Strategy</h3>
            <h3>Content Strategy</h3>
            <h3>UX Design</h3>
            <h3>Web Development</h3>
            <h3>Social Media</h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article><h3>Interior Design</h3></article>
            <article><h3>Web Development</h3></article>
            <article><h3>Personal Brand</h3></article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum...</p>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3>Hoc loco...</h3>
              <p>Lorem ipsum...</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum...</p>
          </div>
        </div>
      </section>

    </main>

    <footer>
      <div>
        <a href="https://www.facebook.com/HolbertonSchool/">Facebook</a>
        <a href="https://twitter.com/holbertonschool">Twitter</a>
        <a href="https://www.instagram.com/holbertonschool/">Instagram</a>
      </div>
    </footer>
  </body>
</html>

```

---
##  22. "Button" links

`22-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav>
          <a href="/">Home</a>
          <a href="#services">Services</a>
          <a href="#works">Works</a>
          <a href="#about">About</a>
          <a href="#latest_news">Latest news</a>
          <a href="#testimonials">Testimonials</a>
          <a href="#contact">Contact</a>
        </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3>Design &amp; Concept</h3>
            <h3>Digital Strategy</h3>
            <h3>Content Strategy</h3>
            <h3>UX Design</h3>
            <h3>Web Development</h3>
            <h3>Social Media</h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article><h3>Interior Design</h3></article>
            <article><h3>Web Development</h3></article>
            <article><h3>Personal Brand</h3></article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum...</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3>Hoc loco...</h3>
              <p>Lorem ipsum...</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum...</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <footer>
      <div>
        <a href="https://www.facebook.com/HolbertonSchool/">Facebook</a>
        <a href="https://twitter.com/holbertonschool">Twitter</a>
        <a href="https://www.instagram.com/holbertonschool/">Instagram</a>
      </div>
    </footer>
  </body>
</html>

```

---
##  23. Services, Works, Latest news links

`23-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav>
          <a href="/">Home</a>
          <a href="#services">Services</a>
          <a href="#works">Works</a>
          <a href="#about">About</a>
          <a href="#latest_news">Latest news</a>
          <a href="#testimonials">Testimonials</a>
          <a href="#contact">Contact</a>
        </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
            </article>
            <article>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
            </article>
            <article>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <footer>
      <div>
        <a href="https://www.facebook.com/HolbertonSchool/">Facebook</a>
        <a href="https://twitter.com/holbertonschool">Twitter</a>
        <a href="https://www.instagram.com/holbertonschool/">Instagram</a>
      </div>
    </footer>
  </body>
</html>
```

---
##  24. List the links

`24-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
            </article>
            <article>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
            </article>
            <article>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <footer>
      <div>
        <ul>
          <li><a href="https://www.facebook.com/HolbertonSchool/">Facebook</a></li>
          <li><a href="https://twitter.com/holbertonschool">Twitter</a></li>
          <li><a href="https://www.instagram.com/holbertonschool/">Instagram</a></li>
        </ul>
      </div>
    </footer>
  </body>
</html>
```

---
##  25. Secondary navigation menu

`25-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
            </article>
            <article>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
            </article>
            <article>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <footer>
      <div>
        <ul>
          <li><a href="https://www.facebook.com/HolbertonSchool/">Facebook</a></li>
          <li><a href="https://twitter.com/holbertonschool">Twitter</a></li>
          <li><a href="https://www.instagram.com/holbertonschool/">Instagram</a></li>
        </ul>
      </div>
      <div>
        <ul>
          <li><a href="#">Terms of Use</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Cookie Policy</a></li>
        </ul>
      </div>
    </footer>
  </body>
</html>
```

---
##  26. Examples of lists for the styleguide

`26-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>

      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>

      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>

          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>

          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>
    </main>
    <footer></footer>
  </body>
</html>
```
---
##  27. Separate content

`27-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet...</p>
            </article>
            <article>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet...</p>
            </article>
            <article>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>Testimonial 1</article>
            <article>Testimonial 2</article>
            <article>Testimonial 3</article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet...</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <footer>
      <div>
        <ul>
          <li><a href="https://www.facebook.com/HolbertonSchool/">Facebook</a></li>
          <li><a href="https://twitter.com/holbertonschool">Twitter</a></li>
          <li><a href="https://www.instagram.com/holbertonschool/">Instagram</a></li>
        </ul>
      </div>

      <hr>
      <p>© 2020 Techium, made with ♥ by students at Holberton School.</p>

      <div>
        <ul>
          <li><a href="#">Terms of Use</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Cookie Policy</a></li>
        </ul>
      </div>
    </footer>

  </body>
</html>

```

---
##  28. Horizontal rule example

`28-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>

      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>

      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>
          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>
          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>
      <!-- Horizontal rule -->
      <section>
        <header>
          <h2>Horizontal rule</h2>
        </header>
        <div>
          <hr>
        </div>
      </section>

    </main>
    <footer></footer>
  </body>
</html>

```

---
##  29. Client quotes

`29-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum, omnis expedita! Eum, praesentium cumque accusantium rem, sit quaerat est nisi ratione, deserunt ducimus quidem iste dicta quibusdam atque maxime cum!</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
            </article>
            <article>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
            </article>
            <article>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>
              <blockquote>
                <p>I am completely blown away. Thanks to Techium, we've just launched our 5th website!</p>
                <cite>Yuri Y.</cite>
              </blockquote>
            </article>
            <article>
              <blockquote>
                <p>Thank you so much for your help. Techium company is awesome!</p>
                <cite>Dorrie S.</cite>
              </blockquote>
            </article>
            <article>
              <blockquote>
                <p>I love your system. Definitely worth the investment. I'd be lost without Techium company.</p>
                <cite>Sven H.</cite>
              </blockquote>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <footer>
      <div>
        <ul>
          <li><a href="https://www.facebook.com/HolbertonSchool/">Facebook</a></li>
          <li><a href="https://twitter.com/holbertonschool">Twitter</a></li>
          <li><a href="https://www.instagram.com/holbertonschool/">Instagram</a></li>
        </ul>
      </div>

      <hr>
      <p>© 2020 Techium, made with ♥ by students at Holberton School.</p>

      <div>
        <ul>
          <li><a href="#">Terms of Use</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Cookie Policy</a></li>
        </ul>
      </div>
    </footer>
  </body>
</html>

```

---
##  30. Examples of quotes

`30-styleguide.html`
```html

```

---
##  31. Address and latest news authors

`31-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <header>
      <div>
        <div>
          <a href="/">
            <span>Techium</span>
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <main>
      <h1>Homepage</h1>

      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
              <small>By Kelly D.</small>
            </article>
            <article>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
              <small>By William A.</small>
            </article>
            <article>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
              <small>By Frances J.</small>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>
              <blockquote>
                <p>I am completely blown away. Thanks to Techium, we've just launched our 5th website!</p>
                <cite>Yuri Y.</cite>
              </blockquote>
            </article>
            <article>
              <blockquote>
                <p>Thank you so much for your help. Techium company is awesome!</p>
                <cite>Dorrie S.</cite>
              </blockquote>
            </article>
            <article>
              <blockquote>
                <p>I love your system. Definitely worth the investment. I'd be lost without Techium company.</p>
                <cite>Sven H.</cite>
              </blockquote>
            </article>
          </div>
        </div>
      </section>

      <section>
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet...</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <footer>
      <address>
        234 Washington Street<br>
        Urbana, Illinois
      </address>
      <div>
        <ul>
          <li><a href="https://www.facebook.com/HolbertonSchool/">Facebook</a></li>
          <li><a href="https://twitter.com/holbertonschool">Twitter</a></li>
          <li><a href="https://www.instagram.com/holbertonschool/">Instagram</a></li>
        </ul>
      </div>

      <hr>
      <p>© 2020 Techium, made with ♥ by students at Holberton School.</p>

      <div>
        <ul>
          <li><a href="#">Terms of Use</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Cookie Policy</a></li>
        </ul>
      </div>
    </footer>
  </body>
</html>

```


---
##  32. Typography section - using the correct tags

`32-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>

      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>

      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>

          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>

          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>

      <section>
        <header>
          <h2>Horizontal rule</h2>
        </header>
        <div>
          <hr>
        </div>
      </section>

      <section>
        <header>
          <h2>Blockquotes</h2>
        </header>
        <div>
          <h3>Inline quote</h3>
          <q>Stay hungry. Stay foolish.</q>
        </div>
        <div>
          <h3>Blockquote</h3>
          <blockquote>
            <p>I will be the leader of a company that ends up being worth billions of dollars, because I got the answers. I understand culture. I am the nucleus. I think that’s a responsibility that I have, to push possibilities, to show people, this is the level that things could be at.</p>
            <cite>Kanye West, Musician</cite>
          </blockquote>
        </div>
      </section>

      <section>
        <header>
          <h2>Typography</h2>
        </header>
        <div>
          <address>
            320 Stewart Avenue, Unit 12<br>
            New York City NY 10001
          </address>
        </div>
        <div>
          <pre>
            <h2>My title</h2>
            <p>Proin lacus turpis, feugiat sit amet sollicitudin non, volutpat in libero. Aenean hendrerit ultrices nulla ac lobortis. Vestibulum consectetur nibh vel ante rhoncus faucibus.</p>
          </pre>
        </div>
        <div>
          <p>Curabitur sit amet turpis cursus massa mollis <mark>highlighted</mark>. Duis finibus leo massa, eget dapibus erat finibus sed. Aenean condimentum sapien magna, eleifend <mark>highlighted</mark> mi consequat ut. Cras nec quam sed sapien ultricies <mark>highlighted</mark> ut sed metus.</p>
        </div>
      </section>

    </main>
    <footer></footer>
  </body>
</html>

```

---
##  33. Table

`33-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
        <!-- Headings -->
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>
      <!-- Paragraph -->
      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>
      <!-- Lists -->
      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>
        
          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>

          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>
      <!-- Horizontal rule -->
      <section>
        <header>
          <h2>Horizontal rule</h2>
        </header>
        <div>
          <hr>
        </div>
      </section>
      <!-- Blockquotes -->
      <section>
        <header>
          <h2>Blockquotes</h2>
        </header>
        <div>
          <h3>Inline quote</h3>
          <q>Stay hungry. Stay foolish.</q>
        </div>
        <div>
          <h3>Blockquote</h3>
          <blockquote>
            <p>I will be the leader of a company that ends up being worth billions of dollars, because I got the answers. I understand culture. I am the nucleus. I think that’s a responsibility that I have, to push possibilities, to show people, this is the level that things could be at.</p>
            <cite>Kanye West, Musician</cite>
          </blockquote>
        </div>
      </section>
      <!-- Typography -->
      <section>
        <header>
          <h2>Typography</h2>
        </header>
        <div>
          <address>
            320 Stewart Avenue, Unit 12<br>
            New York City NY 10001
          </address>
        </div>
        <div>
          <pre>
            &lt;h2&gt;My title&lt;/h2&gt;
            &lt;p&gt;Proin lacus turpis, feugiat sit amet sollicitudin non, volutpat in libero. Aenean hendrerit ultrices nulla ac lobortis. Vestibulum consectetur nibh vel ante rhoncus faucibus.&lt;/p&gt;
          </pre>
        </div>
        <div>
          <p>Curabitur sit amet turpis cursus massa mollis <mark>highlighted</mark>. Duis finibus leo massa, eget dapibus erat finibus sed. Aenean condimentum sapien magna, eleifend <mark>highlighted</mark> mi consequat ut. Cras nec quam sed sapien ultricies <mark>highlighted</mark> ut sed metus.</p>
        </div>
      </section>
      <!-- Table -->
      <section>
        <header>
          <h2>Table</h2>
        </header>
        <table>
          <thead>
            <tr>
              <th scope="col">Title</th>
              <th scope="col">Director</th>
              <th scope="col">Release Date</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Star Wars: Episode IV – A New Hope</th>
              <td>George Lucas</td>
              <td>May 25, 1977</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode V – The Empire Strikes Back</th>
              <td>Irvin Kershner</td>
              <td>May 21, 1980</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode VI – Return of the Jedi</th>
              <td>Richard Marquand</td>
              <td>May 25, 1983</td>
            </tr>
          </tbody>
        </table>
      </section>

    </main>
    <footer></footer>
  </body>
</html>

```

---
##  34. Details

`34-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
        <!-- Headings -->
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>
      <!-- Paragraph -->
      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>
      <!-- Lists -->
      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>
        
          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>

          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>
      <!-- Horizontal rule -->
      <section>
        <header>
          <h2>Horizontal rule</h2>
        </header>
        <div>
          <hr>
        </div>
      </section>
      <!-- Blockquotes -->
      <section>
        <header>
          <h2>Blockquotes</h2>
        </header>
        <div>
          <h3>Inline quote</h3>
          <q>Stay hungry. Stay foolish.</q>
        </div>
        <div>
          <h3>Blockquote</h3>
          <blockquote>
            <p>I will be the leader of a company that ends up being worth billions of dollars, because I got the answers. I understand culture. I am the nucleus. I think that’s a responsibility that I have, to push possibilities, to show people, this is the level that things could be at.</p>
            <cite>Kanye West, Musician</cite>
          </blockquote>
        </div>
      </section>
      <!-- Typography -->
      <section>
        <header>
          <h2>Typography</h2>
        </header>
        <div>
          <address>
            320 Stewart Avenue, Unit 12<br>
            New York City NY 10001
          </address>
        </div>
        <div>
          <pre>
            &lt;h2&gt;My title&lt;/h2&gt;
            &lt;p&gt;Proin lacus turpis, feugiat sit amet sollicitudin non, volutpat in libero. Aenean hendrerit ultrices nulla ac lobortis. Vestibulum consectetur nibh vel ante rhoncus faucibus.&lt;/p&gt;
          </pre>
        </div>
        <div>
          <p>Curabitur sit amet turpis cursus massa mollis <mark>highlighted</mark>. Duis finibus leo massa, eget dapibus erat finibus sed. Aenean condimentum sapien magna, eleifend <mark>highlighted</mark> mi consequat ut. Cras nec quam sed sapien ultricies <mark>highlighted</mark> ut sed metus.</p>
        </div>
      </section>
      <!-- Table -->
      <section>
        <header>
          <h2>Table</h2>
        </header>
        <table>
          <thead>
            <tr>
              <th scope="col">Title</th>
              <th scope="col">Director</th>
              <th scope="col">Release Date</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Star Wars: Episode IV – A New Hope</th>
              <td>George Lucas</td>
              <td>May 25, 1977</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode V – The Empire Strikes Back</th>
              <td>Irvin Kershner</td>
              <td>May 21, 1980</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode VI – Return of the Jedi</th>
              <td>Richard Marquand</td>
              <td>May 25, 1983</td>
            </tr>
          </tbody>
        </table>
      </section>
      <!-- Details -->
      <section>
        <header>
          <h2>Details</h2>
        </header>
        <div>
          <h3>Default</h3>
          <details>
            <summary>Show/Hide me</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
        <div>
          <h3>Open</h3>
          <details open>
            <summary>Always open</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
      </section>

    </main>
    <footer></footer>
  </body>
</html>

```
**Logica**
<details>: Es el contenedor principal para el contenido que se puede expandir o contraer.

<summary>: Es el título o encabezado que siempre es visible. Al hacer clic en él, se muestra el resto del contenido.

Atributo open: Si agregas esta palabra a la etiqueta de apertura (<details open>), el desplegable aparecerá abierto automáticamente cuando cargue la página.

---
##  35. Replace text logo with image logo

`35-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <!-- Header -->
    <header>
      <div>
        <div>
          <a href="/">
            <img src="logo-black.png" alt="Techium logo" width="160" height="40">
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <!-- Main -->
    <main>
      <h1>Homepage</h1>

      <!-- Hero section -->
      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <!-- Services section -->
      <section id="services">
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <!-- Works section -->
      <section id="works">
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <!-- About Us section -->
      <section id="about">
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <!-- Latest news section -->
      <section id="latest_news">
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Id Sextilius factum negabat. Quo tandem modo? At eum nihili facit; Quae contraria sunt his, malane?</p>
              <small>By Kelly D.</small>
            </article>
            <article>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tum mihi Piso: Quid ergo? Tum ille: Ain tandem? Non autem hoc: igitur ne illud quidem. Sed quod proximum fuit non vidit. Nos commodius agimus. An nisi populari fama?</p>
              <small>By William A.</small>
            </article>
            <article>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Non igitur bene. Quid enim est a Chrysippo praetermissum in Stoicis? Pugnant Stoici cum Peripateticis. Prioris generis est docilitas, memoria; Apparet statim, quae sint officia, quae actiones.</p>
              <small>By Frances J.</small>
            </article>
          </div>
        </div>
      </section>

      <!-- Testimonials section -->
      <section id="testimonials">
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>
              <blockquote>
                <p>I am completely blown away. Thanks to Techium, we've just launched our 5th website!</p>
                <cite>Yuri Y.</cite>
              </blockquote>
            </article>
            <article>
              <blockquote>
                <p>Thank you so much for your help. Techium company is awesome!</p>
                <cite>Dorrie S.</cite>
              </blockquote>
            </article>
            <article>
              <blockquote>
                <p>I love your system. Definitely worth the investment. I'd be lost without Techium company.</p>
                <cite>Sven H.</cite>
              </blockquote>
            </article>
          </div>
        </div>
      </section>

      <!-- Contact section -->
      <section id="contact">
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet...</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <!-- Footer -->
    <footer>
      <img src="logo-black.png" alt="Techium logo" width="160" height="40">
      
      <address>
        234 Washington Street<br>
        Urbana, Illinois
      </address>
      <div>
        <ul>
          <li><a href="https://www.facebook.com/HolbertonSchool/">Facebook</a></li>
          <li><a href="https://twitter.com/holbertonschool">Twitter</a></li>
          <li><a href="https://www.instagram.com/holbertonschool/">Instagram</a></li>
        </ul>
      </div>

      <hr>
      <p>© 2020 Techium, made with ♥ by students at Holberton School.</p>

      <div>
        <ul>
          <li><a href="#">Terms of Use</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Cookie Policy</a></li>
        </ul>
      </div>
    </footer>
  </body>
</html>

```

---
##  36. Add images to your sections

`36-index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <!-- Header -->
    <header>
      <div>
        <div>
          <a href="/">
            <img src="logo-black.png" alt="Techium logo" width="160" height="40">
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <!-- Main -->
    <main>
      <h1>Homepage</h1>

      <!-- Hero section -->
      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <!-- Services section -->
      <section id="services">
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <!-- Works section -->
      <section id="works">
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <div>
                <img src="images/pic-work-01.jpg" alt="">
              </div>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <div>
                <img src="images/pic-work-02.jpg" alt="">
              </div>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <div>
                <img src="images/pic-work-03.jpg" alt="">
              </div>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <!-- About Us section -->
      <section id="about">
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <img src="images/pic-about-us.jpg" alt="" width="460" height="447">
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <!-- Latest news section -->
      <section id="latest_news">
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <div>
                <img src="images/pic-blog-01.jpg" alt="" width="305" height="205">
              </div>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
              <small>By Kelly D.</small>
            </article>
            <article>
              <div>
                <img src="images/pic-blog-02.jpg" alt="" width="305" height="205">
              </div>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
              <small>By William A.</small>
            </article>
            <article>
              <div>
                <img src="images/pic-blog-03.jpg" alt="" width="305" height="205">
              </div>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
              <small>By Frances J.</small>
            </article>
          </div>
        </div>
      </section>

      <!-- Testimonials section -->
      <section id="testimonials">
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>
              <img src="images/pic-person-01.jpg" alt="Yuri Y. avatar" width="100" height="100">
              <blockquote>
                <p>I am completely blown away. Thanks to Techium, we've just launched our 5th website!</p>
                <cite>Yuri Y.</cite>
              </blockquote>
            </article>
            <article>
              <img src="images/pic-person-02.jpg" alt="Dorrie S. avatar" width="100" height="100">
              <blockquote>
                <p>Thank you so much for your help. Techium company is awesome!</p>
                <cite>Dorrie S.</cite>
              </blockquote>
            </article>
            <article>
              <img src="images/pic-person-03.jpg" alt="Sven H. avatar" width="100" height="100">
              <blockquote>
                <p>I love your system. Definitely worth the investment. I'd be lost without Techium company.</p>
                <cite>Sven H.</cite>
              </blockquote>
            </article>
          </div>
        </div>
      </section>

      <!-- Contact section -->
      <section id="contact">
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet...</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <!-- Footer -->
    <footer>
      <img src="logo-black.png" alt="Techium logo" width="160" height="40">
      
      <address>
        234 Washington Street<br>
        Urbana, Illinois
      </address>
      <div>
        <ul>
          <li><a href="https://www.facebook.com/HolbertonSchool/">Facebook</a></li>
          <li><a href="https://twitter.com/holbertonschool">Twitter</a></li>
          <li><a href="https://www.instagram.com/holbertonschool/">Instagram</a></li>
        </ul>
      </div>

      <hr>
      <p>© 2020 Techium, made with ♥ by students at Holberton School.</p>

      <div>
        <ul>
          <li><a href="#">Terms of Use</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Cookie Policy</a></li>
        </ul>
      </div>
    </footer>
  </body>
</html>

```

---
##  37. Social icons

`index.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Homepage - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>

    <!-- Header -->
    <header>
      <div>
        <div>
          <a href="/">
            <img src="logo-black.png" alt="Techium logo" width="160" height="40">
          </a>
        </div>
        <nav>
          <ul>
            <li><a href="/">Home</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#works">Works</a></li>
            <li><a href="#about">About</a></li>
            <li><a href="#latest_news">Latest news</a></li>
            <li><a href="#testimonials">Testimonials</a></li>
            <li><a href="#contact">Contact</a></li>
          </ul>
        </nav>
      </div>
    </header>

    <!-- Main -->
    <main>
      <h1>Homepage</h1>

      <!-- Hero section -->
      <section>
        <div>
          <h2>We help you build your brand!</h2>
          <a href="#">Get started</a>
        </div>
      </section>

      <!-- Services section -->
      <section id="services">
        <div>
          <header>
            <h2>Services</h2>
            <p>We work with you</p>
          </header>
          <div>
            <h3><a href="#">Design &amp; Concept</a></h3>
            <h3><a href="#">Digital Strategy</a></h3>
            <h3><a href="#">Content Strategy</a></h3>
            <h3><a href="#">UX Design</a></h3>
            <h3><a href="#">Web Development</a></h3>
            <h3><a href="#">Social Media</a></h3>
          </div>
        </div>
      </section>

      <!-- Works section -->
      <section id="works">
        <div>
          <header>
            <h2>Works</h2>
            <p>Take a look in our portfolio</p>
          </header>
          <div>
            <article>
              <div>
                <img src="images/pic-work-01.jpg" alt="">
              </div>
              <h3><a href="#">Interior Design</a></h3>
            </article>
            <article>
              <div>
                <img src="images/pic-work-02.jpg" alt="">
              </div>
              <h3><a href="#">Web Development</a></h3>
            </article>
            <article>
              <div>
                <img src="images/pic-work-03.jpg" alt="">
              </div>
              <h3><a href="#">Personal Brand</a></h3>
            </article>
          </div>
        </div>
      </section>

      <!-- About Us section -->
      <section id="about">
        <div>
          <header>
            <h2>About Us</h2>
            <p>Everything about us</p>
          </header>
          <div>
            <img src="images/pic-about-us.jpg" alt="" width="460" height="447">
            <h3>Who are we</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>Our culture</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
            <h3>How we work</h3>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit...</p>
          </div>
          <a href="about.html">Learn more about us</a>
        </div>
      </section>

      <!-- Latest news section -->
      <section id="latest_news">
        <div>
          <header>
            <h2>Latest news</h2>
          </header>
          <div>
            <article>
              <div>
                <img src="images/pic-blog-01.jpg" alt="" width="305" height="205">
              </div>
              <p>Career</p>
              <h3><a href="#">Hoc loco tenere se Triarius non potuit.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
              <small>By Kelly D.</small>
            </article>
            <article>
              <div>
                <img src="images/pic-blog-02.jpg" alt="" width="305" height="205">
              </div>
              <p>Digital Life</p>
              <h3><a href="#">Ut alios omittam, hunc appello, quem ille unum secutus est.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
              <small>By William A.</small>
            </article>
            <article>
              <div>
                <img src="images/pic-blog-03.jpg" alt="" width="305" height="205">
              </div>
              <p>Social</p>
              <h3><a href="#">Bestiarum vero nullum iudicium puto.</a></h3>
              <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>
              <small>By Frances J.</small>
            </article>
          </div>
        </div>
      </section>

      <!-- Testimonials section -->
      <section id="testimonials">
        <div>
          <header>
            <h2>Testimonials</h2>
            <p>We are more than a digital company</p>
          </header>
          <div>
            <article>
              <img src="images/pic-person-01.jpg" alt="Yuri Y. avatar" width="100" height="100">
              <blockquote>
                <p>I am completely blown away. Thanks to Techium, we've just launched our 5th website!</p>
                <cite>Yuri Y.</cite>
              </blockquote>
            </article>
            <article>
              <img src="images/pic-person-02.jpg" alt="Dorrie S. avatar" width="100" height="100">
              <blockquote>
                <p>Thank you so much for your help. Techium company is awesome!</p>
                <cite>Dorrie S.</cite>
              </blockquote>
            </article>
            <article>
              <img src="images/pic-person-03.jpg" alt="Sven H. avatar" width="100" height="100">
              <blockquote>
                <p>I love your system. Definitely worth the investment. I'd be lost without Techium company.</p>
                <cite>Sven H.</cite>
              </blockquote>
            </article>
          </div>
        </div>
      </section>

      <!-- Contact section -->
      <section id="contact">
        <div>
          <header>
            <h2>Contact</h2>
            <p>We like to know new people</p>
          </header>
          <div>
            <p>Lorem ipsum dolor sit amet...</p>
          </div>
          <a href="contact.html">Get in touch</a>
        </div>
      </section>

    </main>

    <!-- Footer -->
    <footer>
      <img src="logo-black.png" alt="Techium logo" width="160" height="40">
      
      <address>
        234 Washington Street<br>
        Urbana, Illinois
      </address>
      <div>
        <ul>
          <li>
            <a href="https://www.facebook.com/HolbertonSchool/">
              <svg viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="25" height="25"><title>Facebook icon</title><path d="M23.998 12c0-6.628-5.372-12-11.999-12C5.372 0 0 5.372 0 12c0 5.988 4.388 10.952 10.124 11.852v-8.384H7.078v-3.469h3.046V9.356c0-3.008 1.792-4.669 4.532-4.669 1.313 0 2.686.234 2.686.234v2.953H15.83c-1.49 0-1.955.925-1.955 1.874V12h3.328l-.532 3.469h-2.796v8.384c5.736-.9 10.124-5.864 10.124-11.853z"/></svg>
            </a>
          </li>
          <li>
            <a href="https://twitter.com/holbertonschool">
              <svg viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="25" height="25"><title>Twitter icon</title><path d="M23.954 4.569a10 10 0 0 1-2.825.775 4.958 4.958 0 0 0 2.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 0 0-8.384 4.482C7.691 8.094 4.066 6.13 1.64 3.161a4.822 4.822 0 0 0-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 0 1-2.228-.616v.061a4.923 4.923 0 0 0 3.946 4.827 4.996 4.996 0 0 1-2.212.085 4.937 4.937 0 0 0 4.604 3.417 9.868 9.868 0 0 1-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 0 0 7.557 2.209c9.054 0 13.999-7.496 13.999-13.986 0-.209 0-.42-.015-.63a9.936 9.936 0 0 0 2.46-2.548l-.047-.02z"/></svg>
            </a>
          </li>
          <li>
            <a href="https://www.instagram.com/holbertonschool/">
              <svg viewbox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" width="25" height="25"><title>Instagram icon</title><path d="M12 0C8.74 0 8.333.015 7.053.072 5.775.132 4.905.333 4.14.63c-.789.306-1.459.717-2.126 1.384S.935 3.35.63 4.14C.333 4.905.131 5.775.072 7.053.012 8.333 0 8.74 0 12s.015 3.667.072 4.947c.06 1.277.261 2.148.558 2.913a5.885 5.885 0 0 0 1.384 2.126A5.868 5.868 0 0 0 4.14 23.37c.766.296 1.636.499 2.913.558C8.333 23.988 8.74 24 12 24s3.667-.015 4.947-.072c1.277-.06 2.148-.262 2.913-.558a5.898 5.898 0 0 0 2.126-1.384 5.86 5.86 0 0 0 1.384-2.126c.296-.765.499-1.636.558-2.913.06-1.28.072-1.687.072-4.947s-.015-3.667-.072-4.947c-.06-1.277-.262-2.149-.558-2.913a5.89 5.89 0 0 0-1.384-2.126A5.847 5.847 0 0 0 19.86.63c-.765-.297-1.636-.499-2.913-.558C15.667.012 15.26 0 12 0zm0 2.16c3.203 0 3.585.016 4.85.071 1.17.055 1.805.249 2.227.415.562.217.96.477 1.382.896.419.42.679.819.896 1.381.164.422.36 1.057.413 2.227.057 1.266.07 1.646.07 4.85s-.015 3.585-.074 4.85c-.061 1.17-.256 1.805-.421 2.227a3.81 3.81 0 0 1-.899 1.382 3.744 3.744 0 0 1-1.38.896c-.42.164-1.065.36-2.235.413-1.274.057-1.649.07-4.859.07-3.211 0-3.586-.015-4.859-.074-1.171-.061-1.816-.256-2.236-.421a3.716 3.716 0 0 1-1.379-.899 3.644 3.644 0 0 1-.9-1.38c-.165-.42-.359-1.065-.42-2.235-.045-1.26-.061-1.649-.061-4.844 0-3.196.016-3.586.061-4.861.061-1.17.255-1.814.42-2.234.21-.57.479-.96.9-1.381.419-.419.81-.689 1.379-.898.42-.166 1.051-.361 2.221-.421 1.275-.045 1.65-.06 4.859-.06l.045.03zm0 3.678a6.162 6.162 0 1 0 0 12.324 6.162 6.162 0 1 0 0-12.324zM12 16c-2.21 0-4-1.79-4-4s1.79-4 4-4 4 1.79 4 4-1.79 4-4 4zm7.846-10.405a1.441 1.441 0 0 1-2.88 0 1.44 1.44 0 0 1 2.88 0z"/></svg>
            </a>
          </li>
        </ul>
      </div>

      <hr>
      <p>© 2020 Techium, made with ♥ by students at Holberton School.</p>

      <div>
        <ul>
          <li><a href="#">Terms of Use</a></li>
          <li><a href="#">Privacy Policy</a></li>
          <li><a href="#">Cookie Policy</a></li>
        </ul>
      </div>
    </footer>
  </body>
</html>

```
**Logica**
Para este archivo final (index.html), los cambios principales respecto a la versión anterior (36-index.html) se centran exclusivamente en el Footer y en la identidad del archivo. Aquí tienes el resumen de las modificaciones:

Renombrado del archivo: El contenido se traslada de 36-index.html a index.html, que es el nombre estándar para la página de inicio de cualquier sitio web.

Sustitución de texto por Iconos Sociales (SVG):

Se eliminaron las palabras "Facebook", "Twitter" e "Instagram" que servían como enlaces.

En su lugar, se insertó el código SVG de cada red social.

Esto hace que los enlaces ahora sean visuales (iconos) en lugar de simple texto.

Dimensiones de los iconos:

A cada etiqueta <svg> se le añadieron los atributos width="25" y height="25" para asegurar que todos los iconos tengan un tamaño uniforme y pequeño en el pie de página.

Accesibilidad en los SVG:

Se incluyó la etiqueta <title> dentro de cada código SVG (por ejemplo, Facebook icon), lo cual es una buena práctica para que los lectores de pantalla identifiquen el enlace.

---
##  38. Add a video player in the styleguide

`38-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <!-- Headings -->
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>
      <!-- Paragraph -->
      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>
      <!-- Lists -->
      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>
        
          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>

          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>
      <!-- Horizontal rule -->
      <section>
        <header>
          <h2>Horizontal rule</h2>
        </header>
        <div>
          <hr>
        </div>
      </section>
      <!-- Blockquotes -->
      <section>
        <header>
          <h2>Blockquotes</h2>
        </header>
        <div>
          <h3>Inline quote</h3>
          <q>Stay hungry. Stay foolish.</q>
        </div>
        <div>
          <h3>Blockquote</h3>
          <blockquote>
            <p>I will be the leader of a company that ends up being worth billions of dollars, because I got the answers. I understand culture. I am the nucleus. I think that’s a responsibility that I have, to push possibilities, to show people, this is the level that things could be at.</p>
            <cite>Kanye West, Musician</cite>
          </blockquote>
        </div>
      </section>
      <!-- Typography -->
      <section>
        <header>
          <h2>Typography</h2>
        </header>
        <div>
          <address>
            320 Stewart Avenue, Unit 12<br>
            New York City NY 10001
          </address>
        </div>
        <div>
          <pre>
            &lt;h2&gt;My title&lt;/h2&gt;
            &lt;p&gt;Proin lacus turpis, feugiat sit amet sollicitudin non, volutpat in libero. Aenean hendrerit ultrices nulla ac lobortis. Vestibulum consectetur nibh vel ante rhoncus faucibus.&lt;/p&gt;
          </pre>
        </div>
        <div>
          <p>Curabitur sit amet turpis cursus massa mollis <mark>highlighted</mark>. Duis finibus leo massa, eget dapibus erat finibus sed. Aenean condimentum sapien magna, eleifend <mark>highlighted</mark> mi consequat ut. Cras nec quam sed sapien ultricies <mark>highlighted</mark> ut sed metus.</p>
        </div>
      </section>
      <!-- Table -->
      <section>
        <header>
          <h2>Table</h2>
        </header>
        <table>
          <thead>
            <tr>
              <th scope="col">Title</th>
              <th scope="col">Director</th>
              <th scope="col">Release Date</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Star Wars: Episode IV – A New Hope</th>
              <td>George Lucas</td>
              <td>May 25, 1977</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode V – The Empire Strikes Back</th>
              <td>Irvin Kershner</td>
              <td>May 21, 1980</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode VI – Return of the Jedi</th>
              <td>Richard Marquand</td>
              <td>May 25, 1983</td>
            </tr>
          </tbody>
        </table>
      </section>
      <!-- Details -->
      <section>
        <header>
          <h2>Details</h2>
        </header>
        <div>
          <h3>Default</h3>
          <details>
            <summary>Show/Hide me</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
        <div>
          <h3>Open</h3>
          <details open>
            <summary>Always open</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
      </section>
      <!-- Video -->
      <section>
        <header>
          <h2>Video</h2>
        </header>
        <video src="https://intranet-projects-files.s3.amazonaws.com/webstack/BigBuckBunny.mp4" controls loop poster="https://intranet-projects-files.s3.amazonaws.com/webstack/thumbnail.jpg">
          Sorry, your browser doesn't support HTML5 video
        </video>
      </section>

    </main>
    <footer></footer>
  </body>
</html>

```

---
##  39. Add an audio player in the styleguide

`39-styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <!-- Headings -->
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>
      <!-- Paragraph -->
      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>
      <!-- Lists -->
      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>
        
          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>

          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>
      <!-- Horizontal rule -->
      <section>
        <header>
          <h2>Horizontal rule</h2>
        </header>
        <div>
          <hr>
        </div>
      </section>
      <!-- Blockquotes -->
      <section>
        <header>
          <h2>Blockquotes</h2>
        </header>
        <div>
          <h3>Inline quote</h3>
          <q>Stay hungry. Stay foolish.</q>
        </div>
        <div>
          <h3>Blockquote</h3>
          <blockquote>
            <p>I will be the leader of a company that ends up being worth billions of dollars, because I got the answers. I understand culture. I am the nucleus. I think that’s a responsibility that I have, to push possibilities, to show people, this is the level that things could be at.</p>
            <cite>Kanye West, Musician</cite>
          </blockquote>
        </div>
      </section>
      <!-- Typography -->
      <section>
        <header>
          <h2>Typography</h2>
        </header>
        <div>
          <address>
            320 Stewart Avenue, Unit 12<br>
            New York City NY 10001
          </address>
        </div>
        <div>
          <pre>
            &lt;h2&gt;My title&lt;/h2&gt;
            &lt;p&gt;Proin lacus turpis, feugiat sit amet sollicitudin non, volutpat in libero. Aenean hendrerit ultrices nulla ac lobortis. Vestibulum consectetur nibh vel ante rhoncus faucibus.&lt;/p&gt;
          </pre>
        </div>
        <div>
          <p>Curabitur sit amet turpis cursus massa mollis <mark>highlighted</mark>. Duis finibus leo massa, eget dapibus erat finibus sed. Aenean condimentum sapien magna, eleifend <mark>highlighted</mark> mi consequat ut. Cras nec quam sed sapien ultricies <mark>highlighted</mark> ut sed metus.</p>
        </div>
      </section>
      <!-- Table -->
      <section>
        <header>
          <h2>Table</h2>
        </header>
        <table>
          <thead>
            <tr>
              <th scope="col">Title</th>
              <th scope="col">Director</th>
              <th scope="col">Release Date</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Star Wars: Episode IV – A New Hope</th>
              <td>George Lucas</td>
              <td>May 25, 1977</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode V – The Empire Strikes Back</th>
              <td>Irvin Kershner</td>
              <td>May 21, 1980</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode VI – Return of the Jedi</th>
              <td>Richard Marquand</td>
              <td>May 25, 1983</td>
            </tr>
          </tbody>
        </table>
      </section>
      <!-- Details -->
      <section>
        <header>
          <h2>Details</h2>
        </header>
        <div>
          <h3>Default</h3>
          <details>
            <summary>Show/Hide me</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
        <div>
          <h3>Open</h3>
          <details open>
            <summary>Always open</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
      </section>
      <!-- Video -->
      <section>
        <header>
          <h2>Video</h2>
        </header>
        <video src="https://intranet-projects-files.s3.amazonaws.com/webstack/BigBuckBunny.mp4" controls loop poster="https://intranet-projects-files.s3.amazonaws.com/webstack/thumbnail.jpg">
          Sorry, your browser doesn't support HTML5 video
        </video>
      </section>
      <!-- Audio -->
      <section>
        <header>
          <h2>Audio</h2>
        </header>
        <audio src="https://intranet-projects-files.s3.amazonaws.com/webstack/TroubleChapter8_64kb.mp3" controls>
          Sorry, your browser doesn't support audio element
        </audio>
      </section>

    </main>
    <footer></footer>
  </body>
</html>

```
**Logica**
Resumen de lo logrado:
Audio Nativo: Implementaste el elemento <audio> con el atributo controls (indispensable para que el usuario pueda darle play).

Compatibilidad: Añadiste el mensaje de respaldo para navegadores antiguos.

Orden: La sección de audio aparece correctamente después de la de video.

Herencia: El archivo conserva todo el progreso desde las tareas de tablas, tipografía y detalles.
---
##  40. Add a iframe example in the styleguide

`styleguide.html`
```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Styleguide - Techium</title>
    <meta name="description" content="Techium is a digital agency">
    <link rel="icon" type="image/x-icon" href="./favicon.ico">
    <link rel="icon" type="image/png" href="./favicon.png">
  </head>
  <body>
    <header></header>
    <main>
      <!-- Headings -->
      <section>
        <header>
          <h2>Headings</h2>
        </header>
        <h1>Heading level 1</h1>
        <h2>Heading level 2</h2>
        <h3>Heading level 3</h3>
        <h4>Heading level 4</h4>
        <h5>Heading level 5</h5>
        <h6>Heading level 6</h6>
      </section>
      <!-- Paragraph -->
      <section>
        <header>
          <h2>Paragraph</h2>
        </header>
        <h2>Heading with a subtitle</h2>
        <p>This is my subtitle</p>
        <p>Nunc lacinia ante nunc ac lobortis. Interdum adipiscing gravida odio porttitor sem non mi integer non faucibus ornare mi ut ante amet placerat aliquet. Volutpat eu sed ante lacinia sapien lorem accumsan varius montes viverra nibh in adipiscing blandit tempus accumsan.</p>
      </section>
      <!-- Lists -->
      <section>
        <header>
          <h2>Lists</h2>
        </header>
        <div>
          <h3>Unordered</h3>
          <ul>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ul>
        
          <h3>Ordered</h3>
          <ol>
            <li>Dolor pulvinar etiam magna etiam.</li>
            <li>Sagittis adipiscing lorem eleifend.</li>
            <li>Felis enim feugiat dolore viverra.</li>
          </ol>

          <h3>Definition</h3>
          <dl>
            <dt>Definition List title</dt>
            <dd>Definition text.</dd>
            <dt>Startup</dt>
            <dd>A startup company or startup is a company or temporary organization designed to search for a repeatable and scalable business model.</dd>
            <dt>Water</dt>
            <dd>A colorless, transparent, odorless liquid that forms the seas, lakes, rivers, and rain and is the basis of the fluids of living organisms.</dd>
          </dl>
        </div>
      </section>
      <!-- Horizontal rule -->
      <section>
        <header>
          <h2>Horizontal rule</h2>
        </header>
        <div>
          <hr>
        </div>
      </section>
      <!-- Blockquotes -->
      <section>
        <header>
          <h2>Blockquotes</h2>
        </header>
        <div>
          <h3>Inline quote</h3>
          <q>Stay hungry. Stay foolish.</q>
        </div>
        <div>
          <h3>Blockquote</h3>
          <blockquote>
            <p>I will be the leader of a company that ends up being worth billions of dollars, because I got the answers. I understand culture. I am the nucleus. I think that’s a responsibility that I have, to push possibilities, to show people, this is the level that things could be at.</p>
            <cite>Kanye West, Musician</cite>
          </blockquote>
        </div>
      </section>
      <!-- Typography -->
      <section>
        <header>
          <h2>Typography</h2>
        </header>
        <div>
          <address>
            320 Stewart Avenue, Unit 12<br>
            New York City NY 10001
          </address>
        </div>
        <div>
          <pre>
            &lt;h2&gt;My title&lt;/h2&gt;
            &lt;p&gt;Proin lacus turpis, feugiat sit amet sollicitudin non, volutpat in libero. Aenean hendrerit ultrices nulla ac lobortis. Vestibulum consectetur nibh vel ante rhoncus faucibus.&lt;/p&gt;
          </pre>
        </div>
        <div>
          <p>Curabitur sit amet turpis cursus massa mollis <mark>highlighted</mark>. Duis finibus leo massa, eget dapibus erat finibus sed. Aenean condimentum sapien magna, eleifend <mark>highlighted</mark> mi consequat ut. Cras nec quam sed sapien ultricies <mark>highlighted</mark> ut sed metus.</p>
        </div>
      </section>
      <!-- Table -->
      <section>
        <header>
          <h2>Table</h2>
        </header>
        <table>
          <thead>
            <tr>
              <th scope="col">Title</th>
              <th scope="col">Director</th>
              <th scope="col">Release Date</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">Star Wars: Episode IV – A New Hope</th>
              <td>George Lucas</td>
              <td>May 25, 1977</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode V – The Empire Strikes Back</th>
              <td>Irvin Kershner</td>
              <td>May 21, 1980</td>
            </tr>
            <tr>
              <th scope="row">Star Wars: Episode VI – Return of the Jedi</th>
              <td>Richard Marquand</td>
              <td>May 25, 1983</td>
            </tr>
          </tbody>
        </table>
      </section>
      <!-- Details -->
      <section>
        <header>
          <h2>Details</h2>
        </header>
        <div>
          <h3>Default</h3>
          <details>
            <summary>Show/Hide me</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
        <div>
          <h3>Open</h3>
          <details open>
            <summary>Always open</summary>
            Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.
          </details>
        </div>
      </section>
      <!-- Video -->
      <section>
        <header>
          <h2>Video</h2>
        </header>
        <video src="https://intranet-projects-files.s3.amazonaws.com/webstack/BigBuckBunny.mp4" controls loop poster="https://intranet-projects-files.s3.amazonaws.com/webstack/thumbnail.jpg">
          Sorry, your browser doesn't support HTML5 video
        </video>
      </section>
      <!-- Audio -->
      <section>
        <header>
          <h2>Audio</h2>
        </header>
        <audio src="https://intranet-projects-files.s3.amazonaws.com/webstack/TroubleChapter8_64kb.mp3" controls>
          Sorry, your browser doesn't support audio element
        </audio>
      </section>
      <!-- Iframe -->
      <section>
        <header>
          <h2>Iframe</h2>
        </header>
        <div>
          <iframe title="Holberton School" width="350" height="200" src="https://www.youtube.com/embed/41N6bKO-NVI">
            Holberton Sally
          </iframe>
        </div>
      </section>
    </main>
    <footer></footer>
  </body>
</html>

```
**Logica**
Conceptos clave de la Task 40
<iframe>: Es como una "ventana" que muestra una página web dentro de otra. Es la forma estándar de insertar videos de YouTube o mapas de Google.

title: Es fundamental para la accesibilidad; ayuda a las personas que usan lectores de pantalla a saber qué contenido hay dentro del marco.

Fallback text: El texto "Holberton Sally" solo aparecerá si el navegador del usuario tiene bloqueados los iframes o no los soporta.

Medidas: Al igual que con las imágenes, en HTML ponemos solo el número (width="350"), aunque la consigna mencione "px".
---
