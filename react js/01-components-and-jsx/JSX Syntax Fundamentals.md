# JSX Syntax Fundamentals

## 🎯 What is JSX?
**JSX** = JavaScript XML. It lets you write HTML-like code inside JavaScript.

```jsx
// This is JSX
const element = <h1>Hello, World!</h1>;
```

> [!note] Behind the Scenes
> JSX gets compiled to `React.createElement()` calls. It's just syntactic sugar!

---

## 📝 Basic JSX Rules

### 1. Must Have One Parent Element
```jsx
// ❌ WRONG - Multiple root elements
return (
  <h1>Title</h1>
  <p>Paragraph</p>
);

// ✅ CORRECT - Wrapped in one parent
return (
  <div>
    <h1>Title</h1>
    <p>Paragraph</p>
  </div>
);

// ✅ ALSO CORRECT - Using Fragment
return (
  <>
    <h1>Title</h1>
    <p>Paragraph</p>
  </>
);
```

### 2. All Tags Must Be Closed
```jsx
// ❌ WRONG
<img src="photo.jpg">
<input type="text">
<br>

// ✅ CORRECT - Self-closing tags
<img src="photo.jpg" />
<input type="text" />
<br />
```

### 3. Use `className` Instead of `class`
```jsx
// ❌ WRONG - 'class' is reserved in JS
<div class="container">

// ✅ CORRECT
<div className="container">
```

### 4. Use `htmlFor` Instead of `for`
```jsx
// ❌ WRONG
<label for="email">Email</label>

// ✅ CORRECT
<label htmlFor="email">Email</label>
```

### 5. CamelCase for Attributes
```jsx
// HTML                    →  JSX
onclick                    →  onClick
onchange                   →  onChange
tabindex                   →  tabIndex
maxlength                  →  maxLength
```

---

## 🔄 JSX vs HTML Quick Reference

| HTML | JSX |
|------|-----|
| `class` | `className` |
| `for` | `htmlFor` |
| `onclick` | `onClick` |
| `tabindex` | `tabIndex` |
| `<br>` | `<br />` |
| `style="color: red"` | `style={{ color: 'red' }}` |

---

## 💡 Complete Example

```jsx
function Card() {
  return (
    <div className="card">
      <img src="avatar.jpg" alt="User" />
      <h2>John Doe</h2>
      <p>Frontend Developer</p>
      <button onClick={() => alert('Hi!')}>
        Say Hello
      </button>
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] JSX = HTML-like syntax in JavaScript
- [ ] One root element per return
- [ ] Close all tags (including self-closing)
- [ ] Use `className` not `class`
- [ ] Use `htmlFor` not `for`
- [ ] camelCase for event handlers

[[index|← Back to Module]]
