# Poloshope

A Shopify Online Store 2.0 theme experiment that rebuilds Dawn's header with Tailwind CSS and Alpine.js, compiled through Laravel Mix.

![Shopify](https://img.shields.io/badge/Shopify-Dawn%204.0-7AB55C?logo=shopify&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?logo=tailwindcss&logoColor=white)
![Alpine.js](https://img.shields.io/badge/Alpine.js-3-8BC0D0?logo=alpinedotjs&logoColor=white)

## Overview

Poloshope started in March 2022 from Shopify's Dawn 4.0.0 theme. The goal was to replace Dawn's stylesheet with a Tailwind CSS utility build and add interactivity with Alpine.js, starting with the site header. It is an early-stage project: the header is rewritten, and the rest of the theme is still stock Dawn.

## What Is Custom

- **Tailwind + Sass build**: `src/scss/app.scss` (Tailwind layers plus header grid styles written in SCSS) and `src/js/app.js` (Alpine.js bootstrap) are compiled by Laravel Mix into `assets/app.css` and `assets/app.js`.
- **Tailwind content scanning**: `tailwind.config.js` scans `config`, `layout`, `sections`, `snippets`, and `templates` so utility classes used in Liquid are included in the build.
- **Rebuilt header** (`sections/header.liquid`):
  - CSS grid layout with logo, menu, and icon areas that reorders on mobile (menu, logo, icons)
  - Desktop navigation with hover dropdown submenus, styled with Tailwind utilities
  - Mobile menu button that dispatches an Alpine `toggle-menu` event
  - Account link and cart button with an Alpine-bound cart count badge (`cart-count-updated` event) and a `toggle-cart` event
  - Keeps Dawn's Organization and WebSite JSON-LD structured data
- **New snippet**: `snippets/icon-menu.liquid` (hamburger icon used by the header).
- **Layout change**: `layout/theme.liquid` loads `app.css` in place of Dawn's `base.css`.

Everything else (product, collection, cart, search, blog, and customer templates) is unmodified Dawn 4.0.0.

## Tech Stack

- Shopify Liquid, Online Store 2.0 (Dawn 4.0.0 base)
- Tailwind CSS 3
- Alpine.js 3
- Sass
- Laravel Mix 6 (webpack)

## Getting Started

### Prerequisites

- Node.js and npm
- [Shopify CLI](https://shopify.dev/docs/themes/tools/cli)
- A Shopify development store or Partner account

### Install

```bash
git clone https://github.com/coderasraf/poloshope.git
cd poloshope
npm install
```

### Build assets

`package.json` has no build scripts, so run Laravel Mix directly:

```bash
npx mix            # development build -> assets/app.css, assets/app.js
npx mix watch      # rebuild on changes
npx mix --production
```

### Preview the theme

```bash
shopify theme dev --store your-store.myshopify.com
```

`.shopifyignore` keeps `package.json`, `package-lock.json`, and `mix-manifest.json` out of theme uploads.

## Project Structure

```text
poloshope/
├── src/
│   ├── js/app.js          # Alpine.js entry
│   └── scss/app.scss      # Tailwind layers + header styles
├── assets/                # Dawn assets + compiled app.css / app.js
├── config/                # settings_schema.json, settings_data.json
├── layout/theme.liquid    # loads app.css instead of base.css
├── sections/header.liquid # Tailwind/Alpine header
├── snippets/icon-menu.liquid
├── templates/             # Dawn JSON templates
├── tailwind.config.js
└── webpack.mix.js
```

## Author

Built by **Ashraf Siddik**, Shopify developer & CRO specialist.
- Website: [ashraf-siddik.com](https://ashraf-siddik.com)
- GitHub: [@coderasraf](https://github.com/coderasraf)

## License

Based on Shopify's Dawn theme. See [LICENSE.md](LICENSE.md).
