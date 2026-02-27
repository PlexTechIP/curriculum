---
layout: default
title: "Week 3: JavaScript and React Intro"
---

# Week 3: JavaScript and React Intro

<a href="https://classroom.github.com/a/hJSI9PkS" class="assignment-btn" target="_blank" rel="noopener">Get Starter Code on GitHub →</a>


## Part 1: JavaScript Basics

Before diving into React, make sure you're comfortable with basic JavaScript. To add interactivity to HTML, use the `<script>` tag inside `<body>`. Key syntax:

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

### JavaScript Lab

Download the starter file **`js-lab.html`** and open it in your browser. Complete all 4 exercises inside the file — each one has a clearly marked `// YOUR CODE HERE` section and instructions directly above it.

| # | Exercise | Concepts |
|---|----------|----------|
| 1 | **Variables & Data Types** | `const` vs `let`, template literals, `typeof` |
| 2 | **Functions** | Writing and calling functions, parameters, return values |
| 3 | **Conditionals** | `if / else if / else`, comparison operators |
| 4 | **Objects** | Object literals, dot notation, passing objects to functions |

**Tips:**
- Open your browser's DevTools console (**F12 → Console**) to see `console.log` output and any errors.
- All 4 exercises have built-in "Check" buttons that validate your output.
- For anything you're unsure of, look it up on [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript) — it's your best reference.

---

## Part 2: Counter App

React is a JavaScript library for creating interactive user interfaces (UIs). Here are some useful terms:

| Term | Definition |
|------|-------------|
| **Components** | Small reusable pieces of code that return React elements in *JSX*. React apps contain components, not pages. |
| **State** | Variables stored inside a component. When state changes, the component re-renders. |
| **Props** | Data passed from a parent component to a child component. |

### Resources

Refer to the [Official React Tutorial](https://reactjs.org/tutorial/tutorial.html). Note: it uses older class-based components; the modern approach is functional components with Hooks. Also use Stack Overflow, MDN, W3, and Google for reference.


### Setup


1. Make sure you have npm installed.

3. Go into this directory:
   ```bash
   cd "Static React"
   ```

4. Initialize an empty React app:
   ```bash
   npm install create-react-app
   npx create-react-app counter-app
   ```

5. Start the React server:
   ```bash
   cd counter-app
   npm start
   ```

### Your Task

Build a counter app — an increment/decrement counter. Feel free to make it pretty!

### Walkthrough

#### Step 1: Create a Button Component

Both the `+` and `-` buttons share the same structure. Rather than writing two separate button elements, create a reusable **Button** component that accepts two props:

- **`title`** — the label to display (e.g. `"+"` or `"-"`)
- **`task`** — the function to run when clicked

Create a new file at `src/components/Button.js`. Your component should be a function (or arrow function) that takes `{title, task}` as props and returns a `<button>` element. Hook up the `task` prop to `onClick`, and display `title` as the button's text.

Think about: what does `onClick={task}` do differently than `onClick={task()}`?

<details markdown="1">
<summary>Show solution</summary>

```jsx
// components/Button.js
import React from 'react';

var Button = ({title, task}) => {
    return (
        <button onClick={task}>{title}</button>
    );
}

export default Button;
```

**Breaking it down:**

- `import React from 'react'` — required in every React file
- `({title, task})` — destructures props; equivalent to `props.title` and `props.task`
- `onClick={task}` — attaches the passed-in function as the click handler
- `export default Button` — makes this component importable elsewhere

**Named vs. Default Exports:**
- **Default export**: `import Button from './Button'` — one per file
- **Named export**: `import { Button } from './Button'` — multiple allowed per file

</details>

#### Step 2: State in App.js

Now wire everything together in `App.js`. You'll need:

1. **State** — a variable to hold the current count. Use `useState(0)` to initialize it at zero. Remember, `useState` returns two things: the current value, and a setter function.
2. **Two handler functions** — one to increment, one to decrement. Each should call the setter with the updated count.
3. **JSX** — render a heading, your two `<Button>` components, and the count value in between. Pass each handler as the `task` prop to its button.

Import your `Button` component at the top and make sure to import `useState` from React.

<details markdown="1">
<summary>Show solution</summary>

```jsx
import React, { useState } from 'react';
import Button from './components/Button';

function App() {
    const [count, setCount] = useState(0);

    const incrementCount = () => setCount(count + 1);
    const decrementCount = () => setCount(count - 1);

    return (
        <div>
            <h1>Counter</h1>
            <Button title="+" task={incrementCount} />
            <h2>{count}</h2>
            <Button title="-" task={decrementCount} />
        </div>
    );
}

export default App;
```

**Why `task={incrementCount}` and not `task={incrementCount()}`?**

- `task={incrementCount}` — passes the **function reference** (correct ✓)
- `task={incrementCount()}` — **calls** the function immediately and passes its return value (wrong ✗)
- `task={() => incrementCount()}` — also correct, an arrow function that calls it on click

</details>

#### Step 3: Style It

Add your own CSS to `src/App.css` or use inline styles to make the counter look polished. Get creative!

#### Step 4: Add a Second Page with React Router

React apps don't use multiple HTML files — they simulate "pages" with **React Router**. Each "page" is just a component that renders based on the current URL path.

Your goal: add a simple About page and two navigation buttons — one on the counter to go to About, and one on About to go back.

Before looking at the solution, think through:
- What component renders at `"/"` vs `"/about"`?
- How would a button change the URL without refreshing the page?
- Where does `<BrowserRouter>` need to live relative to your routes?

Install React Router first:
```bash
npm install react-router-dom
```

<details markdown="1">
<summary>Show solution</summary>

Create `src/pages/About.js`:
```jsx
import React from 'react';
import { useNavigate } from 'react-router-dom';

function About() {
    const navigate = useNavigate();
    return (
        <div>
            <h1>About</h1>
            <p>This is a simple counter app built with React.</p>
            <button onClick={() => navigate('/')}>← Back to Counter</button>
        </div>
    );
}

export default About;
```

Update `App.js` to use a Router:
```jsx
import React, { useState } from 'react';
import { BrowserRouter, Routes, Route, useNavigate } from 'react-router-dom';
import Button from './components/Button';
import About from './pages/About';

function Counter() {
    const [count, setCount] = useState(0);
    const navigate = useNavigate();

    return (
        <div>
            <h1>Counter</h1>
            <Button title="+" task={() => setCount(count + 1)} />
            <h2>{count}</h2>
            <Button title="-" task={() => setCount(count - 1)} />
            <br />
            <button onClick={() => navigate('/about')}>About →</button>
        </div>
    );
}

function App() {
    return (
        <BrowserRouter>
            <Routes>
                <Route path="/" element={<Counter />} />
                <Route path="/about" element={<About />} />
            </Routes>
        </BrowserRouter>
    );
}

export default App;
```

**Key ideas:**
- `<BrowserRouter>` wraps your whole app and enables routing
- `<Routes>` + `<Route>` map URL paths to components
- `useNavigate()` gives you a function to programmatically change pages with a button click

</details>


---

## Submission

Push your completed code to your lab repository.
