# Deployment Guide for Remaining Projects

Complete configuration for PROJECT-3 through Tiny-todos deployment on Netlify.

## ✅ Completed Configuration

All remaining projects have been configured with:
- ✅ `package.json` created
- ✅ `netlify.toml` with build.ignore
- ✅ Root package.json updated with build scripts
- ✅ Ready for Netlify deployment

## 📦 Projects Overview

### PROJECT-3-DUO-main (Duo Studio)
**Type**: Static HTML Website  
**Framework**: Vanilla JS  
**Build Output**: Current directory (static files)

### PROJECT-4-REJOY-main (Rejoy)
**Type**: Static HTML Website  
**Framework**: Vanilla JS  
**Build Output**: Current directory (static files)

### PROJECT-5-Sundown-main (Sundown)
**Type**: Static HTML Website  
**Framework**: Vanilla JS  
**Build Output**: Current directory (static files)

### RAY-BAN-REDESIGN-main
**Type**: Static HTML Website  
**Framework**: Vanilla JS with custom fonts  
**Build Output**: Current directory (static files)

### Sneakers-Store-Ecommerce-main
**Type**: Static HTML Website  
**Framework**: Vanilla JS Ecommerce  
**Build Output**: Current directory (static files)

### Tiny-todos-main
**Type**: React + Vite Application  
**Framework**: React 18 with Vite, Tailwind CSS, Framer Motion  
**Build Output**: `dist` directory  
**Special Note**: This is the only project that requires a build step

---

## 🚀 Netlify Dashboard Configuration

### For Static Projects (PROJECT-3, 4, 5, Ray-Ban, Sneakers)

Use these settings in the Netlify dashboard for each project:

#### PROJECT-3-DUO-main
```yaml
Site Name: project-3-duo-studio
Base Directory: [LEAVE EMPTY]
Package Directory: PROJECT-3-DUO-main
Build Command: npm run build:project-3
Publish Directory: PROJECT-3-DUO-main
```

#### PROJECT-4-REJOY-main
```yaml
Site Name: project-4-rejoy
Base Directory: [LEAVE EMPTY]
Package Directory: PROJECT-4-REJOY-main
Build Command: npm run build:project-4
Publish Directory: PROJECT-4-REJOY-main
```

#### PROJECT-5-Sundown-main
```yaml
Site Name: project-5-sundown
Base Directory: [LEAVE EMPTY]
Package Directory: PROJECT-5-Sundown-main
Build Command: npm run build:project-5
Publish Directory: PROJECT-5-Sundown-main
```

#### RAY-BAN-REDESIGN-main
```yaml
Site Name: ray-ban-redesign
Base Directory: [LEAVE EMPTY]
Package Directory: RAY-BAN-REDESIGN-main
Build Command: npm run build:ray-ban
Publish Directory: RAY-BAN-REDESIGN-main
```

#### Sneakers-Store-Ecommerce-main
```yaml
Site Name: sneakers-store-ecommerce
Base Directory: [LEAVE EMPTY]
Package Directory: Sneakers-Store-Ecommerce-main
Build Command: npm run build:sneakers
Publish Directory: Sneakers-Store-Ecommerce-main
```

### For React/Vite Project (Tiny-todos)

#### Tiny-todos-main
```yaml
Site Name: tiny-todos-app
Base Directory: [LEAVE EMPTY]
Package Directory: Tiny-todos-main
Build Command: npm run build:tiny-todos
Publish Directory: Tiny-todos-main/dist
Environment Variables:
  - NODE_VERSION: 18
```

---

## 📋 Quick Deployment Checklist

### Step 1: Push to GitHub
```bash
git add .
git commit -m "Add Netlify configuration for all projects"
git push origin main
```

### Step 2: Create Netlify Sites

For each project, repeat these steps:

1. **Go to Netlify Dashboard**: https://app.netlify.com
2. **Click**: "Add new site" → "Import an existing project"
3. **Select**: Your Git provider (GitHub)
4. **Choose**: WEB_WORKS repository
5. **Configure**: Use the settings from the tables above
6. **Deploy**: Click "Deploy site"

### Step 3: Configure Custom Domains

After each site deploys successfully:

1. Go to **Site settings** → **Domain management**
2. Click **Add a domain**
3. Enter your custom domain
4. Configure DNS records as instructed by Netlify

---

## 🎯 Build Commands Reference

All build commands are defined in root `package.json`:

```bash
# Build individual projects
npm run build:project-3     # Duo Studio
npm run build:project-4     # Rejoy
npm run build:project-5     # Sundown
npm run build:ray-ban       # Ray-Ban Redesign
npm run build:sneakers      # Sneakers Store
npm run build:tiny-todos    # Tiny Todos (React/Vite)

# Development servers
npm run dev:project-3       # Runs on port 3002
npm run dev:project-4       # Runs on port 3003
npm run dev:project-5       # Runs on port 3004
npm run dev:ray-ban         # Runs on port 3005
npm run dev:sneakers        # Runs on port 3006
npm run dev:tiny-todos      # Runs on port 3007

# Install all dependencies
npm run install:all
```

---

## 🔧 netlify.toml Configuration Details

### Static Sites Configuration
All static projects (PROJECT-3, 4, 5, Ray-Ban, Sneakers) use this pattern:

```toml
[build]
  publish = "."                    # Publish from current directory
  command = "echo 'Static site'"   # No build needed

[build.ignore]
  # Only rebuild when this project changes
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- [PROJECT-DIR]"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200                     # SPA redirect support
```

### React/Vite Configuration (Tiny-todos)

```toml
[build]
  publish = "dist"                 # Vite outputs to dist
  command = "npm run build"        # Runs vite build

[build.ignore]
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- Tiny-todos-main"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[build.environment]
  NODE_VERSION = "18"              # Required Node version
```

---

## 📊 Deployment Summary Table

| Project | Type | Build Time | Publish Dir | Port | Status |
|---------|------|------------|-------------|------|--------|
| PROJECT-1 | Static (Built) | ~30s | `public` | 3000 | ✅ Configured |
| PROJECT-2 | Static HTML | ~5s | `.` | 3001 | ✅ Configured |
| PROJECT-3 | Static HTML | ~5s | `.` | 3002 | ✅ Ready |
| PROJECT-4 | Static HTML | ~5s | `.` | 3003 | ✅ Ready |
| PROJECT-5 | Static HTML | ~5s | `.` | 3004 | ✅ Ready |
| Ray-Ban | Static HTML | ~5s | `.` | 3005 | ✅ Ready |
| Sneakers | Static HTML | ~5s | `.` | 3006 | ✅ Ready |
| Tiny-todos | React/Vite | ~45s | `dist` | 3007 | ✅ Ready |

---

## 🎨 Domain Mapping Template

Prepare your custom domains:

| Project | Suggested Domain | Netlify Subdomain |
|---------|------------------|-------------------|
| Duo Studio | duo-studio.yoursite.com | project-3-duo-studio.netlify.app |
| Rejoy | rejoy.yoursite.com | project-4-rejoy.netlify.app |
| Sundown | sundown.yoursite.com | project-5-sundown.netlify.app |
| Ray-Ban | ray-ban.yoursite.com | ray-ban-redesign.netlify.app |
| Sneakers | sneakers.yoursite.com | sneakers-store.netlify.app |
| Tiny-todos | todos.yoursite.com | tiny-todos-app.netlify.app |

---

## 🔍 Testing Before Deployment

Test each project locally before deploying:

```bash
# Test PROJECT-3
cd PROJECT-3-DUO-main
npm install
npm run dev
# Visit: http://localhost:3002

# Test PROJECT-4
cd ../PROJECT-4-REJOY-main
npm install
npm run dev
# Visit: http://localhost:3003

# Test PROJECT-5
cd ../PROJECT-5-Sundown-main
npm install
npm run dev
# Visit: http://localhost:3004

# Test Ray-Ban
cd ../RAY-BAN-REDESIGN-main
npm install
npm run dev
# Visit: http://localhost:3005

# Test Sneakers
cd ../Sneakers-Store-Ecommerce-main
npm install
npm run dev
# Visit: http://localhost:3006

# Test Tiny-todos
cd ../Tiny-todos-main
npm install
npm run dev
# Visit: http://localhost:5173 (Vite default)
```

---

## 🚨 Troubleshooting

### Static Sites Not Loading?
1. Check that `index.html` exists in the project root
2. Verify Publish Directory is set to the project name (not `public`)
3. Check redirects are configured for SPA behavior

### Tiny-todos Build Failing?
1. Ensure Node version is 18 or higher
2. Check that `vite.config.js` exists
3. Verify all dependencies in `package.json` are correct
4. Try local build first: `npm run build`

### Build.ignore Not Working?
1. Verify the directory path matches exactly
2. Check that you're using `--` before the directory name
3. Test locally: `git diff HEAD~1 HEAD -- PROJECT-NAME`

### Fonts Not Loading?
1. Check font files are in the correct directory
2. Verify font paths in CSS are relative
3. Ensure fonts are not in `.gitignore`

---

## ✨ Advanced Configuration

### Environment Variables per Project

For projects needing API keys or environment variables:

```bash
# In Netlify Dashboard for each site
Site Settings → Environment variables → Add variable

# Example for Tiny-todos (if needed)
VITE_API_URL=https://api.example.com
VITE_APP_NAME=Tiny Todos
```

### Custom Headers

Add to any `netlify.toml`:

```toml
[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
```

### Build Plugins

For optimization, add to `netlify.toml`:

```toml
[[plugins]]
  package = "@netlify/plugin-lighthouse"

[[plugins]]
  package = "netlify-plugin-cache"
```

---

## 📈 Performance Tips

### For All Static Sites
1. **Enable Asset Optimization** in Netlify dashboard
2. **Enable Netlify CDN** (automatic)
3. **Compress images** before deployment
4. **Minify CSS/JS** if not already minified

### For Tiny-todos (React/Vite)
1. **Code Splitting**: Already handled by Vite
2. **Lazy Loading**: Use React.lazy() for routes
3. **Bundle Analysis**: Run `npm run build -- --mode production`
4. **Tree Shaking**: Vite handles this automatically

---

## 🎉 Deployment Order Recommendation

Deploy in this order to test the setup incrementally:

1. ✅ **PROJECT-3-DUO-main** (Simple static site)
2. ✅ **PROJECT-4-REJOY-main** (Simple static site)
3. ✅ **PROJECT-5-Sundown-main** (Simple static site)
4. ✅ **RAY-BAN-REDESIGN-main** (Custom fonts)
5. ✅ **Sneakers-Store-Ecommerce-main** (Ecommerce features)
6. ✅ **Tiny-todos-main** (React/Vite - most complex)

---

## 💡 Quick Commands

```bash
# Check if all files are committed
git status

# View root package.json scripts
cat package.json | grep "build:"

# Test all netlify.toml files exist
ls -la PROJECT-*/netlify.toml */netlify.toml

# Install dependencies for all projects
npm run install:all

# Build all projects (test locally)
npm run build:project-3
npm run build:project-4
npm run build:project-5
npm run build:ray-ban
npm run build:sneakers
npm run build:tiny-todos
```

---

## 📝 Post-Deployment Checklist

After deploying each site:

- [ ] Site builds successfully without errors
- [ ] Site loads correctly at Netlify subdomain
- [ ] All images and assets load properly
- [ ] Fonts display correctly
- [ ] Navigation works (all links functional)
- [ ] Mobile responsive design works
- [ ] Custom domain configured (if applicable)
- [ ] HTTPS certificate active
- [ ] build.ignore works (test by pushing a change to another project)
- [ ] Analytics configured (optional)
- [ ] Form submissions work (if applicable)

---

## 🔗 Useful Resources

- [Netlify Build Plugins](https://www.netlify.com/products/build/plugins/)
- [Vite Deployment](https://vitejs.dev/guide/static-deploy.html#netlify)
- [React Performance](https://react.dev/learn/render-and-commit)
- [Netlify Forms](https://docs.netlify.com/forms/setup/)

---

**Need Help?** 
- Check build logs in Netlify dashboard
- Review `NETLIFY_MONOREPO_SETUP.md` for detailed guidance
- Test locally before deploying
- Check Netlify Status: https://www.netlifystatus.com/

🎉 **Happy Deploying!**
