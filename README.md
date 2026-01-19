# Hanjie Jiang - Personal Website

Personal website built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.

**Live site:** [hanjie-jiang.github.io/personal-website](https://hanjie-jiang.github.io/personal-website/)

## Features

- Responsive design with pastel purple aesthetic
- Dark/light mode toggle
- Timeline view for projects
- Blog posts with tags and categories
- Search functionality
- RSS feed

## Local Development

```bash
# Install Hugo (https://gohugo.io/installation/)
# On Windows with winget:
winget install Hugo.Hugo.Extended

# Clone with submodules (for theme)
git clone --recurse-submodules https://github.com/hanjie-jiang/personal-website.git

# Start dev server
hugo server --buildDrafts

# Build for production
hugo --gc --minify
```

## Structure

```
.
├── content/           # Markdown content
│   ├── about.md
│   ├── experience.md
│   ├── projects.md
│   ├── publications.md
│   ├── awards.md
│   └── posts/         # Blog posts
├── assets/css/        # Custom CSS
├── themes/PaperMod/   # Theme (git submodule)
├── hugo.toml          # Site configuration
└── .github/workflows/ # GitHub Actions for deployment
```

## Deployment

Automatic deployment via GitHub Actions on push to `main` branch.

## Version History

- **2026-01-19**: Migrated to Hugo with PaperMod theme
- **2020**: Original static HTML/CSS site
