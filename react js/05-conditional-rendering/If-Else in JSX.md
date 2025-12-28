# If-Else in JSX

## 🎯 The Problem
You can't use `if` statements directly inside JSX.

```jsx
// ❌ This doesn't work
return (
  <div>
    if (isLoggedIn) {
      <Dashboard />
    }
  </div>
);
```

---

## ✅ Solutions

### 1. If-Else Before Return
```jsx
function App({ isLoggedIn }) {
  if (isLoggedIn) {
    return <Dashboard />;
  } else {
    return <Login />;
  }
}

// Or without else
function App({ isLoggedIn }) {
  if (isLoggedIn) {
    return <Dashboard />;
  }
  return <Login />;
}
```

### 2. Variable Assignment
```jsx
function App({ isLoggedIn }) {
  let content;
  
  if (isLoggedIn) {
    content = <Dashboard />;
  } else {
    content = <Login />;
  }
  
  return <div>{content}</div>;
}
```

### 3. Ternary Operator (Inline)
```jsx
function App({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <Dashboard /> : <Login />}
    </div>
  );
}
```

---

## 📋 Multi-Condition Examples

### Multiple If-Else
```jsx
function StatusMessage({ status }) {
  if (status === 'loading') {
    return <p>Loading...</p>;
  } else if (status === 'error') {
    return <p>Error occurred</p>;
  } else if (status === 'success') {
    return <p>Success!</p>;
  } else {
    return <p>Unknown status</p>;
  }
}
```

### Switch Statement
```jsx
function StatusIcon({ status }) {
  let icon;
  
  switch (status) {
    case 'pending':
      icon = '⏳';
      break;
    case 'approved':
      icon = '✅';
      break;
    case 'rejected':
      icon = '❌';
      break;
    default:
      icon = '❓';
  }
  
  return <span>{icon}</span>;
}
```

---

## 💡 Practical Examples

### User Auth
```jsx
function App({ user }) {
  if (!user) {
    return <Login />;
  }
  
  if (user.role === 'admin') {
    return <AdminDashboard />;
  }
  
  return <UserDashboard />;
}
```

### Loading States
```jsx
function DataDisplay({ data, loading, error }) {
  if (loading) {
    return <div>Loading...</div>;
  }
  
  if (error) {
    return <div>Error: {error.message}</div>;
  }
  
  if (!data || data.length === 0) {
    return <div>No data available</div>;
  }
  
  return (
    <ul>
      {data.map(item => <li key={item.id}>{item.name}</li>)}
    </ul>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Can't use `if` directly in JSX
- [ ] Use `if-else` before `return`
- [ ] Use ternary `?:` for simple inline conditions
- [ ] Use early returns for guard clauses
- [ ] Assign to variable for complex conditions

[[index|← Back to Module]]
