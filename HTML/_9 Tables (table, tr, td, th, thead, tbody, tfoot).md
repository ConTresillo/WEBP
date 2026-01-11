# 🟠 HTML — Tables (`<table>`, `<tr>`, `<td>`, `<th>`, `<thead>`, `<tbody>`, `<tfoot>`) — Methods, Pitfalls, Fixes

> `HTML Tables` define **two-dimensional, row–column data structures** with explicit relationships between headers and cells; they represent **tabular data**, not layout grids.

---

---

## 1️⃣ `<table>` — Table Container

### **Purpose (Mandatory — do not skip)**

- Defines a **tabular data context**
    
- Establishes a grid of rows and columns
    
- Provides semantic scope for headers and cells
    
- **Block-level**, **finite**, **eager**
    

---

### **Method**

```html
<table>
  ...
</table>
```

---

### **Correct usage**

```html
<table>
  <tr>
    <td>A</td>
    <td>B</td>
  </tr>
</table>
```

---

### **Observed output**

```text
A | B
```

---

### **Common pitfalls**

- ❌ Using `<table>` for page layout
    
- ❌ Placing text directly inside `<table>`
    
- ❌ Assuming `<table>` implies accessibility
    

---

### **Failure example**

```html
<table>
  Plain text
</table>
```

**Failure:**  
Invalid table structure (missing rows and cells)

---

### **Correct alternative**

```html
<table>
  <tr>
    <td>Plain text</td>
  </tr>
</table>
```

---

### **Observed output**

```text
Plain text
```

---

## 2️⃣ `<tr>` — Table Row

### **Purpose (Mandatory — do not skip)**

- Represents a **single horizontal row**
    
- Groups header or data cells
    
- Must be a child of `<table>`, `<thead>`, `<tbody>`, or `<tfoot>`
    
- **Finite**, **eager**
    

---

### **Method**

```html
<tr>
  <td>...</td>
</tr>
```

---

### **Correct usage**

```html
<tr>
  <td>1</td>
  <td>2</td>
</tr>
```

---

### **Observed output**

```text
1 | 2
```

---

### **Common pitfalls**

- ❌ Using `<tr>` outside table context
    
- ❌ Mixing inconsistent column counts
    

---

### **Failure example**

```html
<tr>
  <td>Item</td>
</tr>
```

**Failure:**  
Invalid placement (row outside table)

---

### **Correct alternative**

```html
<table>
  <tr>
    <td>Item</td>
  </tr>
</table>
```

---

### **Observed output**

```text
Item
```

---

## 3️⃣ `<td>` — Table Data Cell

### **Purpose (Mandatory — do not skip)**

- Represents a **data cell**
    
- Belongs to a specific row and column
    
- Inherits meaning from associated headers
    
- **Finite**, **eager**
    

---

### **Method**

```html
<td>data</td>
```

---

### **Correct usage**

```html
<tr>
  <td>John</td>
  <td>20</td>
</tr>
```

---

### **Observed output**

```text
John | 20
```

---

### **Common pitfalls**

- ❌ Using `<td>` for headers
    
- ❌ Relying on position instead of headers
    

---

### **Failure example**

```html
<td>Data</td>
```

**Failure:**  
Invalid context (cell outside row)

---

### **Correct alternative**

```html
<tr>
  <td>Data</td>
</tr>
```

---

### **Observed output**

```text
Data
```

---

## 4️⃣ `<th>` — Table Header Cell

### **Purpose (Mandatory — do not skip)**

- Represents a **header for a row or column**
    
- Establishes **semantic association** with `<td>`
    
- Defaults to bold and centered (CSS)
    
- **Finite**, **eager**
    

---

### **Method**

```html
<th scope="col|row">header</th>
```

---

### **Correct usage**

```html
<tr>
  <th>Name</th>
  <th>Age</th>
</tr>
```

---

### **Observed output**

```text
Name | Age
```

---

### **Common pitfalls**

- ❌ Using `<td>` instead of `<th>` for headers
    
- ❌ Omitting `scope` in complex tables
    

---

### **Failure example**

```html
<tr>
  <td>Name</td>
</tr>
```

**Failure:**  
Loss of header semantics

---

### **Correct alternative**

```html
<tr>
  <th>Name</th>
</tr>
```

---

### **Observed output**

```text
Name
```

---

## 5️⃣ `<thead>` — Table Header Group

### **Purpose (Mandatory — do not skip)**

- Groups **header rows**
    
- Improves accessibility and structure
    
- Enables browser/AT optimizations
    
- **Optional**, **finite**, **eager**
    

---

### **Method**

```html
<thead>
  <tr>...</tr>
</thead>
```

---

### **Correct usage**

```html
<table>
  <thead>
    <tr>
      <th>Item</th>
      <th>Price</th>
    </tr>
  </thead>
</table>
```

---

### **Observed output**

```text
Item | Price
```

---

### **Common pitfalls**

- ❌ Styling without semantic grouping
    
- ❌ Placing `<thead>` after `<tbody>`
    

---

### **Failure example**

```html
<table>
  <tbody></tbody>
  <thead></thead>
</table>
```

**Failure:**  
Invalid table section order

---

### **Correct alternative**

```html
<table>
  <thead></thead>
  <tbody></tbody>
</table>
```

---

### **Observed output**

```text
Table rendered correctly
```

---

## 6️⃣ `<tbody>` — Table Body Group

### **Purpose (Mandatory — do not skip)**

- Groups **primary data rows**
    
- Default container if omitted
    
- Separates data from headers/footers
    
- **Finite**, **eager**
    

---

### **Method**

```html
<tbody>
  <tr>...</tr>
</tbody>
```

---

### **Correct usage**

```html
<table>
  <tbody>
    <tr>
      <td>Pen</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
```

---

### **Observed output**

```text
Pen | 10
```

---

### **Common pitfalls**

- ❌ Assuming `<tbody>` is optional semantically
    
- ❌ Mixing header rows inside `<tbody>`
    

---

### **Failure example**

```html
<tbody>
  <th>Header</th>
</tbody>
```

**Failure:**  
Invalid row structure

---

### **Correct alternative**

```html
<thead>
  <tr><th>Header</th></tr>
</thead>
```

---

### **Observed output**

```text
Header
```

---

## 7️⃣ `<tfoot>` — Table Footer Group

### **Purpose (Mandatory — do not skip)**

- Groups **summary or total rows**
    
- Semantically distinct from body
    
- Rendered last but may appear earlier in source
    
- **Optional**, **finite**, **eager**
    

---

### **Method**

```html
<tfoot>
  <tr>...</tr>
</tfoot>
```

---

### **Correct usage**

```html
<table>
  <tfoot>
    <tr>
      <td>Total</td>
      <td>100</td>
    </tr>
  </tfoot>
</table>
```

---

### **Observed output**

```text
Total | 100
```

---

### **Common pitfalls**

- ❌ Using `<tfoot>` for styling only
    
- ❌ Duplicating body rows
    

---

### **Failure example**

```html
<tfoot>
  <td>Total</td>
</tfoot>
```

**Failure:**  
Missing `<tr>`

---

### **Correct alternative**

```html
<tfoot>
  <tr>
    <td>Total</td>
  </tr>
</tfoot>
```

---

### **Observed output**

```text
Total
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **Tables vs Layout**

```html
<table>
  <tr><td>Column</td></tr>
</table>
```

```text
Layout misuse
```

✅ Tables are for **data relationships**, not grids

---

❌ **Headers by styling**

```html
<td><b>Name</b></td>
```

```text
No header semantics
```

✅ Use `<th>` for meaning

---

❌ **Missing associations**

```html
<th>Name</th>
<td>Alice</td>
```

```text
Weak accessibility
```

✅ Use proper row/column structure

---

## 🧠 Mental Model (Exam + Design)

- Tables encode **data relationships**
    
- `<table>` defines the data space
    
- `<tr>` defines records
    
- `<th>` defines meaning
    
- `<td>` defines values
    
- Sectioning tags improve **accessibility**, not layout
    
- Visual styling is **orthogonal** to semantics
    

---

## 📌 Summary Table

|Tag|Purpose|Common Pitfall|
|---|---|---|
|`<table>`|Data container|Used for layout|
|`<tr>`|Row|Outside table|
|`<td>`|Data cell|Used as header|
|`<th>`|Header cell|Styled `<td>` instead|
|`<thead>`|Header group|Wrong order|
|`<tbody>`|Data group|Mixed headers|
|`<tfoot>`|Summary group|Styling misuse|

---

## ✅ Golden Rule

Use tables **only when data forms rows and columns**.  
Headers (`<th>`) define meaning; cells (`<td>`) hold values.  
If removing CSS breaks understanding, the table is semantically correct.