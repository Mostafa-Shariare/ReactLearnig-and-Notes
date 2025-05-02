

## 🧠 What is `useEffect`?

`useEffect` is a **React Hook** that lets you **run side effects** in function components.

### 🎯 What's a “side effect”?

A side effect is anything that happens **outside** the component's return statement.
Examples:

* Fetching data from an API
* Updating the DOM
* Setting up subscriptions or timers
* Listening for events (like window resize)
* Local storage interaction

---

## 🧪 Basic Syntax

```jsx
import { useEffect } from 'react';

useEffect(() => {
  // Code to run
}, [dependencies]);
```

* The function runs **after** the component renders.
* The second argument (dependency array) controls **when** the effect runs.

---

## 🔰 Example 1: `useEffect` Without Dependency

```jsx
import { useEffect } from 'react';

function App() {
  useEffect(() => {
    console.log('Component rendered or updated');
  });

  return <h1>Hello, React!</h1>;
}
```

### 🧠 What’s happening?

* This `useEffect` runs **after every render**, including the first one and every update.
* Not recommended for most real use cases — can cause performance issues.

---

## 🧰 Example 2: `useEffect` With Empty Dependency Array (`[]`)

```jsx
import { useEffect } from 'react';

function App() {
  useEffect(() => {
    console.log('Runs only once on mount (like componentDidMount)');
  }, []);

  return <h1>Welcome!</h1>;
}
```

### ✅ Use this when:

You want to **run something once** — like fetching data or setting up a timer when the component loads.

---

## 🕐 Example 3: useEffect + `setTimeout`

```jsx
import { useEffect, useState } from 'react';

function Timer() {
  const [message, setMessage] = useState("Waiting...");

  useEffect(() => {
    const timeout = setTimeout(() => {
      setMessage("3 seconds passed ⏱️");
    }, 3000);

    return () => clearTimeout(timeout); // cleanup (optional here)
  }, []);

  return <h2>{message}</h2>;
}
```

---

## 🔄 Example 4: `useEffect` With State Dependency

```jsx
import { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('Count updated:', count);
  }, [count]); // Only runs when `count` changes

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

### 🧠 Logic:

* `useEffect` runs **only when `count` changes**, not on every render.

---

## 🧹 Example 5: useEffect Cleanup Function (like `componentWillUnmount`)

```jsx
import { useState, useEffect } from 'react';

function MouseTracker() {
  const [x, setX] = useState(0);
  const [y, setY] = useState(0);

  useEffect(() => {
    const handleMouseMove = (e) => {
      setX(e.clientX);
      setY(e.clientY);
    };

    window.addEventListener('mousemove', handleMouseMove);

    // Cleanup function
    return () => {
      console.log("Cleanup: removing event listener");
      window.removeEventListener('mousemove', handleMouseMove);
    };
  }, []);

  return (
    <h2>
      Mouse Position: X: {x}, Y: {y}
    </h2>
  );
}
```

### 🔥 Logic:

* We’re setting up an event listener when the component mounts.
* And **cleaning it up** when the component unmounts or re-renders.

---

## 🧠 Summary Table

| Scenario                             | Dependency        | Behavior                                  |
| ------------------------------------ | ----------------- | ----------------------------------------- |
| Run on every render                  | None              | Executes every time the component renders |
| Run once after mount                 | `[]`              | Executes once (like `componentDidMount`)  |
| Run when specific value changes      | `[value]`         | Executes only when `value` changes        |
| Run with cleanup (e.g. event, timer) | `[value]` or `[]` | Clean up old effect before new one runs   |

---

## 🚀 Real-World Tip

If you're fetching data:

```jsx
useEffect(() => {
  async function fetchData() {
    const res = await fetch('https://api.example.com/data');
    const data = await res.json();
    console.log(data);
  }

  fetchData();
}, []);
```

[⏮️Previous]() || [Next⏭️]()

