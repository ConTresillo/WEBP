# 🟠 HTML — Media (`<audio>`, `<video>`, `<source>`, Fallback Content) — Methods, Pitfalls, Fixes

> `HTML Media Elements` define **time-based audio and video playback** with native controls, decoding, buffering, and accessibility semantics; they embed **media content**, not custom players by default.

---

---

## 1️⃣ `<audio>` — Audio Playback Element

### **Purpose (Mandatory — do not skip)**

- Embeds **audio-only media**
    
- Handles loading, decoding, buffering, playback
    
- May expose native controls
    
- **Inline**, **finite**, **eager or lazy (browser-defined)**
    

---

### **Method**

```html
<audio src="file.mp3"></audio>
```

---

### **Correct usage**

```html
<audio controls>
  <source src="song.mp3" type="audio/mpeg">
</audio>
```

---

### **Observed output**

```text
Audio player with play/pause controls
```

---

### **Common pitfalls**

- ❌ Omitting `controls` (no user interaction)
    
- ❌ Assuming autoplay works everywhere
    
- ❌ Relying on a single audio format
    

---

### **Failure example**

```html
<audio src="song.mp3"></audio>
```

**Failure:**  
Audio is not controllable by the user

---

### **Correct alternative**

```html
<audio controls src="song.mp3"></audio>
```

---

### **Observed output**

```text
User-controllable audio playback
```

---

## 2️⃣ `<video>` — Video Playback Element

### **Purpose (Mandatory — do not skip)**

- Embeds **audio–visual media**
    
- Provides native playback UI
    
- Supports captions, tracks, fullscreen
    
- **Block-level**, **finite**, **eager or lazy**
    

---

### **Method**

```html
<video src="file.mp4"></video>
```

---

### **Correct usage**

```html
<video controls width="400">
  <source src="movie.mp4" type="video/mp4">
</video>
```

---

### **Observed output**

```text
Video player with playback controls
```

---

### **Common pitfalls**

- ❌ Missing `controls`
    
- ❌ Hardcoding unsupported codecs
    
- ❌ Assuming autoplay with sound
    

---

### **Failure example**

```html
<video autoplay src="movie.mp4"></video>
```

**Failure:**  
Autoplay blocked (especially with audio)

---

### **Correct alternative**

```html
<video autoplay muted src="movie.mp4"></video>
```

---

### **Observed output**

```text
Muted autoplay allowed
```

---

## 3️⃣ `<source>` — Media Source Declaration

### **Purpose (Mandatory — do not skip)**

- Declares **alternative media sources**
    
- Enables browser to select compatible format
    
- Order matters (first supported wins)
    
- **Declarative**, **finite**
    

---

### **Method**

```html
<source src="file.ext" type="mime/type">
```

---

### **Correct usage**

```html
<video controls>
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
</video>
```

---

### **Observed output**

```text
Best supported format selected
```

---

### **Common pitfalls**

- ❌ Missing `type` attribute
    
- ❌ Assuming fallback without `<source>`
    
- ❌ Incorrect MIME types
    

---

### **Failure example**

```html
<source src="video.xyz">
```

**Failure:**  
Browser may skip unsupported format

---

### **Correct alternative**

```html
<source src="video.mp4" type="video/mp4">
```

---

### **Observed output**

```text
Media loads correctly
```

---

## 4️⃣ Fallback Content — Unsupported Media Handling

### **Purpose (Mandatory — do not skip)**

- Provides **content shown when media cannot play**
    
- Ensures graceful degradation
    
- Displayed only if element unsupported
    
- **Static**, **conditional**
    

---

### **Method**

```html
<audio>Fallback text</audio>
```

---

### **Correct usage**

```html
<video controls>
  <source src="movie.mp4" type="video/mp4">
  Your browser does not support HTML video.
</video>
```

---

### **Observed output**

```text
Fallback message displayed if unsupported
```

---

### **Common pitfalls**

- ❌ Assuming fallback shows on load failure
    
- ❌ Placing fallback outside media element
    

---

### **Failure example**

```html
<video src="x.mp4"></video>
<p>No support</p>
```

**Failure:**  
Fallback never triggered

---

### **Correct alternative**

```html
<video>
  No video support
</video>
```

---

### **Observed output**

```text
Fallback correctly associated
```

---

## 5️⃣ Media Attributes — Playback Control

### **Purpose (Mandatory — do not skip)**

- Modify **loading, playback, and UX behavior**
    
- Affect buffering and policy compliance
    
- Declarative hints to browser
    
- **Evaluated at runtime**
    

---

### **Method**

```html
controls
autoplay
muted
loop
preload
```

---

### **Correct usage**

```html
<audio controls loop preload="metadata"></audio>
```

---

### **Observed output**

```text
Looping audio with metadata preloaded
```

---

### **Common pitfalls**

- ❌ Expecting `autoplay` without `muted`
    
- ❌ Overusing `preload="auto"`
    
- ❌ Ignoring user preferences
    

---

### **Failure example**

```html
<audio autoplay src="a.mp3"></audio>
```

**Failure:**  
Autoplay blocked

---

### **Correct alternative**

```html
<audio autoplay muted src="a.mp3"></audio>
```

---

### **Observed output**

```text
Autoplay succeeds silently
```

---

## 🚨 Conceptual Pitfalls (Very Important)

❌ **Media = decoration**

```html
<video autoplay loop></video>
```

```text
Unexpected behavior
```

✅ Media is **interactive content**, not background

---

❌ **Autoplay assumptions**

```html
<audio autoplay></audio>
```

```text
Blocked by browser
```

✅ Respect autoplay policies

---

❌ **Single-format dependency**

```html
<video src="video.avi"></video>
```

```text
May not play
```

✅ Always provide compatible formats

---

## 🧠 Mental Model (Exam + Design)

- `<audio>` / `<video>` manage **media lifecycle**
    
- `<source>` enables format negotiation
    
- Browsers enforce **user-centric policies**
    
- Fallback ensures resilience
    
- Controls expose native accessibility
    
- Custom players require JS, not HTML alone
    

---

## 📌 Summary Table

|Element|Purpose|Common Pitfall|
|---|---|---|
|`<audio>`|Audio playback|No controls|
|`<video>`|Video playback|Autoplay blocked|
|`<source>`|Format choice|Missing type|
|Fallback|Graceful failure|Misplaced text|
|Media attrs|Playback hints|Policy violation|

---

## ✅ Golden Rule

Media elements **serve users, not developers**.  
If playback surprises the user or breaks without controls, the implementation is wrong.