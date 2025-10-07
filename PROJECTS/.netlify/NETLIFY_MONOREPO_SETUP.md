# Netlify Monorepo Setup Guide

Complete guide for hosting multiple website projects with specific domains from a single monorepo on Netlify.

## 📁 Project Structure

```
PROJECTS/
├── package.json                    # Root package.json with build scripts
├── PROJECT-1/
│   ├── package.json
│   ├── netlify.toml
│   └── public/                     # Build output
├── PROJECT-2/
│   ├── package.json
│   ├── netlify.toml
│   └── index.html                  # Static files
├── PROJECT-3-DUO-main/
├── PROJECT-4-REJOY-main/
├── PROJECT-5-Sundown-main/
├── RAY-BAN-REDESIGN-main/
├── Sneakers-Store-Ecommerce-main/
└── Tiny-todos-main/
```

## 🎯 Approach Overview

This setup uses **separate Netlify sites** for each project in the monorepo. Each site can have:
- ✅ Its own custom domain
- ✅ Independent build settings
- ✅ Unique environment variables
- ✅ Conditional builds (only rebuild when that project changes)

## 🚀 Step-by-Step Setup

### Step 1: Configure Root Package.json

✅ **Already Created**: `PROJECTS/package.json`

This file contains build scripts for each project:
```json
{
  "scripts": {
    "build:project-1": "cd PROJECT-1 && npm install && npm run build",
    "build:project-2": "cd PROJECT-2 && npm install && npm run build"
  }
}
```

### Step 2: Configure Each Project's netlify.toml

Each project has its own `netlify.toml` file with:
- Build command
- Publish directory
- **build.ignore** script for conditional builds

#### PROJECT-1 Example:
✅ **Already Configured**: `PROJECT-1/netlify.toml`
```toml
[build]
  publish = "public"
  command = "npm run build"

[build.ignore]
  # Only build if there are changes in the PROJECT-1 directory
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- PROJECT-1"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

#### PROJECT-2 Example:
✅ **Already Configured**: `PROJECT-2/netlify.toml`
```toml
[build]
  publish = "."
  command = "echo 'Static site - no build step required'"

[build.ignore]
  # Only build if there are changes in the PROJECT-2 directory
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- PROJECT-2"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### Step 3: Create Netlify Sites (For Each Project)

For **each project** you want to deploy, create a separate Netlify site:

#### 3.1 Create New Site
1. Log into [Netlify Dashboard](https://app.netlify.com)
2. Click **"Add new site"** → **"Import an existing project"**
3. Connect to your Git provider (GitHub/GitLab/Bitbucket)
4. Select your **WEB_WORKS** repository

#### 3.2 Configure Build Settings

**IMPORTANT**: Configure these settings carefully for each project:

##### For PROJECT-1:
```
Site name: project-1-yourname (or your preferred name)

Base directory: [LEAVE EMPTY]
  ↳ This allows Netlify to install dependencies from the root

Package directory: PROJECT-1
  ↳ This tells Netlify where to find your project files and netlify.toml

Build command: npm run build:project-1
  ↳ Uses the script from root package.json

Publish directory: PROJECT-1/public
  ↳ Path to the build output relative to repository root
```

##### For PROJECT-2:
```
Site name: project-2-yourname (or your preferred name)

Base directory: [LEAVE EMPTY]

Package directory: PROJECT-2

Build command: npm run build:project-2

Publish directory: PROJECT-2
  ↳ For static sites, publish the directory itself
```

#### 3.3 Deploy Settings Summary Table

| Project | Package Directory | Build Command | Publish Directory |
|---------|------------------|---------------|-------------------|
| PROJECT-1 | `PROJECT-1` | `npm run build:project-1` | `PROJECT-1/public` |
| PROJECT-2 | `PROJECT-2` | `npm run build:project-2` | `PROJECT-2` |
| PROJECT-3-DUO | `PROJECT-3-DUO-main` | `npm run build:project-3` | `PROJECT-3-DUO-main/dist` |
| PROJECT-4-REJOY | `PROJECT-4-REJOY-main` | `npm run build:project-4` | `PROJECT-4-REJOY-main/dist` |
| PROJECT-5-Sundown | `PROJECT-5-Sundown-main` | `npm run build:project-5` | `PROJECT-5-Sundown-main/dist` |

### Step 4: Configure Custom Domains

For each Netlify site, add your custom domain:

1. Navigate to **Site settings** → **Domain management**
2. Click **"Add a domain"**
3. Enter your domain (e.g., `project1.com`, `project2.com`)
4. Follow the DNS configuration instructions:
   - Add **A record** or **CNAME record** as instructed
   - Wait for DNS propagation (can take up to 48 hours)

#### Example DNS Configuration:
```
PROJECT-1 → www.yourproject1.com
  Type: CNAME
  Name: www
  Value: [your-netlify-site].netlify.app

PROJECT-2 → www.yourproject2.com
  Type: CNAME
  Name: www
  Value: [your-netlify-site].netlify.app
```

### Step 5: Enable Automatic Deployments

Each site will automatically deploy when you push changes to your repository, **but only if files in that project's directory changed** (thanks to `build.ignore`).

1. Go to **Site settings** → **Build & deploy**
2. Ensure **Continuous deployment** is enabled
3. Configure branch deploys if needed (e.g., `main` for production)

## 🎨 How build.ignore Works

The `build.ignore` command prevents unnecessary builds:

```toml
[build.ignore]
  command = "git diff --quiet $CACHED_COMMIT_REF $COMMIT_REF -- PROJECT-1"
```

**How it works:**
- `$CACHED_COMMIT_REF`: Last deployed commit
- `$COMMIT_REF`: Current commit
- `git diff --quiet`: Checks for differences
- `-- PROJECT-1`: Only checks the PROJECT-1 directory
- **Exit code 0**: No changes → Skip build ✅
- **Exit code 1**: Changes detected → Run build 🔨

## 🔧 Additional Configuration Options

### Environment Variables

Set different environment variables for each site:
1. **Site settings** → **Environment variables**
2. Add variables specific to each project:
   ```
   API_URL=https://api.project1.com
   ENVIRONMENT=production
   ```

### Build Hooks

Create build hooks for manual deployments:
1. **Site settings** → **Build & deploy** → **Build hooks**
2. Create a webhook URL
3. Trigger builds via POST request:
   ```bash
   curl -X POST -d {} https://api.netlify.com/build_hooks/YOUR_HOOK_ID
   ```

### Deploy Previews

Enable deploy previews for pull requests:
1. **Site settings** → **Build & deploy** → **Deploy contexts**
2. Enable **Deploy Preview** for pull requests
3. Each PR will get a unique preview URL

## 📊 Monitoring & Management

### Build Status
- Dashboard shows build status for each site independently
- Check logs in **Deploys** tab for each site

### Analytics
- Each site has separate analytics
- View in **Analytics** tab for each site

### Functions (Optional)
If using Netlify Functions:
```toml
[build]
  functions = "PROJECT-1/netlify/functions"
```

## 🚨 Troubleshooting

### Build Failing?

1. **Check Build Logs**: Click on failed deploy → View logs
2. **Common Issues**:
   - Wrong publish directory path
   - Missing dependencies in package.json
   - Build command not found

### Build Not Triggering?

1. Check `build.ignore` logic
2. Verify changes were made in the project directory
3. Manually trigger deploy: **Deploys** → **Trigger deploy**

### Wrong Files Being Deployed?

1. Verify **Publish directory** setting
2. Check that build command generates files in correct location
3. Use `netlify.toml` to override UI settings

## 📝 Best Practices

### 1. Use Consistent Naming
```
project-1-production
project-1-staging
project-2-production
```

### 2. Version Control netlify.toml
Always commit `netlify.toml` files to Git for reproducible builds.

### 3. Test Locally First
Use Netlify CLI to test builds locally:
```bash
npm install -g netlify-cli
cd PROJECT-1
netlify build
netlify dev
```

### 4. Use Branch Deploys
Set up different branches for staging:
```toml
[context.staging]
  command = "npm run build:staging"
  
[context.production]
  command = "npm run build:production"
```

### 5. Optimize Build Times
- Use build caching
- Only install necessary dependencies
- Consider using build plugins

## 🔗 Useful Links

- [Netlify Monorepo Documentation](https://docs.netlify.com/build/configure-builds/monorepos/)
- [Build Configuration Reference](https://docs.netlify.com/configure-builds/file-based-configuration/)
- [Deploy Contexts](https://docs.netlify.com/site-deploys/overview/#deploy-contexts)
- [Custom Domains](https://docs.netlify.com/domains-https/custom-domains/)

## 📦 Next Steps

1. ✅ Root package.json created
2. ✅ PROJECT-1 netlify.toml configured
3. ✅ PROJECT-2 netlify.toml created
4. ⏳ Create Netlify sites in dashboard for each project
5. ⏳ Configure custom domains
6. ⏳ Test deployments
7. ⏳ Repeat for remaining projects (PROJECT-3, PROJECT-4, etc.)

## 💡 Quick Reference Commands

```bash
# Install all dependencies
npm run install:all

# Build specific project
npm run build:project-1
npm run build:project-2

# Test locally with Netlify CLI
netlify dev --filter PROJECT-1

# Deploy manually
netlify deploy --filter PROJECT-1 --prod
```

---

**Need Help?** Check the [Netlify Community Forums](https://answers.netlify.com/) or [Netlify Support](https://www.netlify.com/support/).
