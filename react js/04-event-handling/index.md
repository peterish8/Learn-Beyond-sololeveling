# 🖱️ Event Handling

## Module Progress
- [ ] [[onClick and Common Events]] 🎯 Basic event handlers
- [ ] [[Event Handler Syntax]] ✍️ Proper function references
- [ ] [[Passing Arguments to Handlers]] 📤 Sending data with events
- [ ] [[Event Object]] 📋 Accessing event properties
- [ ] [[Preventing Default Behavior]] 🚫 Stopping form submissions etc.
- [ ] [[Synthetic Events]] 🔄 React's cross-browser wrapper

---

## 🎯 Learning Objectives
- Handle user interactions with onClick, onChange, etc.
- Write event handlers correctly (avoid common mistakes)
- Pass additional data to event handlers
- Use the event object to get input values
- Prevent default browser behaviors
- Understand React's synthetic event system

## 📌 Key Concepts
> Pass function reference, not function call: `onClick={handleClick}` ✅ not `onClick={handleClick()}` ❌

> To pass arguments: `onClick={() => handleClick(id)}` or `onClick={(e) => handleClick(e, id)}`

> Use `e.preventDefault()` to stop form submissions or link navigation.

[[React JS Hub|← Back to Hub]]
