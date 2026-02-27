---
name: astro
description: Deploy multilingual static websites for free on Cloudflare using Astro framework with markdown source files. Use when: (1) Creating new static sites or blogs, (2) Setting up multilingual (i18n) content, (3) Deploying to Cloudflare Pages, (4) Converting markdown to static websites, (5) Setting up free hosting infrastructure.
---

# Astro Static Site Generator

Deploy multilingual static websites for free on Cloudflare using Astro framework.

## Quick Start

### 1. Create Project

```bash
npm create astro@latest my-site -- --template minimal
cd my-site
npm install
```

### 2. Add Cloudflare Adapter

```bash
npm install @astrojs/cloudflare
```

Update `astro.config.mjs`:

```javascript
import { defineConfig } from 'astro/config';
import cloudflare from '@astrojs/cloudflare';

export default defineConfig({
  output: 'static',
  adapter: cloudflare(),
  site: 'https://your-site.pages.dev',
});
```

### 3. Deploy to Cloudflare

**Git Integration (Recommended)**

1. Push to GitHub/GitLab
2. Cloudflare Dashboard → Pages → Create project → Connect to Git
3. Configure:
   - Build command: `npm run build`
   - Build output: `dist`

**Direct Upload**

```bash
npx wrangler pages deploy dist
```

## Multilingual Configuration

### Astro Config

```javascript
// astro.config.mjs
export default defineConfig({
  i18n: {
    defaultLocale: 'en',
    locales: ['en', 'es', 'fr', 'de'],
    routing: {
      prefixDefaultLocale: false,
    },
  },
});
```

### Content Structure

```
src/content/
├── config.ts          # Content collection schema
└── docs/
    ├── en/
    │   ├── index.md
    │   └── guide.md
    ├── es/
    │   ├── index.md
    │   └── guide.md
    └── fr/
        ├── index.md
        └── guide.md
```

### Content Collection Schema

```typescript
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const docs = defineCollection({
  type: 'content',
  schema: z.object({
    title: z.string(),
    description: z.string(),
    lang: z.enum(['en', 'es', 'fr', 'de']),
  }),
});

export const collections = { docs };
```

### Language Switcher Component

```astro
---
// src/components/LanguageSwitcher.astro
const languages = {
  en: 'English',
  es: 'Español',
  fr: 'Français',
  de: 'Deutsch',
};

const currentPath = Astro.url.pathname;
const currentLang = Astro.currentLocale || 'en';
---

<select onchange="window.location = this.value">
  {Object.entries(languages).map(([code, name]) => (
    <option 
      value={`/${code}${currentPath}`} 
      selected={code === currentLang}
    >
      {name}
    </option>
  ))}
</select>
```

## File Structure

```
my-site/
├── astro.config.mjs      # Astro + Cloudflare config
├── package.json
├── public/
│   └── favicon.svg
├── src/
│   ├── components/
│   │   └── LanguageSwitcher.astro
│   ├── content/
│   │   ├── config.ts
│   │   └── blog/
│   │       ├── en/
│   │       └── es/
│   ├── layouts/
│   │   └── BaseLayout.astro
│   └── pages/
│       ├── index.astro
│       ├── en/
│       │   └── index.astro
│       └── es/
│           └── index.astro
└── wrangler.toml         # Cloudflare config (optional)
```

## Cloudflare Pages Settings

| Setting | Value |
|---------|-------|
| Build command | `npm run build` |
| Build output | `dist` |
| Node version | `18` |

### Custom Domain

Cloudflare Dashboard → Pages → your-site → Custom domains → Add domain

### Redirects

Create `public/_redirects`:

```
/  /en/  302
/old-page  /new-page  301
```

## Commands Reference

| Command | Description |
|---------|-------------|
| `npm run dev` | Start dev server |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build |
| `npx wrangler pages deploy dist` | Deploy to Cloudflare |

## Blog with Content Collections

```astro
---
// src/pages/blog/[...slug].astro
import { getCollection } from 'astro:content';

export async function getStaticPaths() {
  const posts = await getCollection('blog');
  return posts.map(post => ({
    params: { slug: post.slug },
    props: { post },
  }));
}

const { post } = Astro.props;
const { Content } = await post.render();
---

<article>
  <h1>{post.data.title}</h1>
  <Content />
</article>
```

## Troubleshooting

### Build Fails on Cloudflare

Set `NODE_VERSION=18` in environment variables.

### 404 on Nested Routes

```javascript
// astro.config.mjs
export default defineConfig({
  trailingSlash: 'always',
});
```

### i18n Not Working

Ensure:
1. Locales match folder names exactly
2. Content files have correct `lang` frontmatter

## Resources

- [Astro Docs](https://docs.astro.build)
- [Cloudflare Pages Docs](https://developers.cloudflare.com/pages)
- [Astro i18n Guide](https://docs.astro.build/en/guides/i18n/)
- [Cloudflare Adapter](https://docs.astro.build/en/guides/deploy/cloudflare/)

## Scripts

| Script | Description |
|--------|-------------|
| `scripts/astro-new-post.py` | Create multilingual blog posts |
| `scripts/astro-i18n-check.py` | Validate translation coverage |

All scripts use only Python standard library (no dependencies).
