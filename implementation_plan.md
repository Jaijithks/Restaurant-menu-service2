# Implementation Plan - Ochre & Ember Restaurant Menu Website

Build a premium, mobile-first website for "Ochre & Ember" featuring a smooth storefront-to-menu zoom scroll animation, an interactive search/filter menu matching the end animation frame, a contact section, and automated PDF export of the implementation plan.

## User Review Required

> [!IMPORTANT]
> **Performance Optimization**: Preloading 120 high-quality frames (`000.webp` to `119.webp`, totaling ~96MB) on mobile devices can be slow. To ensure a premium, lag-free user experience, I will implement a custom preloader showing a premium gold loading screen with a progress percentage. Once the frames are fully loaded, the site will transition smoothly.

> [!NOTE]
> **Typography and Color Palette**: I will load `Cormorant Garamond` (a serif typeface for headings matching the classic logo) and `Inter` (for readable, modern body copy) from Google Fonts. The styling will use a refined color palette of deep blacks, soft warm cream backgrounds, and gold accents.

## Open Questions

- **Menu Data**: The final frame of the animation sequence shows three Mandi dishes. To make the categories (All, Mandi, Al-farm, Biriyani, Drinks, Noodles, Fried Rice, Others) fully interactive, I will add high-quality dummy items for the other categories. Please let me know if you would prefer different dishes.

---

## Proposed Changes

### Configuration & Layout

#### [MODIFY] [layout.tsx](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/app/layout.tsx)
- Load Google Fonts (`Cormorant Garamond` and `Inter`) using Next.js Google Fonts optimization.
- Set up global meta titles, description, and mobile-friendly viewport configurations.

#### [MODIFY] [globals.css](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/app/globals.css)
- Define CSS custom properties for colors (backgrounds, text, gold, highlights).
- Set up utilities for smooth scroll, premium animations, custom styling for the rounded inputs and pills.

---

### Home Page & Components

#### [NEW] [components/Preloader.tsx](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/components/Preloader.tsx)
- Premium dark fullscreen loader.
- Displays "Ochre & Ember" logo and a gold circular loading percentage.
- Preloads all 120 frames in the background, updating the loading percentage dynamically.
- Triggers a callback to hide the loader once all assets are cached in memory.

#### [NEW] [components/Hero.tsx](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/components/Hero.tsx)
- Display welcoming page with "Ochre & Ember".
- Background using `/background_hero.jpeg` set to absolute center with overlay.
- Features a subtle pulsing arrow instructing the user to scroll down to explore.

#### [NEW] [components/ScrollAnimation.tsx](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/components/ScrollAnimation.tsx)
- Render canvas-based scroll sequence.
- Tracks page scroll percentage inside a `400vh` height container.
- Uses `requestAnimationFrame` to draw the corresponding frame (`000.webp` to `119.webp`) on a sticky high-DPI `<canvas>`.
- Smoothly fades in the interactive HTML menu UI when the scroll reaches the end frame.

#### [NEW] [components/InteractiveMenu.tsx](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/components/InteractiveMenu.tsx)
- Interactive menu UI replicating the layout of `119.webp`:
  - **Header**: "OUR EXQUISITE MENU" and subtitle in serif typography.
  - **Search Input**: Fully functional input box to search dishes.
  - **Category Filter**: Clickable pills that dynamically filter dishes with slick animation.
  - **Menu List**: Cards displaying name, description, rating badge, price, and tags (Best Seller, Chef's Special) matching the image exactly.
- Beautiful HSL cream background matching the final frames.

#### [NEW] [components/ContactSection.tsx](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/components/ContactSection.tsx)
- Elegant restaurant contact card.
- Location, Opening/Closing times (9:00 AM - 10:00 PM), phone number.
- Soft shadow container, map placeholder, links to dial/navigate.

#### [MODIFY] [page.tsx](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/src/app/page.tsx)
- Assemble components: `Preloader` -> `Hero` -> `ScrollAnimation` -> `InteractiveMenu` -> `ContactSection` -> `Footer`.
- Manage global animation/interaction state.

---

### PDF & Logging Scripts

#### [NEW] [scripts/generate-pdf.js](file:///c:/test%20projects/websites%20i%20build/Restauarant-menu-2/my-app/scripts/generate-pdf.js)
- A Node.js script using `pdfkit` to write a professionally formatted PDF copy of this implementation plan directly to `public/implementation_plan.pdf`.
- Can be run with `node scripts/generate-pdf.js`.

---

## Verification Plan

### Automated Tests
- Run `npm run build` to verify standard build compilation and check for TypeScript errors.
- Run `node scripts/generate-pdf.js` to ensure the PDF generated is readable and matches the implementation plan.

### Manual Verification
- **Preloading & Animation**: Open the site, verify the preloading screen animates to 100%, and fades out. Check that scrolling down runs the storefront-to-menu canvas animation at a smooth 60fps on mobile sizes.
- **Visual Accuracy**: Verify the HTML menu looks identical to frame `119.webp` in typography, colors, and layout.
- **Interactivity**: Search for "Chicken" or "Mutton" in the search box, verify matching items remain, and others disappear. Click different category pills and verify that the items animate gracefully.
- **Contact Details**: Ensure location, hours of opening (9:00 AM to 10:00 PM), and phone details are legible and buttons are clickable.
- **Log Verification**: Verify that `GEMINI.md` in the root workspace has accurate logs of steps completed.
