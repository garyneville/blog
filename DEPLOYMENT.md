# Deployment Guide

## Your blog is ready to deploy! 🚀

### Cloudflare Pages Setup

1. **Build Settings**:
   - Build command: `npm run build`
   - Build output: `dist`
   - Node.js: `18`

2. **Environment Variables** (if needed):
   - `NODE_VERSION`: `18`

### Authentication Setup

For production authentication:

1. **GitHub OAuth App**:
   - Homepage URL: Your Cloudflare Pages URL
   - Callback URL: `https://api.netlify.com/auth/done`

2. **Netlify Identity** (recommended):
   - Create free Netlify account
   - Enable Identity + Git Gateway
   - Configure GitHub OAuth

### Post-Deployment

1. Update `astro.config.mjs` with your actual Pages URL
2. Update GitHub OAuth app with correct callback URL
3. Configure giscus comments with your repository
4. Test the `/admin` interface

### Local Development

- Main site: `npm run dev` (port 4321)
- CMS backend: `npx decap-server` (port 8081)
- Admin: `http://localhost:4321/admin`

The blog will auto-deploy on every push to main branch!