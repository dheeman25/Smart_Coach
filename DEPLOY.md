# Vercel Deployment Fix

## The Issue
Vercel was failing to build because of the absolute path `/src/main.tsx` in `index.html`.

## The Fix
Changed the import path from `/src/main.tsx` to `./src/main.tsx` (relative path).

## Deploy to Vercel

### Option 1: Via Vercel Website (Easiest)

1. Go to **https://vercel.com**
2. Sign up/Login (use GitHub account for easier setup)
3. Click **"Add New Project"**
4. Import your GitHub repository
5. Vercel will auto-detect it's a Vite project
6. Click **"Deploy"**
7. Wait 1-2 minutes
8. Done! You'll get a live URL like `your-app.vercel.app`

### Option 2: Via Vercel CLI

```bash
# Install Vercel CLI globally
npm install -g vercel

# Deploy (run from project directory)
cd "c:\Smart Coach"
vercel

# Follow the prompts:
# - Set up and deploy? Yes
# - Which scope? (your account)
# - Link to existing project? No
# - Project name? interview-practice-app
# - Directory? ./
# - Override settings? No
```

## No Environment Variables Needed!

Since you're using mock AI (no API key), you don't need to configure any environment variables in Vercel. Just deploy and it works!

## After Deployment

You'll get a URL like:
`https://interview-practice-app-xxx.vercel.app`

Share this with:
- Hackathon judges
- On your resume
- With friends

## Future Updates

To redeploy after making changes:

```bash
git add .
git commit -m "Updated features"
git push
```

Vercel will automatically redeploy when you push to GitHub!
