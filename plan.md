# Portfolio Website Plan

## Recommended Tech Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | **Astro** | Zero-JS by default, fast builds, great SEO, easy to add sections |
| Styling | **Tailwind CSS v4** | Utility-first, dark mode support, responsive out of the box |
| Animations | **Framer Motion** (hero) + CSS transitions (everywhere else) | Smooth entry animations without bloat |
| Deployment | **Netlify** | Free tier, auto-deploy from Git, built-in form handling for contact |
| Language | **TypeScript** | Type safety, better DX as the project grows |

> **Alternative:** If you want richer interactivity or plan to add a blog/CMS later, swap Astro for **Next.js 15** (App Router). The file structure below works for both.

---

## File Structure

```
portfolio/
├── public/
│   ├── favicon.ico
│   └── images/
│       └── projects/          # Project screenshots
├── src/
│   ├── components/
│   │   ├── Hero.astro          # Name, tagline, CTA
│   │   ├── Projects.astro      # Project grid/cards
│   │   ├── ProjectCard.astro   # Individual project card
│   │   ├── About.astro         # Bio, skills, photo
│   │   ├── Contact.astro       # Email + LinkedIn links
│   │   └── Nav.astro           # Sticky navigation
│   ├── data/
│   │   └── projects.ts         # Project list (title, description, links, tags)
│   ├── layouts/
│   │   └── BaseLayout.astro    # HTML shell, meta tags, fonts
│   ├── pages/
│   │   └── index.astro         # Assembles all sections
│   └── styles/
│       └── global.css          # Base styles, CSS variables, font imports
├── astro.config.mjs
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

### Adding New Sections Later
1. Create `src/components/NewSection.astro`
2. Add data to `src/data/` if needed
3. Import and place it in `src/pages/index.astro`
4. Add a nav link in `Nav.astro`

No routing changes needed — the single-page structure scales cleanly.

---

## Design Considerations

### Layout & Navigation
- Single-page app with anchor-link navigation (`/#projects`, `/#about`, etc.)
- Sticky top nav that highlights the active section on scroll
- Smooth scroll behavior via CSS (`scroll-behavior: smooth`)
- Mobile-first responsive design; hamburger menu on small screens

### Hero Section
- Full-viewport height (`min-h-screen`)
- Name as `<h1>`, tagline as `<p>` or `<h2>`
- Optional: animated text reveal (Framer Motion fade-in + slide-up)
- CTA buttons: "View My Work" (scrolls to projects) + "Contact Me"

### Projects Section
- Responsive CSS grid: 1 col mobile → 2 col tablet → 3 col desktop
- Each card: project name, short description, tech tags, links (GitHub + live demo)
- Data-driven: edit `src/data/projects.ts` to add/remove projects without touching markup
- Optional: filter by tag/technology

### About Section
- Short bio paragraph
- Skills as a tag cloud or icon grid
- Optional: headshot image (use `aspect-ratio: 1/1`, `object-fit: cover`)

### Contact Section
- Simple — no form needed; direct `mailto:` link and LinkedIn URL
- If a contact form is desired later: Netlify Forms (zero backend, just add `netlify` attribute to `<form>`)

### Typography & Color
- Font pairing suggestion: **Inter** (body) + **Cal Sans** or **Geist** (headings) — both free on Google Fonts / Fontsource
- Define a small color palette via CSS custom properties in `global.css`:
  - Primary accent (your brand color)
  - Background, surface, text, muted text
- Support dark mode via `prefers-color-scheme` media query or a toggle

### Performance & SEO
- Add `<meta>` description and Open Graph tags in `BaseLayout.astro`
- Compress all images; use `<img loading="lazy">` for project screenshots
- Astro ships 0 KB of JS by default — only hydrate components that need it
- Target Lighthouse score ≥ 90 across all categories

---

## Suggested Order of Implementation

1. Scaffold Astro project + install Tailwind
2. Build `BaseLayout.astro` (fonts, meta, global styles)
3. Build `Nav.astro`
4. Build `Hero.astro`
5. Populate `projects.ts`, build `ProjectCard.astro` + `Projects.astro`
6. Build `About.astro`
7. Build `Contact.astro`
8. Polish: animations, responsive tweaks, dark mode
9. Deploy to Netlify
