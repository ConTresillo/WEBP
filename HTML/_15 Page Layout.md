# 🟠 HTML — Page Layout (Semantic Structure & Patterns) — Methods, Pitfalls, Fixes

> `HTML Page Layout` defines **how major content regions are structured and related** using semantic elements; it encodes **document hierarchy and landmarks**, not visual positioning.

---

---

## 1️⃣ Semantic Page Skeleton — Base Layout

### **Purpose (Mandatory — do not skip)**

- Establishes **global document regions**
    
- Creates navigable **landmarks** for accessibility
    
- Separates primary content from auxiliary content
    
- **Block-level**, **finite**, **eager**
    

---

### **Method**

```html
<header></header>
<nav></nav>
<main></main>
<footer></footer>
```

---

### **Correct usage**

```html
<header>Site Header</header>
<nav>Main Navigation</nav>
<main>
  <article>Main Content</article>
</main>
<footer>Footer</footer>
```

---

### **Observed output**

```text
Header → Navigation → Main → Footer landmarks
```

---

### **Common pitfalls**

- ❌ Using `<div>` for all regions
    
- ❌ Multiple `<main>` elements
    
- ❌ Placing navigation inside `<main>` without intent
    

---

### **Failure example**

```html
<div>Header</div>
<div>Nav</div>
<div>Main</div>
```

**Failure:**  
No semantic landmarks

---

### **Correct alternative**

```html
<header>Header</header>
<nav>Nav</nav>
<main>Main</main>
```

---

### **Observed output**

```text
Semantic regions exposed to assistive tech
```

---

## 2️⃣ Content Grouping Pattern — Sections & Articles

### **Purpose (Mandatory — do not skip)**

- Groups content by **theme** (`<section>`)
    
- Encapsulates **standalone units** (`<article>`)
    
- Enables hierarchical document outlines
    
- **Block-level**, **finite**, **eager**
    

---

### **Method**

```html
<section>
  <article></article>
</section>
```

---

### **Correct usage**

```html
<section>
  <h2>News</h2>
  <article>
    <h3>Update</h3>
    <p>Details</p>
  </article>
</section>
```

---

### **Observed output**

```text
Section → Article hierarchy
```

---

### **Common pitfalls**

- ❌ Using `<section>` without a heading
    
- ❌ Wrapping every element in `<article>`
    
- ❌ Confusing layout blocks with semantic units
    

---

### **Failure example**

```html
<section>
  <p>Text</p>
</section>
```

**Failure:**  
Section lacks thematic identity

---

### **Correct alternative**

```html
<section>
  <h2>Topic</h2>
  <p>Text</p>
</section>
```

---

### **Observed output**

```text
Section announced with heading
```

---

## 3️⃣ Sidebar Pattern — `<aside>`

### **Purpose (Mandatory — do not skip)**

- Holds **tangential or complementary content**
    
- Related to surrounding main content
    
- Recognized as a landmark in some contexts
    
- **Block-level**, **finite**, **eager**
    

---

### **Method**

```html
<aside>...</aside>
```

---

### **Correct usage**

```html
<main>
  <article>Main article</article>
  <aside>Related links</aside>
</main>
```

---

### **Observed output**

```text
Primary content with related aside
```

---

### **Common pitfalls**

- ❌ Using `<aside>` as primary content
    
- ❌ Treating `<aside>` as mandatory sidebar
    
- ❌ Nesting unrelated content
    

---

### **Failure example**

```html
<aside>Main content</aside>
```

**Failure:**  
Incorrect semantic role

---

### **Correct alternative**

```html
<article>Main content</article>
```

---

### **Observed output**

```text
Correct content role
```

---

## 4️⃣ Header/Footer Scoping — Local vs Global

### **Purpose (Mandatory — do not skip)**

- Allows **multiple headers and footers**
    
- Scope is defined by nearest sectioning ancestor
    
- Distinguishes page-level vs section-level metadata
    
- **Block-level**, **finite**, **eager**
    

---

### **Method**

```html
<header>...</header>
<footer>...</footer>
```

---

### **Correct usage**

```html
<article>
  <header>
    <h2>Post title</h2>
  </header>
  <p>Post body</p>
  <footer>Author info</footer>
</article>
```

---

### **Observed output**

```text
Article-scoped header and footer
```

---

### **Common pitfalls**

- ❌ Assuming only one header/footer per page
    
- ❌ Putting main content inside footer
    

---

### **Failure example**

```html
<footer>
  <article>Content</article>
</footer>
```

**Failure:**  
Footer misused as container

---

### **Correct alternative**

```html
<article>
  <footer>Meta info</footer>
</article>
```

---

### **Observed output**

```text
Footer scoped correctly
```

---

## 5️⃣ Layout vs Semantics — Separation of Concerns

### **Purpose (Mandatory — do not skip)**

- Ensures **HTML encodes meaning**
    
- CSS handles **visual layout**
    
- Prevents accessibility and SEO failures
    
- **Conceptual**, **non-visual**
    

---

### **Method**

```html
<!-- HTML for structure -->
<!-- CSS for layout -->
```

---

### **Correct usage**

```html
<main>
  <section>Content</section>
</main>
```

---

### **Observed output**

```text
Meaning preserved without CSS
```

---

### **Common pitfalls**

- ❌ Using tables/divs for layout only
    
- ❌ Encoding grid intent in HTML
    
- ❌ Relying on CSS classes for meaning
    

---

### **Failure example**

```html
<table>
  <tr><td>Main</td></tr>
</table>
```

**Failure:**  
Layout masquerading as data

---

### **Correct alternative**

```html
<main>Main</main>
```

---

### **Observed output**

```text
Correct semantic structure
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **Layout-first thinking**

```html
<div class="row">
  <div class="col">A</div>
</div>
```

```text
No semantic meaning
```

✅ Semantics first, layout second

---

❌ **Everything is a section**

```html
<section><section><section>Text</section></section></section>
```

```text
Outline noise
```

✅ Use sections sparingly and intentionally

---

❌ **Visual position = semantic role**

```html
<div class="sidebar">Important</div>
```

```text
No role conveyed
```

✅ Use `<aside>` for tangential content

---

## 🧠 Mental Model (Exam + Design)

- Layout is a **document map**, not a grid
    
- Semantic tags create **landmarks**
    
- Headings define the outline
    
- `<main>` is unique and central
    
- CSS can change appearance without breaking meaning
    
- Removing CSS should preserve understanding
    

---

## 📌 Summary Table

|Pattern|Purpose|Common Pitfall|
|---|---|---|
|Page skeleton|Global structure|Div-only layout|
|Sections|Thematic grouping|No heading|
|Articles|Standalone units|Layout misuse|
|Aside|Related content|Primary misuse|
|Headers/Footers|Scoped metadata|Content misuse|

---

## ✅ Golden Rule

If removing CSS **breaks understanding**, the layout is wrong.  
HTML defines **structure and meaning**; CSS defines **appearance**.