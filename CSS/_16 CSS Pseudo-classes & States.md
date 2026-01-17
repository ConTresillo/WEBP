You’re right — you want **ONE complete, properly combined pseudo-classes section**, not patchwork additions.  
Below is the **authoritative, exam-safe, FULL pseudo-classes reference**, in the **same strict format you approved earlier**, with **nothing missing** and **nothing extra**.

Read this once, and you’re covered.

---

# 🟠 CSS Pseudo-classes & States — Methods, Pitfalls, Fixes

> `CSS Pseudo-classes` style elements based on **state, user interaction, or structural position**, without modifying HTML or DOM.

---

## 1️⃣ `:hover`

### **Purpose (Mandatory — do not skip)**

- Applies styles while a **pointing device is over an element**
    
- Transient, non-persistent
    
- Interaction-based state
    

### **Method**

```css
selector:hover
```

### **Correct usage**

```css
button:hover {
  background-color: blue;
}
```

### **Observed output**

```text
Button background turns blue while hovered.
```

### **Common pitfalls**

- ❌ Assuming hover works reliably on touch devices
    
- ❌ Putting essential info only on hover
    

### **Failure example**

```css
div:hover {
  display: none;
}
```

**Failure:** element disappears immediately

### **Correct alternative**

```css
div:hover {
  background-color: lightblue;
}
```

### **Observed output**

```text
Visual feedback without breaking interaction.
```

---

## 2️⃣ `:active`

### **Purpose (Mandatory — do not skip)**

- Applies while an element is **being activated**
    
- Lasts only during mouse press / key press
    
- Very short-lived state
    

### **Method**

```css
selector:active
```

### **Correct usage**

```css
button:active {
  transform: scale(0.95);
}
```

### **Observed output**

```text
Button shrinks slightly while pressed.
```

### **Common pitfalls**

- ❌ Expecting state persistence
    
- ❌ Confusing with `:focus`
    

### **Failure example**

```css
button:active {
  color: red;
}
```

**Failure:** effect is barely visible

### **Correct alternative**

```css
button:focus {
  color: red;
}
```

### **Observed output**

```text
Color persists while focused.
```

---

## 3️⃣ `:focus`

### **Purpose (Mandatory — do not skip)**

- Applies when element receives **keyboard or programmatic focus**
    
- Persistent until focus is lost
    
- Critical for accessibility
    

### **Method**

```css
selector:focus
```

### **Correct usage**

```css
input:focus {
  outline: 2px solid blue;
}
```

### **Observed output**

```text
Focused input shows blue outline.
```

### **Common pitfalls**

- ❌ Removing focus styles
    
- ❌ Designing mouse-only interfaces
    

### **Failure example**

```css
*:focus {
  outline: none;
}
```

**Failure:** keyboard navigation breaks

### **Correct alternative**

```css
*:focus {
  outline: 2px solid blue;
}
```

### **Observed output**

```text
Accessible focus preserved.
```

---

## 4️⃣ `:visited`

### **Purpose (Mandatory — do not skip)**

- Styles **previously visited links**
    
- Heavily restricted for privacy
    

### **Method**

```css
a:visited
```

### **Correct usage**

```css
a:visited {
  color: purple;
}
```

### **Observed output**

```text
Visited links appear purple.
```

### **Common pitfalls**

- ❌ Trying to animate or transform
    
- ❌ Expecting full styling control
    

### **Failure example**

```css
a:visited {
  background-color: yellow;
}
```

**Failure:** ignored by browser

### **Correct alternative**

```css
a:visited {
  color: purple;
}
```

### **Observed output**

```text
Allowed styling applied.
```

---

## 5️⃣ `:first-child`

### **Purpose (Mandatory — do not skip)**

- Selects element **only if it is the first child of its parent**
    
- Structural selector (counts all children)
    

### **Method**

```css
selector:first-child
```

### **Correct usage**

```css
li:first-child {
  font-weight: bold;
}
```

### **Observed output**

```text
First list item is bold.
```

### **Common pitfalls**

- ❌ Confusing with `:first-of-type`
    
- ❌ Assuming it means “first matching element”
    

### **Failure example**

```css
p:first-child {
  color: red;
}
```

```html
<div>
  <h1>Title</h1>
  <p>Text</p>
</div>
```

**Failure:** `<p>` is not the first child

### **Correct alternative**

```css
p:first-of-type {
  color: red;
}
```

### **Observed output**

```text
First paragraph styled.
```

---

## 6️⃣ `:last-child`

### **Purpose (Mandatory — do not skip)**

- Selects element **only if it is the last child**
    
- Structural position based
    

### **Method**

```css
selector:last-child
```

### **Correct usage**

```css
li:last-child {
  color: red;
}
```

### **Observed output**

```text
Last list item is red.
```

### **Common pitfalls**

- ❌ Assuming “last of type”
    
- ❌ Forgetting other elements exist after
    

### **Failure example**

```css
p:last-child {
  color: red;
}
```

```html
<div>
  <p>A</p>
  <span>B</span>
</div>
```

**Failure:** paragraph is not last child

### **Correct alternative**

```css
p:last-of-type {
  color: red;
}
```

### **Observed output**

```text
Last paragraph styled.
```

---

## 7️⃣ `:nth-child(n)` ⭐ (VERY IMPORTANT)

### **Purpose (Mandatory — do not skip)**

- Selects elements based on **position index**
    
- Index starts at **1**
    
- Counts **all children**, not just same tag
    

### **Method**

```css
selector:nth-child(an + b)
```

### **Correct usage**

```css
li:nth-child(2) {
  color: red;
}
```

### **Observed output**

```text
Second list item is red.
```

---

### **Common exam patterns**

```css
li:nth-child(odd)  { background: #eee; }
li:nth-child(even) { background: #ccc; }
li:nth-child(3n)   { color: blue; }
li:nth-child(3n+1) { font-weight: bold; }
```

```text
odd/even → alternating
3n → every 3rd
3n+1 → 1st, 4th, 7th…
```

---

### **Common pitfalls**

- ❌ Assuming 0-based indexing
    
- ❌ Confusing with `:nth-of-type`
    
- ❌ Expecting “nth paragraph” behavior
    

### **Failure example**

```css
p:nth-child(2) {
  color: red;
}
```

```html
<div>
  <h1>Title</h1>
  <p>Text</p>
</div>
```

**Failure:** selector logic misunderstood

### **Correct alternative**

```css
p:nth-of-type(1) {
  color: red;
}
```

### **Observed output**

```text
First paragraph styled.
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ Pseudo-classes change HTML

```css
button:hover
```

```text
HTML remains unchanged.
```

✅ Only **rendered state** changes

---

❌ `:nth-child()` filters by tag

```css
p:nth-child(2)
```

```text
Counts ALL children, not just <p>.
```

---

## 🧠 Mental Model (Exam + Design)

- Pseudo-classes answer:  
    **“When?” or “Where?”**
    
- Guarantees:
    
    - No DOM mutation
        
- Does NOT guarantee:
    
    - Persistence
        
    - Type filtering
        
- Rules live in:
    
    - CSS Selectors specification
        

---

## 📌 Summary Table

|Pseudo-class|Purpose|Common Pitfall|
|---|---|---|
|`:hover`|Pointer over|Touch misuse|
|`:active`|Activation|Too brief|
|`:focus`|Keyboard focus|Removed outline|
|`:visited`|Visited links|Styling limits|
|`:first-child`|First child|Type confusion|
|`:last-child`|Last child|Type confusion|
|`:nth-child()`|Positional match|Wrong counting|

---

## ✅ Golden Rule

**If state matters → pseudo-class.  
If structure matters → child selectors.  
If type matters → `*-of-type`.**

---

Now this section is **complete and correct**.

👉 **Next topic:** Transitions