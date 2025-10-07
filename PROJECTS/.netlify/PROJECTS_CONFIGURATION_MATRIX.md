# Complete Projects Configuration Matrix

Quick reference for all 8 projects in the WEB_WORKS monorepo.

## 📊 Complete Configuration Table

| Project | Type | Framework | Build Time | Build Output | Dev Port | Node Version | Status |
|---------|------|-----------|------------|--------------|----------|--------------|--------|
| PROJECT-1 | Built Site | Custom/Webpack | ~30s | `public/` | 3000 | 14+ | ✅ Deployed |
| PROJECT-2 | Static HTML | Vanilla JS | ~5s | `.` (root) | 3001 | 14+ | ✅ Ready |
| PROJECT-3-DUO | Static HTML | Vanilla JS | ~5s | `.` (root) | 3002 | 14+ | ✅ Ready |
| PROJECT-4-REJOY | Static HTML | Vanilla JS | ~5s | `.` (root) | 3003 | 14+ | ✅ Ready |
| PROJECT-5-Sundown | Static HTML | Vanilla JS | ~5s | `.` (root) | 3004 | 14+ | ✅ Ready |
| Ray-Ban Redesign | Static HTML | Vanilla JS + Fonts | ~5s | `.` (root) | 3005 | 14+ | ✅ Ready |
| Sneakers Store | Static HTML | Vanilla JS | ~5s | `.` (root) | 3006 | 14+ | ✅ Ready |
| Tiny-todos | SPA | React 18 + Vite | ~45s | `dist/` | 5173* | 18+ | ✅ Ready |

_* Tiny-todos uses Vite's default port (5173) for dev server_

---

## 🎯 Netlify Dashboard Settings

### Copy-Paste Ready Configuration

#### PROJECT-1 (Already Deployed)
```
Site Name: project-1-portfolio
Base Directory: [EMPTY]
Package Directory: PROJECT-1
Build Command: npm run build:project-1
Publish Directory: PROJECT-1/public
Node Version: 14
```

#### PROJECT-2
```
Site Name: project-2-static
Base Directory: [EMPTY]
Package Directory: PROJECT-2
Build Command: npm run build:project-2
Publish Directory: PROJECT-2
Node Version: 14
```

#### PROJECT-3-DUO-main
```
Site Name: project-3-duo-studio
Base Directory: [EMPTY]
Package Directory: PROJECT-3-DUO-main
Build Command: npm run build:project-3
Publish Directory: PROJECT-3-DUO-main
Node Version: 14
```

#### PROJECT-4-REJOY-main
```
Site Name: project-4-rejoy
Base Directory: [EMPTY]
Package Directory: PROJECT-4-REJOY-main
Build Command: npm run build:project-4
Publish Directory: PROJECT-4-REJOY-main
Node Version: 14
```

#### PROJECT-5-Sundown-main
```
Site Name: project-5-sundown
Base Directory: [EMPTY]
Package Directory: PROJECT-5-Sundown-main
Build Command: npm run build:project-5
Publish Directory: PROJECT-5-Sundown-main
Node Version: 14
```

#### RAY-BAN-REDESIGN-main
```
Site Name: ray-ban-redesign
Base Directory: [EMPTY]
Package Directory: RAY-BAN-REDESIGN-main
Build Command: npm run build:ray-ban
Publish Directory: RAY-BAN-REDESIGN-main
Node Version: 14
```

#### Sneakers-Store-Ecommerce-main
```
Site Name: sneakers-store-ecommerce
Base Directory: [EMPTY]
Package Directory: Sneakers-Store-Ecommerce-main
Build Command: npm run build:sneakers
Publish Directory: Sneakers-Store-Ecommerce-main
Node Version: 14
```

#### Tiny-todos-main (React + Vite)
```
Site Name: tiny-todos-app
Base Directory: [EMPTY]
Package Directory: Tiny-todos-main
Build Command: npm run build:tiny-todos
Publish Directory: Tiny-todos-main/dist
Node Version: 18
Environment Variables:
  NODE_VERSION=18
```

---

## 📦 Dependencies Overview

### Static HTML Projects (PROJECT-2 through Sneakers)
```json
{
  "devDependencies": {
    "live-server": "^1.2.2"
  }
}
```

### PROJECT-1 (Custom Build)
```json
{
  "devDependencies": {
    "live-server": "^1.2.2"
  },
  "scripts": {
    "build": "npm run copy-assets"
  }
}
```

### Tiny-todos (React + Vite)
```json
{
  "dependencies": {
    "framer-motion": "^11.0.28",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-icons": "^5.0.1",
    "react-select": "^5.8.0"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.2.1",
    "autoprefixer": "^10.4.19",
    "tailwindcss": "^3.4.3",
    "vite": "^5.2.0"
  }
}
```

---

## 🚀 Root Package.json Scripts

All projects can be built/run from the root:

### Build Commands
```bash
npm run build:project-1    # PROJECT-1
npm run build:project-2    # PROJECT-2
npm run build:project-3    # PROJECT-3-DUO-main
npm run build:project-4    # PROJECT-4-REJOY-main
npm run build:project-5    # PROJECT-5-Sundown-main
npm run build:ray-ban      # RAY-BAN-REDESIGN-main
npm run build:sneakers     # Sneakers-Store-Ecommerce-main
npm run build:tiny-todos   # Tiny-todos-main
```

### Development Servers
```bash
npm run dev:project-1      # http://localhost:3000
npm run dev:project-2      # http://localhost:3001
npm run dev:project-3      # http://localhost:3002
npm run dev:project-4      # http://localhost:3003
npm run dev:project-5      # http://localhost:3004
npm run dev:ray-ban        # http://localhost:3005
npm run dev:sneakers       # http://localhost:3006
npm run dev:tiny-todos     # http://localhost:5173 (Vite default)
```

### Batch Operations
```bash
npm run install:all        # Install dependencies for all projects
```

---

## 🔧 netlify.toml Patterns

### Pattern 1: Static HTML Sites (Most Projects)
```toml
[build]
  publish = "."
  command = "echo 'Static site - no build step required'"

[build.ignore]
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- [PROJECT-DIR]"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

**Used by**: PROJECT-2, PROJECT-3, PROJECT-4, PROJECT-5, Ray-Ban, Sneakers

### Pattern 2: Built Static Site (PROJECT-1)
```toml
[build]
  publish = "public"
  command = "npm run build"

[build.ignore]
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- PROJECT-1"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

**Used by**: PROJECT-1

### Pattern 3: React/Vite SPA (Tiny-todos)
```toml
[build]
  publish = "dist"
  command = "npm run build"

[build.ignore]
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- Tiny-todos-main"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200

[build.environment]
  NODE_VERSION = "18"
```

**Used by**: Tiny-todos-main

---

## 🎨 Project Features Breakdown

### PROJECT-1: Portfolio
- Custom build process
- Source files in `src/`
- Output to `public/`
- Custom fonts and icons
- Multiple pages

### PROJECT-2: Static Site
- Simple HTML/CSS/JS
- Image gallery
- Multiple product pages
- Contact forms

### PROJECT-3-DUO: Duo Studio
- Animated landing page
- Custom marquee effects
- Modern design
- Custom fonts in `/fonts`

### PROJECT-4-REJOY: Rejoy
- Minimalist design
- Single-page layout
- Media-heavy content

### PROJECT-5-Sundown: Sundown
- Interactive website
- Custom animations
- Font directory included
- Responsive design

### Ray-Ban Redesign
- E-commerce style
- Custom fonts (Gilroy, Kajiro)
- Product showcase
- Mobile responsive
- Sample implementations

### Sneakers Store
- E-commerce template
- Product catalog
- Shopping cart interface
- Image gallery

### Tiny-todos: React App
- Modern React 18
- Vite build system
- Tailwind CSS styling
- Framer Motion animations
- Component-based architecture
- Production optimized

---

## 📈 Expected Build Times

| Project | Local Build | Netlify Build | Notes |
|---------|-------------|---------------|-------|
| PROJECT-1 | 5-10s | 30-45s | File copying + install |
| PROJECT-2 | <1s | 10-15s | Static, minimal |
| PROJECT-3 | <1s | 10-15s | Static, minimal |
| PROJECT-4 | <1s | 10-15s | Static, minimal |
| PROJECT-5 | <1s | 10-15s | Static, minimal |
| Ray-Ban | <1s | 10-15s | Static with fonts |
| Sneakers | <1s | 10-15s | Static, minimal |
| Tiny-todos | 10-15s | 45-60s | Full React build + deps |

---

## 🌐 Suggested Domain Structure

### Option 1: Subdomains
```
project1.yoursite.com    → PROJECT-1
project2.yoursite.com    → PROJECT-2
duo.yoursite.com         → PROJECT-3
rejoy.yoursite.com       → PROJECT-4
sundown.yoursite.com     → PROJECT-5
rayban.yoursite.com      → Ray-Ban
sneakers.yoursite.com    → Sneakers
todos.yoursite.com       → Tiny-todos
```

### Option 2: Separate Domains
```
myportfolio.com          → PROJECT-1
mystatic.com             → PROJECT-2
duostudio.com            → PROJECT-3
rejoyapp.com             → PROJECT-4
sundownstudio.com        → PROJECT-5
raybanredesign.com       → Ray-Ban
sneakerstore.com         → Sneakers
tinytodos.app            → Tiny-todos
```

### Option 3: Netlify Subdomains (Default)
```
project-1-yourname.netlify.app
project-2-yourname.netlify.app
project-3-duo-studio.netlify.app
project-4-rejoy.netlify.app
project-5-sundown.netlify.app
ray-ban-redesign.netlify.app
sneakers-store.netlify.app
tiny-todos-app.netlify.app
```

---

## 🔍 File Structure Comparison

### Static Projects Structure
```
PROJECT-NAME/
├── index.html
├── style.css
├── script.js
├── package.json     ← Created
├── netlify.toml     ← Created
├── README.md
└── assets/
    ├── images/
    └── fonts/
```

### PROJECT-1 Structure
```
PROJECT-1/
├── package.json
├── netlify.toml
├── src/
│   ├── index.html
│   ├── assets/
│   └── scripts/
└── public/          ← Build output
```

### Tiny-todos Structure
```
Tiny-todos-main/
├── package.json
├── netlify.toml     ← Created
├── vite.config.js
├── tailwind.config.js
├── index.html
├── src/
│   ├── App.jsx
│   ├── main.jsx
│   └── components/
└── dist/            ← Build output
```

---

## ✅ Verification Checklist

Before deploying each project, verify:

- [ ] `package.json` exists
- [ ] `netlify.toml` exists
- [ ] `index.html` exists
- [ ] All assets/images are committed
- [ ] No absolute paths in CSS/JS
- [ ] Fonts are in repository (not CDN only)
- [ ] Build command works locally
- [ ] Dev server runs without errors
- [ ] No console errors in browser
- [ ] Responsive design works
- [ ] All links are relative or valid

---

## 🎯 Deployment Priority

### Phase 1: Low Risk (Start Here)
1. ✅ PROJECT-2 (Simple static)
2. ✅ PROJECT-3-DUO (Static with animations)
3. ✅ PROJECT-5-Sundown (Static)

### Phase 2: Medium Complexity
4. ✅ PROJECT-4-REJOY (Media-heavy)
5. ✅ Sneakers-Store (Ecommerce template)

### Phase 3: Higher Complexity
6. ✅ Ray-Ban Redesign (Custom fonts + ecommerce)
7. ✅ Tiny-todos (React + Vite build)

---

## 💾 Size Estimates

| Project | Source Size | Build Size | Assets |
|---------|-------------|------------|--------|
| PROJECT-1 | ~5 MB | ~3 MB | Images, fonts |
| PROJECT-2 | ~50 MB | ~50 MB | Many images |
| PROJECT-3 | ~2 MB | ~2 MB | Minimal |
| PROJECT-4 | ~5 MB | ~5 MB | Media files |
| PROJECT-5 | ~3 MB | ~3 MB | Fonts, images |
| Ray-Ban | ~8 MB | ~8 MB | Images, fonts |
| Sneakers | ~2 MB | ~2 MB | Product images |
| Tiny-todos | ~200 KB | ~150 KB | React bundle |

---

## 🔄 Git Workflow

```bash
# Add all new files
git add .

# Commit configurations
git commit -m "Add Netlify config for all remaining projects"

# Push to trigger deployments
git push origin main

# Each configured Netlify site will detect changes
# Only projects with changes will rebuild (thanks to build.ignore)
```

---

## 🎉 Success Metrics

After all deployments:
- [ ] 8 sites live on Netlify
- [ ] Each site has unique URL
- [ ] HTTPS enabled on all sites
- [ ] Builds only trigger for relevant changes
- [ ] All sites load in < 3 seconds
- [ ] No 404 errors
- [ ] Custom domains configured (optional)
- [ ] Mobile responsive verified

---

**Last Updated**: Configuration complete for all 8 projects  
**Next Step**: Deploy each project to Netlify dashboard using the settings above
