# Netlify Monorepo - Visual Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        WEB_WORKS Repository                      │
│                        (Single Git Repo)                         │
└─────────────────────────────────────────────────────────────────┘
                                 │
                                 │
                    ┌────────────┴────────────┐
                    │   PROJECTS (Root)       │
                    │   package.json          │
                    │   - Build scripts       │
                    │   - Workspaces config   │
                    └────────────┬────────────┘
                                 │
                ┌────────────────┼────────────────┐
                │                │                │
       ┌────────▼─────┐  ┌──────▼──────┐  ┌─────▼──────┐
       │  PROJECT-1   │  │  PROJECT-2  │  │ PROJECT-3  │  ...
       │              │  │             │  │            │
       │ package.json │  │package.json │  │package.json│
       │ netlify.toml │  │netlify.toml │  │netlify.toml│
       │ /public      │  │ index.html  │  │ /dist      │
       └──────┬───────┘  └──────┬──────┘  └─────┬──────┘
              │                 │                │
              │                 │                │
    ┌─────────▼──────┐ ┌────────▼─────┐ ┌───────▼────────┐
    │ Netlify Site 1 │ │Netlify Site 2│ │Netlify Site 3  │
    │                │ │              │ │                │
    │ Package Dir:   │ │Package Dir:  │ │Package Dir:    │
    │  PROJECT-1     │ │ PROJECT-2    │ │ PROJECT-3      │
    │                │ │              │ │                │
    │ Build Cmd:     │ │Build Cmd:    │ │Build Cmd:      │
    │  npm run       │ │ npm run      │ │ npm run        │
    │  build:p1      │ │ build:p2     │ │ build:p3       │
    │                │ │              │ │                │
    │ Publish:       │ │Publish:      │ │Publish:        │
    │  PROJECT-1/    │ │ PROJECT-2    │ │ PROJECT-3/dist │
    │  public        │ │              │ │                │
    └────────┬───────┘ └──────┬───────┘ └────────┬───────┘
             │                │                   │
             │                │                   │
    ┌────────▼────┐  ┌────────▼────┐    ┌────────▼────┐
    │  Domain 1   │  │  Domain 2   │    │  Domain 3   │
    │             │  │             │    │             │
    │ project1.com│  │project2.com │    │ project3.com│
    └─────────────┘  └─────────────┘    └─────────────┘
```

## 🔄 Build Workflow

```
┌──────────────────────────────────────────────────────────────┐
│ 1. Developer pushes changes to Git repository               │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│ 2. Netlify detects commit for each configured site          │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│ 3. build.ignore checks if files changed in project dir      │
│    git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- DIR   │
└────────────────────────┬─────────────────────────────────────┘
                         │
                ┌────────┴────────┐
                │                 │
                ▼                 ▼
        ┌───────────────┐  ┌──────────────┐
        │ Changes Found │  │ No Changes   │
        │ Exit Code: 1  │  │ Exit Code: 0 │
        └───────┬───────┘  └───────┬──────┘
                │                  │
                ▼                  ▼
        ┌───────────────┐  ┌──────────────┐
        │ BUILD RUNS    │  │ BUILD SKIPPED│
        └───────┬───────┘  └──────────────┘
                │
                ▼
┌──────────────────────────────────────────────────────────────┐
│ 4. Run build command from root:                             │
│    npm run build:project-X                                   │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│ 5. Deploy files from publish directory                      │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│ 6. Site live at custom domain                               │
└──────────────────────────────────────────────────────────────┘
```

## 📊 Configuration Mapping

| Component | Location | Purpose |
|-----------|----------|---------|
| **Root package.json** | `/PROJECTS/package.json` | Orchestrate builds for all projects |
| **Project netlify.toml** | `/PROJECT-X/netlify.toml` | Build config + conditional logic |
| **Package Directory** | Netlify UI Setting | Tell Netlify where project lives |
| **Base Directory** | Netlify UI (empty) | Use repo root for dependencies |
| **Build Command** | Netlify UI | Execute root script for project |
| **Publish Directory** | Netlify UI | Where built files are located |

## 🎯 Key Principles

### 1. One Repository, Multiple Sites
```
1 Git Repo → N Netlify Sites → N Custom Domains
```

### 2. Independent Builds
```
Change in PROJECT-1 → Only PROJECT-1 rebuilds
Change in PROJECT-2 → Only PROJECT-2 rebuilds
```

### 3. Shared Root, Isolated Projects
```
Root: Common dependencies & build orchestration
Projects: Independent configurations & outputs
```

## 🔐 Security Best Practices

```
┌─────────────────────────────────────────┐
│ Environment Variables per Site          │
├─────────────────────────────────────────┤
│ Site 1:                                 │
│   API_KEY_1=xxxxx                       │
│   DATABASE_URL_1=xxxxx                  │
│                                         │
│ Site 2:                                 │
│   API_KEY_2=yyyyy                       │
│   DATABASE_URL_2=yyyyy                  │
│                                         │
│ ✅ Isolated & Secure                    │
└─────────────────────────────────────────┘
```

## ⚡ Performance Optimization

### Build Caching
- Netlify caches `node_modules` between builds
- Each site has independent cache
- Speeds up builds by 50-70%

### Conditional Builds
- Skip unnecessary builds with `build.ignore`
- Saves build minutes
- Faster deployment times

### Concurrent Deployments
- All projects can deploy simultaneously
- No blocking between projects
- Parallel CI/CD pipeline

## 🎨 Deploy Contexts

```
Branch: main
├── Site 1 (Production) → project1.com
├── Site 2 (Production) → project2.com
└── Site 3 (Production) → project3.com

Branch: staging
├── Site 1 (Staging) → staging-project1.netlify.app
├── Site 2 (Staging) → staging-project2.netlify.app
└── Site 3 (Staging) → staging-project3.netlify.app

Pull Request #42
├── Site 1 (Preview) → deploy-preview-42--project1.netlify.app
├── Site 2 (Preview) → deploy-preview-42--project2.netlify.app
└── Site 3 (Preview) → deploy-preview-42--project3.netlify.app
```

## 📈 Scaling Considerations

### Adding New Projects
1. Add to root `package.json` workspaces
2. Create build script: `build:project-N`
3. Add `netlify.toml` to project
4. Create new Netlify site
5. Configure with package directory

### Removing Projects
1. Delete from Netlify dashboard
2. Remove from root `package.json`
3. Delete project directory
4. Update documentation

### Team Collaboration
- Each project can have different team members
- Site-level access control in Netlify
- Separate deploy notifications per project
- Individual deploy hooks for automation

---

**Legend:**
- 📁 Directory
- 📄 File
- 🌐 Netlify Site
- 🔗 Custom Domain
- ⚙️ Configuration
- 🚀 Deployment
