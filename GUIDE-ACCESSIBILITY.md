# Accessibility Best Practices Guide

## Centre des Loisirs de Fatima

This document explains the accessibility improvements that have been implemented and how to maintain accessibility when adding new content.

> **French version:** [GUIDE-ACCESSIBILITE.md](GUIDE-ACCESSIBILITE.md)

## ✅ Implemented Improvements

### 1. **Custom Accessibility CSS**

File: `assets/scss/accessibility-improvements.scss`

**Features added:**

- Enhanced focus indicators (3px outline)
- Improved color contrast (text #1a1a1a on white background)
- Minimum click/touch target size of 44×44 pixels
- User preference support (reduced motion, high contrast)
- Accessible form styles
- Improved readability (line height, spacing)

### 2. **Semantic HTML Structure**

- Changed `<section id="content">` to `<main id="content">`
- Proper use of `<header>`, `<nav>`, `<article>`, `<footer>`
- "Skip to content" link already in place
- Semantic `<h2>` headings for event sections (previously styled `<span>` and `<div>` elements)
- `<h3>` heading for each board member's name (previously `<p>` elements)

### 3. **Keyboard Navigation**

- All interactive elements are keyboard accessible
- Visible focus indicators
- Logical tab order

### 4. **Color Contrast**

- Contrast ratios meeting WCAG 2.1 AA (minimum 4.5:1)
- Underlined links for better visibility
- Primary colors adjusted for better contrast

### 5. **ARIA Attributes**

- **Mobile menu**: the hamburger button exposes its open/closed state via `aria-expanded` (toggled in JavaScript on each click)
- **Navigation bar**: `<nav>` carries a bilingual `aria-label` ("Main navigation" / "Navigation principale") to distinguish navigation landmarks
- **Carousel**: marked as a region (`role="region"`) with `aria-label`; an `aria-live="polite"` zone announces the active slide to screen readers; the active dot button receives `aria-current="true"`
- **Callout blocks**: `warning`/`danger` callouts use `role="alert"`, all others use `role="note"`
- **Forms**: all required fields carry `aria-required="true"` in addition to the HTML `required` attribute
- **Board member photos**: alt text includes the person's title (e.g., `alt="Guillaume Prince, Président du CA"`)
- **Ticketing links**: `aria-label` indicates the link opens in a new tab

### 6. **Correct Use of `aria-hidden`**

- `aria-hidden="true"` is reserved for elements truly hidden from assistive technologies (decorative SVG icons, etc.)
- Purely visual spacing `<div>` elements no longer use `aria-hidden` — spacing is handled by CSS

---

## 📝 Content Best Practices

### Images

Always add descriptive alternative text:

```markdown
![Description of the image](path/to/image.jpg)
```

**Good example:**

```markdown
![Group of children playing soccer at Centre des Loisirs de Fatima](images/soccer-2024.jpg)
```

**Bad example:**

```markdown
![image](image.jpg)
```

For decorative images, use an empty alt:

```markdown
![ ](decoration.png)
```

### Links

Use explicit link text:

**Good:**

```markdown
[View our 2026 activity calendar](/activities/)
```

**Bad:**

```markdown
[Click here](/activities/)
```

When a link opens in a new tab, mention it in the text or aria-label:

**Good:**

```markdown
[Buy tickets (opens in new tab)](https://...)
```

### Headings

Respect heading hierarchy (do not skip levels):

```markdown
# Main title (H1) — Only one per page

## Section (H2)

### Sub-section (H3)

#### Sub-sub-section (H4)
```

### Tables

Always use column headers:

```markdown
| Name | Date | Location |
|------|------|----------|
| Bingo | March 15 | Main Hall |
```

### Lists

Use appropriate list types:

```markdown
<!-- Unordered list -->
- Item 1
- Item 2

<!-- Ordered list (when order matters) -->
1. First step
2. Second step
```

### Video content

If you add videos:

- Include captions
- Provide a text transcript
- Use the theme's YouTube shortcode, which is accessible

### Colors

- Never use color alone to convey information
- Example: "Click the green button" → "Click the Register button"

### Forms

Recommended structure:

```html
<label for="name">Name:</label>
<input type="text" id="name" name="name" required aria-required="true">

<label for="email">Email:</label>
<input type="email" id="email" name="email" required aria-required="true">
```

---

## 🔍 Accessibility Testing

### Manual tests to perform regularly

1. **Keyboard navigation**
   - Use only the Tab key
   - Verify all elements are reachable
   - Verify focus indicators are visible

2. **Zoom**
   - Test the site at 200% zoom
   - Verify no content is cut off
   - Verify everything remains functional

3. **Screen reader**
   - Windows: NVDA (free) or JAWS
   - Mac: VoiceOver (built-in)
   - Verify content is read in a logical order

### Recommended automated tools

1. **Browser extension: axe DevTools**
   - Automatic accessibility issue analysis
   - Free and easy to use

2. **WAVE Web Accessibility Evaluation Tool**
   - <https://wave.webaim.org/>
   - Visual display of accessibility issues

3. **W3C HTML Validator**
   - <https://validator.w3.org/>
   - Validates HTML correctness

4. **Contrast Checker**
   - <https://webaim.org/resources/contrastchecker/>
   - Verifies contrast ratios

---

## 🎯 Pre-publication Checklist

- [ ] All images have appropriate alternative text
- [ ] Links have descriptive text
- [ ] Heading hierarchy is respected
- [ ] Tables have headers
- [ ] Forms have labels and `aria-required` on required fields
- [ ] Color contrast is sufficient
- [ ] Content is readable at 200% zoom
- [ ] Page is keyboard navigable
- [ ] Videos have captions (if applicable)
- [ ] Links opening in a new tab are clearly identified

---

## 🔗 Useful Resources

- [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG21/)
- [Introduction to Web Accessibility](https://www.w3.org/WAI/fundamentals/accessibility-intro/)
- [Government of Canada Web Accessibility Guide](https://www.canada.ca/en/treasury-board-secretariat/services/government-communications/canada-content-information-architecture-specification/web-accessibility.html)

---

## 💡 Important Reminder

Accessibility is not a one-time task — it is an ongoing process. Every time you add content, think about people who use:

- Screen readers
- Keyboard-only navigation
- Screen magnification tools
- Various assistive technologies

**Question to ask yourself:** "If I couldn't use a mouse or see the screen, could I still access this information?"
