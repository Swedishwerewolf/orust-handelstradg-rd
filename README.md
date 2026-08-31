# Orust Handelsträdgård Website

A modern, responsive, and beautifully animated single-page website for "Orust Handelsträdgård".

## Setup Instructions
1. Save the `index.html` code block into a file named `index.html`.
2. Ensure the provided logo image is named `orust-logo.png.jpg` and sits in the same directory as the HTML file.
3. Open `index.html` in any modern web browser to view the final result.

---

## Design Rationale

**1. Overall arrangement of elements — layout** The site is built utilizing a mobile-first CSS logic, relying on modern `Flexbox` and `CSS Grid` properties for structured, fluid layouts. Elements flow naturally down the page: fixed header -> large welcoming hero -> video block -> horizontal scrolling carousel -> grid gallery -> empty states -> FAQ -> contact & footer. This logic creates a journey for the user rather than an overwhelming dump of information.

**2. Background and foreground relationships — visual composition** The color palette was directly inspired by the provided logo. The background is a soft beige (`#F4EFE6`), contrasted heavily by a deep green text/heading color (`#1b432d`). This creates an earthy, organic visual composition. The header utilizes `backdrop-filter: blur` to ensure the background naturally melts beneath it while scrolling, keeping the content readable without breaking immersion.

**3. How sections move or appear while scrolling — scroll behavior** Taking inspiration from *locomotive.ca*, an `IntersectionObserver` is heavily employed. Instead of using a heavy 3rd-party library that highjacks native scrolling (which often introduces accessibility issues), native CSS `scroll-behavior: smooth` is paired with JavaScript that watches elements enter the viewport.

**4. Elements that slide, expand, or roll out — transitions and animations** Interactive elements scale and color-shift on hover. The language dropdown features a CSS `@keyframes` fade/slide-up animation. The horizontal image carousel utilizes native CSS `scroll-snap` features to give users a native app-like swipe/drag feel on touch devices.

**5. How content enters or leaves the screen — motion design** Content enters utilizing a `.reveal` utility class. By default, these sections are nudged downward and have an opacity of 0. When JavaScript detects they are in the viewport, an `.is-visible` class is applied, firing a `1.2s cubic-bezier` transition that elegantly floats the content into place. `prefers-reduced-motion` is strictly respected in the CSS to disable this for sensitive users.

**6. Fixed elements versus scrolling content** The header and the "Back to top" button are fixed. The header provides quick access to the language toggle. The back-to-top button only appears after traversing 500px down the Y-axis to avoid cluttering the initial viewport.

**7. The overall visual appearance — visual design** The design communicates "Premium Garden Center". Google Fonts are imported specifically for this: *Cormorant Garamond* for beautiful, sophisticated serif headings, and *Inter* for highly legible UI and body text. Visual borders are softened with heavy `border-radius` variables (e.g., `20px` to `40px`), mimicking organic shapes rather than sharp tech-driven boxes. 

**8. Other relevant aspects** * **Accessibility:** Semantic tags (`<main>`, `<section>`, `<details>`, `<summary>`) are used. Elements feature `aria-labels` and `aria-expanded` toggles for screen readers. 
* **Localization (Checked Requirement):** A lightweight vanilla JS localization script dynamically targets `data-i18n` attributes. This avoids page reloads and instantly translates between English and Swedish. 
* **Empty States (Checked Requirement):** Designed as a dashed-border "Upcoming Events" placeholder, proving the component exists without feeling like broken UI. 
* **Video/Images:** Unsplash and Coverr CDN placeholders are utilized for royalty-free nature/garden imagery as requested.
