### 🧠 What Are Hooks?

**Hooks** are special functions that let you "hook into" React features from **functional components**. Before hooks, we used class components to manage state and lifecycle methods—but now, hooks make things easier and cleaner.

Some common hooks:

* `useState` – for state management
* `useEffect` – for side effects (API calls, subscriptions, etc.)
* `useContext` – for global state/context
* `useRef`, `useReducer`, `useCallback`, `useMemo`, etc.

---

### 📦 What is State?

**State** is a way to store data that can **change over time** and causes the component to re-render when updated.

With the `useState` hook, you can easily manage local state in a functional component.

---

### ✅ Syntax – `useState`

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // state variable + updater

  const handleIncrement = () => setCount((prevCount) => prevCount + 1);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
}
```

### Explanation:

* `useState(0)` initializes the state variable `count` to 0.
* `setCount` is the function used to update `count`.
* When you call `setCount`, React re-renders the component with the new value.

---

### ✅ Syntax – `useEffect`

Let’s say we want to log something whenever the `count` changes:

```jsx
import { useEffect, useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(`Count changed to ${count}`);
  }, [count]); // Runs when 'count' changes

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

---

### 🧪 Bonus: `useState` with Objects

```jsx
function UserForm() {
  const [user, setUser] = useState({ name: '', age: '' });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setUser((prev) => ({
      ...prev,
      [name]: value
    }));
  };

  return (
    <form>
      <input name="name" onChange={handleChange} value={user.name} placeholder="Name" />
      <input name="age" onChange={handleChange} value={user.age} placeholder="Age" />
    </form>
  );
}
```

---

### ⚠️ Things to Remember

* You **cannot** use hooks inside loops, conditions, or nested functions—only **at the top level** of the component.
* Hooks are **only usable in functional components** or **custom hooks**.


  [⬅️ Previous](https://github.com/your-username/your-repo/blob/main/previous-page.md) | [Next ➡️](https://github.com/your-username/your-repo/blob/main/next-page.md)



