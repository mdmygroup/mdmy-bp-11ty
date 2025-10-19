# Bizot Paysagistes - Eleventy (11ty) Website

This is the Eleventy-powered version of the Bizot Paysagistes website, converted from plain HTML to a modern static site generator.

## 🚀 Stack

- **Eleventy (11ty)**: Static site generator with Nunjucks templating
- **Tailwind CSS**: Utility-first CSS (via CDN)
- **Alpine.js**: Minimal JavaScript framework for interactivity
- **AOS**: Animate On Scroll library
- **Heroicons**: Icon library (inline SVG)

## 📁 Project Structure

```
mdmy-bp-11ty/
├── _includes/           # Eleventy layouts and partials
│   ├── base.njk        # Base layout template
│   ├── header.njk      # Header component
│   └── footer.njk      # Footer component
├── _site/              # Generated output (git-ignored)
├── assets/             # Static assets (images, logos)
├── index.njk           # Homepage
├── services.njk        # Services page
├── realisations.njk    # Portfolio/realizations page
├── a-propos.njk        # About page
├── contact.njk         # Contact page
├── .eleventy.js        # Eleventy configuration
├── package.json        # Node dependencies
└── README.md           # This file
```

## 🛠️ Setup & Installation

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Installation

```bash
npm install
```

## 🏃 Development

### Start development server:

```bash
npm start
```

This will:
- Build the site
- Start a local development server at `http://localhost:8080`
- Watch for file changes and rebuild automatically

### Build for production:

```bash
npm run build
```

This generates the static site in the `_site/` directory.

### Clean build directory:

```bash
npm run clean
```

## 📝 Key Features

### Templating with Nunjucks

- **Base Layout**: All pages extend `_includes/base.njk`
- **Reusable Components**: Header and footer are separate includes
- **Front Matter**: Each page has YAML front matter for metadata

Example:
```yaml
---
layout: base.njk
title: "Page Title"
description: "Page description"
permalink: /page-url/
---
```

### Dynamic Navigation

The header automatically highlights the active page based on `page.url`.

### SEO Optimization

- Meta tags for description, keywords, author
- Open Graph tags for social media
- Semantic HTML structure

### Performance

- Lazy loading images
- Responsive images with `srcset`
- CDN-hosted libraries
- Minimal JavaScript

## 🎨 Color Palette

```javascript
{
  brand: '#80ab97',        // Main brand green
  brandLight: '#cbecdd',   // Light green
  brandDark: '#386D56',    // Dark green
  accent: '#F97316',       // Orange accent
  bgColor: '#FFFFFF',      // Background
  textColor: '#102611'     // Text color
}
```

## 🔗 URL Structure

Eleventy generates clean URLs:

| Source File       | Output URL         |
|-------------------|--------------------|
| `index.njk`       | `/`                |
| `services.njk`    | `/services/`       |
| `realisations.njk`| `/realisations/`   |
| `a-propos.njk`    | `/a-propos/`       |
| `contact.njk`     | `/contact/`        |

## 📦 Deployment

The `_site/` directory contains the complete static website ready for deployment to Netlify, Vercel, GitHub Pages, or any static host.

### Netlify Configuration

Create `netlify.toml`:

```toml
[build]
  command = "npm run build"
  publish = "_site"
```

## 🗑️ Migration Notes

### HTML to Eleventy Conversion

All original HTML files have been converted to `.njk` (Nunjucks) format:

- ✅ Header and footer extracted to reusable components
- ✅ Page-specific content moved to individual `.njk` files
- ✅ Front matter added for metadata and SEO
- ✅ URLs converted from `.html` to clean URLs
- ✅ Asset paths updated to absolute paths

### Original HTML Files

The original `.html` files are present for reference. You can remove them once everything is working:

```bash
rm -f *.html
```

## 📚 Resources

- [Eleventy Documentation](https://www.11ty.dev/docs/)
- [Nunjucks Templating](https://mozilla.github.io/nunjucks/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Alpine.js](https://alpinejs.dev/)

---

**Built with ❤️ using Eleventy (11ty)**