# List Best Practices

## 🎯 Essential Rules

### 1. Always Use Keys
```jsx
// ❌ BAD
{items.map(item => <li>{item}</li>)}

// ✅ GOOD
{items.map(item => <li key={item.id}>{item.name}</li>)}
```

### 2. Keys Must Be Unique & Stable
```jsx
// ❌ BAD - not unique
{users.map(user => <li key={user.role}>{user.name}</li>)}

// ❌ BAD - unstable
{users.map(user => <li key={Math.random()}>{user.name}</li>)}

// ✅ GOOD
{users.map(user => <li key={user.id}>{user.name}</li>)}
```

### 3. Filter/Sort BEFORE map
```jsx
// ✅ GOOD - clear pipeline
{users
  .filter(user => user.isActive)
  .sort((a, b) => a.name.localeCompare(b.name))
  .map(user => <UserCard key={user.id} user={user} />)
}
```

---

## 📦 Performance

### Extract Components
```jsx
// ❌ BAD - inline component recreated every render
{items.map(item => {
  const Component = () => <div>{item.name}</div>;
  return <Component key={item.id} />;
})}

// ✅ GOOD - component defined once
function ItemComponent({ item }) {
  return <div>{item.name}</div>;
}

{items.map(item => (
  <ItemComponent key={item.id} item={item} />
))}
```

### Memoization for Large Lists
```jsx
import { useMemo } from 'react';

function LargeList({ items, filter }) {
  const filtered = useMemo(() => {
    return items.filter(item => item.category === filter);
  }, [items, filter]);
  
  return (
    <ul>
      {filtered.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

---

## 🎯 Empty State Handling

```jsx
function ItemList({ items }) {
  if (items.length === 0) {
    return (
      <div className="empty-state">
        <p>No items found</p>
        <button>Add Item</button>
      </div>
    );
  }
  
  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

---

## 📋 Complete Pattern

```jsx
function DataList({ data, loading, error, onDelete }) {
  // Loading state
  if (loading) {
    return <div className="spinner">Loading...</div>;
  }
  
  // Error state
  if (error) {
    return <div className="error">Error: {error.message}</div>;
  }
  
  // Empty state
  if (!data || data.length === 0) {
    return <div className="empty">No data available</div>;
  }
  
  // Main render
  return (
    <ul className="data-list">
      {data.map(item => (
        <li key={item.id} className="data-item">
          <span>{item.name}</span>
          <button onClick={() => onDelete(item.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}
```

---

## ⚡ Common Patterns

### Conditional Item Rendering
```jsx
{items.map(item => (
  <div key={item.id}>
    <h3>{item.title}</h3>
    {item.description && <p>{item.description}</p>}
    {item.isPremium && <span className="badge">Premium</span>}
  </div>
))}
```

### Nested Lists
```jsx
{categories.map(category => (
  <div key={category.id}>
    <h2>{category.name}</h2>
    <ul>
      {category.items.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  </div>
))}
```

### Alternating Styles
```jsx
{items.map((item, index) => (
  <div 
    key={item.id}
    className={index % 2 === 0 ? 'even-row' : 'odd-row'}
  >
    {item.name}
  </div>
))}
```

---

## 🎓 Checklist

- [ ] Always include unique `key` prop
- [ ] Use database ID as key (not index unless static)
- [ ] Filter/sort before mapping
- [ ] Handle empty state
- [ ] Extract complex list items to components
- [ ] Consider useMemo for expensive operations
- [ ] Show loading and error states

[[index|← Back to Module]]
