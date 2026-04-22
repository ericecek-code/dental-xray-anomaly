# Deployment Variants - Dental X-ray Anomaly Detection

## Quick Comparison

| Variant | Platform | Free Tier | Best For | Difficulty |
|---------|----------|-----------|----------|------------|
| **1. Render** | render.com | 750h/month | Full-stack apps | ⭐ Easy |
| **2. Railway** | railway.app | $5 credit | Docker-based | ⭐⭐ Medium |
| **3. VPS/Docker** | DigitalOcean/Hetzner | From $4/mo | Production | ⭐⭐⭐ Advanced |
| **4. Vercel** | vercel.com | Serverless | Frontend/Edge | ⭐ Easy |
| **5. Cloudflare** | cloudflare.com | Unlimited bandwidth | Edge computing | ⭐ Easy |
| **6. Netlify** | netlify.com | 100GB/month | Static + functions | ⭐ Easy |
| **7. Fly.io** | fly.io | 3 apps free | Global edge | ⭐⭐ Medium |
| **8. Deta Space** | deta.space | Personal use free | Quick deploy | ⭐ Easy |

---

## Variant 1: Render (Recommended for Beginners)

### Pros:
- ✅ Free tier available (750 hours/month)
- ✅ Easy GitHub integration
- ✅ Python built-in support
- ✅ Auto-deploy on push

### Cons:
- ⛔ Sleeps after 15 min inactivity
- ⛔ Limited compute resources

### Setup:

```bash
# 1. Create render.yaml in project root
cat > render.yaml << 'EOF'
services:
  - name: dental-xray-app
    type: web
    env: python
    region: frankfurt
    buildCommand: pip install -r requirements.txt
    startCommand: python app.py
    envVars:
      - key: PYTHON_VERSION
        value: "3.10"
    autoDeploy: true
    repoUrl: https://github.com/YOUR_USERNAME/Dental-X-ray-Anomaly-Detection-System
EOF

# 2. Push to GitHub and connect in Render dashboard
```

### URL: `https://dental-xray-app.onrender.com`

---

## Variant 2: Railway (Better Performance)

### Pros:
- ✅ $5/month credit free
- ✅ Better performance
- ✅ Docker support
- ✅ No cold starts on paid plan

### Cons:
- ⛔ Requires credit card (for verification)
- ⛔ More expensive than Render

### Setup:

1. Install Railway CLI:
```bash
npm install -g @railway/cli
```

2. Login and init:
```bash
railway login
railway init
railway up
```

### URL: `https://dental-xray-app.railway.app`

---

## Variant 3: VPS with Docker (Production)

### Pros:
- ✅ Full control
- ✅ No cold starts
- ✅ Can run multiple services
- ✅ Permanent uptime

### Cons:
- ⛔ Requires server management
- ⛔ Cost from $4/month

### Setup on DigitalOcean/Hetzner:

```bash
# 1. Create Droplet/VPS (Ubuntu 22.04)

# 2. Install Docker
curl -fsSL https://get.docker.com | sh
usermod -aG docker $USER

# 3. Build and run
docker build -t dental-xray .
docker run -d -p 80:5000 --name dental-xray dental-xray
```

### URL: `http://YOUR_SERVER_IP`

---

## Variant 4: Vercel (Serverless)

### Pros:
- ✅ Generous free tier
- ✅ Global CDN
- ✅ Edge functions
- ✅ Auto-deploy

### Cons:
- ⛔ Python via serverless functions (requires adapter)
- ⛔ Timeout limits (10s free tier)
- ⛔ No persistent storage

### Setup:

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel
```

**Note:** Requires WSGI/ASGI adapter for Flask. Add `vercel.json`:

```json
{
  "builds": [
    {
      "src": "app.py",
      "use": "@vercel/python"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "app.py"
    }
  ]
}
```

### URL: `https://dental-xray-app.vercel.app`

---

## Variant 5: Cloudflare Pages (Edge)

### Pros:
- ✅ Unlimited bandwidth
- ✅ Edge computing
- ✅ Free SSL
- ✅ Fast global CDN

### Cons:
- ⛔ Python via Cloudflare Workers (different API)
- ⛔ Limited execution time

### Setup:

1. Connect GitHub to Cloudflare Dashboard
2. Select "Pages" → "Create project"
3. Build command: `pip install -r requirements.txt`
4. Output directory: (empty for Python)

### URL: `https://dental-xray.pages.dev`

---

## Variant 6: Netlify

### Pros:
- ✅ Free tier: 100GB bandwidth
- ✅ Easy deploy
- ✅ Form handling
- ✅ Edge functions

### Cons:
- ⛔ Sleeps after 30 min (free tier)
- ⛔ Python via Functions

### Setup:

```bash
# netlify.toml
[build]
  command = "pip install -r requirements.txt"
  publish = "."
  functions = "functions"

[[redirect]]
  from = "/*"
  to = "/app.py"
  status = 200
```

### URL: `https://dental-xray.netlify.app`

---

## Variant 7: Fly.io (Global Edge)

### Pros:
- ✅ 3 apps free
- ✅ Global edge deployment
- ✅ Docker-native
- ✅ Persistent volumes

### Cons:
- ⛔ Requires credit card
- ⛔ More complex setup

### Setup:

```bash
# Install Fly CLI
brew install flyctl

# Login and deploy
fly auth login
fly launch
fly deploy
```

### URL: `https://dental-xray.fly.dev`

---

## Variant 8: Deta Space (Personal)

### Pros:
- ✅ Completely free for personal use
- ✅ No credit card needed
- ✅ Simple push-to-deploy
- ✅ Built-in database

### Cons:
- ⛔ Personal use only (not commercial)
- ⛔ Limited resources

### Setup:

```bash
# Install Space CLI
brew install deta-cli

# Login and create
deta login
deta new --python

# Push updates
deta push
```

### URL: `https://your-app.deta.space`

---

## Summary Table

| Platform | Free Tier | Sleep | Python | Docker | Credit Card |
|----------|-----------|-------|--------|--------|-------------|
| **Render** | 750h | Yes | ✅ | ✅ | No |
| **Railway** | $5/mo | No | ✅ | ✅ | Yes |
| **Vercel** | Serverless | No | ✅* | ❌ | No |
| **Cloudflare** | Unlimited | No | ✅** | ❌ | No |
| **Netlify** | 100GB | Yes | ✅* | ❌ | No |
| **Fly.io** | 3 apps | No | ✅ | ✅ | Yes |
| **Deta Space** | Free | No | ✅ | ❌ | No |

*Via serverless/edge functions
**Via Cloudflare Workers

---

## Recommendation

| Use Case | Best Platform |
|----------|---------------|
| **Personal demo** | Deta Space, Render |
| **Production** | Railway, Fly.io, VPS |
| **High traffic** | Cloudflare, Netlify |
| **Quick test** | Vercel, Deta Space |