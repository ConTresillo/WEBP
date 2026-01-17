# 🟠 CSS Lists & Tables — Methods, Pitfalls, Fixes

> `CSS Lists & Tables` control **marker styling, alignment, and table border behavior** without changing document semantics.

---

## 1️⃣ `list-style-type(markerShape)`

### **Purpose (Mandatory — do not skip)**

- Defines the **bullet or numbering style**
    
- Applies to list items (`<li>`)
    
- Visual-only change
    

### **Method**

```css
list-style-type: disc | circle | square | decimal | none;
```

### **Correct usage**

```css
ul {
  list-style-type: square;
}
```

### **Observed output**

```text
List items display square bullets.
```

### **Common pitfalls**

- ❌ Applying to `<li>` inconsistently
    
- ❌ Expecting semantic change
    

### **Failure example**

```css
ul {
  list-style-type: triangle;
}
```

**Failure:** invalid value → ignored

### **Correct alternative**

```css
ul {
  list-style-type: disc;
}
```

### **Observed output**

```text
Default bullet restored.
```

---

## 2️⃣ `list-style-position(markerPlacement)`

### **Purpose (Mandatory — do not skip)**

- Controls **where bullet is drawn**
    
- Affects text alignment
    
- Impacts wrapping behavior
    

### **Method**

```css
list-style-position: inside | outside;
```

### **Correct usage**

```css
ul {
  list-style-position: inside;
}
```

### **Observed output**

```text
Bullets align with text block.
```

### **Common pitfalls**

- ❌ Unexpected text wrapping
    
- ❌ Assuming indentation unchanged
    

### **Failure example**

```css
ul {
  list-style-position: inside;
}
```

(with long text)

**Failure:** awkward wrapped lines

### **Correct alternative**

```css
ul {
  list-style-position: outside;
}
```

### **Observed output**

```text
Clean indentation preserved.
```

---

## 3️⃣ `list-style(shorthand)`

### **Purpose (Mandatory — do not skip)**

- Combines list-style properties
    
- Resets unspecified values
    
- Order-insensitive
    

### **Method**

```css
list-style: <type> <position>;
```

### **Correct usage**

```css
ul {
  list-style: square inside;
}
```

### **Observed output**

```text
Square bullets inside text block.
```

### **Common pitfalls**

- ❌ Forgetting shorthand resets defaults
    
- ❌ Assuming image persists
    

### **Failure example**

```css
ul {
  list-style: none;
}
```

**Failure:** bullets removed unintentionally

### **Correct alternative**

```css
ul {
  list-style: disc outside;
}
```

### **Observed output**

```text
Bullets restored.
```

---

## 4️⃣ `table-border(borderDefinition)`

### **Purpose (Mandatory — do not skip)**

- Defines visible borders on tables
    
- Applies to table, rows, and cells
    
- Affects layout
    

### **Method**

```css
table, th, td {
  border: <width> <style> <color>;
}
```

### **Correct usage**

```css
table, th, td {
  border: 1px solid black;
}
```

### **Observed output**

```text
Grid lines appear around all cells.
```

### **Common pitfalls**

- ❌ Border duplication
    
- ❌ Forgetting collapse behavior
    

### **Failure example**

```css
table {
  border: 1px solid black;
}
```

**Failure:** inner cell borders missing

### **Correct alternative**

```css
table, th, td {
  border: 1px solid black;
}
```

### **Observed output**

```text
Complete grid visible.
```

---

## 5️⃣ `border-collapse(collapseMode)`

### **Purpose (Mandatory — do not skip)**

- Controls whether borders merge
    
- Impacts spacing and thickness
    
- Table-only property
    

### **Method**

```css
border-collapse: collapse | separate;
```

### **Correct usage**

```css
table {
  border-collapse: collapse;
}
```

### **Observed output**

```text
Adjacent borders merge into single lines.
```

### **Common pitfalls**

- ❌ Forgetting default is `separate`
    
- ❌ Expecting margin-like gaps
    

### **Failure example**

```css
table {
  border-collapse: separate;
}
```

**Failure:** double borders appear

### **Correct alternative**

```css
table {
  border-collapse: collapse;
}
```

### **Observed output**

```text
Clean table borders.
```

---

## 6️⃣ `table-alignment(textAlign)`

### **Purpose (Mandatory — do not skip)**

- Aligns text inside cells
    
- Horizontal alignment only
    
- Does not move table itself
    

### **Method**

```css
text-align: left | center | right;
```

### **Correct usage**

```css
td {
  text-align: center;
}
```

### **Observed output**

```text
Cell content centered.
```

### **Common pitfalls**

- ❌ Confusing cell vs table alignment
    
- ❌ Expecting vertical centering
    

### **Failure example**

```css
table {
  text-align: center;
}
```

**Failure:** headers and cells all affected unintentionally

### **Correct alternative**

```css
th, td {
  text-align: center;
}
```

### **Observed output**

```text
Explicit alignment applied.
```

---

## 🚨 Conceptual Pitfalls (Very Important)

- ❌ List styling changes meaning
    
- ✅ List styling is **purely visual**
    
- ❌ `border-collapse` affects spacing like margin
    
- ✅ It merges border rendering only
    

---

## 🧠 Mental Model (Exam + Design)

- Lists and tables have **fixed semantics**
    
- CSS controls **presentation only**
    
- Guarantees:
    
    - Structural meaning preserved
        
- Rules live in:
    
    - CSS Lists spec
        
    - CSS Tables spec
        

---

## 📌 Summary Table

|Property|Purpose|Common Pitfall|
|---|---|---|
|list-style-type|Bullet shape|Invalid values|
|list-style-position|Bullet placement|Text wrap issues|
|list-style|Shorthand|Unintended reset|
|table borders|Grid lines|Missing cells|
|border-collapse|Merge borders|Double lines|
|text-align (tables)|Cell text align|Over-broad scope|

---

## ✅ Golden Rule

**Style lists and tables visually — never rely on CSS to change their meaning.**  
If structure feels wrong, fix the HTML, not the CSS.

**Next topic:** CSS Grid