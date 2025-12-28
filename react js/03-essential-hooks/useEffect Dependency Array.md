# useEffect Dependency Array

## 🎯 What is the Dependency Array?
The second argument to `useEffect` that controls **when** the effect runs.

```jsx
useEffect(() => {
  // Effect code
}, [/* dependencies here */]);
```

---

## 📊 Three Patterns

### 1. No Array - Runs Every Render
```jsx
useEffect(() => {
  console.log('Runs after EVERY render');
});
// Runs on mount + every update
```

### 2. Empty Array - Runs Once
```jsx
useEffect(() => {
  console.log('Runs ONCE on mount');
}, []);
// Runs only when component mounts
```

### 3. With Dependencies - Runs When They Change
```jsx
useEffect(() => {
  console.log('Runs when count changes');
}, [count]);
// Runs on mount + when count changes
```

---

## 📋 Dependency Rules

> [!warning] Golden Rule
> Include **every value** from component scope that the effect uses (props, state, functions, variables).

```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    // Uses: userId, setUser
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => setUser(data));
  }, [userId]);  // ✅ userId is listed

  useEffect(() => {
    // Uses: userId, setPosts
    fetch(`/api/users/${userId}/posts`)
      .then(res => res.json())
      .then(data => setPosts(data));
  }, [userId]);  // ✅ userId is listed (setters are stable, can omit)
}
```

---

## ⚠️ Common Mistakes

### Missing Dependencies
```jsx
const [count, setCount] = useState(0);
const [multiplier, setMultiplier] = useState(2);

// ❌ WRONG - Uses multiplier but not in deps
useEffect(() => {
  console.log(count * multiplier);
}, [count]);  // multiplier changes won't trigger effect!

// ✅ CORRECT
useEffect(() => {
  console.log(count * multiplier);
}, [count, multiplier]);
```

### Functions as Dependencies
```jsx
// ❌ PROBLEM - Function recreated every render
function SearchBox() {
  const [query, setQuery] = useState('');
  
  const search = () => {
    fetch(`/api/search?q=${query}`);
  };
  
  useEffect(() => {
    search();
  }, [search]);  // search is new every render = infinite loop!
}

// ✅ SOLUTION 1 - Include query directly
function SearchBox() {
  const [query, setQuery] = useState('');
  
  useEffect(() => {
    fetch(`/api/search?q=${query}`);
  }, [query]);
}

// ✅ SOLUTION 2 - useCallback (advanced)
function SearchBox() {
  const [query, setQuery] = useState('');
  
  const search = useCallback(() => {
    fetch(`/api/search?q=${query}`);
  }, [query]);
  
  useEffect(() => {
    search();
  }, [search]);
}
```

---

## 💡 Practical Examples

### Fetch Data on ID Change
```jsx
function Post({ postId }) {
  const [post, setPost] = useState(null);

  useEffect(() => {
    fetch(`/api/posts/${postId}`)
      .then(res => res.json())
      .then(data => setPost(data));
  }, [postId]);  // Re-fetch when postId changes

  return post ? <h1>{post.title}</h1> : <p>Loading...</p>;
}
```

### Sync with Multiple Dependencies
```jsx
function FilteredList({ category, sortBy }) {
  const [items, setItems] = useState([]);

  useEffect(() => {
    fetch(`/api/items?category=${category}&sort=${sortBy}`)
      .then(res => res.json())
      .then(data => setItems(data));
  }, [category, sortBy]);  // Re-fetch when either changes

  return <ul>{items.map(i => <li key={i.id}>{i.name}</li>)}</ul>;
}
```

### Debounced Search
```jsx
function Search() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);

  useEffect(() => {
    if (!query) return;
    
    const timer = setTimeout(() => {
      fetch(`/api/search?q=${query}`)
        .then(res => res.json())
        .then(data => setResults(data));
    }, 500);  // Wait 500ms after user stops typing

    return () => clearTimeout(timer);
  }, [query]);  // Trigger on every query change

  return (
    <div>
      <input value={query} onChange={(e) => setQuery(e.target.value)} />
      <ul>{results.map(r => <li key={r.id}>{r.name}</li>)}</ul>
    </div>
  );
}
```

---

## 🧪 Debugging Tips

Use ESLint plugin for exhaustive deps:
```bash
npm install eslint-plugin-react-hooks
```

It will warn you about missing dependencies!

---

## 🎓 Key Takeaways

- [ ] No array = every render
- [ ] `[]` = once on mount
- [ ] `[dep]` = when dep changes
- [ ] Include ALL values used in effect
- [ ] Setters from `useState` are stable (safe to omit)

[[index|← Back to Module]]
