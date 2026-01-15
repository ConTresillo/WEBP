# 🟠 HTML — Basic Tags (Headings, Paragraph, Line Break, Horizontal Line)

> `HTML Basic Tags` are **structural and semantic primitives** used to represent **text blocks and document flow**; they define **meaning and layout intent**, not styling or behavior.

---

---

## 1️⃣ `<h1>` … `<h6>` — Headings

### **Purpose (Mandatory — do not skip)**

- Represent **section headings** with **semantic importance**
    
- Define the **document outline** used by browsers, screen readers, and search engines
    
- `<h1>` is highest priority, `<h6>` is lowest
    
- **Eager**, **finite**, **non-nestable hierarchy**
    

---

### **Method**

```html
<h1> … </h1>
<h2> … </h2>
<h3> … </h3>
<h4> … </h4>
<h5> … </h5>
<h6> … </h6>
```

---

### **Correct usage**

```html
<h1>Main Title</h1>
<h2>Section</h2>
<h3>Subsection</h3>
```

---

### **Observed output**

```text
Main Title
  Section
    Subsection
```

(Rendered with decreasing default font size and weight)

---

### **Common pitfalls**

- ❌ Using headings for font size only
    
- ❌ Skipping heading levels (`h1` → `h4`)
    
- ❌ Multiple `<h1>` without structural reason
    

---

### **Failure example**

```html
<h1>Main</h1>
<h4>Sub</h4>
```

**Failure:**  
Broken document outline (accessibility + SEO impact)

---

### **Correct alternative**

```html
<h1>Main</h1>
<h2>Sub</h2>
```

---

### **Observed output**

```text
Logical heading hierarchy preserved
```

---

## 2️⃣ `<p>` — Paragraph

### **Purpose (Mandatory — do not skip)**

- Represents a **block-level paragraph of text**
    
- Automatically creates **vertical separation**
    
- Cannot contain block-level elements
    
- **Eager**, **finite**, **block-level**
    

---

### **Method**

```html
<p> … </p>
```

---

### **Correct usage**

```html
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```

---

### **Observed output**

```text
This is a paragraph.

This is another paragraph.
```

---

### **Common pitfalls**

- ❌ Using `<p>` as a generic container
    
- ❌ Nesting block elements inside `<p>`
    
- ❌ Expecting line breaks without `<br>`
    

---

### **Failure example**

```html
<p>
  <h1>Title</h1>
</p>
```

**Failure:**  
Browser implicitly closes `<p>` → invalid structure

---

### **Correct alternative**

```html
<h1>Title</h1>
<p>Description</p>
```

---

### **Observed output**

```text
Title
Description
```

---

## 3️⃣ `<br>` — Line Break

### **Purpose (Mandatory — do not skip)**

- Forces a **line break within inline content**
    
- Does **not** create a new paragraph
    
- **Void element**, no closing tag
    
- **Inline-level**, **eager**
    

---

### **Method**

```html
<br>
```

---

### **Correct usage**

```html
<p>
  Line one<br>
  Line two
</p>
```

---

### **Observed output**

```text
Line one
Line two
```

---

### **Common pitfalls**

- ❌ Using `<br>` for spacing/layout
    
- ❌ Replacing paragraphs with `<br><br>`
    

---

### **Failure example**

```html
Line one<br><br><br>Line two
```

**Failure:**  
Unsemantic spacing, poor maintainability

---

### **Correct alternative**

```html
<p>Line one</p>
<p>Line two</p>
```

---

### **Observed output**

```text
Line one

Line two
```

---

## 4️⃣ `<hr>` — Horizontal Rule

### **Purpose (Mandatory — do not skip)**

- Represents a **thematic break** between sections
    
- Semantic meaning: **context shift**
    
- **Void element**, block-level
    
- Styling handled via CSS
    

---

### **Method**

```html
<hr>
```

---

### **Correct usage**

```html
<p>Section A</p>
<hr>
<p>Section B</p>
```

---

### **Observed output**

```text
Section A
--------------------
Section B
```

(Default horizontal line rendered)

---

### **Common pitfalls**

- ❌ Using `<hr>` purely as decoration
    
- ❌ Expecting spacing control without CSS
    

---

### **Failure example**

```html
<hr><hr><hr>
```

**Failure:**  
Semantic misuse (no thematic meaning)

---

### **Correct alternative**

```html
<hr class="section-divider">
```

```css
.section-divider {
  margin: 2rem 0;
}
```

---

### **Observed output**

```text
Single meaningful section break
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **Headings vs Styling**

```html
<h1>Big Text</h1>
```

```text
Looks large but also changes document structure
```

✅ Use headings for **meaning**, CSS for size

---

❌ **`<br>` vs `<p>`**

```html
Hello<br>World
```

```text
Single paragraph with line break
```

✅ Paragraphs represent **separate thoughts**

---

❌ **`<hr>` vs `<div>`**

```html
<div></div>
```

```text
No semantic meaning
```

✅ `<hr>` conveys **thematic separation**

---

## 🧠 Mental Model (Exam + Design)

- Headings define **document hierarchy**
    
- Paragraphs define **content units**
    
- `<br>` affects **line flow**, not structure
    
- `<hr>` signals **semantic separation**
    
- Visual appearance is **incidental**, not guaranteed
    
- Accessibility tools rely on correct tag choice
    

---

## 📌 Summary Table

|Tag|Purpose|Common Pitfall|
|---|---|---|
|`<h1>`–`<h6>`|Section hierarchy|Used for font size|
|`<p>`|Text block|Nested blocks|
|`<br>`|Line break|Used for layout|
|`<hr>`|Thematic break|Decorative misuse|

---

## ✅ Golden Rule

Use basic HTML tags to express **meaning and structure**,  
never to control **appearance or layout**.