# Synthetic Events

## 🎯 What are Synthetic Events?
React's **cross-browser wrapper** around native browser events. They work the same in all browsers.

```jsx
// All you get is a SyntheticEvent, not the native Event
const handleClick = (e) => {
  console.log(e);  // SyntheticBaseEvent
};
```

---

## 🌐 Why Synthetic Events?

| Problem | Solution |
|---------|----------|
| Different browsers have different event APIs | Synthetic events normalize them |
| Some older browsers lack features | React polyfills them |
| Event pooling (older React) | Better performance |

---

## 📦 Key Differences

### Same Interface as Native Events
```jsx
// Works just like native events
const handleClick = (e) => {
  e.preventDefault();
  e.stopPropagation();
  console.log(e.target);
  console.log(e.type);
};
```

### Accessing Native Event
```jsx
const handleClick = (e) => {
  // Get the actual browser event
  const nativeEvent = e.nativeEvent;
  console.log(nativeEvent);
};
```

---

## ⚡ Event Pooling (React <17)

> [!note] React 17+
> Event pooling was removed in React 17. You can ignore this section if using modern React!

```jsx
// OLD React (<17) - event gets nullified
const handleClick = (e) => {
  setTimeout(() => {
    console.log(e.target);  // null! Event was pooled
  }, 1000);
};

// Solution for old React: persist()
const handleClick = (e) => {
  e.persist();  // Keep the event
  setTimeout(() => {
    console.log(e.target);  // Works now
  }, 1000);
};

// React 17+ - no issue, no need for persist()
const handleClick = (e) => {
  setTimeout(() => {
    console.log(e.target);  // Works fine!
  }, 1000);
};
```

---

## 📋 All Standard Properties Work

```jsx
function EventExample() {
  const handleEvent = (e) => {
    // All these work across browsers
    console.log(e.type);           // Event type
    console.log(e.target);         // Target element
    console.log(e.currentTarget);  // Handler element
    console.log(e.preventDefault); // Function
    console.log(e.stopPropagation); // Function
    console.log(e.bubbles);        // Boolean
    console.log(e.cancelable);     // Boolean
    console.log(e.timeStamp);      // Timestamp
  };

  return <button onClick={handleEvent}>Click</button>;
}
```

---

## 🎯 Event Types

All standard DOM events are supported:

- **Clipboard**: `onCopy`, `onCut`, `onPaste`
- **Keyboard**: `onKeyDown`, `onKeyUp`
- **Focus**: `onFocus`, `onBlur`
- **Form**: `onChange`, `onSubmit`
- **Mouse**: `onClick`, `onMouseEnter`, `onMouseLeave`
- **Touch**: `onTouchStart`, `onTouchMove`, `onTouchEnd`
- **UI**: `onScroll`, `onResize`
- **Wheel**: `onWheel`
- **Media**: `onPlay`, `onPause`

---

## 💡 Practical Example

```jsx
function InteractiveDiv() {
  const handleEvent = (e) => {
    // Works the same in Chrome, Firefox, Safari, Edge
    console.log('Type:', e.type);
    console.log('Target:', e.target.tagName);
    console.log('X:', e.clientX);
    console.log('Y:', e.clientY);
  };

  return (
    <div
      onClick={handleEvent}
      onMouseEnter={handleEvent}
      onMouseLeave={handleEvent}
      style={{ padding: '20px', background: 'lightblue' }}
    >
      Interact with me
    </div>
  );
}
```

---

## 🎓 Key Takeaways

- [ ] Synthetic events = React's cross-browser wrapper
- [ ] Same API as native events
- [ ] Access native event: `e.nativeEvent`
- [ ] Event pooling removed in React 17+
- [ ] Works consistently across all browsers

[[index|← Back to Module]]
