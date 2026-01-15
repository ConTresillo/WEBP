# 🟠 HTML — Images (`<img>`)

> `<img>` is a **void, replaced element** that embeds an **external image resource** into the document; it contributes **content**, not decoration, and participates in layout as a single atomic box.

---

---

## 5️⃣ `<img>` — Image Element

### **Purpose (Mandatory — do not skip)**

- Embeds an **image resource** into the page
    
- Image data is fetched **externally** via URL
    
- Element has **no closing tag**
    
- **Eager by default**, **finite**, **non-container**
    
- Always participates in layout, even if image fails
    

---

### **Method**

```html
<img src="URL" alt="text">
```

---

### **Correct usage**

```html
<img src="photo.jpg" alt="A sunset over the sea">
```

---

### **Observed output**

```text
Image rendered; alt text available to screen readers
```

---

### **Common pitfalls**

- ❌ Missing `alt`
    
- ❌ Treating `<img>` as decorative by default
    
- ❌ Assuming image size equals file size
    
- ❌ Forgetting broken-image behavior
    

---

### **Failure example**

```html
<img src="photo.jpg">
```

**Failure:**  
Accessibility violation (missing alternative text)

---

### **Correct alternative**

```html
<img src="photo.jpg" alt="A sunset over the sea">
```

---

### **Observed output**

```text
Accessible image with fallback text
```

---

## 6️⃣ `src`

### **Purpose (Mandatory — do not skip)**

- Specifies the **image resource URL**
    
- Required for image loading
    
- Can be **relative, absolute, or data URL**
    

---

### **Method**

```html
<img src="path-or-url">
```

---

### **Correct usage**

```html
<img src="/images/logo.png" alt="Company logo">
```

---

### **Observed output**

```text
Image fetched and displayed
```

---

### **Common pitfalls**

- ❌ Invalid path
    
- ❌ Assuming browser errors are visible
    
- ❌ Using large images without optimization
    

---

### **Failure example**

```html
<img src="missing.png" alt="Logo">
```

**Failure:**  
Broken image icon shown

---

### **Correct alternative**

```html
<img src="logo.png" alt="Logo">
```

---

### **Observed output**

```text
Logo image rendered
```

---

## 7️⃣ `alt`

### **Purpose (Mandatory — do not skip)**

- Provides **text alternative** for the image
    
- Used by **screen readers**
    
- Displayed when image fails to load
    
- Mandatory for **meaningful images**
    

---

### **Method**

```html
<img alt="description">
```

---

### **Correct usage**

```html
<img src="chart.png" alt="Bar chart showing sales growth">
```

---

### **Observed output**

```text
Chart described to assistive technologies
```

---

### **Common pitfalls**

- ❌ Leaving `alt` empty for meaningful images
    
- ❌ Stuffing keywords
    
- ❌ Repeating surrounding text
    

---

### **Failure example**

```html
<img src="chart.png" alt="">
```

**Failure:**  
Loss of information for non-visual users

---

### **Correct alternative**

```html
<img src="chart.png" alt="Quarterly sales increased by 20%">
```

---

### **Observed output**

```text
Information preserved without image
```

---

## 8️⃣ `width` and `height`

### **Purpose (Mandatory — do not skip)**

- Define **intrinsic display dimensions**
    
- Reserve layout space **before image loads**
    
- Reduce layout shift (CLS)
    
- Values are in **CSS pixels**
    

---

### **Method**

```html
<img src="x" alt="y" width="300" height="200">
```

---

### **Correct usage**

```html
<img src="photo.jpg" alt="Landscape" width="600" height="400">
```

---

### **Observed output**

```text
Image rendered with reserved layout space
```

---

### **Common pitfalls**

- ❌ Omitting dimensions
    
- ❌ Assuming they resize the file
    
- ❌ Distorting aspect ratio
    

---

### **Failure example**

```html
<img src="photo.jpg" alt="Landscape" width="600">
```

**Failure:**  
Layout shift during load

---

### **Correct alternative**

```html
<img src="photo.jpg" alt="Landscape" width="600" height="400">
```

---

### **Observed output**

```text
Stable layout
```

---

## 9️⃣ `loading`

### **Purpose (Mandatory — do not skip)**

- Controls **lazy vs eager loading**
    
- Optimizes performance
    
- Browser hint, not a guarantee
    

---

### **Method**

```html
<img loading="lazy|eager">
```

---

### **Correct usage**

```html
<img src="gallery.jpg" alt="Gallery image" loading="lazy">
```

---

### **Observed output**

```text
Image loads when near viewport
```

---

### **Common pitfalls**

- ❌ Using lazy loading for above-the-fold images
    
- ❌ Assuming deterministic behavior
    

---

### **Failure example**

```html
<img src="hero.jpg" alt="Hero" loading="lazy">
```

**Failure:**  
Perceived slow load of main content

---

### **Correct alternative**

```html
<img src="hero.jpg" alt="Hero" loading="eager">
```

---

### **Observed output**

```text
Hero image loads immediately
```

---

## 🔟 `title`

### **Purpose (Mandatory — do not skip)**

- Provides **supplementary tooltip text**
    
- Not a replacement for `alt`
    
- Often ignored on touch devices
    

---

### **Method**

```html
<img title="text">
```

---

### **Correct usage**

```html
<img src="map.png" alt="World map" title="Political boundaries">
```

---

### **Observed output**

```text
Tooltip shown on hover (desktop)
```

---

### **Common pitfalls**

- ❌ Using `title` instead of `alt`
    
- ❌ Relying on it for accessibility
    

---

### **Failure example**

```html
<img src="map.png" title="World map">
```

**Failure:**  
Screen readers lack description

---

### **Correct alternative**

```html
<img src="map.png" alt="World map showing continents">
```

---

### **Observed output**

```text
Accessible description provided
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **`<img>` vs CSS background-image**

```html
<div style="background-image:url(x.png)"></div>
```

```text
No semantic image content
```

✅ Use `<img>` for **content**, CSS backgrounds for **decoration**

---

❌ **Missing dimensions**

```html
<img src="large.jpg" alt="Image">
```

```text
Layout jumps during load
```

✅ Always specify `width` and `height`

---

❌ **Decorative images with alt text**

```html
<img src="divider.png" alt="decorative line">
```

```text
Noise for screen readers
```

✅ Use empty alt for decoration

```html
<img src="divider.png" alt="">
```

---

## 🧠 Mental Model (Exam + Design)

- `<img>` embeds **external content**
    
- `src` defines resource identity
    
- `alt` defines **meaning when image is unavailable**
    
- Dimensions stabilize layout
    
- Loading behavior is **hint-based**
    
- Accessibility rules are **non-optional**
    

---

## 📌 Summary Table

|Attribute|Purpose|Common Pitfall|
|---|---|---|
|`src`|Image URL|Broken path|
|`alt`|Text alternative|Missing or empty|
|`width/height`|Layout size|Layout shift|
|`loading`|Performance hint|Lazy hero image|
|`title`|Tooltip|Used as alt|

---

## ✅ Golden Rule

If removing the image loses information,  
that information **must exist in `alt`**.

## QnA
### ❓ Is it possible to have a fallback image in HTML?

**Yes — but not automatically via HTML attributes.**  
HTML allows image fallbacks only through **two specific mechanisms**, each with clear limitations.

---

### ❓ How does a JavaScript-based image fallback work?

**It listens for image load failure and swaps the source.**

- Triggered when the image **fails to load**
    
- Uses the `error` event on `<img>`
    
- Deterministic and widely supported
    

```html
<img
  src="primary.jpg"
  alt="Profile photo"
  onerror="this.onerror=null; this.src='fallback.jpg';"
/>
```

**Runtime behavior**

```text
If primary.jpg fails → fallback.jpg is loaded
```

**Constraints**

- Requires JavaScript
    
- Must prevent infinite loops (`this.onerror = null`)
    
- Works for same-origin and cross-origin images
    

---

### ❓ Can `<picture>` be used as a fallback mechanism?

**Yes — but only for format or capability fallback, not failures.**

- Browser selects the **first supported source**
    
- Designed for **responsive images and format support**
    
- Not triggered by broken URLs or network errors
    

```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Landscape">
</picture>
```

**Runtime behavior**

```text
Browser picks first supported format
Falls back to <img> if none match
```

**Constraints**

- ❌ Does NOT handle broken URLs
    
- ❌ Does NOT react to network failures
    
- ✅ Handles format support only
    

---

### ❓ Is there a native HTML attribute for image fallback?

**No. HTML does not provide such an attribute.**

```html
<img src="a.jpg" fallback="b.jpg">
```

```text
Ignored — no such attribute exists
```

---

### ❓ What role does `alt` play in fallback behavior?

**`alt` is a text fallback, not an image fallback.**

- Used by screen readers
    
- Shown when images fail
    
- Does not load another image
    

---

### ❓ What are the key differences between the fallback approaches?

- `<picture>` → **capability-based fallback**
    
- `onerror` → **failure-based fallback**
    
- `alt` → **text fallback only**
    

---

### ❓ What is the correct conclusion (interview-ready)?

- **Yes**, fallback images are possible
    
- **No**, HTML alone cannot express “try another image if this fails”
    
- **JavaScript is required** for true runtime image fallback
    

**Interview trap to remember:**  
HTML has **no native image-fallback attribute**.