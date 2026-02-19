---
layout: default
title: "Week 3: Static React — Counter App"
---

# Static React — Counter App

React is a JavaScript library for building interactive user interfaces. In this lab you'll build a counter app and learn core React concepts: components, state, and props.

---

## Key Concepts

| Term | Definition |
|------|-----------|
| **Component** | A reusable piece of UI that returns JSX |
| **State** | Variables stored inside a component; when state changes, the component re-renders |
| **Props** | Data passed from a parent component to a child component |

---

## Setup

1. Pull starter code:
   ```bash
   git pull starter main
   ```

2. Navigate into the project folder:
   ```bash
   cd "Static React"
   ```

3. Create a new React app:
   ```bash
   npm install create-react-app
   npx create-react-app counter-app
   ```

4. Start the dev server:
   ```bash
   cd counter-app
   npm start
   ```

---

## Your Task: Counter App

You'll be building [this counter app](https://i1.wp.com/www.techomoro.com/wp-content/uploads/2020/04/counter-app-working.gif?fit=640%2C335&ssl=1) — an increment/decrement counter. Feel free to make it prettier!

---

## Walkthrough

### Step 1: Create a Button Component

Both the `+` and `-` buttons share the same structure, so build a reusable **Button** component.

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

---

### Step 2: State in App.js

In `App.js`, set up state to track the count.

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

---

### Step 3: Style It

Add your own CSS to `src/App.css` or use inline styles to make the counter look polished. Get creative!

---

## Group Project: Mini Budget App

Build a two-page budget tracking app using React Router.

### Requirements

#### General (both pages)
- Use **React Router** to navigate between pages via buttons
- Create at least **4 different components**

#### Page 1: Data Entry
- At least **3 food categories** (e.g., apples, donuts, pizza), each with a fixed price
- A **counter** for each category, displayed in 3 columns
- A **running list** of purchased items showing name + price per item
- A **Reset** button that clears all purchases

#### Page 2: Recommendations
- Display **2 recommendations**:
  1. One based on **total money spent**
  2. One based on **distribution of items bought**

### Hints

- Pass data between pages using React Router's state
- Use `display: grid` or `flex` for 3-column layout
- Declare separate `useState` variables for each category in the page file and pass them as props to child components
- Suggested file structure:
  ```
  App.js          ← Router lives here
  pages/
  components/     ← Button, LogCounter, Recommendation, etc.
  ```

---

## Resources

- [Official React Tutorial](https://reactjs.org/tutorial/tutorial.html)
- [Functional Components vs Class Components](https://medium.com/star-gazers/react-class-vs-functional-components-a49383f65f0e)
- [JSX Explained](https://www.geeksforgeeks.org/jsx-full-form/)
- [React Router Docs](https://reactrouter.com/)

---

## Submission

Push your completed `counter-app/` and group budget app to your forked repository.
