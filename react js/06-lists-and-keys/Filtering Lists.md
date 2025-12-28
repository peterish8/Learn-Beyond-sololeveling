# Filtering Lists

## 🎯 The filter() Method
Creates a new array with elements that pass a test.

```jsx
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(num => num % 2 === 0);
// [2, 4]
```

---

## 📝 Basic Filtering

```jsx
function ActiveUsers({ users }) {
  const activeUsers = users.filter(user => user.isActive);
  
  return (
    <ul>
      {activeUsers.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

## 💡 Common Patterns

### Filter by Property
```jsx
function ProductList({ products, category }) {
  const filteredProducts = products.filter(p => p.category === category);
  
  return (
    <div>
      {filteredProducts.map(product => (
        <ProductCard key={product.id} product={product} />
      ))}
    </div>
  );
}
```

### Filter by Search Query
```jsx
function SearchableList({ items, query }) {
  const filtered = items.filter(item =>
    item.name.toLowerCase().includes(query.toLowerCase())
  );
  
  return (
    <ul>
      {filtered.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

### Multiple Conditions
```jsx
function UserList({ users, showAdmin, showActive }) {
  const filtered = users.filter(user => {
    if (showAdmin && !user.isAdmin) return false;
    if (showActive && !user.isActive) return false;
    return true;
  });
  
  return (
    <ul>
      {filtered.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

---

## 🔧 Inline vs Variable

### Inline (Simple)
```jsx
<ul>
  {users
    .filter(user => user.isActive)
    .map(user => (
      <li key={user.id}>{user.name}</li>
    ))
  }
</ul>
```

### Variable (Complex/Reused)
```jsx
const activeAdmins = users.filter(user => user.isActive && user.isAdmin);

return (
  <div>
    <h2>Admins: {activeAdmins.length}</h2>
    <ul>
      {activeAdmins.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  </div>
);
```

---

## 📋 Complete Examples

### Search Filter
```jsx
function UserSearch() {
  const [query, setQuery] = useState('');
  const users = [
    { id: 1, name: 'Alice' },
    { id: 2, name: 'Bob' },
    { id: 3, name: 'Charlie' }
  ];
  
  const filteredUsers = users.filter(user =>
    user.name.toLowerCase().includes(query.toLowerCase())
  );
  
  return (
    <div>
      <input 
        value={query}
        onChange={(e) => setQuery(e.target.value)}
        placeholder="Search users..."
      />
      <ul>
        {filteredUsers.map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}
```

### Multi-Filter
```jsx
function ProductFilter() {
  const [category, setCategory] = useState('all');
  const [priceRange, setPriceRange] = useState('all');
  
  const products = [...]; // Your products
  
  const filtered = products.filter(product => {
    if (category !== 'all' && product.category !== category) {
      return false;
    }
    if (priceRange === 'cheap' && product.price > 50) {
      return false;
    }
    if (priceRange === 'expensive' && product.price <= 50) {
      return false;
    }
    return true;
  });
  
  return (
    <div>
      <select value={category} onChange={(e) => setCategory(e.target.value)}>
        <option value="all">All Categories</option>
        <option value="electronics">Electronics</option>
        <option value="clothing">Clothing</option>
      </select>
      
      <select value={priceRange} onChange={(e) => setPriceRange(e.target.value)}>
        <option value="all">All Prices</option>
        <option value="cheap">Under $50</option>
        <option value="expensive">Over $50</option>
      </select>
      
      <div className="grid">
        {filtered.map(product => (
          <ProductCard key={product.id} product={product} />
        ))}
      </div>
    </div>
  );
}
```

---

## ⚠️ Don't Modify Original Array

```jsx
// ❌ WRONG - mutates original
users.filter(...);  // If modifying in place

// ✅ CORRECT - filter creates new array
const filtered = users.filter(...);
```

---

## 🎓 Key Takeaways

- [ ] Use `.filter()` before `.map()`
- [ ] Filter returns a new array
- [ ] Combine with `.includes()` for search
- [ ] Chain filter and map together
- [ ] Don't mutate the original array

[[index|← Back to Module]]
