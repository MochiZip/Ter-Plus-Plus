# GitHub Pages Setup Guide

Complete step-by-step instructions to launch your Ter-Plus-Plus website.

## Enable GitHub Pages

### Step 1: Open Repository Settings
1. Navigate to your repository: https://github.com/MochiZip/Ter-Plus-Plus
2. Click the **Settings** tab (top right)
3. In the left sidebar, scroll down and click **Pages**

### Step 2: Configure Publishing Source
1. Under "Build and deployment" section, find the "Source" dropdown
2. Select **Deploy from a branch**
3. In the "Branch" section:
   - Select **main** from the first dropdown
   - Select **/ (root)** from the second dropdown
   - Click **Save**

### Step 3: Wait for Deployment
- GitHub will automatically build and deploy your site
- Wait 1-2 minutes for the process to complete
- You'll see a green checkmark when deployment is successful

### Step 4: Access Your Website
Your website is now live at:
```
https://mochizip.github.io/Ter-Plus-Plus
```

## Custom Domain (Optional)

To use a custom domain like `ter-plus-plus.com`:

1. In **Settings → Pages**, scroll to "Custom domain"
2. Enter your domain name: `ter-plus-plus.com`
3. Click **Save**
4. Update your domain's DNS records to point to GitHub Pages:
   ```
   A Record: 185.199.108.153
   A Record: 185.199.109.153
   A Record: 185.199.110.153
   A Record: 185.199.111.153
   ```
5. Add CNAME record: `www.ter-plus-plus.com` → `mochizip.github.io`

## HTTPS & SSL Certificate

GitHub Pages automatically provides free HTTPS with Let's Encrypt:

1. After enabling Pages, go back to **Settings → Pages**
2. Scroll to "HTTPS" section
3. Check **Enforce HTTPS** (recommended)
4. Wait for SSL certificate to be issued (usually 5-10 minutes)

## Custom Theme & Jekyll Configuration

Create a `_config.yml` file in your repository root for advanced customization:

```yaml
title: Ter-Plus-Plus
description: A modern, fast, and lightweight web browser
theme: jekyll-theme-cayman
show_downloads: true
github:
  repository_url: https://github.com/MochiZip/Ter-Plus-Plus
```

Available themes:
- `jekyll-theme-cayman` (recommended)
- `jekyll-theme-slate`
- `jekyll-theme-architect`
- `jekyll-theme-merlot`
- `jekyll-theme-midnight`
- `jekyll-theme-minimal`
- `jekyll-theme-time-machine`

## Create Navigation Menu

Add a `_includes/nav.md` file to create a custom navigation:

```markdown
| [Home](/) | [Download](./downloads.md) | [Docs](./docs/) | [Build](./BUILDING.md) | [Contribute](./CONTRIBUTING.md) |
```

## Add Custom CSS

Create `.github/workflows/pages.yml`:

```yaml
name: Deploy to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Pages
        uses: actions/configure-pages@v3

      - name: Build with Jekyll
        uses: actions/jekyll-build-pages@v1
        with:
          source: ./
          destination: ./_site

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

## Add Custom Logo

1. Create a `assets/` folder in your repository
2. Add your logo as `assets/logo.png`
3. Update `_config.yml`:
   ```yaml
   logo: /assets/logo.png
   ```

## Create a Custom Layout

Create `_layouts/default.html` for complete control:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ page.title }} - Ter-Plus-Plus</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        nav {
            background: #333;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 30px;
        }
        nav a {
            color: white;
            text-decoration: none;
            margin-right: 20px;
        }
        nav a:hover {
            color: #0366d6;
        }
    </style>
</head>
<body>
    <nav>
        <a href="/">Home</a>
        <a href="/downloads.html">Download</a>
        <a href="/docs/">Docs</a>
        <a href="/BUILDING.html">Build</a>
        <a href="/CONTRIBUTING.html">Contribute</a>
    </nav>
    <main>
        {{ content }}
    </main>
</body>
</html>
```

## Set Up Redirects

Create `_redirects` to handle URL redirects:

```
/download /downloads.html 301
/docs /docs/README.html 301
/build /BUILDING.html 301
```

## Analytics & Tracking (Optional)

Add to `_config.yml` for Google Analytics:

```yaml
google_analytics: UA-XXXXXXXXX-X
```

Or use Microsoft Clarity:

```html
<script type="text/javascript">
    (function(c,l,a,r,i,t,y){
        c[a]=c[a]||function(){(c[a].q=c[a].q||[]).push(arguments)};
        t=l.createElement(r);t.async=1;t.src="https://www.clarity.ms/tag/"+i;
        y=l.getElementsByTagName(r)[0];y.parentNode.insertBefore(t,y);
    })(window, document, "clarity", "script", "YOUR_CLARITY_ID");
</script>
```

## Troubleshooting

### Pages not showing up
- Ensure you have at least one commit with markdown files
- Check **Settings → Pages** shows "Your site is published"
- Clear your browser cache (Ctrl+Shift+Delete)

### Styles not loading
- GitHub Pages is case-sensitive on Linux servers
- Check file names match exactly
- Rebuild by pushing a new commit

### Custom domain not working
- Wait 24 hours for DNS propagation
- Verify DNS records with: `nslookup ter-plus-plus.com`
- Check the CNAME file was created in your repo

### HTTPS certificate not issued
- Can take up to 10 minutes
- Check **Settings → Pages** for certificate status
- Try disabling and re-enabling HTTPS

## Performance Optimization

### Image Optimization
1. Compress images before uploading
2. Use WebP format when possible
3. Add images to `assets/images/` folder

### Minify CSS/JavaScript
Use GitHub Actions to automatically minify:

```yaml
- name: Minify CSS
  run: |
    npm install csso-cli -g
    csso assets/style.css -o assets/style.min.css
```

## Update Your Site

Any changes you push to the `main` branch will automatically update your site within 1-2 minutes.

```bash
git add .
git commit -m "Update website content"
git push origin main
```

## Additional Resources

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Jekyll Documentation](https://jekyllrb.com/)
- [Markdown Guide](https://www.markdownguide.org/)

---

**Your website is now live and ready to serve users!** 🚀
