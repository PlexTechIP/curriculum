---
layout: default
title: "Week 3: JavaScript and React Intro"
---
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

**JavaScript Assignment:** Complete the exercises at [W3Schools JS Exercises](https://www.w3schools.com/js/exercise_js.asp?filename=exercise_js_variables1). For anything not covered in lecture, look it up!

---

## Part 2: Counter App

<a href="https://github.com/som1shi/sp26-plextech-fswd-intro-projects/tree/main/Static%20React" class="assignment-btn" target="_blank" rel="noopener">Get Starter Code on GitHub →</a>

React is a JavaScript library for creating interactive user interfaces (UIs). Here are some useful terms:

| Term | Definition |
|------|-------------|
| **Components** | Small reusable pieces of code that return React elements in *JSX*. React apps contain components, not pages. |
| **State** | Variables stored inside a component. When state changes, the component re-renders. |
| **Props** | Data passed from a parent component to a child component. |

### Resources

Refer to the [Official React Tutorial](https://reactjs.org/tutorial/tutorial.html). Note: it uses older class-based components; the modern approach is functional components with Hooks. Also use Stack Overflow, MDN, W3, and Google for reference.

### A Note on Collaboration

This is a partner project! You will both keep up with your own versions of the code, but should work through this assignment together with constant communication.

### Setup

1. Pull the starter code:
   ```bash
   git pull starter main
   ```

2. Make sure you have npm installed.

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

Build [this counter app](https://i1.wp.com/www.techomoro.com/wp-content/uploads/2020/04/counter-app-working.gif?fit=640%2C335&ssl=1) — an increment/decrement counter. Feel free to make it prettier!

### Walkthrough

#### Step 1: Create a Button Component

Both the `+` and `-` buttons share the same structure, so create a reusable **Button** component.

Create `src/components/Button.js`:

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

#### Step 2: State in App.js

In `App.js`, set up state to track the count using `useState`:

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

#### Step 3: Style It

Add your own CSS to `src/App.css` or use inline styles to make the counter look polished. Get creative!

---

## Group Project: Mini Budget App

Build a mini budget app with 2 pages using React Router.

### General Requirements

- Use **React Router** to navigate between the 2 pages with buttons
- Create at least **4 different components**

### Page 1: Data Entry

- At least **3 different categories** (e.g., apples, donuts, pizza), each with a predetermined price per item
- One **counter** for each category (split across 3 columns)
- A **list** of products that updates when you add or subtract items. Each list item must show name and price
- A **Reset** button that clears all purchases

### Page 2: Recommendations

- Display **2 recommendations**:
  1. One based on **total money spent**
  2. One based on **distribution of items bought**

### Hints

- Pass data between pages using React Router's state
- Use `display: grid` or `flex` for 3-column layout
- Declare separate `useState` variables for each category in the page file; pass them as props to child components
- Suggested file structure:
  ```
  App.js          ← Router lives here
  pages/
  components/     ← Button, LogCounter, Recommendation, etc.
  ```

---

## Submission

Push your completed `counter-app/` and group budget app to your forked repository.
