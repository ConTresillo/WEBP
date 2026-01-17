# 🟠 CSS Text & Fonts — Methods, Pitfalls, Fixes

> `CSS Text & Fonts` control **how textual content is rendered, spaced, transformed, and aligned** without affecting document structure.

---

## 1️⃣ `font-family(typefaceStack)`

### **Purpose (Mandatory — do not skip)**

- Defines the **font selection order**
    
- Browser picks the **first available font**
    
- Falls back deterministically
    

### **Method**

```css
font-family: <family-name>, <generic-family>;
```

### **Correct usage**

```css
p {
  font-family: "Arial", "Helvetica", sans-serif;
}
```

### **Observed output**

```text
Text renders using the first available font in the list.
```

### **Common pitfalls**

- ❌ Missing generic fallback
    
- ❌ Forgetting quotes for multi-word fonts
    

### **Failure example**

```css
p {
  font-family: Times New Roman;
}
```

**Failure:** parsed as multiple identifiers → invalid

### **Correct alternative**

```css
p {
  font-family: "Times New Roman", serif;
}
```

### **Observed output**

```text
Font renders correctly with fallback.
```

---

## 2️⃣ `font-size(textScale)`

### **Purpose (Mandatory — do not skip)**

- Sets the **size of glyphs**
    
- Accepts absolute and relative units
    
- Inherited by default
    

### **Method**

```css
font-size: <length> | <percentage>;
```

### **Correct usage**

```css
p {
  font-size: 1rem;
}
```

### **Observed output**

```text
Text scales relative to root font size.
```

### **Common pitfalls**

- ❌ Using px everywhere
    
- ❌ Forgetting inheritance
    

### **Failure example**

```css
p {
  font-size: 12px;
}
```

**Failure:** poor accessibility scaling

### **Correct alternative**

```css
p {
  font-size: 1em;
}
```

### **Observed output**

```text
Text scales with parent.
```

---

## 3️⃣ `font-weight(strokeThickness)`

### **Purpose (Mandatory — do not skip)**

- Controls **boldness**
    
- Accepts keywords or numeric weights
    
- Depends on font support
    

### **Method**

```css
font-weight: normal | bold | 100–900;
```

### **Correct usage**

```css
strong {
  font-weight: 700;
}
```

### **Observed output**

```text
Text appears bold.
```

### **Common pitfalls**

- ❌ Using unsupported weights
    
- ❌ Expecting visual difference always
    

### **Failure example**

```css
p {
  font-weight: 900;
}
```

(on a font with only regular/bold)

**Failure:** browser maps to nearest weight

### **Correct alternative**

```css
p {
  font-weight: bold;
}
```

### **Observed output**

```text
Predictable bold rendering.
```

---

## 4️⃣ `font-style(posture)`

### **Purpose (Mandatory — do not skip)**

- Applies italic or oblique style
    
- Oblique may be synthetic
    
- Inherited property
    

### **Method**

```css
font-style: normal | italic | oblique;
```

### **Correct usage**

```css
em {
  font-style: italic;
}
```

### **Observed output**

```text
Text rendered in italic.
```

### **Common pitfalls**

- ❌ Expecting italic font to exist
    
- ❌ Confusing italic with oblique
    

### **Failure example**

```css
p {
  font-style: oblique;
}
```

**Failure:** artificial slant if font lacks oblique

### **Correct alternative**

```css
p {
  font-style: italic;
}
```

### **Observed output**

```text
True italic used if available.
```

---

## 5️⃣ `text-align(inlineAlignment)`

### **Purpose (Mandatory — do not skip)**

- Aligns **inline content horizontally**
    
- Does not move block elements
    
- Applies to container, not text itself
    

### **Method**

```css
text-align: left | right | center | justify;
```

### **Correct usage**

```css
div {
  text-align: center;
}
```

### **Observed output**

```text
Text centered inside container.
```

### **Common pitfalls**

- ❌ Expecting block centering
    
- ❌ Applying to inline elements
    

### **Failure example**

```css
p {
  text-align: center;
}
```

(trying to center the paragraph block)

**Failure:** only text centered, not block

### **Correct alternative**

```css
p {
  margin: 0 auto;
}
```

### **Observed output**

```text
Paragraph block centered.
```

---

## 6️⃣ `text-decoration(lineEffects)`

### **Purpose (Mandatory — do not skip)**

- Adds decorative lines
    
- Does not affect layout
    
- Commonly used for links
    

### **Method**

```css
text-decoration: none | underline | line-through;
```

### **Correct usage**

```css
a {
  text-decoration: none;
}
```

### **Observed output**

```text
Underline removed from link.
```

### **Common pitfalls**

- ❌ Removing link affordance without replacement
    
- ❌ Assuming decoration affects spacing
    

### **Failure example**

```css
a {
  text-decoration: none;
}
```

**Failure:** links indistinguishable

### **Correct alternative**

```css
a {
  text-decoration: underline;
}
```

### **Observed output**

```text
Link visibly indicated.
```

---

## 7️⃣ `text-transform(letterCase)`

### **Purpose (Mandatory — do not skip)**

- Controls letter casing
    
- Visual only; content unchanged
    
- Inherited
    

### **Method**

```css
text-transform: uppercase | lowercase | capitalize;
```

### **Correct usage**

```css
h1 {
  text-transform: uppercase;
}
```

### **Observed output**

```text
Heading text appears uppercase.
```

### **Common pitfalls**

- ❌ Expecting data transformation
    
- ❌ Using capitalize blindly
    

### **Failure example**

```css
p {
  text-transform: capitalize;
}
```

**Failure:** improper capitalization of names

### **Correct alternative**

```css
p {
  text-transform: none;
}
```

### **Observed output**

```text
Original text preserved.
```

---

## 8️⃣ `line-height(verticalSpacing)`

### **Purpose (Mandatory — do not skip)**

- Controls vertical spacing between lines
    
- Inherited
    
- Accepts unitless values (recommended)
    

### **Method**

```css
line-height: <number> | <length>;
```

### **Correct usage**

```css
p {
  line-height: 1.6;
}
```

### **Observed output**

```text
Comfortable vertical spacing between lines.
```

### **Common pitfalls**

- ❌ Using px values
    
- ❌ Forgetting inheritance behavior
    

### **Failure example**

```css
p {
  line-height: 16px;
}
```

**Failure:** cramped text at different sizes

### **Correct alternative**

```css
p {
  line-height: 1.6;
}
```

### **Observed output**

```text
Responsive spacing preserved.
```

---

## 9️⃣ `letter-spacing(characterGap)`

### **Purpose (Mandatory — do not skip)**

- Adjusts space between characters
    
- Does not change word boundaries
    
- Can harm readability
    

### **Method**

```css
letter-spacing: <length>;
```

### **Correct usage**

```css
h2 {
  letter-spacing: 0.05em;
}
```

### **Observed output**

```text
Letters appear slightly spaced.
```

### **Common pitfalls**

- ❌ Over-spacing body text
    
- ❌ Using negative values blindly
    

### **Failure example**

```css
p {
  letter-spacing: 2px;
}
```

**Failure:** text becomes hard to read

### **Correct alternative**

```css
p {
  letter-spacing: normal;
}
```

### **Observed output**

```text
Text readability restored.
```

---

## 🚨 Conceptual Pitfalls (Very Important)

- ❌ `text-align` centers blocks
    
- ✅ It centers **inline content only**
    
- ❌ `text-transform` modifies data
    
- ✅ It is **visual-only**
    

---

## 🧠 Mental Model (Exam + Design)

- Text properties affect **glyph rendering**
    
- Guarantees:
    
    - No layout restructuring
        
- Undefined:
    
    - Font availability
        
- Rules live in:
    
    - CSS Fonts & Text specs
        
    - Text shaping engine
        

---

## 📌 Summary Table

|Property|Purpose|Common Pitfall|
|---|---|---|
|font-family|Typeface selection|Missing fallback|
|font-size|Text scale|Fixed px|
|font-weight|Boldness|Unsupported weights|
|font-style|Italic/slant|Synthetic oblique|
|text-align|Inline alignment|Block centering|
|text-decoration|Lines|Removing affordance|
|text-transform|Case|Data confusion|
|line-height|Vertical spacing|px misuse|
|letter-spacing|Char spacing|Overuse|

---

## ✅ Golden Rule

Text properties **change appearance, not structure**.  
If layout shifts, you’re using the **wrong category of CSS**.

**Next topic:** Lists & Tables