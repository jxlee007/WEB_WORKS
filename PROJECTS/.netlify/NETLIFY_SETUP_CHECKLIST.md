# Quick Start Checklist for Netlify Monorepo

Use this checklist to quickly set up each project in your monorepo.

## 📋 For Each Project

### Project: PROJECT-1
- [x] Create `netlify.toml` with build.ignore
- [x] Configure `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `PROJECT-1`
  - Build command: `npm run build:project-1`
  - Publish directory: `PROJECT-1/public`
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

### Project: PROJECT-2
- [x] Create `netlify.toml` with build.ignore
- [x] Configure `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `PROJECT-2`
  - Build command: `npm run build:project-2`
  - Publish directory: `PROJECT-2`
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

### Project: PROJECT-3-DUO-main
- [x] Create `netlify.toml` with build.ignore
- [x] Check/update `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `PROJECT-3-DUO-main`
  - Build command: `npm run build:project-3`
  - Publish directory: `PROJECT-3-DUO-main`
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

### Project: PROJECT-4-REJOY-main
- [x] Create `netlify.toml` with build.ignore
- [x] Check/update `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `PROJECT-4-REJOY-main`
  - Build command: `npm run build:project-4`
  - Publish directory: `PROJECT-4-REJOY-main`
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

### Project: PROJECT-5-Sundown-main
- [x] Create `netlify.toml` with build.ignore
- [x] Check/update `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `PROJECT-5-Sundown-main`
  - Build command: `npm run build:project-5`
  - Publish directory: `PROJECT-5-Sundown-main`
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

### Project: RAY-BAN-REDESIGN-main
- [x] Create `netlify.toml` with build.ignore
- [x] Check/update `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `RAY-BAN-REDESIGN-main`
  - Build command: `npm run build:ray-ban`
  - Publish directory: `RAY-BAN-REDESIGN-main`
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

### Project: Sneakers-Store-Ecommerce-main
- [x] Create `netlify.toml` with build.ignore
- [x] Check/update `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `Sneakers-Store-Ecommerce-main`
  - Build command: `npm run build:sneakers`
  - Publish directory: `Sneakers-Store-Ecommerce-main`
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

### Project: Tiny-todos-main
- [x] Create `netlify.toml` with build.ignore
- [x] Check/update `package.json`
- [ ] Create Netlify site in dashboard
  - Site URL: _______________________
  - Custom Domain: _______________________
- [ ] Configure build settings:
  - Package directory: `Tiny-todos-main`
  - Build command: `npm run build:tiny-todos`
  - Publish directory: `Tiny-todos-main/dist`
  - Environment: NODE_VERSION=18
- [ ] Add custom domain
- [ ] Test deployment
- [ ] Configure environment variables (if needed)

## 🔑 Key Configuration Values

Remember these for **EVERY** project:

### In Netlify Dashboard:
1. **Base directory**: `[LEAVE EMPTY]`
2. **Package directory**: `[PROJECT-NAME]`
3. **Build command**: `npm run build:[project-name]`
4. **Publish directory**: `[PROJECT-NAME]/[build-output]`

### netlify.toml Template:
```toml
[build]
  publish = "[output-directory]"
  command = "npm run build"

[build.ignore]
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- [PROJECT-NAME]"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

## 🎯 Common Publish Directories by Framework

- **React/Vue/Angular**: `dist` or `build`
- **Next.js**: `out` or `.next`
- **Static HTML**: `.` (current directory)
- **Gatsby**: `public`
- **Vite**: `dist`
- **Webpack**: `dist` or `build`

## 📞 DNS Configuration Template

For each custom domain:

```
Type: CNAME
Name: www (or @)
Value: [your-site-name].netlify.app
TTL: 3600
```

## ✅ Final Verification

After setup, verify:
- [ ] All sites deploy successfully
- [ ] Custom domains resolve correctly
- [ ] HTTPS certificates are active
- [ ] Builds only trigger for relevant changes
- [ ] Environment variables are set (if needed)
- [ ] Redirects work as expected

## 🚀 Deployment Commands

```bash
# Manual deploy (if needed)
netlify deploy --filter [PROJECT-NAME] --prod

# Test build locally
cd [PROJECT-NAME]
npm run build

# Check build status
netlify status

# View site info
netlify sites:list
```
