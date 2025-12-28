# Fragment Usage

## 🎯 The Problem
React components must return **one root element**. But sometimes you don't want an extra `<div>` wrapper.

```jsx
// ❌ This won't work - multiple root elements
function Columns() {
  return (
    <td>Hello</td>
    <td>World</td>
  );
}
```

---

## 🧩 Solution: Fragments

Fragments let you group elements **without adding extra DOM nodes**.

### Syntax 1: `<React.Fragment>`
```jsx
import React from 'react';

function Columns() {
  return (
    <React.Fragment>
      <td>Hello</td>
      <td>World</td>
    </React.Fragment>
  );
}
```

### Syntax 2: Short Syntax `<>` (Preferred)
```jsx
function Columns() {
  return (
    <>
      <td>Hello</td>
      <td>World</td>
    </>
  );
}
```

---

## 🆚 Fragment vs Div

```jsx
// With div - adds extra node to DOM
function WithDiv() {
  return (
    <div>           {/* ← This div appears in HTML */}
      <h1>Title</h1>
      <p>Text</p>
    </div>
  );
}

// With Fragment - no extra node!
function WithFragment() {
  return (
    <>              {/* ← This disappears in HTML */}
      <h1>Title</h1>
      <p>Text</p>
    </>
  );
}
```

### Resulting HTML:
```html
<!-- With div -->
<div>
  <h1>Title</h1>
  <p>Text</p>
</div>

<!-- With Fragment - cleaner! -->
<h1>Title</h1>
<p>Text</p>
```

---

## 🔑 Fragments with Keys

When rendering lists, use `<React.Fragment>` to add a key:

```jsx
function Glossary({ items }) {
  return (
    <dl>
      {items.map(item => (
        // Can't use <> here because we need key
        <React.Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </React.Fragment>
      ))}
    </dl>
  );
}
```

> [!warning] Short syntax `<>` cannot have attributes
> Use `<React.Fragment key={...}>` when you need to pass a key.

---

## 📋 When to Use Fragments

| Use Case | Use Fragment? |
|----------|---------------|
| Table rows returning multiple `<td>` | ✅ Yes |
| Flex/Grid children (avoid wrapper bugs) | ✅ Yes |
| Returning multiple elements from component | ✅ Yes |
| Need CSS styling on wrapper | ❌ Use div |
| Need click handler on wrapper | ❌ Use div |

---

## 💡 Practical Example

```jsx
function UserInfo({ user }) {
  return (
    <>
      <h1>{user.name}</h1>
      <p>Email: {user.email}</p>
      <p>Role: {user.role}</p>
    </>
  );
}

function Table({ users }) {
  return (
    <table>
      <tbody>
        {users.map(user => (
          <tr key={user.id}>
            <React.Fragment>
              <td>{user.name}</td>
              <td>{user.age}</td>
            </React.Fragment>
          </tr>
        ))}
      </tbody>
    </table>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Fragments group elements without extra DOM nodes
- [ ] Use `<>...</>` for short syntax
- [ ] Use `<React.Fragment>` when you need a key
- [ ] Keeps DOM clean and avoids styling issues

[[index|← Back to Module]]
