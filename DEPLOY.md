# Kwanim — Vercel Deployment Guide

## What's in this folder

```
kwanim-vercel/
├── api/
│   └── oracle.js        ← Secure proxy to Anthropic API (your API key lives here, never in the browser)
├── public/
│   └── index.html       ← The full Kwanim website
├── vercel.json          ← Vercel routing config
└── DEPLOY.md            ← This guide
```

---

## Step 1 — Create your accounts (free)

1. **Vercel account** → https://vercel.com/signup (sign up with GitHub, Google, or email)
2. **Anthropic account** → https://console.anthropic.com (you need this for your API key)

---

## Step 2 — Get your Anthropic API key

1. Go to https://console.anthropic.com
2. Click **API Keys** in the left sidebar
3. Click **Create Key** → give it a name like "kwanim-production"
4. Copy the key — it starts with `sk-ant-...`
5. **Save it somewhere safe** — you won't be able to see it again

---

## Step 3 — Deploy to Vercel (two options)

### Option A — Drag and drop (easiest, no coding required)

1. Go to https://vercel.com/new
2. Click **"Browse"** and select this entire `kwanim-vercel` folder
3. Vercel detects the config automatically
4. Click **Deploy**
5. It gives you a live URL like `kwanim-vercel.vercel.app`

### Option B — Via GitHub (recommended for ongoing updates)

1. Create a free GitHub account at https://github.com if you don't have one
2. Create a new repository called `kwanim`
3. Upload the contents of this folder to that repository
4. Go to https://vercel.com/new → click **"Import Git Repository"**
5. Select your `kwanim` repo → click **Deploy**

GitHub method means future updates are as simple as uploading a new `index.html` to GitHub.

---

## Step 4 — Add your API key to Vercel (IMPORTANT)

This is what keeps your API key secret and out of the code.

1. In your Vercel dashboard, go to your project
2. Click **Settings** → **Environment Variables**
3. Click **Add New**
   - Name: `ANTHROPIC_API_KEY`
   - Value: paste your `sk-ant-...` key here
   - Environment: tick **Production**, **Preview**, and **Development**
4. Click **Save**
5. Go to **Deployments** → click the three dots on your latest deployment → **Redeploy**

The oracle and divination features will now work securely on your live site.

---

## Step 5 — Connect your kwanim.ai domain

1. In Vercel dashboard → your project → **Settings** → **Domains**
2. Type `kwanim.ai` → click **Add**
3. Vercel shows you DNS records to add (usually two: an A record and a CNAME)
4. Log into wherever you bought `kwanim.ai` (GoDaddy, Namecheap, etc.)
5. Go to DNS settings and add those records exactly as Vercel shows
6. Wait 10–30 minutes for DNS to propagate
7. Vercel automatically issues an SSL certificate (the padlock) — free

---

## Costs to expect

| Item | Cost |
|---|---|
| Vercel hosting | Free (Hobby plan) |
| SSL certificate | Free (included) |
| kwanim.ai domain | ~$15–20/year (already purchased) |
| Anthropic API calls | ~$0.003 per oracle/divination response |

At 1,000 paying users/month using the $2 divination feature, your Anthropic API costs would be roughly $3/month.

---

## Updating the site later

If you used **Option A (drag and drop):**
- Go to your Vercel project → **Deployments** → drag a new folder

If you used **Option B (GitHub):**
- Upload the new `index.html` to your GitHub repository
- Vercel automatically redeploys within 30 seconds

---

## If something doesn't work

**Oracle/divination not responding?**
→ Check that `ANTHROPIC_API_KEY` is set correctly in Vercel Environment Variables and that you redeployed after adding it.

**Domain not connecting?**
→ DNS changes can take up to 48 hours. Check your DNS settings match exactly what Vercel specified.

**Site not loading?**
→ Make sure `index.html` is inside the `public/` folder, not at the root level.
