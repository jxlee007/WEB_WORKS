# 🎴 Quick Reference Card - Netlify Monorepo

**Print or keep this handy while deploying!**

---

## 📋 6 Projects - Copy & Paste Ready

### 1️⃣ PROJECT-3-DUO-main
```
Package Directory: PROJECT-3-DUO-main
Build Command: npm run build:project-3
Publish Directory: PROJECT-3-DUO-main
Base Directory: [EMPTY]
```
**Type**: Static HTML | **Port**: 3002 | **Build Time**: ~10s

---

### 2️⃣ PROJECT-4-REJOY-main
```
Package Directory: PROJECT-4-REJOY-main
Build Command: npm run build:project-4
Publish Directory: PROJECT-4-REJOY-main
Base Directory: [EMPTY]
```
**Type**: Static HTML | **Port**: 3003 | **Build Time**: ~10s

---

### 3️⃣ PROJECT-5-Sundown-main
```
Package Directory: PROJECT-5-Sundown-main
Build Command: npm run build:project-5
Publish Directory: PROJECT-5-Sundown-main
Base Directory: [EMPTY]
```
**Type**: Static HTML | **Port**: 3004 | **Build Time**: ~10s

---

### 4️⃣ RAY-BAN-REDESIGN-main
```
Package Directory: RAY-BAN-REDESIGN-main
Build Command: npm run build:ray-ban
Publish Directory: RAY-BAN-REDESIGN-main
Base Directory: [EMPTY]
```
**Type**: Static HTML + Fonts | **Port**: 3005 | **Build Time**: ~10s

---

### 5️⃣ Sneakers-Store-Ecommerce-main
```
Package Directory: Sneakers-Store-Ecommerce-main
Build Command: npm run build:sneakers
Publish Directory: Sneakers-Store-Ecommerce-main
Base Directory: [EMPTY]
```
**Type**: Static HTML | **Port**: 3006 | **Build Time**: ~10s

---

### 6️⃣ Tiny-todos-main ⚛️
```
Package Directory: Tiny-todos-main
Build Command: npm run build:tiny-todos
Publish Directory: Tiny-todos-main/dist
Base Directory: [EMPTY]
Environment Variables: NODE_VERSION=18
```
**Type**: React + Vite | **Port**: 5173 | **Build Time**: ~45s

---

## ⚡ Quick Commands

### Test Locally (from root)
```bash
npm run dev:project-3      # http://localhost:3002
npm run dev:project-4      # http://localhost:3003
npm run dev:project-5      # http://localhost:3004
npm run dev:ray-ban        # http://localhost:3005
npm run dev:sneakers       # http://localhost:3006
npm run dev:tiny-todos     # http://localhost:5173
```

### Build (from root)
```bash
npm run build:project-3
npm run build:project-4
npm run build:project-5
npm run build:ray-ban
npm run build:sneakers
npm run build:tiny-todos
```

---

## ✅ Pre-Deployment Checklist

For EACH project before deploying:

- [ ] Files committed to Git
- [ ] Pushed to remote repository
- [ ] `package.json` exists in project
- [ ] `netlify.toml` exists in project
- [ ] Tested locally with `npm run dev:[project]`
- [ ] No console errors when running
- [ ] All assets loading correctly

---

## 🎯 Netlify Dashboard Steps

1. **Login**: https://app.netlify.com
2. **Click**: "Add new site" → "Import an existing project"
3. **Connect**: Your Git provider
4. **Select**: WEB_WORKS repository
5. **Paste**: Configuration from above ☝️
6. **Deploy**: Click "Deploy site"
7. **Wait**: For build to complete
8. **Test**: Click on the deployed URL
9. **Domain**: (Optional) Add custom domain

---

## 🚨 Important Notes

### Always Keep Base Directory EMPTY
❌ **Wrong**: `Base Directory: PROJECT-3-DUO-main`  
✅ **Right**: `Base Directory: [leave empty]`

### Package Directory is KEY
This tells Netlify where your project lives in the monorepo.

### Build Commands Use Root Scripts
All build commands run from repository root, not project directory.

---

## 🎨 Project Overview

| # | Name | Framework | Build Output |
|---|------|-----------|--------------|
| 3 | Duo Studio | Vanilla JS | `.` (root) |
| 4 | Rejoy | Vanilla JS | `.` (root) |
| 5 | Sundown | Vanilla JS | `.` (root) |
| 6 | Ray-Ban | Vanilla JS | `.` (root) |
| 7 | Sneakers | Vanilla JS | `.` (root) |
| 8 | Tiny-todos | React/Vite | `dist/` |

---

## 🔄 After First Deploy

1. **Check Deploy Log** for any errors
2. **Visit Site** at provided URL
3. **Test All Pages** and links
4. **Check Mobile** responsiveness
5. **Verify Assets** (images, fonts)
6. **Configure Domain** (optional)
7. **Enable HTTPS** (automatic)

---

## 💡 Pro Tips

### Tip 1: Deploy Simple First
Start with PROJECT-3 (simplest) before Tiny-todos (React).

### Tip 2: Build Times
- Static sites: 10-15 seconds
- React/Vite: 45-60 seconds

### Tip 3: Build Minutes
Free tier = 300 minutes/month  
Static sites use minimal minutes!

### Tip 4: Caching Works
Second builds are faster due to caching.

### Tip 5: Build.ignore Magic
Projects only rebuild when their files change. 🎯

---

## 📞 Need Help?

1. **Check Build Logs** in Netlify dashboard
2. **Test Locally** with `npm run dev:[project]`
3. **Review Docs**: `NETLIFY_MONOREPO_SETUP.md`
4. **Read Guide**: `DEPLOYMENT_GUIDE_REMAINING_PROJECTS.md`
5. **Check Matrix**: `PROJECTS_CONFIGURATION_MATRIX.md`

---

## 🎉 Deploy Order (Recommended)

```
1. PROJECT-3 (Duo Studio)     - Simplest
2. PROJECT-4 (Rejoy)          - Simple
3. PROJECT-5 (Sundown)        - Simple
4. Sneakers Store             - Simple
5. Ray-Ban Redesign           - Custom Fonts
6. Tiny-todos                 - React Build
```

---

**Keep this card handy while deploying! 🎴**

**Status**: ✅ All projects configured and ready  
**Next**: Deploy to Netlify dashboard  
**Goal**: 6 live sites! 🚀

---

## 📊 Progress Tracker

Track your deployment progress:

- [ ] PROJECT-3-DUO-main deployed
- [ ] PROJECT-4-REJOY-main deployed
- [ ] PROJECT-5-Sundown-main deployed
- [ ] RAY-BAN-REDESIGN-main deployed
- [ ] Sneakers-Store-Ecommerce-main deployed
- [ ] Tiny-todos-main deployed

**All Done? Celebrate! 🎊**
