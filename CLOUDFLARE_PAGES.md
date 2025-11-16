# Cloudflare Pages Configuration

## Build Settings
- **Build command**: `npm run build`
- **Build output directory**: `dist`
- **Node.js version**: `18.x`

## Environment Variables
No environment variables required for basic setup.

## Deployment
Cloudflare Pages will automatically:
1. Install dependencies with `npm install`
2. Run build command `npm run build`
3. Deploy the `dist` folder
4. Serve your static site globally

## Custom Domains
After deployment, you can add a custom domain in the Cloudflare Pages dashboard.