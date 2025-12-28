# Conditional CSS Classes

## 🎯 Goal
Apply different CSS classes based on state or props.

---

## 📝 Basic Patterns

### 1. Ternary Operator
```jsx
function Button({ isPrimary }) {
  return (
    <button className={isPrimary ? 'btn-primary' : 'btn-secondary'}>
      Click
    </button>
  );
}
```

### 2. Template Literals
```jsx
function Card({ isActive }) {
  return (
    <div className={`card ${isActive ? 'active' : ''}`}>
      Content
    </div>
  );
}
```

### 3. Conditional with AND
```jsx
function Alert({ type, isDismissible }) {
  return (
    <div className={`alert alert-${type} ${isDismissible ? 'dismissible' : ''}`}>
      Alert message
    </div>
  );
}
```

---

## 💡 Multiple Conditions

```jsx
function Button({ variant, size, disabled }) {
  return (
    <button 
      className={`
        btn 
        btn-${variant} 
        btn-${size} 
        ${disabled ? 'disabled' : ''}
      `.trim()}
    >
      Click
    </button>
  );
}

// Usage
<Button variant="primary" size="lg" disabled={false} />
// className="btn btn-primary btn-lg"
```

---

## 🔧 Using Objects

```jsx
function Status({ status }) {
  const classes = {
    success: 'bg-green text-white',
    error: 'bg-red text-white',
    warning: 'bg-yellow text-black',
    info: 'bg-blue text-white'
  };
  
  return (
    <div className={classes[status]}>
      Status message
    </div>
  );
}
```

---

## 📦 Array Join Method

```jsx
function Card({ isActive, isHighlighted, size }) {
  const classes = [
    'card',
    `card-${size}`,
    isActive && 'active',
    isHighlighted && 'highlighted'
  ].filter(Boolean).join(' ');
  
  return <div className={classes}>Content</div>;
}
```

---

## 🎨 Practical Examples

### Toggle Active Class
```jsx
function NavItem({ isActive, label }) {
  return (
    <a 
      href="#" 
      className={`nav-item ${isActive ? 'active' : ''}`}
    >
      {label}
    </a>
  );
}
```

### Multiple States
```jsx
function Input({ value, error, disabled }) {
  return (
    <input
      value={value}
      disabled={disabled}
      className={`
        input
        ${error ? 'input-error' : ''}
        ${disabled ? 'input-disabled' : ''}
      `.trim()}
    />
  );
}
```

### Theme Classes
```jsx
function Card({ theme, bordered, elevated }) {
  return (
    <div 
      className={`
        card 
        card-${theme}
        ${bordered ? 'card-bordered' : ''}
        ${elevated ? 'card-elevated' : ''}
      `.trim()}
    >
      Content
    </div>
  );
}
```

---

## 🛠️ Helper Function

```jsx
function classNames(...classes) {
  return classes.filter(Boolean).join(' ');
}

// Usage
function Button({ isPrimary, isLarge, isDisabled }) {
  return (
    <button 
      className={classNames(
        'btn',
        isPrimary && 'btn-primary',
        isLarge && 'btn-lg',
        isDisabled && 'disabled'
      )}
    >
      Click
    </button>
  );
}
```

---

## 📚 Using `classnames` Library

```bash
npm install classnames
```

```jsx
import classNames from 'classnames';

function Button({ variant, size, active, disabled }) {
  return (
    <button 
      className={classNames(
        'btn',
        `btn-${variant}`,
        `btn-${size}`,
        {
          active: active,
          disabled: disabled
        }
      )}
    >
      Click
    </button>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Use ternary for simple true/false classes
- [ ] Use template literals for multiple classes
- [ ] Use `${condition && 'class'}` pattern
- [ ] Filter falsy values before joining
- [ ] Consider `classnames` library for complex cases

[[index|← Back to Module]]
