# Custom Hooks Introduction

## 🎯 What are Custom Hooks?
Functions that let you **extract and reuse stateful logic** across components. They start with `use` and can call other hooks.

---

## 📝 Why Custom Hooks?

| Without Custom Hook | With Custom Hook |
|---------------------|------------------|
| Duplicate logic in multiple components | Write once, use anywhere |
| Hard to test logic | Test hook separately |
| Component code is cluttered | Clean, focused components |

---

## 🏗️ Basic Structure

```jsx
function useCustomHook() {
  // Can use any hooks (useState, useEffect, etc.)
  const [state, setState] = useState();
  
  useEffect(() => {
    // Side effects
  }, []);
  
  // Return anything you want
  return [state, setState];
}
```

---

## 💡 Simple Custom Hook Examples

### 1. useToggle
```jsx
function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);

  const toggle = () => setValue(prev => !prev);
  const setTrue = () => setValue(true);
  const setFalse = () => setValue(false);

  return [value, { toggle, setTrue, setFalse }];
}

// Usage
function Modal() {
  const [isOpen, { toggle, setFalse }] = useToggle(false);

  return (
    <>
      <button onClick={toggle}>Toggle</button>
      {isOpen && (
        <div className="modal">
          <button onClick={setFalse}>Close</button>
        </div>
      )}
    </>
  );
}
```

### 2. useLocalStorage
```jsx
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const saved = localStorage.getItem(key);
    return saved ? JSON.parse(saved) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}

// Usage
function App() {
  const [name, setName] = useLocalStorage('name', '');
  
  return (
    <input 
      value={name} 
      onChange={(e) => setName(e.target.value)}
      placeholder="Your name (persisted!)"
    />
  );
}
```

### 3. useFetch
```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    setLoading(true);
    setError(null);
    
    fetch(url)
      .then(res => res.json())
      .then(data => {
        setData(data);
        setLoading(false);
      })
      .catch(err => {
        setError(err.message);
        setLoading(false);
      });
  }, [url]);

  return { data, loading, error };
}

// Usage
function UserProfile({ userId }) {
  const { data: user, loading, error } = useFetch(`/api/users/${userId}`);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  
  return <h1>{user.name}</h1>;
}
```

### 4. useDebounce
```jsx
function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => clearTimeout(timer);
  }, [value, delay]);

  return debouncedValue;
}

// Usage
function SearchBox() {
  const [query, setQuery] = useState('');
  const debouncedQuery = useDebounce(query, 500);

  useEffect(() => {
    if (debouncedQuery) {
      fetch(`/api/search?q=${debouncedQuery}`)
        .then(res => res.json())
        .then(data => console.log(data));
    }
  }, [debouncedQuery]);

  return (
    <input 
      value={query} 
      onChange={(e) => setQuery(e.target.value)}
    />
  );
}
```

### 5. useWindowSize
```jsx
function useWindowSize() {
  const [size, setSize] = useState({
    width: window.innerWidth,
    height: window.innerHeight
  });

  useEffect(() => {
    const handleResize = () => {
      setSize({
        width: window.innerWidth,
        height: window.innerHeight
      });
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  return size;
}

// Usage
function App() {
  const { width, height } = useWindowSize();
  
  return (
    <p>Window: {width}px × {height}px</p>
  );
}
```

---

## 📋 Custom Hook Rules

1. **Must start with `use`**: `useMyHook` ✅, `myHook` ❌
2. **Can call other hooks**: useState, useEffect, etc.
3. **Can call other custom hooks**
4. **Must be called at top level** (like regular hooks)

---

## ✅ When to Create Custom Hooks

- Logic used in multiple components
- Complex stateful logic that clutters components
- Want to test logic separately
- Wrapping third-party libraries

---

## 🎓 Key Takeaways

- [ ] Custom hooks = reusable stateful logic
- [ ] Must start with `use`
- [ ] Can use any hooks inside
- [ ] Return any data structure (array, object, value)
- [ ] Makes components cleaner and more focused

[[index|← Back to Module]]
