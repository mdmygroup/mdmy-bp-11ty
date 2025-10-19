# Overview

You are assisting in building static websites using Eleventy (11ty) with a modern enhancement stack.
Your goal is to write clean, semantic, production-ready front-end code.
The stack is: **Eleventy (11ty) + Nunjucks/Liquid Templates + Tailwind CSS + Alpine.js + AOS + Heroicons**.
Use Eleventy's templating features (layouts, includes, partials) for reusable components.
All front-end libraries remain CDN-ready for simplicity.
Each page should be fully responsive, accessible, and lightweight.

## General Style Guide

**Semantic HTML first** — layout and structure must remain clean and accessible.
Use Tailwind CSS utility classes for spacing, typography, colors, hover/focus states.
Introduce Alpine.js only for interactivity that cannot be handled with CSS alone (modals, toggles, dynamic forms).
Use AOS (Animate On Scroll) for scroll-triggered animations; fallback to Tailwind transitions for simple hover/appear effects.
Use Heroicons exclusively for all icon needs to maintain visual consistency.
Always use semantic HTML5 tags (header, nav, main, section, article, footer).
Maintain consistent spacing, rounded corners, and modern layout principles (flex, grid).
Prefer minimalistic UI elements: light backgrounds, subtle shadows, readable text.
Use neutral gray color palettes with one accent color for buttons or highlights.
Ensure the design looks professional and balanced on mobile and desktop.

## File Structure

**Eleventy-specific structure:**
- `_includes/` → layouts and partials (e.g., `base.njk`, `header.njk`, `footer.njk`)
- `index.njk` or `index.html` → main landing page
- `a-propos.njk`, `services.njk`, `contact.njk`, `realisations.njk` → content pages
- `assets/images/` → static images (use responsive variants: image-480.jpg, image-960.jpg, image-1920.jpg)
- `assets/css/` → custom CSS if needed (Tailwind CSS via CDN in base layout)
- `.eleventy.js` → Eleventy configuration file
- `_site/` → output directory (generated, not tracked in git)

Use Nunjucks (`.njk`) or Liquid templating for layouts and includes.
Leverage Eleventy's data cascade for site-wide variables (e.g., site title, navigation).

## Coding Guidelines

When generating Eleventy templates:

Create a base layout in `_includes/base.njk` with:
  - Minimal boilerplate using `<!DOCTYPE html>`
  - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
  - Required CDN libraries in the `<head>`:
    * Google Fonts API for typography
    * Tailwind CSS
    * Heroicons (if icons are needed)
    * AOS CSS
  - Alpine.js and AOS JavaScript before closing `</body>`
  - Dynamic `<title>` using front matter: `{{ title }}` or `{{ title | default: "Site Name" }}`
  - Comment key layout sections for readability

Create reusable components:
  - `_includes/header.njk` → site header and navigation
  - `_includes/footer.njk` → site footer
  - Use `{% include "header.njk" %}` or `{% include 'header.njk' %}` to embed partials

Use front matter in content pages:
```yaml
---
layout: base.njk
title: Page Title
permalink: /page-url/
---
```

Leverage Eleventy features:
  - Use `{{ content | safe }}` in layouts to render page content
  - Access data via `_data/` folder for site-wide configuration
  - Use collections for grouping related pages if needed

### Image Best Practices

Always use lazy loading: <img loading="lazy" ...>
Use responsive images with srcset and sizes:
  <img src="hero.jpg" srcset="hero-480.jpg 480w, hero-960.jpg 960w, hero-1920.jpg 1920w" 
       sizes="(max-width: 600px) 480px, (max-width: 1200px) 960px, 1920px" 
       alt="Descriptive text" loading="lazy">
Provide meaningful alt text for accessibility.

### Interactivity Guidelines

**CSS-first approach**: Use Tailwind utilities for hover, focus, group-hover, transitions.
**Alpine.js**: Only for dynamic behavior (dropdowns, modals, tabs, accordions, form validation).
  - Use x-data, x-show, x-if, x-on:click, x-transition sparingly.
**AOS**: For scroll animations — add data-aos="fade-up" or similar.
**Heroicons**: Use inline SVG icons from Heroicons for consistency.

Example Eleventy structure:

**_includes/base.njk** (Base Layout):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{{ title | default: "Company Name" }}</title>
  
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  
  <!-- Tailwind CSS -->
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@3.4.0/dist/tailwind.min.css" rel="stylesheet">
  
  <!-- AOS CSS -->
  <link href="https://unpkg.com/aos@2.3.4/dist/aos.css" rel="stylesheet">
  
  <style>
    body { font-family: 'Inter', sans-serif; }
  </style>
</head>
<body class="antialiased text-gray-800 bg-gray-50">
  
  {% include "header.njk" %}

  <!-- Main Content -->
  <main class="py-16 px-4">
    {{ content | safe }}
  </main>

  {% include "footer.njk" %}

  <!-- Alpine.js -->
  <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
  
  <!-- AOS JavaScript -->
  <script src="https://unpkg.com/aos@2.3.4/dist/aos.js"></script>
  <script>
    AOS.init({
      duration: 800,
      once: true,
      offset: 100
    });
  </script>

</body>
</html>
```

**_includes/header.njk** (Header Component):
```html
<header class="py-6 shadow-md bg-white">
  <div class="container mx-auto flex justify-between items-center px-4" x-data="{ mobileMenuOpen: false }">
    <h1 class="text-2xl font-bold">Company Name</h1>
    
    <!-- Desktop Navigation -->
    <nav class="hidden md:flex space-x-4 text-sm font-medium">
      <a href="/" class="hover:text-blue-600 transition">Accueil</a>
      <a href="/a-propos/" class="hover:text-blue-600 transition">À Propos</a>
      <a href="/services/" class="hover:text-blue-600 transition">Services</a>
      <a href="/realisations/" class="hover:text-blue-600 transition">Réalisations</a>
      <a href="/contact/" class="hover:text-blue-600 transition">Contact</a>
    </nav>
    
    <!-- Mobile Menu Button -->
    <button @click="mobileMenuOpen = !mobileMenuOpen" class="md:hidden">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
      </svg>
    </button>
    
    <!-- Mobile Menu -->
    <div x-show="mobileMenuOpen" x-transition class="absolute top-16 left-0 right-0 bg-white shadow-lg md:hidden">
      <nav class="flex flex-col p-4 space-y-2">
        <a href="/" class="hover:text-blue-600 transition">Accueil</a>
        <a href="/a-propos/" class="hover:text-blue-600 transition">À Propos</a>
        <a href="/services/" class="hover:text-blue-600 transition">Services</a>
        <a href="/realisations/" class="hover:text-blue-600 transition">Réalisations</a>
        <a href="/contact/" class="hover:text-blue-600 transition">Contact</a>
      </nav>
    </div>
  </div>
</header>
```

**_includes/footer.njk** (Footer Component):
```html
<footer class="py-8 bg-gray-100 text-center text-sm text-gray-500">
  © 2025 Company Name. All rights reserved.
</footer>
```

**index.njk** (Content Page):
```yaml
---
layout: base.njk
title: Accueil
permalink: /
---

<!-- Hero Section with AOS -->
<section class="container mx-auto text-center" data-aos="fade-up">
  <h2 class="text-4xl font-bold mb-4">Bienvenue</h2>
  <p class="text-lg text-gray-600 mb-8">Votre partenaire de confiance pour un service de qualité</p>
  <img src="/assets/images/hero.jpg" 
       srcset="/assets/images/hero-480.jpg 480w, /assets/images/hero-960.jpg 960w, /assets/images/hero-1920.jpg 1920w" 
       sizes="(max-width: 600px) 480px, (max-width: 1200px) 960px, 1920px" 
       alt="Hero image showing our services" 
       loading="lazy"
       class="rounded-lg shadow-lg mx-auto">
</section>
```

## Tone and Context

The user is a developer working on a client's small business website (e.g., landscaper, artisan, small retailer).
Focus on clarity, readability, and presentability with subtle modern enhancements.
Keep JavaScript minimal — Alpine.js for essential interactivity only.
Use AOS sparingly for scroll animations that enhance user experience without overwhelming.
Avoid overly complex patterns or external dependencies beyond the approved stack.

## Technology Stack Summary

**Eleventy (11ty)**: Static site generator with Nunjucks/Liquid templating
**Templating**: Nunjucks (`.njk`) for layouts, includes, and data-driven pages
**HTML5**: Semantic structure (header, nav, main, section, article, footer)
**Tailwind CSS**: Utility-first styling for layout, spacing, typography, colors
**Alpine.js**: Minimal JavaScript for dropdowns, modals, tabs, toggles
**AOS**: Scroll-triggered animations (fade, slide, zoom)
**Heroicons**: Consistent icon library (inline SVG)
**Google Fonts**: Typography via Google Fonts API
**Best Practices**: Lazy loading, responsive images (srcset/sizes), accessibility, DRY templates

## When Unsure

If the user's prompt is ambiguous:
Default to simple Eleventy templates with a base layout and reusable includes.
Create separate `.njk` files for header and footer components.
Include clean hero sections, short service grids, and a contact call-to-action in content pages.
Use Tailwind defaults only — no plugins, no dark mode unless specified.
Add subtle AOS animations (fade-up, fade-in) to key sections.
Use Alpine.js only if interactivity is essential (e.g., mobile menu, accordion).
Always implement lazy loading and responsive images by default.
Use Heroicons for any icons needed.
Leverage Eleventy's front matter for page-specific metadata (title, description, permalink).