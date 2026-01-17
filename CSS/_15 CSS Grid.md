# 🟠 CSS Grid (Exam-Level) — Methods, Pitfalls, Fixes

> `CSS Grid` is a **two-dimensional layout system** that controls rows and columns simultaneously at the container level.

---

## 1️⃣ `display:grid`

### **Purpose (Mandatory — do not skip)**

- Turns an element into a **grid container**
    
- Establishes a new grid formatting context
    
- Child elements become **grid items**
    
- Layout is eager and deterministic
    

### **Method**

```css
display: grid;
```

### **Correct usage**

```css
.container {
  display: grid;
}
```

### **Observed output**

```text
Children participate in grid layout instead of normal flow.
```

### **Common pitfalls**

- ❌ Expecting grid behavior without `display:grid`
    
- ❌ Confusing grid container vs grid items
    

### **Failure example**

```css
.container {
  grid-template-columns: 1fr 1fr;
}
```

**Failure:** ignored because container is not a grid

### **Correct alternative**

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
```

### **Observed output**

```text
Two equal columns created.
```

---

## 2️⃣ `grid-template-columns(columnTracks)`

### **Purpose (Mandatory — do not skip)**

- Defines **column structure**
    
- Establishes explicit grid columns
    
- Accepts fixed, flexible, or mixed units
    

### **Method**

```css
grid-template-columns: <track-size> ...;
```

### **Correct usage**

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 1fr;
}
```

### **Observed output**

```text
Three columns: fixed + two flexible.
```

### **Common pitfalls**

- ❌ Forgetting total width constraints
    
- ❌ Assuming columns auto-wrap
    

### **Failure example**

```css
grid-template-columns: 1fr 1fr 1fr 1fr;
```

(on narrow screen)

**Failure:** overflow occurs

### **Correct alternative**

```css
grid-template-columns: repeat(4, 1fr);
```

### **Observed output**

```text
Same layout, clearer intent.
```

---

## 3️⃣ `grid-template-rows(rowTracks)`

### **Purpose (Mandatory — do not skip)**

- Defines **row structure**
    
- Controls vertical layout
    
- Rows grow to fit content by default
    

### **Method**

```css
grid-template-rows: <track-size> ...;
```

### **Correct usage**

```css
.container {
  grid-template-rows: 100px auto;
}
```

### **Observed output**

```text
First row fixed, second adapts to content.
```

### **Common pitfalls**

- ❌ Using fixed heights everywhere
    
- ❌ Expecting rows to auto-equalize
    

### **Failure example**

```css
grid-template-rows: 100px 100px;
```

(with more content)

**Failure:** content overflow

### **Correct alternative**

```css
grid-template-rows: auto auto;
```

### **Observed output**

```text
Rows expand naturally.
```

---

## 4️⃣ `gap(rowColumnSpacing)`

### **Purpose (Mandatory — do not skip)**

- Adds spacing **between grid tracks**
    
- Does not affect outer edges
    
- Replaces `grid-row-gap` / `grid-column-gap`
    

### **Method**

```css
gap: <length>;
```

### **Correct usage**

```css
.container {
  gap: 16px;
}
```

### **Observed output**

```text
Uniform spacing between grid items.
```

### **Common pitfalls**

- ❌ Expecting margin-like behavior
    
- ❌ Using margins instead of gap
    

### **Failure example**

```css
.item {
  margin: 16px;
}
```

**Failure:** outer spacing also added unintentionally

### **Correct alternative**

```css
.container {
  gap: 16px;
}
```

### **Observed output**

```text
Clean internal spacing only.
```

---

## 5️⃣ `grid-column(itemPlacementX)`

### **Purpose (Mandatory — do not skip)**

- Places item **horizontally** in grid
    
- Can span multiple columns
    
- Overrides auto-placement
    

### **Method**

```css
grid-column: <start> / <end>;
```

### **Correct usage**

```css
.item {
  grid-column: 1 / 3;
}
```

### **Observed output**

```text
Item spans first two columns.
```

### **Common pitfalls**

- ❌ Off-by-one errors
    
- ❌ Assuming columns start at 0
    

### **Failure example**

```css
grid-column: 0 / 2;
```

**Failure:** invalid line index

### **Correct alternative**

```css
grid-column: 1 / 3;
```

### **Observed output**

```text
Item placed correctly.
```

---

## 6️⃣ `grid-row(itemPlacementY)`

### **Purpose (Mandatory — do not skip)**

- Places item **vertically** in grid
    
- Can span rows
    
- Independent of column placement
    

### **Method**

```css
grid-row: <start> / <end>;
```

### **Correct usage**

```css
.item {
  grid-row: 2 / 4;
}
```

### **Observed output**

```text
Item spans rows 2 and 3.
```

### **Common pitfalls**

- ❌ Confusing row and column lines
    
- ❌ Expecting auto centering
    

### **Failure example**

```css
grid-row: 3 / 2;
```

**Failure:** invalid range

### **Correct alternative**

```css
grid-row: 2 / 3;
```

### **Observed output**

```text
Valid placement applied.
```

---

## 7️⃣ `gridLayout(pageStructure)`

### **Purpose (Mandatory — do not skip)**

- Creates **page-level layouts**
    
- Replaces float-based and table layouts
    
- Deterministic and readable
    

### **Method**

```css
grid-template-areas
```

### **Correct usage**

```css
.container {
  display: grid;
  grid-template-columns: 1fr 3fr;
}
```

### **Observed output**

```text
Sidebar + content layout achieved.
```

### **Common pitfalls**

- ❌ Overusing grid for one-dimensional layouts
    
- ❌ Forgetting responsiveness
    

### **Failure example**

```css
grid-template-columns: 300px 900px;
```

**Failure:** breaks on small screens

### **Correct alternative**

```css
grid-template-columns: 1fr 3fr;
```

### **Observed output**

```text
Layout adapts to screen width.
```

---

## 🚨 Conceptual Pitfalls (Very Important)

- ❌ Grid is one-dimensional
    
- ✅ Grid is **two-dimensional** (rows + columns)
    
- ❌ Grid items affect container size
    
- ✅ Container defines layout; items obey
    

---

## 🧠 Mental Model (Exam + Design)

- Grid exists to **control layout at the container level**
    
- Guarantees:
    
    - Explicit row/column control
        
- Undefined:
    
    - Content semantics
        
- Rules live in:
    
    - CSS Grid Layout spec
        
    - Layout engine
        

---

## 📌 Summary Table

|Property|Purpose|Common Pitfall|
|---|---|---|
|display:grid|Enable grid|Missing declaration|
|grid-template-columns|Column structure|Overflow|
|grid-template-rows|Row structure|Fixed heights|
|gap|Track spacing|Using margins|
|grid-column|Horizontal placement|Wrong indices|
|grid-row|Vertical placement|Reversed range|
|Grid layout|Page structure|Non-responsive|

---

## ✅ Golden Rule

Use **Grid for two-dimensional layout**, not alignment hacks.  
If you’re positioning items individually, you’re **missing Grid’s intent**.

**Next topic:** Pseudo-classes & States

---

# 🟠 CSS Grid — Combat Sheet 

---

## 1️⃣ Equal Columns Grid

**Use when:** cards, sections, uniform layouts.

### RAW (renders in Obsidian)
<div style="
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  background: #f5f5f5;
  padding: 12px;
">
  <div style="background:#add8e6; padding:16px; color:black;">A</div>
  <div style="background:#90ee90; padding:16px; color:black;">B</div>
  <div style="background:#ffcccb; padding:16px; color:black;">C</div>
</div>
### FENCED (for reading)

```html
<div style="
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  background: #f5f5f5;
  padding: 12px;
">
  <div style="background:#add8e6; padding:16px; color:black;">A</div>
  <div style="background:#90ee90; padding:16px; color:black;">B</div>
  <div style="background:#ffcccb; padding:16px; color:black;">C</div>
</div>
```

---

## 2️⃣ Full-Width Item (Exam Favorite)

**Use when:** banner, header, separator.

### RAW
<div style="
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  background: #f5f5f5;
  padding: 12px;
">
  <div style="background:#add8e6; padding:16px; color:black;">A</div>
  <div style="background:#90ee90; padding:16px; color:black;">B</div>
  <div style="background:#ffcccb; padding:16px; color:black;">C</div>

  <div style="
    background:#ffd700;
    padding:16px;
    grid-column: 1 / -1; color:black;
  ">
    FULL WIDTH
  </div>
</div>
### FENCED

```html
<div style="
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  background: #f5f5f5;
  padding: 12px;
">
  <div style="background:#add8e6; padding:16px;">A</div>
  <div style="background:#90ee90; padding:16px;">B</div>
  <div style="background:#ffcccb; padding:16px;">C</div>

  <div style="
    background:#ffd700;
    padding:16px;
    grid-column: 1 / -1;
  ">
    FULL WIDTH
  </div>
</div>
```

---

## 3️⃣ Sidebar + Content

**Use when:** dashboards, blogs, admin panels.

### RAW
<div style="
  display: grid;
  grid-template-columns: 200px 1fr;
  gap: 12px;
  background: #f5f5f5;
  padding: 12px;
">
  <div style="background:#ccc; padding:16px; color:black;">Sidebar</div>
  <div style="background:#eee; padding:16px; color:black;">Main Content</div>
</div>

### FENCED

```html
<div style="
  display: grid;
  grid-template-columns: 20px 1fr;
  gap: 12px;
  background: #f5f5f5;
  padding: 12px;
">
  <div style="background:#ccc; padding:16px; color:black;">Sidebar</div>
  <div style="background:#eee; padding:16px; color:black;">Main Content</div>
</div>
```

---

## 4️⃣ Responsive Card Grid (Auto-Fit)

**Use when:** galleries, product grids.

### RAW
<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 5fr));
  gap: 12px;
  background: #f5f5f5;
  padding: 12px; color:black;
">
  <div style="background:#add8e6; padding:16px;">Card 1</div>
  <div style="background:#90ee90; padding:16px;">Card 2</div>
  <div style="background:#ffcccb; padding:16px;">Card 3</div>
  <div style="background:#dda0dd; padding:16px;">Card 4</div>
  <div style="background:#dda0dd; padding:16px;">Card 5</div>
  <div style="background:#dda0dd; padding:16px;">Card 6</div>
</div>
### FENCED

```html
<div style="
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 5fr));
  gap: 12px;
  background: #f5f5f5;
  padding: 12px; color:black;
">
  <div style="background:#add8e6; padding:16px;">Card 1</div>
  <div style="background:#90ee90; padding:16px;">Card 2</div>
  <div style="background:#ffcccb; padding:16px;">Card 3</div>
  <div style="background:#dda0dd; padding:16px;">Card 4</div>
  <div style="background:#dda0dd; padding:16px;">Card 5</div>
  <div style="background:#dda0dd; padding:16px;">Card 6</div>
</div>
```

---

## 5️⃣ Center Everything (Hero Section)

**Use when:** landing page hero, empty states.

### RAW
<div style="
  display: grid;
  place-items: center;
  min-height: 200px;
  background: #def;
">
  <div style="background:#add8e6; padding:20px; color:black;">
    Centered Content
  </div>
</div>
### FENCED

```html
<div style="
  display: grid;
  place-items: center;
  min-height: 200px;
  background: #def;
">
  <div style="background:#add8e6; padding:20px; color:black;">
    Centered Content
  </div>
</div>
```

---

## 6️⃣ Navbar Layout (Logo — Links — Action)

### RAW
<div style="
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  padding: 12px;
  background: #ccc;
">
  <div style="color:black;">Logo</div>
  <div style="text-align:center;">Links</div>
  <div style="color:black;">Login</div>
</div>
### FENCED

```html
<div style="
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  padding: 12px;
  background: #ccc;
">
  <div>Logo</div>
  <div style="text-align:center;">Links</div>
  <div>Login</div>
</div>
```

---

## 🧠 FINAL PRESSURE RULE (MEMORIZE)

> **If you can draw boxes on paper, you can build it with Grid.**  
> Columns first → gap → span if needed → done.

If you want next, I can:

- Convert this into a **single Obsidian note**
    
- Add **exam MCQs under each pattern**
    
- Do **Flex vs Grid side-by-side**
    
- Create **timed layout drills**
    

Just say which.