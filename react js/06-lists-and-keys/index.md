# 📋 Lists & Keys

## Module Progress
- [ ] [[Rendering Arrays with Map]] 🔁 Displaying lists of data
- [ ] [[The Key Prop]] 🔑 Why keys matter for React
- [ ] [[Using Index as Key]] ⚠️ When it's okay (and when not)
- [ ] [[Filtering Lists]] 🔍 Displaying filtered data
- [ ] [[Sorting Lists]] 📊 Ordering data before display
- [ ] [[List Best Practices]] ✅ Common patterns and tips

---

## 🎯 Learning Objectives
- Render arrays of data using `map()`
- Understand why React needs unique keys
- Know when index keys are acceptable
- Filter arrays before rendering
- Sort data for display
- Follow best practices for list rendering

## 📌 Key Concepts
> Use `.map()` to transform data into JSX: `{items.map(item => <Item key={item.id} {...item} />)}`

> **Keys** help React identify which items changed, added, or removed.

> ⚠️ Index as key is okay ONLY if:
> - List is static (no adds/removes/reorders)
> - Items have no stable IDs

> Always filter/sort BEFORE mapping, not during.

[[React JS Hub|← Back to Hub]]
