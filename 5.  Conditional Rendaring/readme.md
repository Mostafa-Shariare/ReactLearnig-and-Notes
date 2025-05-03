## 🧠 What is Conditional Rendering?

In React, **conditional rendering** means **rendering different JSX based on a condition**, just like `if` statements in regular JavaScript.

React components **return JSX**, and you can use **JavaScript expressions** in that JSX to show/hide or switch parts of the UI.

---

## ✅ Common Techniques for Conditional Rendering

### 1. **Using if...else**

```jsx
function Greeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  } else {
    return <h1>Please sign in.</h1>;
  }
}
```

> ✔️ Clean and readable when you have **completely different JSX blocks**.

---

### 2. **Using Ternary Operator (`? :`)**

Best for **inline conditions**.

```jsx
function Greeting({ isLoggedIn }) {
  return (
    <h1>{isLoggedIn ? "Welcome back!" : "Please sign in."}</h1>
  );
}
```

> ✔️ One-liner, but can get messy if too complex.

---

### 3. **Using Logical AND (`&&`)**

Useful when you want to render **something or nothing**.

```jsx
function Notification({ hasNewMessages }) {
  return (
    <div>
      <h2>Inbox</h2>
      {hasNewMessages && <p>You have new messages!</p>}
    </div>
  );
}
```

> ✔️ Clean and perfect for optional content.

---

### 4. **Using early return (`if`)**

For **skipping render early**.

```jsx
function Profile({ isVisible }) {
  if (!isVisible) return null; // don't render anything

  return <h2>User Profile</h2>;
}
```

> ✔️ Avoids nesting and makes the component simpler.

---

### 5. **IIFE (Immediately Invoked Function Expression)**

Advanced, but useful for **multi-branch rendering** inside JSX.

```jsx
function Status({ status }) {
  return (
    <div>
      {(() => {
        if (status === "loading") return <p>Loading...</p>;
        if (status === "error") return <p>Something went wrong</p>;
        return <p>Data loaded!</p>;
      })()}
    </div>
  );
}
```

---

## 🧪 Real-Life Example: Login System

```jsx
import React, { useState } from "react";

function LoginApp() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <div>
      {isLoggedIn ? (
        <div>
          <h2>Welcome, User!</h2>
          <button onClick={() => setIsLoggedIn(false)}>Logout</button>
        </div>
      ) : (
        <div>
          <h2>Please login</h2>
          <button onClick={() => setIsLoggedIn(true)}>Login</button>
        </div>
      )}
    </div>
  );
}
```

---

## 🎯 Best Practices

| Tip                                      | Why                      |
| ---------------------------------------- | ------------------------ |
| Keep logic simple in JSX                 | Makes UI easier to read  |
| Use early return if possible             | Avoids nested conditions |
| Extract JSX blocks into small components | For better readability   |
| Don't overuse ternary inside JSX         | Becomes unreadable       |

---

## ⚠️ Bad Example

```jsx
return (
  <div>
    {isLoggedIn ? (
      isAdmin ? (
        <AdminPanel />
      ) : (
        <UserDashboard />
      )
    ) : (
      <LoginPage />
    )}
  </div>
);
```

> ❌ Way too nested, hard to read.

---

## ✅ Good Refactor

```jsx
if (!isLoggedIn) return <LoginPage />;
if (isAdmin) return <AdminPanel />;
return <UserDashboard />;
```

---

## 🔥 Summary Table

| Method        | Best For                       |
| ------------- | ------------------------------ |
| `if...else`   | Full block rendering           |
| `? :` ternary | Inline JSX rendering           |
| `&&`          | Optional single render         |
| `return null` | Skip render                    |
| `IIFE`        | Complex expressions inside JSX |

