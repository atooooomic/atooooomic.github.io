# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **AstroPaper** blog - a minimal, responsive, accessible and SEO-friendly Astro blog theme. The site is built with Astro, TypeScript, and TailwindCSS, featuring static site generation with dynamic OG image generation, fuzzy search via Pagefind, and markdown-based content.

**Tech Stack:**
- Framework: Astro (SSG)
- Language: TypeScript
- Styling: TailwindCSS v4
- Search: Pagefind (static search)
- OG Images: Satori + Resvg
- Code Highlighting: Shiki with custom transformers

## Development Commands

```bash
# Install dependencies
pnpm install

# Start dev server (localhost:4321)
pnpm run dev

# Build for production (includes type checking, build, and search index generation)
pnpm run build

# Preview production build locally
pnpm run preview

# Type checking and sync
pnpm run sync        # Generate TypeScript types for Astro modules

# Code quality
pnpm run lint        # Run ESLint
pnpm run format      # Format with Prettier
pnpm run format:check # Check formatting without modifying
```

**Note:** The build command runs `astro check && astro build && pagefind --site dist && cp -r dist/pagefind public/` which:
1. Type checks the entire codebase
2. Builds the site
3. Generates the Pagefind search index
4. Copies the search index to public for future builds

## Architecture

### Content Management

**Blog Posts**: All blog posts live in `src/data/blog/` as markdown files. The content collection is defined in `src/content.config.ts` with schema validation using Zod.

**Content Schema** (frontmatter):
- `title`: Post title (required)
- `pubDatetime`: Publication date (required, Date object)
- `description`: Post description for SEO (required)
- `author`: Author name (defaults to SITE.author)
- `tags`: Array of tags (defaults to ["others"])
- `featured`: Boolean to mark featured posts
- `draft`: Boolean to hide posts in production
- `modDatetime`: Last modified date
- `ogImage`: Custom OG image (string or image import)
- `canonicalURL`: Canonical URL for SEO
- `hideEditPost`: Hide edit post link
- `timezone`: Post-specific timezone (IANA format)

**Post Filtering Logic** (`src/utils/postFilter.ts`):
- Posts with `draft: true` are hidden in production
- Posts can be scheduled with `pubDatetime` + `SITE.scheduledPostMargin` (15 min buffer)
- All drafts are visible in dev mode

### Routing Structure

Astro uses file-based routing in `src/pages/`:

```
/                           → index.astro (homepage)
/posts/[...page]           → Post list with pagination
/posts/[...slug]           → Individual post detail pages
/tags/                     → Tag index
/tags/[tag]/[...page]      → Posts filtered by tag with pagination
/search                    → Search page (uses Pagefind)
/archives                  → Archive view (if enabled)
/og.png.ts                 → Dynamic OG image generation endpoint
/rss.xml.ts                → RSS feed
/robots.txt.ts             → Robots.txt
```

### Key Utilities

**Post Processing** (`src/utils/`):
- `getSortedPosts.ts`: Filters and sorts posts by date (uses modDatetime or pubDatetime)
- `postFilter.ts`: Filters out drafts and scheduled posts
- `getPostsByTag.ts`: Retrieves posts by tag
- `getUniqueTags.ts`: Extracts all unique tags from posts
- `slugify.ts`: Generates URL-friendly slugs

**OG Image Generation** (`src/utils/generateOgImages.ts`):
- Uses Satori to render React-like templates to SVG
- Converts SVG to PNG using Resvg
- Templates in `src/utils/og-templates/` (post.js and site.js)
- Dynamically generates images for each post at build time

**Custom Shiki Transformer** (`src/utils/transformers/fileName.js`):
- Adds file name labels to code blocks via `file="filename"` meta attribute
- Supports two styling variants (v1: tab-style, v2: badge-style)
- Example: ` ```js file="example.js" `

### Layouts

- `Layout.astro`: Base HTML layout with SEO, fonts, and theme support
- `Main.astro`: Main content wrapper with header/footer
- `PostDetails.astro`: Individual post layout with TOC, breadcrumbs, share links
- `AboutLayout.astro`: About page layout

### Configuration Files

**`src/config.ts`**: Main site configuration
- Site metadata (website URL, author, title, description)
- Display settings (posts per page, dark mode, archives visibility)
- Edit post URL configuration
- Timezone settings
- Dynamic OG image toggle

**`astro.config.ts`**: Astro framework configuration
- Site URL from SITE.website
- Sitemap integration (filters based on showArchives)
- Markdown: Remark plugins (TOC, collapse), Shiki themes (min-light, night-owl)
- TailwindCSS via Vite plugin
- Environment variables schema (Google Site Verification, AdSense)
- Experimental font providers (Google Sans Code)

**`src/constants.ts`**: Social links and share links configuration
- SOCIALS: Social media links for the site footer/header
- SHARE_LINKS: Share buttons for individual posts

### Component Structure

Components in `src/components/` are mostly presentational Astro components:
- **Header.astro**: Navigation with logo and theme toggle
- **Footer.astro**: Site footer with social links
- **Card.astro**: Blog post card for lists
- **Datetime.astro**: Formatted datetime display
- **Tag.astro**: Tag badge component
- **Pagination.astro**: Pagination controls
- **ShareLinks.astro**: Social share buttons
- **Breadcrumb.astro**: Breadcrumb navigation
- **BackButton.astro**: Back navigation button

### Markdown Features

Configured in `astro.config.ts`:
- **remark-toc**: Auto-generates table of contents
- **remark-collapse**: Collapses sections with "Table of contents" heading
- **Shiki transformers**:
  - `transformerFileName`: File name labels on code blocks
  - `transformerNotationHighlight`: Line highlighting
  - `transformerNotationWordHighlight`: Word highlighting
  - `transformerNotationDiff`: Diff highlighting (v3 algorithm)

### Search Implementation

- **Pagefind**: Static search generated at build time
- Search index created in `dist/pagefind/` during build
- Copied to `public/pagefind/` for future incremental builds
- Search UI at `/search` page

### Development Patterns

**Adding a New Blog Post**:
1. Create a markdown file in `src/data/blog/`
2. Add required frontmatter (title, pubDatetime, description)
3. Write content in markdown
4. Set `draft: false` when ready to publish
5. Run `pnpm run build` to generate search index and OG images

**Modifying Site Config**:
- Update `src/config.ts` for site-wide settings
- Update `src/constants.ts` for social/share links
- Update `astro.config.ts` for framework-level settings

**Customizing Styles**:
- TailwindCSS v4 configuration via CSS imports
- Theme styles in `src/styles/`
- Dark mode toggle via `src/scripts/theme.ts`

### Environment Variables

Optional variables (defined in `.env`):
- `PUBLIC_GOOGLE_SITE_VERIFICATION`: Google Search Console verification
- `PUBLIC_GOOGLE_ADSENSE_ID`: Google AdSense publisher ID

### Deployment

The site is configured for **Cloudflare Pages** deployment:
- Build command: `pnpm run build`
- Output directory: `dist/`
- Supports Docker deployment (Dockerfile and docker-compose.yml included)

### TypeScript Configuration

- Strict mode enabled
- Path alias: `@/` maps to `src/`
- Astro and content collection types auto-generated via `astro sync`
