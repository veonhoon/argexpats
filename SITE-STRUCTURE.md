# ArgExpats Site Structure

Complete file structure of the ArgExpats Hugo static site.

```
argexpats/
│
├── archetypes/                       # Content templates for hugo new
│   ├── posts.md                      # Template for new blog posts
│   └── projects.md                   # Template for new projects
│
├── content/                          # All site content (Markdown files)
│   ├── about.md                      # About page content
│   ├── posts/                        # Blog posts section
│   │   ├── _index.md                 # Posts section metadata
│   │   ├── getting-started-with-dni.md
│   │   ├── cost-of-living-buenos-aires.md
│   │   └── learning-spanish-argentina.md
│   └── projects/                     # Projects section
│       ├── _index.md                 # Projects section metadata
│       ├── expat-cost-calculator.md
│       └── visa-tracker.md
│
├── static/                           # Static assets (copied as-is to public/)
│   ├── css/
│   │   └── main.css                  # Main stylesheet with theme variables
│   ├── js/
│   │   └── theme-toggle.js           # Light/dark mode toggle script
│   ├── images/                       # Images directory
│   │   └── OG-IMAGE-INSTRUCTIONS.txt # Guide for adding OG image
│   ├── _headers                      # Cloudflare Pages security headers
│   ├── _redirects                    # Cloudflare Pages redirects
│   └── FAVICON-INSTRUCTIONS.txt      # Guide for adding favicon
│
├── themes/                           # Hugo themes directory
│   └── argexpats/                    # Custom ArgExpats theme
│       ├── layouts/                  # HTML templates
│       │   ├── _default/             # Default layouts
│       │   │   ├── baseof.html       # Base template (wraps all pages)
│       │   │   ├── list.html         # Default list page template
│       │   │   └── single.html       # Default single page template
│       │   ├── partials/             # Reusable template components
│       │   │   ├── head.html         # <head> section (meta tags, fonts, SEO)
│       │   │   ├── header.html       # Site header with nav
│       │   │   └── footer.html       # Site footer
│       │   ├── posts/                # Post-specific layouts
│       │   │   ├── list.html         # Posts archive page
│       │   │   └── single.html       # Individual post page
│       │   ├── projects/             # Project-specific layouts
│       │   │   ├── list.html         # Projects archive page
│       │   │   └── single.html       # Individual project page
│       │   └── index.html            # Homepage template
│       └── theme.toml                # Theme metadata
│
├── .gitignore                        # Git ignore rules
├── hugo.toml                         # Hugo site configuration
├── LICENSE                           # MIT License
├── README.md                         # Comprehensive documentation
└── SITE-STRUCTURE.md                 # This file

Generated after running `hugo`:
├── public/                           # Generated static site (deploy this)
└── resources/                        # Hugo cache (gitignored)
```

## Key Files Explained

### Configuration
- **hugo.toml**: Main site configuration (title, URLs, menus, params)

### Content
- **content/*.md**: Markdown files that become pages
- **content/posts/*.md**: Individual blog posts
- **content/projects/*.md**: Individual project showcases
- **content/*/_index.md**: Section metadata and descriptions

### Layouts (Templates)
- **baseof.html**: The wrapper template for all pages
- **index.html**: Homepage template
- **single.html**: Template for individual pages/posts/projects
- **list.html**: Template for archive/listing pages
- **partials/**: Reusable components included in other templates

### Styles & Scripts
- **static/css/main.css**: All site styles including themes
- **static/js/theme-toggle.js**: Dark mode toggle functionality

### Cloudflare Pages
- **static/_headers**: HTTP security and caching headers
- **static/_redirects**: URL redirects

### SEO & Meta
- Sitemap: Auto-generated at `/sitemap.xml`
- RSS: Auto-generated at `/index.xml`
- robots.txt: Auto-generated
- Meta tags: Configured in `partials/head.html`

## Content Front Matter

### Posts
```yaml
---
title: "Post Title"
date: 2026-01-19
draft: false
description: "SEO description"
tags: ["tag1", "tag2"]
---
```

### Projects
```yaml
---
title: "Project Name"
date: 2026-01-19
draft: false
description: "Project description"
tech: ["React", "TypeScript"]
github: "https://github.com/user/repo"
demo: "https://demo.com"
website: "https://website.com"
---
```

## Build Output

When you run `hugo`, it generates:

- **public/**: Complete static site ready for deployment
- **public/index.html**: Homepage
- **public/posts/**: All posts as static HTML
- **public/projects/**: All projects as static HTML
- **public/css/**, **public/js/**: Static assets
- **public/index.xml**: RSS feed
- **public/sitemap.xml**: XML sitemap
- **public/robots.txt**: Robots file

## Theme Structure

The ArgExpats theme follows Hugo's standard theme structure:

- **layouts/_default/**: Fallback templates
- **layouts/[section]/**: Section-specific templates
- **layouts/partials/**: Reusable components
- **layouts/index.html**: Homepage (special case)

Templates cascade:
1. Section-specific template (e.g., `layouts/posts/single.html`)
2. Default template (e.g., `layouts/_default/single.html`)
3. Hugo's built-in template

## Adding New Sections

To add a new section (e.g., "guides"):

1. Create directory: `content/guides/`
2. Add section index: `content/guides/_index.md`
3. Create archetype: `archetypes/guides.md`
4. Add layouts: `themes/argexpats/layouts/guides/`
5. Update menu in `hugo.toml`

## Notes

- All paths in `static/` are copied to `public/` root
- Theme files in `themes/argexpats/` override Hugo defaults
- Content files must be in `content/` directory
- Drafts (`draft: true`) are excluded from production builds
