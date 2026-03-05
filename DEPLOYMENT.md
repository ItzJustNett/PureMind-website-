# Netlify Deployment Guide

This project is configured for deployment on Netlify. Follow the steps below to deploy your Next.js application.

## Prerequisites

- A Netlify account (free at [netlify.com](https://www.netlify.com))
- Git repository (already set up)
- GitHub/GitLab/Bitbucket account (for continuous deployment)

## Deployment Methods

### Option 1: Automatic Deployment with Git (Recommended)

1. **Push to your repository** (GitHub, GitLab, or Bitbucket)
   ```bash
   git add .
   git commit -m "Configure Netlify deployment"
   git push origin master
   ```

2. **Connect to Netlify**
   - Go to [app.netlify.com](https://app.netlify.com)
   - Click "New site from Git"
   - Select your Git provider and repository
   - Choose the branch (default: `master`)

3. **Configure build settings**
   - Build command: `npm run build`
   - Publish directory: `.next`
   - Leave other settings as default (Netlify will auto-detect Next.js)

4. **Set environment variables** (if needed)
   - Go to Site settings → Environment variables
   - Add any required environment variables

5. **Deploy**
   - Click "Deploy site"
   - Netlify will build and deploy automatically
   - Enable auto-deploy on push for continuous deployment

### Option 2: Deploy with Netlify CLI

1. **Install Netlify CLI**
   ```bash
   npm install -g netlify-cli
   ```

2. **Authenticate with Netlify**
   ```bash
   netlify login
   ```

3. **Deploy**
   ```bash
   netlify deploy --prod
   ```

### Option 3: Manual Upload

1. **Build the project locally**
   ```bash
   npm install
   npm run build
   ```

2. **Deploy to Netlify**
   - Go to [app.netlify.com/drop](https://app.netlify.com/drop)
   - Drag and drop the `.next` folder
   - Your site will be deployed with a temporary URL

## Configuration Files

- **netlify.toml**: Contains build settings, redirects, headers, and caching rules
- **.netlifyignore**: Specifies files to exclude from deployment

## API Configuration

The application is configured to use the API at: `https://api.xoperr.dev/api`

API requests are automatically proxied through:
```
/api/* → https://api.xoperr.dev/api/*
```

This is configured in `netlify.toml` and `next.config.mjs`.

## Important Notes

- **Static Site Generation (SSG)**: This Next.js app uses server-side features. Netlify will handle this automatically.
- **Environment Variables**: Any sensitive data should be set in Netlify's environment variables, not in version control.
- **Build Time**: First builds may take 2-5 minutes. Subsequent deploys are faster due to caching.
- **Custom Domain**: After initial deployment, you can add a custom domain in Site settings.

## Troubleshooting

### Build Fails
- Check build logs in Netlify's dashboard
- Ensure `npm run build` works locally
- Verify all dependencies are in `package.json`

### API Calls Failing
- Verify API endpoint is correct: `https://api.xoperr.dev/api`
- Check CORS headers are properly set
- Review browser console for error details

### 404 Errors
- Next.js client-side routing is configured in `netlify.toml`
- If issues persist, check that the redirect rule is active

## Support

- Netlify Documentation: https://docs.netlify.com/
- Next.js on Netlify: https://docs.netlify.com/integrations/frameworks/next-js/
- Community: https://community.netlify.com/
