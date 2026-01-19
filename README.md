# ArgExpats.com

A minimal, distraction-free Hugo static site for resources and guides for expats in Argentina.

## Features

- Clean, minimal design inspired by Obsidian's Minimal theme
- Light/dark mode with system preference detection and manual toggle
- EB Garamond typography for body text
- JetBrains Mono for code and labels
- Fully responsive mobile design
- SEO optimized with meta tags, Open Graph, and JSON-LD structured data
- RSS feed at `/index.xml`
- Auto-generated sitemap
- Cloudflare Pages ready with security headers

## Prerequisites

You need Hugo installed on your machine. Install Hugo:

**macOS:**
```bash
brew install hugo
```

**Windows:**
```bash
choco install hugo-extended
```

**Linux:**
```bash
snap install hugo
```

Or download from [Hugo Releases](https://github.com/gohugoio/hugo/releases).

## Local Development

1. **Clone or navigate to the project directory:**
   ```bash
   cd argexpats
   ```

2. **Start the Hugo development server:**
   ```bash
   hugo server -D
   ```

   The `-D` flag includes draft content. Omit it to preview only published content.

3. **View the site:**
   Open http://localhost:1313 in your browser.

   The site will auto-reload when you make changes to content or templates.

## Project Structure

```
argexpats/
├── archetypes/          # Content templates
│   ├── posts.md         # Template for new posts
│   └── projects.md      # Template for new projects
├── content/             # All site content
│   ├── about.md         # About page
│   ├── posts/           # Blog posts
│   └── projects/        # Project showcases
├── static/              # Static assets
│   ├── css/
│   │   └── main.css     # Site styles
│   ├── js/
│   │   └── theme-toggle.js  # Dark mode toggle
│   ├── _headers         # Cloudflare Pages headers
│   └── _redirects       # Cloudflare Pages redirects
├── themes/              # Hugo theme
│   └── argexpats/
│       └── layouts/     # HTML templates
│           ├── _default/
│           ├── partials/
│           ├── posts/
│           ├── projects/
│           └── index.html
└── hugo.toml            # Site configuration
```

## Creating Content

### Create a New Blog Post

```bash
hugo new posts/your-post-title.md
```

This creates a new post in `content/posts/` using the post archetype template. Edit the file:

```markdown
---
title: "Your Post Title"
date: 2026-01-19
draft: false        # Set to false when ready to publish
description: "A brief description for SEO"
tags: ["tag1", "tag2"]
---

Your content here...
```

### Create a New Project

```bash
hugo new projects/your-project-name.md
```

This creates a new project in `content/projects/`. Edit the file:

```markdown
---
title: "Your Project Name"
date: 2026-01-19
draft: false
description: "Project description"
tech: ["React", "TypeScript", "Tailwind CSS"]
github: "https://github.com/username/repo"
demo: "https://example.com"
website: "https://example.com"
---

Your project description...
```

### Edit the About Page

Edit `content/about.md` directly to update the about page content.

## Configuration

Edit `hugo.toml` to customize:

- Site title and description
- Base URL (important for production)
- Menu items
- Social media links
- SEO settings

Key settings to update for production:

```toml
baseURL = 'https://argexpats.com/'
title = 'ArgExpats'

[params]
  description = 'Resources and guides for expats in Argentina'
  author = 'ArgExpats'
  twitter = '@argexpats'
```

## Building for Production

Generate the static site:

```bash
hugo
```

This creates a `public/` directory with all static files ready for deployment.

To build without draft content and minify output:

```bash
hugo --minify
```

## Deploying to Cloudflare Pages

### Initial Setup

1. **Push your code to GitHub:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/yourusername/argexpats.git
   git push -u origin main
   ```

2. **Connect to Cloudflare Pages:**
   - Go to [Cloudflare Dashboard](https://dash.cloudflare.com/)
   - Navigate to Pages
   - Click "Create a project"
   - Connect your GitHub repository
   - Select the `argexpats` repository

3. **Configure Build Settings:**
   - **Framework preset:** Hugo
   - **Build command:** `hugo --minify`
   - **Build output directory:** `public`
   - **Environment variables:**
     - `HUGO_VERSION`: `0.121.0` (or your Hugo version, check with `hugo version`)

4. **Deploy:**
   Click "Save and Deploy"

### Automatic Deployments

Cloudflare Pages will automatically deploy when you push to your main branch:

```bash
git add .
git commit -m "Update content"
git push
```

### Custom Domain Setup

1. **In Cloudflare Pages:**
   - Go to your project
   - Click "Custom domains"
   - Click "Set up a custom domain"
   - Enter `argexpats.com`

2. **DNS Configuration:**
   - If your domain is already on Cloudflare, DNS records are configured automatically
   - If not, add a CNAME record pointing to your Pages URL

3. **SSL/TLS:**
   - Cloudflare automatically provisions SSL certificates
   - Ensure SSL/TLS mode is set to "Full" or "Full (strict)"

## Customization

### Styling

Edit `static/css/main.css` to customize:
- Colors (change CSS variables in `:root` and `[data-theme="dark"]`)
- Typography
- Spacing
- Layout

### Fonts

The site uses Google Fonts by default. To change fonts, edit the link in `themes/argexpats/layouts/partials/head.html`:

```html
<link href="https://fonts.googleapis.com/css2?family=Your+Font&display=swap" rel="stylesheet">
```

Then update CSS variables in `main.css`:

```css
:root {
  --font-serif: 'Your Font', serif;
  --font-mono: 'Your Mono Font', monospace;
}
```

### Navigation Menu

Edit `hugo.toml` to modify the navigation menu:

```toml
[menu]
  [[menu.main]]
    name = 'Posts'
    url = '/posts/'
    weight = 1
  [[menu.main]]
    name = 'Your New Page'
    url = '/your-page/'
    weight = 4
```

## SEO Best Practices

The site includes comprehensive SEO features:

- ✅ Semantic HTML5
- ✅ Meta tags (title, description)
- ✅ Open Graph tags (Facebook, LinkedIn)
- ✅ Twitter Cards
- ✅ JSON-LD structured data
- ✅ Canonical URLs
- ✅ XML sitemap
- ✅ Robots.txt
- ✅ RSS feed

**Important:** Update `baseURL` in `hugo.toml` to your actual domain for proper SEO.

## Performance

The site is optimized for performance:

- Minimal CSS and JavaScript
- System fonts with fallbacks
- Lazy loading images (browser-native)
- Static generation (no server-side processing)
- Cloudflare CDN (when deployed to Cloudflare Pages)
- Aggressive caching headers in `_headers`

## Browser Support

- Chrome (last 2 versions)
- Firefox (last 2 versions)
- Safari (last 2 versions)
- Edge (last 2 versions)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Troubleshooting

### Site not updating locally

Clear Hugo's cache:
```bash
hugo --gc
```

### Build fails on Cloudflare Pages

Check the HUGO_VERSION environment variable matches your local version:
```bash
hugo version
```

### Dark mode not working

Ensure JavaScript is enabled and check browser console for errors.

### Styles not loading

Run Hugo server with:
```bash
hugo server -D --disableFastRender
```

## License

This project is open source and available under the MIT License.

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Support

For questions or issues:
- Open an issue on GitHub
- Email: hello@argexpats.com

## Credits

- Design inspired by [Minimal Theme](https://github.com/kepano/obsidian-minimal) by @kepano
- Built with [Hugo](https://gohugo.io/)
- Fonts: EB Garamond and JetBrains Mono via Google Fonts
- Hosted on [Cloudflare Pages](https://pages.cloudflare.com/)

---

Built with ❤️ for the Argentina expat community
