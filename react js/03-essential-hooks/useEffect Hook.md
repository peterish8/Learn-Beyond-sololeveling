# useEffect Hook

## 🎯 What is useEffect?
A hook for handling **side effects** in functional components. Side effects are operations that interact with the outside world.

```jsx
import { useEffect } from 'react';
```

---

## 📦 What Are Side Effects?

- Fetching data from API
- Setting up subscriptions
- Manually changing the DOM
- Timers (setTimeout, setInterval)
- Logging
- Local storage operations

---

## 📝 Basic Syntax

```jsx
useEffect(() => {
  // Effect code runs here
}, [dependencies]);
```

---

## 🔄 When Does useEffect Run?

### After Every Render (No dependencies)
```jsx
useEffect(() => {
  console.log('Runs after every render');
});
```

### Once on Mount (Empty array)
```jsx
useEffect(() => {
  console.log('Runs only once when component mounts');
}, []);
```

### When Dependencies Change
```jsx
useEffect(() => {
  console.log('Runs when count changes');
}, [count]);
```

---

## 📊 Dependency Array Explained

| Dependency | When Effect Runs |
|------------|------------------|
| Not provided | Every render |
| `[]` | Once on mount |
| `[a]` | On mount + when `a` changes |
| `[a, b]` | On mount + when `a` or `b` changes |

---

## 💡 Common Use Cases

### 1. Fetching Data
```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    setLoading(true);
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => {
        setUser(data);
        setLoading(false);
      });
  }, [userId]);  // Runs when userId changes

  if (loading) return <p>Loading...</p>;
  return <h1>{user.name}</h1>;
}
```

### 2. Document Title
```jsx
function Page({ title }) {
  useEffect(() => {
    document.title = title;
  }, [title]);

  return <h1>{title}</h1>;
}
```

### 3. Event Listeners
```jsx
function WindowSize() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);
    
    // Cleanup
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  return <p>Width: {width}px</p>;
}
```

### 4. Timers
```jsx
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    // Cleanup
    return () => clearInterval(interval);
  }, []);

  return <p>Seconds: {seconds}</p>;
}
```

### 5. Local Storage
```jsx
function PersistentCounter() {
  const [count, setCount] = useState(() => {
    const saved = localStorage.getItem('count');
    return saved ? JSON.parse(saved) : 0;
  });

  useEffect(() => {
    localStorage.setItem('count', JSON.stringify(count));
  }, [count]);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

---

## ⚠️ Common Mistakes

```jsx
// ❌ Missing dependency
const [count, setCount] = useState(0);
useEffect(() => {
  console.log(count);  // Uses count but not in deps
}, []);  // Should include [count]

// ❌ Infinite loop
useEffect(() => {
  setCount(count + 1);  // This triggers re-render
}, [count]);  // Which triggers effect again... forever!

// ✅ Correct
useEffect(() => {
  console.log(count);
}, [count]);
```

---

## 🎓 Key Takeaways

- [ ] `useEffect` handles side effects
- [ ] Runs after render, not during
- [ ] `[]` = once on mount
- [ ] `[dep]` = when dep changes
- [ ] Always include all used variables in deps

[[index|← Back to Module]]
