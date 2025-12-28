# Logical AND Operator

## 🎯 Syntax
```jsx
{condition && <Component />}
```

Short-circuit evaluation: if `condition` is truthy, render the component.

---

## 📝 How It Works

```jsx
// If true, shows the message
{true && <p>This will show</p>}

// If false, shows nothing
{false && <p>This won't show</p>}
```

---

## 💡 Common Use Cases

### Show When True
```jsx
function UserPanel({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn && <p>Welcome back!</p>}
    </div>
  );
}
```

### Show Message
```jsx
function Form({ error }) {
  return (
    <div>
      <input />
      {error && <p style={{ color: 'red' }}>{error}</p>}
    </div>
  );
}
```

### Conditional Section
```jsx
function Profile({ user }) {
  return (
    <div>
      <h1>{user.name}</h1>
      {user.isAdmin && (
        <div className="admin-panel">
          <h2>Admin Controls</h2>
          <button>Manage Users</button>
        </div>
      )}
    </div>
  );
}
```

---

## ⚠️ Common Gotcha: Falsy Values

```jsx
const count = 0;

// ❌ PROBLEM - renders "0"
{count && <p>Count: {count}</p>}

// ✅ SOLUTION - explicit boolean check
{count > 0 && <p>Count: {count}</p>}

// ✅ ALTERNATIVE - double negation
{!!count && <p>Count: {count}</p>}
```

> [!warning] Falsy Values
> Be careful with `0`, `''`, `NaN`, `null`, `undefined`, `false`. React renders `0` but not the others!

---

## 📋 Safe Patterns

### Arrays
```jsx
function UserList({ users }) {
  return (
    <div>
      {users.length > 0 && (
        <ul>
          {users.map(u => <li key={u.id}>{u.name}</li>)}
        </ul>
      )}
    </div>
  );
}
```

### Booleans
```jsx
function Alert({ showAlert, message }) {
  return (
    <div>
      {showAlert && <div className="alert">{message}</div>}
    </div>
  );
}
```

### Objects (Check First)
```jsx
function UserCard({ user }) {
  return (
    <div>
      {user && (
        <div>
          <h2>{user.name}</h2>
          <p>{user.email}</p>
        </div>
      )}
    </div>
  );
}
```

---

## 🆚 && vs Ternary

| Use && When | Use Ternary When |
|-------------|------------------|
| Only show if true | Show different things for true/false |
| No "else" needed | Need both true and false cases |
| Simpler, cleaner | More explicit |

```jsx
// && - only one case
{isLoggedIn && <Dashboard />}

// Ternary - two cases
{isLoggedIn ? <Dashboard /> : <Login />}
```

---

## 💡 Practical Examples

### Loading Indicator
```jsx
function DataList({ data, isLoading }) {
  return (
    <div>
      {isLoading && <p>Loading...</p>}
      {!isLoading && data && (
        <ul>
          {data.map(item => <li key={item.id}>{item.name}</li>)}
        </ul>
      )}
    </div>
  );
}
```

### Premium Badge
```jsx
function UserCard({ user }) {
  return (
    <div>
      <h2>{user.name}</h2>
      {user.isPremium && <span className="badge">⭐ Premium</span>}
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Use `&&` to conditionally render
- [ ] Left side must be truthy to render right side
- [ ] ⚠️ Watch out for `0` - it renders!
- [ ] Use explicit boolean checks: `count > 0 &&`
- [ ] Best for "show or nothing" scenarios

[[index|← Back to Module]]
