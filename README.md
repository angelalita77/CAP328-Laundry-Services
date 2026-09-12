# Laundry Services Website - Capstone Project


## Capstone Project Checklist

Use this interactive markdown checklist to track your progress as you complete each requirement for your capstone submission.

---
A web application built using HTML5, CSS3, JavaScript (ES6+), and modern CSS frameworks.

## 🛠️ Tech Stack & Badges

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)<br>

# 🧺 Fores Laundry Service — Website

A responsive, multi-page website for a fictional laundry service, built from scratch with HTML, CSS, and JavaScript as a front-end fundamentals portfolio project.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Status](https://img.shields.io/badge/status-in%20progress-yellow)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Technical Deep Dive](#technical-deep-dive)
  - [JavaScript DOM Selectors](#1-javascript-dom-selectors)
  - [DRY Principle](#2-dry-principle-dont-repeat-yourself)
  - [CSS Root Colors](#3-css-root-colors-css-variables)
  - [Navigation](#4-navigation)
- [Roadmap](#roadmap)
- [Author](#author)

---

## Overview

**Fores** is a fictional laundry service, and this repo is its marketing homepage. The site introduces the business with a hero section, highlights three core info areas (Services, Hours & Pricing, and Location) in a card layout, and includes a fully responsive navigation bar with a mobile hamburger menu.

This project was built to practice core front-end fundamentals — semantic HTML structure, maintainable CSS architecture (custom properties, reusable classes), and vanilla JavaScript DOM manipulation — without relying on any frameworks or libraries.

## Features

- 🖼️ Hero section with headline, description, and dual call-to-action buttons
- 🗂️ Three-card info grid (Services / Hours & Pricing / Location)
- 🧭 Responsive top navigation with active-link highlighting
- 📱 Mobile hamburger menu powered by vanilla JavaScript
- 🎨 Centralized color system via CSS custom properties for easy re-theming
- 🔘 Consistent, reusable button styles (filled + outlined variants)
- 📄 Footer with business contact info and hours

## Tech Stack

| Layer | Technology |
|---|---|
| Structure | HTML5 |
| Styling | CSS3 (custom properties, Flexbox, media queries) |
| Interactivity | Vanilla JavaScript (DOM API) |
| Fonts | Google Fonts (Lexend, Lora, Source Sans 3) |

No frameworks, build tools, or dependencies — the project runs directly in the browser.

## Project Structure

```
fores-laundry/
├── index.html          # Homepage (hero, info cards, nav, footer)
├── services.html        # Services page (linked from nav)
├── hours-pricing.html   # Hours & Pricing page (linked from nav)
├── style.css            # All site-wide styles, incl. :root color variables
└── script.js             # Mobile menu toggle logic
```

## Getting Started

No build step or dependencies required.

1. Clone the repo:
   ```bash
   git clone https://github.com/your-username/fores-laundry.git
   ```
2. Open `index.html` directly in your browser, **or** serve it locally:
   ```bash
   npx serve .
   ```
3. Resize your browser window below 768px to see the responsive mobile menu in action.

## Technical Deep Dive

This section highlights four key implementation decisions and the reasoning behind them.

### 1. JavaScript DOM Selectors

All interactivity lives in `script.js` (3 lines total). It uses `querySelector()` to grab elements and `addEventListener()` to react to a click:

```javascript
const burger = document.querySelector('.menu-toggle');   // grabs the hamburger button
const menu = document.querySelector('.nav-links');        // grabs the nav link list
burger.addEventListener('click', () => {
    menu.classList.toggle('open');                          // shows/hides the mobile menu
});
```

- `querySelector('.menu-toggle')` targets the `<button class="menu-toggle">` in `index.html`.
- `querySelector('.nav-links')` targets the `<ul class="nav-links">` holding all page links.
- `addEventListener('click', ...)` waits for a tap/click on the button.
- `classList.toggle('open')` is the actual action — it adds the `open` class if missing, removes it if present. The `.nav-links.open` rule in `style.css` (inside the `@media (max-width: 768px)` block) is what makes the menu visible, so toggling this one class is what drives the whole mobile menu behavior.

### 2. DRY Principle (Don't Repeat Yourself)

**Reusable button classes** (`style.css`, ~lines 34–60): every button shares a base `.btn` class for shape (padding, border-radius, font-weight), then a modifier class (`.btn-filled` or `.btn-empty`) adds only the color:

```css
.btn {
    text-decoration: none;
    font-weight: bold;
    border: 2px black;
    border-radius: 6px;
    padding: 12px 24px;
}

.btn-filled {
    background-color: var(--btn-color);
    color: white;
}
```

Any element becomes a matching button just by combining `class="btn btn-filled"` in HTML — no need to write a new style block per button. If the button shape changes, it's a one-line edit instead of a site-wide find-and-replace.

**One shared rule for all nav links**: instead of styling each `<li><a>` individually, a single `.nav-links a` rule (`style.css`, ~lines 79–83) applies the same color, padding, and hover effect to every link at once. Adding a new nav link automatically inherits the same styling.

### 3. CSS Root Colors (CSS Variables)

All colors and a key layout value are defined once in a `:root` block (`style.css`, lines 9–21):

```css
:root {
    --cream-main-bkgd: #faf7f2;
    --nav-color: #ffffff;
    --ink: #1c1a17;
    --accent: #3581ce;
    --accent-light: #eaf2fc;
    --btn-color: #3581cf;
    --btn-color-hover: #29659e;
    --nav-height: 68px;
}
```

These are reused throughout the stylesheet, e.g.:

```css
body {
    background-color: var(--cream-main-bkgd);
}

.nav-links a:hover {
    color: var(--accent);
    background-color: var(--accent-light);
}
```

**Why it matters:** the accent blue (`#3581ce`) appears in multiple selectors. Hardcoding it everywhere risks inconsistency and makes rebranding painful. With `--accent` defined once, updating the brand color is a single-line change that propagates instantly across the entire site.

### 4. Navigation

**Structure** (`index.html`, `<nav>` element): a logo link, an unordered list of page links, and a hamburger button for mobile:

```html
<nav>
    <div class="inner-nav">
        <a href="index.html" class="nav-logo">LOGO</a>
        <ul class="nav-links">
            <li><a href="index.html">Home</a></li>
            <li><a href="services.html">Services</a></li>
            <li><a href="hours-pricing.html">Hours & Pricing</a></li>
        </ul>
        <button class="menu-toggle">
            <span class="bar"></span>
            <span class="bar"></span>
            <span class="bar"></span>
        </button>
    </div>
</nav>
```

- **Page-to-page navigation** happens via standard `href` links (`services.html`, `hours-pricing.html`, etc.), plus shortcut buttons in the hero section styled with the same `.btn` classes.
- **Active link highlighting**: the `.active` class (`style.css`, ~lines 100–105) shades whichever link matches the current page.
- **Mobile menu toggle**: the `@media (max-width: 768px)` rule (`style.css`, ~lines 121–140) hides nav links and shows the hamburger; the JavaScript in Section 1 handles opening/closing it. CSS defines *what* the mobile menu looks like — JS controls *when* it appears.

## Roadmap

- [ ] Build out Contact and Testimonials pages (currently placeholder `#` links)
- [ ] Add form validation for a contact form
- [ ] Replace inline hero image URL with a local, optimized asset
- [ ] Add automated active-link highlighting via JavaScript instead of manual class placement

## Author

Built by Jeanette as a front-end fundamentals portfolio project.
