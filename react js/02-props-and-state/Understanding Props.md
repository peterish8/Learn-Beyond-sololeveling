# Understanding Props

## 🎯 What are Props?
**Props** (short for "properties") are how you pass data from a **parent component to a child component**.

> Think of props like function arguments – they let you customize components!

---

## 📤 Passing Props

```jsx
// Parent component passes props
function App() {
  return (
    <UserCard 
      name="John Doe"
      age={25}
      isAdmin={true}
      hobbies={['reading', 'gaming']}
    />
  );
}
```

---

## 📥 Receiving Props

### Method 1: Using `props` Object
```jsx
function UserCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>Age: {props.age}</p>
      <p>Admin: {props.isAdmin ? 'Yes' : 'No'}</p>
    </div>
  );
}
```

### Method 2: Destructuring (Preferred ✅)
```jsx
function UserCard({ name, age, isAdmin }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>Admin: {isAdmin ? 'Yes' : 'No'}</p>
    </div>
  );
}
```

---

## 📦 What Can Be Props?

| Type | Example |
|------|---------|
| String | `name="John"` |
| Number | `age={25}` |
| Boolean | `isActive={true}` |
| Array | `items={[1, 2, 3]}` |
| Object | `user={{ name: 'John' }}` |
| Function | `onClick={() => {}}` |
| Component | `icon={<Icon />}` |

---

## ⚠️ Props are Read-Only

```jsx
function UserCard({ name }) {
  // ❌ WRONG - Never modify props!
  name = "New Name";
  
  // ✅ CORRECT - Props are immutable
  return <h2>{name}</h2>;
}
```

> [!warning] Golden Rule
> Props flow **down** (parent → child) and are **read-only**. If you need to change data, use **state** instead.

---

## 🔄 Props Flow (One-Way Data Flow)

```
┌─────────────┐
│    App      │ (parent)
│  name="Jon" │
└──────┬──────┘
       │ props
       ▼
┌─────────────┐
│  UserCard   │ (child)
│  {name}     │
└─────────────┘
```

---

## 💡 Practical Example

```jsx
// Reusable Button with props
function Button({ text, color, size, onClick }) {
  const styles = {
    backgroundColor: color,
    padding: size === 'large' ? '15px 30px' : '8px 16px',
    fontSize: size === 'large' ? '18px' : '14px'
  };
  
  return (
    <button style={styles} onClick={onClick}>
      {text}
    </button>
  );
}

// Usage - same component, different props
function App() {
  return (
    <>
      <Button text="Save" color="blue" size="large" onClick={() => save()} />
      <Button text="Cancel" color="gray" size="small" onClick={() => cancel()} />
      <Button text="Delete" color="red" size="small" onClick={() => remove()} />
    </>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Props pass data from parent to child
- [ ] Props are **read-only** (immutable)
- [ ] Use destructuring for cleaner code
- [ ] Any JavaScript value can be a prop
- [ ] Data flows **one way**: parent → child

[[index|← Back to Module]]
