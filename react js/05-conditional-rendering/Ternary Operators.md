# Ternary Operators

## 🎯 Syntax
```jsx
condition ? valueIfTrue : valueIfFalse
```

The **inline** way to write if-else in JSX.

---

## 📝 Basic Usage

```jsx
function Greeting({ isLoggedIn }) {
  return (
    <h1>
      {isLoggedIn ? 'Welcome back!' : 'Please log in'}
    </h1>
  );
}
```

---

## 💡 Common Patterns

### Show/Hide Component
```jsx
function App({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <Dashboard /> : <Login />}
    </div>
  );
}
```

### Conditional Text
```jsx
function Counter({ count }) {
  return (
    <p>
      You have {count} {count === 1 ? 'item' : 'items'}
    </p>
  );
}
```

### Conditional Style
```jsx
function Status({ isActive }) {
  return (
    <span style={{ color: isActive ? 'green' : 'red' }}>
      {isActive ? 'Active' : 'Inactive'}
    </span>
  );
}
```

### Conditional Class
```jsx
function Button({ isPrimary }) {
  return (
    <button className={isPrimary ? 'btn-primary' : 'btn-secondary'}>
      Click
    </button>
  );
}
```

---

## ⚠️ Nested Ternaries (Use Sparingly)

```jsx
// ❌ Hard to read
function Status({ status }) {
  return (
    <span>
      {status === 'loading' 
        ? 'Loading...' 
        : status === 'error' 
          ? 'Error!' 
          : 'Done'}
    </span>
  );
}

// ✅ Better - use if-else or separate function
function Status({ status }) {
  if (status === 'loading') return <span>Loading...</span>;
  if (status === 'error') return <span>Error!</span>;
  return <span>Done</span>;
}
```

---

## 📦 Practical Examples

### Protected Route
```jsx
function ProtectedPage({ user }) {
  return (
    <div>
      {user ? (
        <div>
          <h1>Welcome, {user.name}</h1>
          <Dashboard />
        </div>
      ) : (
        <div>
          <h1>Access Denied</h1>
          <Login />
        </div>
      )}
    </div>
  );
}
```

### Loading Button
```jsx
function SubmitButton({ isSubmitting }) {
  return (
    <button disabled={isSubmitting}>
      {isSubmitting ? 'Submitting...' : 'Submit'}
    </button>
  );
}
```

### Icon Toggle
```jsx
function LikeButton({ isLiked }) {
  return (
    <button>
      {isLiked ? '❤️' : '🤍'} Like
    </button>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Ternary = inline if-else
- [ ] Syntax: `condition ? true : false`
- [ ] Great for simple conditions
- [ ] Avoid deeply nested ternaries
- [ ] Use for conditional text, components, styles

[[index|← Back to Module]]
