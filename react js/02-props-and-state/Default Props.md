# Default Props

## 🎯 What are Default Props?
Fallback values for props when they're not provided by the parent.

---

## 📝 Two Ways to Set Defaults

### 1. Destructuring Defaults (Modern Way ✅)
```jsx
function Button({ 
  text = 'Click me',
  color = 'blue',
  size = 'medium',
  disabled = false 
}) {
  return (
    <button 
      style={{ backgroundColor: color }}
      disabled={disabled}
    >
      {text}
    </button>
  );
}

// Usage
<Button />  // Uses all defaults
<Button text="Submit" color="green" />  // Overrides some
```

### 2. defaultProps Property (Legacy Way)
```jsx
function Button({ text, color, size }) {
  return (
    <button style={{ backgroundColor: color }}>
      {text}
    </button>
  );
}

Button.defaultProps = {
  text: 'Click me',
  color: 'blue',
  size: 'medium'
};
```

> [!tip] Use Destructuring Defaults
> The modern destructuring approach is preferred. `defaultProps` may be deprecated in future React versions.

---

## ⚠️ Gotcha: `undefined` vs `null`

```jsx
function Greeting({ name = 'Guest' }) {
  return <h1>Hello, {name}!</h1>;
}

// undefined → default is used
<Greeting name={undefined} />  // Hello, Guest!
<Greeting />                   // Hello, Guest!

// null → default is NOT used
<Greeting name={null} />       // Hello, !
```

> Defaults only apply when value is `undefined`, not `null`!

---

## 🔄 Combining with Required Props

```jsx
// Some props required, some optional with defaults
function UserCard({ 
  name,           // Required (no default)
  role = 'User',  // Optional with default
  avatar = '/default-avatar.png',
  isOnline = false
}) {
  return (
    <div>
      <img src={avatar} alt={name} />
      <h2>{name}</h2>
      <span>{role}</span>
      <span>{isOnline ? '🟢' : '⚫'}</span>
    </div>
  );
}

// name is required, others have defaults
<UserCard name="John" />
<UserCard name="Jane" role="Admin" isOnline={true} />
```

---

## 📦 Default Props for Objects/Arrays

```jsx
function DataTable({ 
  data = [],           // Default empty array
  config = {},         // Default empty object
  columns = ['name', 'value']  // Default array with values
}) {
  return (
    <table>
      {data.map((item, i) => (
        <tr key={i}>
          {columns.map(col => <td key={col}>{item[col]}</td>)}
        </tr>
      ))}
    </table>
  );
}
```

---

## 💡 Practical Example

```jsx
function Alert({ 
  type = 'info',
  message = 'Something happened',
  dismissible = true,
  icon = true,
  onClose = () => {}
}) {
  const icons = {
    info: 'ℹ️',
    success: '✅',
    warning: '⚠️',
    error: '❌'
  };

  return (
    <div className={`alert alert-${type}`}>
      {icon && <span>{icons[type]}</span>}
      <span>{message}</span>
      {dismissible && (
        <button onClick={onClose}>×</button>
      )}
    </div>
  );
}

// Minimal usage
<Alert />

// Custom usage
<Alert 
  type="error" 
  message="Something went wrong!" 
  onClose={() => setShowAlert(false)}
/>
```

---

## 🎓 Key Takeaways

- [ ] Use destructuring defaults: `{ prop = 'default' }`
- [ ] Defaults apply only for `undefined`, not `null`
- [ ] Required props = no default value
- [ ] Provide sensible defaults for optional props
- [ ] Default empty arrays/objects prevent errors

[[index|← Back to Module]]
