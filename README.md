# Astro Blog with Decap CMS

A modern blog built with Astro, Decap CMS, and deployed on Cloudflare Pages. This setup provides a WordPress-like experience with the performance and simplicity of a static site.

## 🚀 Features

- **Fast & Modern**: Built with Astro for optimal performance
- **Content Management**: Decap CMS provides a user-friendly admin interface at `/admin`
- **Comments**: GitHub Discussions-powered comments via giscus
- **Edge Deployment**: Hosted on Cloudflare Pages for global performance
- **Content Types**: Blog posts, code snippets, and photo posts
- **Dark Mode**: Automatic theme switching with system preference
- **TypeScript**: Full TypeScript support throughout

## 📁 Project Structure

```
├── public/
│   ├── admin/          # Decap CMS admin interface
│   └── images/         # Static images
├── src/
│   ├── components/     # Reusable components
│   ├── content/        # Content collections
│   │   ├── blog/       # Blog posts (Markdown)
│   │   ├── snippets/   # Code snippets (Markdown)
│   │   └── photos/     # Photo posts (Markdown)
│   ├── layouts/        # Page layouts
│   ├── pages/          # Routes and pages
│   └── styles/         # Global styles
├── astro.config.mjs    # Astro configuration
├── tailwind.config.mjs # Tailwind CSS configuration
└── wrangler.toml       # Cloudflare Pages configuration
```

## 🛠️ Setup Instructions

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure GitHub Repository

1. Update the repository name in:
   - `public/admin/config.yml` (line 2): `repo: your-username/your-repo`
   - `astro.config.mjs` (line 12): Update the site URL
   - `src/layouts/BlogPost.astro` (line 67): Update giscus repo settings

### 3. Set Up Decap CMS Authentication

1. Go to your GitHub repository Settings → Developer settings → OAuth Apps
2. Create a new OAuth App with:
   - Homepage URL: `https://your-blog.pages.dev`
   - Authorization callback URL: `https://api.netlify.com/auth/done`
3. Note the Client ID for later use

### 4. Configure giscus Comments

1. Enable GitHub Discussions in your repository
2. Visit [giscus.app](https://giscus.app) to configure:
   - Enter your repository name
   - Choose "Discussions" mapping
   - Select a discussion category
3. Copy the generated values to `src/layouts/BlogPost.astro`:
   - `repo`: Your repository
   - `repoId`: Generated repo ID  
   - `category`: Discussion category name
   - `categoryId`: Generated category ID

### 5. Set Up Cloudflare Pages

1. Connect your GitHub repository to Cloudflare Pages
2. Configure build settings:
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Node.js version: `18` or higher

3. Add environment variables in Cloudflare Pages:
   - `NODE_VERSION`: `18`

### 6. Configure GitHub Actions (Optional)

If you want automated deployments:

1. Get your Cloudflare API token and Account ID
2. Add these as repository secrets:
   - `CLOUDFLARE_API_TOKEN`
   - `CLOUDFLARE_ACCOUNT_ID`
3. Update the project name in `.github/workflows/deploy.yml`

## 🎯 Usage

### Development

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

### Content Management

1. **Via CMS**: Visit `/admin` for a user-friendly editor
2. **Direct editing**: Edit Markdown files in `src/content/`

### Content Types

- **Blog Posts** (`src/content/blog/`): Long-form articles
- **Snippets** (`src/content/snippets/`): Code snippets and quick tips  
- **Photos** (`src/content/photos/`): Photo posts with captions

### Adding Content

Each content type has a specific schema defined in `src/content/config.ts`. Required frontmatter fields vary by type but typically include:

```yaml
---
title: "Your Post Title"
description: "Brief description"
publishDate: 2024-11-16
tags: ["tag1", "tag2"]
draft: false
---
```

## 🔧 Customization

### Styling
- Main styles: `src/styles/global.css`
- Tailwind config: `tailwind.config.mjs`
- Color scheme: Modify CSS custom properties in layouts

### Layout
- Base layout: `src/layouts/BaseLayout.astro`
- Blog post layout: `src/layouts/BlogPost.astro`

### Content Collections
- Schema definitions: `src/content/config.ts`
- Add new collections by extending the schema and creating corresponding pages

## 📦 Deployment

### Cloudflare Pages (Recommended)

1. Push to your main branch
2. Cloudflare Pages will automatically build and deploy
3. Your site will be available at `https://your-project.pages.dev`

### Manual Deployment

```bash
# Build the site
npm run build

# Deploy with Wrangler (requires setup)
npm run deploy
```

## 🐛 Troubleshooting

### Common Issues

**Decap CMS not loading**: Check OAuth App configuration and repository settings in `config.yml`

**Comments not appearing**: Verify giscus configuration and ensure GitHub Discussions are enabled

**Build failures**: Check Node.js version (requires 18+) and verify all dependencies are installed

**Images not displaying**: Ensure images are in `public/images/` and paths start with `/images/`

## 🤝 Contributing

This is a personal blog template, but suggestions and improvements are welcome! Please open an issue or pull request.

## 📄 License

MIT License - feel free to use this as a template for your own blog!

## 🙏 Acknowledgments

- [Astro](https://astro.build) - The web framework
- [Decap CMS](https://decapcms.org) - Content management
- [giscus](https://giscus.app) - Comments system
- [Cloudflare Pages](https://pages.cloudflare.com) - Hosting platform