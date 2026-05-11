# Deploy IronFeather Website to Cloudflare Pages

✅ **Git repo initialized and first commit done**

Now you need to:
1. Push to GitHub
2. Connect Cloudflare Pages
3. Update DNS

---

## Step 1: Create GitHub Repository

### Option A: Via GitHub Web (Easiest)

1. Go to https://github.com/new
2. Repository name: `ironfeather-website`
3. Description: `IronFeather AI landing page`
4. **Private** repository (keep it private for now)
5. **DO NOT** initialize with README, .gitignore, or license (we already have files)
6. Click **Create repository**

### Option B: Via Terminal (if you prefer)

```bash
# Install GitHub CLI first
brew install gh

# Authenticate
gh auth login

# Create repo
gh repo create ironfeather-website --private --source=. --remote=origin --push
```

---

## Step 2: Push to GitHub (if using Option A above)

After creating the repo on GitHub, it will show you commands. Run these from the website directory:

```bash
cd ~/.openclaw/workspace/ironfeather/website

# Add GitHub as remote (replace YOUR_USERNAME with your actual GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/ironfeather-website.git

# Push
git push -u origin main
```

**Note:** GitHub will ask for authentication. You'll need a Personal Access Token:
- Go to https://github.com/settings/tokens
- Generate new token (classic)
- Select scopes: `repo` (full control)
- Copy the token and use it as your password when pushing

---

## Step 3: Connect Cloudflare Pages

1. Go to https://dash.cloudflare.com
2. Select your account
3. Go to **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
4. Connect your GitHub account (authorize Cloudflare)
5. Select `ironfeather-website` repository
6. Configure build:
   - **Production branch:** `main`
   - **Build command:** (leave empty - static HTML)
   - **Build output directory:** `/`
   - **Root directory:** `/`
7. Click **Save and Deploy**

Cloudflare will:
- Build and deploy your site
- Give you a `*.pages.dev` URL
- Auto-deploy on every git push to `main`

---

## Step 4: Connect Custom Domain (ironfeather.ai)

**Current status:** ironfeather.ai is on **Namecheap DNS** (not Cloudflare yet)

You have two options:

### Option A: Move to Cloudflare DNS (Recommended)

**Why:** Full Cloudflare features, auto-configuration, better performance

1. In Cloudflare dashboard, click **Add site**
2. Enter: `ironfeather.ai`
3. Choose Free plan
4. Cloudflare will scan existing DNS records
5. Review and confirm records
6. Cloudflare will give you 2 nameservers (e.g., `chad.ns.cloudflare.com`)
7. Go to Namecheap → Domain List → ironfeather.ai → Manage
8. Change nameservers from "Namecheap BasicDNS" to "Custom DNS"
9. Enter the 2 Cloudflare nameservers
10. Wait 15-60 minutes for DNS propagation
11. Return to Cloudflare Pages → Custom domains → Add `ironfeather.ai` (auto-configures)

### Option B: Keep Namecheap DNS (Quick but limited)

**Why:** Faster setup, but you lose some Cloudflare features

1. Deploy to Cloudflare Pages first (it will give you a `*.pages.dev` URL)
2. In Cloudflare Pages → Custom domains → Add `ironfeather.ai`
3. Cloudflare will show you CNAME records needed
4. Go to Namecheap → Domain List → ironfeather.ai → Advanced DNS
5. Add CNAME records:
   - `@` → `ironfeather-website.pages.dev` (or the Pages URL given)
   - `www` → `ironfeather-website.pages.dev`
6. Wait 5-15 minutes for DNS propagation

**Recommendation:** Option A for full Cloudflare power

---

## Step 5: Test and Verify

1. Visit https://ironfeather.ai
2. Check logo loads ✅
3. Check Friday avatar loads ✅
4. Check video plays ✅

---

## Future Updates

To update the site, just commit and push:

```bash
cd ~/.openclaw/workspace/ironfeather/website

# Make your changes to files...

git add .
git commit -m "Update: [describe your changes]"
git push

# Cloudflare automatically deploys in ~30 seconds
```

---

## Need Help?

- **GitHub issues?** Run `gh auth login` or use web interface
- **Cloudflare issues?** Make sure ironfeather.ai nameservers point to Cloudflare
- **DNS not working?** Check https://dash.cloudflare.com → ironfeather.ai → DNS

---

🦾 Friday can handle future commits and pushes for you once the repo is connected.
