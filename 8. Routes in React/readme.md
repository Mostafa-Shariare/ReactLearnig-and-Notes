## 📦 What is React Router?

**React Router** is a library that lets you handle **client-side routing** in React apps. It allows you to:

* Switch between components (pages) without reloading the page
* Build **Single Page Applications (SPA)**
* Control routes with dynamic paths (like `/user/:id`)
* Handle 404 pages, nested routes, redirects, and more!

---

## 🧱 Step 1: Installing React Router

First, install the package:

```bash
npm install react-router-dom
```

For React Router v6+ (the latest and recommended version), use:

```bash
npm install react-router-dom@6
```

---

## 🔧 Step 2: Basic Setup of Routing

Create this folder structure:

```
/src
 ┣ /pages
 ┃ ┣ Home.js
 ┃ ┣ About.js
 ┃ ┗ Contact.js
 ┣ App.js
 ┗ index.js
```

---

### ✅ `index.js` - Wrap your app in `BrowserRouter`

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { BrowserRouter } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

---

### ✅ `App.js` - Define Your Routes

```jsx
import React from 'react';
import { Routes, Route, Link } from 'react-router-dom';
import Home from './pages/Home';
import About from './pages/About';
import Contact from './pages/Contact';

function App() {
  return (
    <div>
      <nav style={{ marginBottom: '20px' }}>
        <Link to="/">Home</Link> | {' '}
        <Link to="/about">About</Link> | {' '}
        <Link to="/contact">Contact</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </div>
  );
}

export default App;
```

---

### ✅ Example Page Components

```jsx
// pages/Home.js
export default function Home() {
  return <h1>🏠 Welcome to the Home Page!</h1>;
}
```

```jsx
// pages/About.js
export default function About() {
  return <h1>📘 About Us Page</h1>;
}
```

```jsx
// pages/Contact.js
export default function Contact() {
  return <h1>📞 Contact Page</h1>;
}
```

---

## 🔀 Step 3: Dynamic Routes (URL Params)

Let’s say we want a route like `/user/5` or `/user/123`.

### Add Route in App.js:

```jsx
import UserProfile from './pages/UserProfile';

<Route path="/user/:id" element={<UserProfile />} />
```

### Create the Component:

```jsx
// pages/UserProfile.js
import { useParams } from 'react-router-dom';

export default function UserProfile() {
  const { id } = useParams();

  return <h2>👤 User ID: {id}</h2>;
}
```

Now navigating to `/user/7` shows `User ID: 7`.

---

## 💡 Step 4: Navigation with `useNavigate()`

Sometimes you need to navigate programmatically (after login or a button click).

```jsx
import { useNavigate } from 'react-router-dom';

export default function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // pretend login is successful
    navigate('/dashboard');
  };

  return <button onClick={handleLogin}>Login</button>;
}
```

---

## ❌ Step 5: 404 Not Found Page

Add this route **last** so it matches everything else first:

```jsx
<Route path="*" element={<h2>404 Not Found 🚫</h2>} />
```

---

## 🧱 Step 6: Nested Routes

Say we want `/dashboard/settings` and `/dashboard/profile` under `/dashboard`.

### App.js:

```jsx
import Dashboard from './pages/Dashboard';
import Profile from './pages/Profile';
import Settings from './pages/Settings';

<Route path="/dashboard/*" element={<Dashboard />} />
```

### Dashboard Component:

```jsx
// pages/Dashboard.js
import { Link, Routes, Route } from 'react-router-dom';
import Profile from './Profile';
import Settings from './Settings';

export default function Dashboard() {
  return (
    <div>
      <h1>📊 Dashboard</h1>
      <nav>
        <Link to="profile">Profile</Link> | {' '}
        <Link to="settings">Settings</Link>
      </nav>

      <Routes>
        <Route path="profile" element={<Profile />} />
        <Route path="settings" element={<Settings />} />
      </Routes>
    </div>
  );
}
```

---

## 🔁 Step 7: Redirects

Want to redirect after an action? Use `navigate()` or the `<Navigate />` component.

```jsx
<Route path="/old-about" element={<Navigate to="/about" />} />
```

Or programmatically:

```jsx
navigate('/about');
```

---

## 📦 Summary of React Router Essentials

| Feature            | Use                                  |
| ------------------ | ------------------------------------ |
| `BrowserRouter`    | Wraps your whole app (in `index.js`) |
| `Routes` & `Route` | Define paths and components          |
| `Link`             | Navigation without refresh           |
| `useParams()`      | Get dynamic URL params               |
| `useNavigate()`    | Navigate programmatically            |
| `Navigate`         | Component-based redirect             |
| Nested `<Routes>`  | Handle sub-routes                    |

---

