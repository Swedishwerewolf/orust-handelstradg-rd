# Design Rationale: Orust Handelsträdgård

This document outlines the architectural and design decisions made to address every specific constraint and web design feature from the checklist.

### 1. Overall Arrangement of Elements (Layout)
The layout relies on a clear, single-page, vertically scrolling hierarchy. It begins with a sticky header containing the logo and language toggle. The page flows linearly: Hero (brand introduction) ➔ Gallery ➔ Carousel (products/seasons) ➔ Empty State (events) ➔ Video (ambience) ➔ FAQ ➔ Contact ➔ Footer. I utilized a mobile-first responsive approach but ensured a robust desktop grid (`max-width: 1440px`), relying on CSS Grid (`grid-template-columns: repeat(auto-fit...)`) for the gallery and FAQ to guarantee fluid adaptation across breakpoints.

### 2. Background and Foreground Relationships (Visual Composition)
To ensure accessibility and contrast, the color palette draws heavily from the uploaded logo image. I utilized a deep forest green (`#193f2c`) paired with gold (`#c4a775`) on a warm off-white background (`#fdfbf7`). Shadows (`box-shadow`) and blending modes (`mix-blend-mode: multiply`) are used in the hero section to isolate the bright typography from the dark, rich photographic background layers.

### 3. Scroll Behavior and Interactions (Depth Parallax)
**Parallax depth effects were marked as a MUST.** Instead of standard, often buggy, CSS 3D transforms (`perspective`), I implemented a high-performance JavaScript-driven depth parallax. The hero section contains three layers:
* A background image (slower, `data-speed="0.5"`)
* A midground botanical overlay (`data-speed="0.2"`)
* Foreground typography (moves upward slightly faster, `data-speed="-0.15"`)
This creates a distinct 3D depth field that dynamically reacts as the user scrolls, creating an immersive, premium feel.

### 4. Transitions and Animations
All interactive elements (buttons, image hovers, language dropdown) use a global CSS variable (`--transition-smooth: all 0.4s cubic-bezier(...)`). The gallery features a subtle `.gallery-item:hover img { transform: scale(1.08); }` to reward user exploration without overwhelming the senses. The "Back to Top" button fades and slides in smoothly once the user scrolls past 400px.

### 5. Motion Design (Content Entering/Leaving)
Motion is constrained to essential user actions. I avoided heavy scroll-trigger entry animations for performance and accessibility (respecting users who prefer reduced motion). Instead, horizontal motion is delegated to the Carousel scroll area via CSS `scroll-snap-type`. Language switching happens instantaneously via DOM manipulation to avoid layout shift.

### 6. Fixed Elements vs. Scrolling Content
The **Header** and **Back-to-Top Button** are fixed (`position: fixed`). 
* *Rationale:* A sticky header keeps the brand identity (logo) and the primary utility (language selection dropdown) accessible at all times. To prevent the header from breaking the visual flow, it utilizes a semi-transparent background with `backdrop-filter: blur(10px)`.

### 7. Visual Design & Typography
The site employs two Google Fonts: **Playfair Display** (a classic serif that closely matches the botanical, heritage aesthetic of the provided logo) and **Lato** (a clean, legible sans-serif for paragraph text). The aesthetic is rooted in Scandinavian nature—minimalistic spacing, large photographic areas, and earthy tones.

### 8. Checklist Features Addressed
* **Header, Logo, Footer, Contact:** Built semantically (`<header>`, `<footer>`, `<section>`).
* **Language Selection & Dropdown Menu:** Implemented via a custom JSON dictionary in JavaScript, toggled by a CSS hover dropdown in the header.
* **Image Gallery & Image Carousel:** Gallery uses CSS Grid; Carousel is a touch-friendly CSS flex container utilizing `overflow-x: auto` (Scroll Areas).
* **Empty States:** An "Upcoming Events" section actively utilizes an "Empty State" design pattern (dashed border, muted text/icon) as requested.
* **Video Section:** Standard HTML5 `<video>` tag integrated smoothly with auto-play background capabilities. 
* **FAQ Section:** Structured clearly as an information grid (H3 / P) rather than Accordions (as Accordion was unchecked).
