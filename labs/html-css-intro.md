---
layout: default
title: "Week 2: HTML/CSS Introduction"
---

# HTML/CSS Introduction

<a href="https://classroom.github.com/a/2Qs30stP" class="assignment-btn" target="_blank" rel="noopener">Accept Assignment on GitHub Classroom →</a>

This project will guide you through how to use HTML to build web pages, style them with CSS, and add basic interactivity with JavaScript.

---

## Part 1: Structure of HTML

Every HTML document is made up of tags that denote elements and define where they appear on the page. Every document starts with this skeleton:

```html
<!DOCTYPE html>
<html>
    <head>
        ...
    </head>
    <body>
        ...
    </body>
</html>
```

Key tags:

- `<!DOCTYPE html>` — defines the document type (HTML5)
- `<html>` — root element wrapping all content
- `<head>` — metadata (title, favicon, author, description) — not visible on the page
- `<body>` — visible page content

### Your Task

Open `activity.html` in the project folder. To open it in Git Bash, run:

```bash
start ./activity.html
```

You'll see an empty page. Complete the following:

- Add a **title** of your choice to the webpage
- Add a **favicon** of your choice
- Change the **author** to your name
- Add a custom **description**

> *You won't be able to see some of these changes reflected on the page — why?*

---

## Part 2: Elements

These are the most common tags you'll use inside `<body>`:

| Tag | Purpose |
|-----|---------|
| `<div>` | Generic container, useful for layout |
| `<p>` | Paragraph text |
| `<h1>` to `<h6>` | Headers, largest to smallest |
| `<img>` | Embed images |
| `<ul>`, `<ol>`, `<li>` | Unordered and ordered lists |
| `<a>` | Hyperlinks |

HTML also provides **semantic elements** that behave exactly like `<div>` but carry meaning about their purpose:

| Tag | Meaning |
|-----|---------|
| `<header>` | Top section of a page, typically a title or nav |
| `<nav>` | Navigation links |
| `<main>` | Primary content area |
| `<footer>` | Bottom section, often credits or links |

`<header>My Site</header>` and `<div>My Site</div>` render identically — but the semantic version makes your code immediately readable.

### Flexboxes

For positioning, use **flexbox** — a container that automatically arranges its children in a row or column. Enable it with `display: flex` on a parent element.

Key properties:

| Property | What it does |
|----------|-------------|
| `flex-direction` | `row` (default) or `column` |
| `justify-content` | Aligns along main axis: `flex-start`, `center`, `space-between`, etc. |
| `align-items` | Aligns along cross axis: `center` to vertically center in a row |
| `gap` | Space between children, e.g. `gap: 10px` |
| `flex-wrap` | `wrap` or `nowrap` — whether children wrap to a new line |
| `flex` / `flex-grow` | How much a child grows to fill available space |

Full guide: [CSS Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

### Your Task

Build out the body of `activity.html` with the following structure. Use **inline styling** for now.

- A **header** with a title
- A **sidebar or navbar**
- A **main body** with multiple images
- A **footer**

> *Hint: Plan out your layout on paper before writing code.*

---

## Part 3: JavaScript

To add interactivity, use the `<script>` tag inside `<body>`. Key syntax:

```javascript
// Variables
const name = "Plextech";  // read-only reference
let count = 0;             // reassignable
var x = 5;                 // also reassignable (older style)

// Functions
function greet(p1, p2) {
    // BODY
}
```

To reference elements on the page, use the `document` object:

```javascript
document.getElementById("my-id")
```

Example — display today's date:

```html
<script>
    let d = new Date();
    document.body.innerHTML = "<h1>Today's date is " + d + "</h1>";
</script>
```

Example — button that changes text color on click:

```html
<p id="demo">click on the button</p>
<button onclick="green()">Change to green</button>
<script>
    function green() {
        var el = document.getElementById("demo");
        el.style.color = "#00FF00";
    }
</script>
```

### Your Task

Add two buttons to your header that toggle **light mode** and **dark mode**. These should change:
- Background colors
- Font colors

Use a variety of shades for each theme — your choice of colors.

---

## Part 4: CSS Styling

There are three ways to apply CSS:

| Type | Where | Notes |
|------|-------|-------|
| **Inline** | `style` attribute on each element | Quick but messy |
| **Internal** | `<style>` tag in `<head>` | Better organization |
| **External** | Separate `.css` file linked with `<link>` | Best practice ✓ |

### Selectors

```css
/* All <p> tags */
p { color: green; }

/* Multiple tags — comma-separated */
p, h1 { color: green; }

/* Element with id="example" — IDs must be unique on the page */
#example { font-size: 20px; }

/* All elements with class="example" — many elements can share a class */
.example { font-size: 30px; }

/* Chain classes: elements with both "example" and "other" */
.example.other { color: blue; }

/* <h1> that is a direct child of a <div> */
div > h1 { color: red; }
```

> **`id` vs `class`:** Use `id` for a single unique element (e.g. `#navbar`). Use `class` for styles applied to many elements (e.g. `.card`).

To link an external stylesheet in your HTML:

```html
<head>
    <link rel="stylesheet" href="styles.css">
</head>
```

### Your Task

Transfer all your inline styles from `activity.html` into an **external CSS file** and link it.

---

## JavaScript Assignment

Complete the exercises at [W3Schools JS Exercises](https://www.w3schools.com/js/exercise_js.asp?filename=exercise_js_variables1).

For anything not covered in lecture, look it up!

---

## Divs & Rectangles Assignment

### Intro

Now that you understand HTML and CSS basics, practice **flexbox layout** by recreating a set of styled rectangles. This is a classic layout exercise used in Brown University's CSCI 1320.

### Resources

- [CSS Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [MDN Web Docs](https://developer.mozilla.org/), [W3Schools](https://www.w3schools.com/), Stack Overflow

### Your Task

Open `part1/index.html`. There are 9 green rectangles — the first two are already built for you.

**Add divs and styles inside the next 7 to match the finished layout. The blocks must be responsive** — they should resize correctly when the window narrows.

### Row Requirements

| Row | Behavior | Hint |
|-----|----------|------|
| **3** | Red and blue ends stay fixed width; green space shrinks | Use `justify-content` |
| **4** | Blue end stays fixed; red shrinks | Use `flex-grow` on the red div |
| **5** | Red square stays fixed, always centered in green area | Fixed size + `justify-content: center` + `align-items: center` |
| **6** | Blue stays fixed and centered; red rectangles shrink on both sides | Use two red divs |
| **7** | Red stays the same width | Nest divs, use `background-color: transparent` |
| **8** | Orange rectangles stay fixed; green space between them shrinks | Fixed-width orange divs |
| **9** | Green space stays fixed; orange rectangles narrow | Fixed-width gap between flex children |

### Rules

- Only use `<div>` elements inside the wrapper divs
- No inner divs should have `background-color: green`
- Colors: `red`, `blue`, `orange`
- Reference dimensions: `20px`, `40px`, `80px`

---

## Submission

Accept the assignment above, clone your repo, and push your completed `activity.html`, CSS file, and `part1/index.html`.
