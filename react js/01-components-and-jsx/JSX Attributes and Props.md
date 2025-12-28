# JSX Attributes and Props

## 🎯 What Are Attributes in JSX?
Attributes pass data to HTML elements. In React, we use **camelCase** naming.

```jsx
<input type="text" placeholder="Enter name" maxLength={50} />
```

---

## 📝 Attribute Syntax

### String Attributes (Use Quotes)
```jsx
<img src="photo.jpg" alt="Profile" />
<input type="email" placeholder="Enter email" />
<a href="https://google.com">Google</a>
```

### Dynamic Attributes (Use Curly Braces)
```jsx
const imageUrl = "avatar.png";
const inputType = "password";

<img src={imageUrl} alt="Avatar" />
<input type={inputType} />
```

### Boolean Attributes
```jsx
// These are equivalent
<input disabled={true} />
<input disabled />

// To set false, must use expression
<input disabled={false} />
```

---

## 🔀 HTML → JSX Attribute Changes

| HTML Attribute | JSX Attribute |
|---------------|---------------|
| `class` | `className` |
| `for` | `htmlFor` |
| `tabindex` | `tabIndex` |
| `maxlength` | `maxLength` |
| `readonly` | `readOnly` |
| `colspan` | `colSpan` |
| `rowspan` | `rowSpan` |
| `autocomplete` | `autoComplete` |
| `autofocus` | `autoFocus` |

---

## 🎨 The `style` Attribute

Style must be an **object** with camelCase properties:

```jsx
// ❌ WRONG - String syntax doesn't work
<div style="color: red; font-size: 16px">

// ✅ CORRECT - Object syntax
<div style={{ color: 'red', fontSize: '16px' }}>

// ✅ With variable
const myStyle = {
  backgroundColor: '#f0f0f0',
  padding: '20px',
  borderRadius: '8px'
};
<div style={myStyle}>Content</div>
```

### CSS Property Conversion

| CSS | JSX Style Object |
|-----|------------------|
| `background-color` | `backgroundColor` |
| `font-size` | `fontSize` |
| `border-radius` | `borderRadius` |
| `z-index` | `zIndex` |
| `margin-top` | `marginTop` |

---

## 🔗 Props in Components

When you pass attributes to custom components, they become **props**:

```jsx
// Passing props
<UserCard 
  name="John" 
  age={25} 
  isAdmin={true}
  onClick={() => console.log('clicked')}
/>

// Receiving props
function UserCard(props) {
  return (
    <div>
      <p>Name: {props.name}</p>
      <p>Age: {props.age}</p>
      {props.isAdmin && <span>👑 Admin</span>}
    </div>
  );
}

// Or with destructuring (cleaner)
function UserCard({ name, age, isAdmin }) {
  return (
    <div>
      <p>Name: {name}</p>
      <p>Age: {age}</p>
      {isAdmin && <span>👑 Admin</span>}
    </div>
  );
}
```

---

## 📦 Spread Attributes

Pass all object properties as props at once:

```jsx
const buttonProps = {
  type: 'submit',
  disabled: false,
  className: 'btn-primary'
};

// Instead of writing each one
<button type={buttonProps.type} disabled={buttonProps.disabled} className={buttonProps.className}>

// Use spread
<button {...buttonProps}>Submit</button>
```

---

## 🎓 Key Takeaways

- [ ] Use camelCase for JSX attributes
- [ ] Strings use quotes, expressions use `{}`
- [ ] `style` needs object with camelCase properties
- [ ] Props = attributes passed to components
- [ ] Use `{...obj}` to spread all properties

[[index|← Back to Module]]
