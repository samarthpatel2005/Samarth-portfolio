# Deployment Guide

## 🚀 Quick Deployment Options

### 1. Vercel (Recommended)

**Why Vercel?**
- Zero configuration deployment
- Automatic HTTPS
- Global CDN
- Perfect for SvelteKit projects

**Steps:**
1. Push your code to GitHub
2. Visit [vercel.com](https://vercel.com)
3. Import your repository
4. Deploy automatically

**Custom Domain:**
1. Add your domain in Vercel dashboard
2. Update DNS records as instructed
3. Automatic SSL certificate

### 2. Netlify

**Steps:**
1. Connect GitHub repository to Netlify
2. Build settings:
   - Build command: `npm run build`
   - Publish directory: `dist`
3. Deploy

**Netlify.toml configuration:**
```toml
[build]
  command = "npm run build"
  publish = "dist"

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### 3. GitHub Pages

**Steps:**
1. Install GitHub Pages adapter:
```bash
npm install -D @sveltejs/adapter-static
```

2. Update `svelte.config.js`:
```js
import adapter from '@sveltejs/adapter-static';

export default {
  kit: {
    adapter: adapter({
      pages: 'build',
      assets: 'build',
      fallback: null,
      precompress: false,
      strict: true
    })
  }
};
```

3. Create `.github/workflows/deploy.yml`:
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: ['main']

jobs:
  build_site:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Install Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: npm

      - name: Install dependencies
        run: npm install

      - name: Build
        run: npm run build

      - name: Upload Artifacts
        uses: actions/upload-pages-artifact@v1
        with:
          path: 'build/'

  deploy:
    needs: build_site
    runs-on: ubuntu-latest
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy
        id: deployment
        uses: actions/deploy-pages@v1
```

### 4. Self-Hosted (VPS/Dedicated Server)

**Using PM2 and Nginx:**

1. **Server Setup:**
```bash
# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install PM2
npm install -g pm2

# Install Nginx
sudo apt update
sudo apt install nginx
```

2. **Build and Deploy:**
```bash
# Build the project
npm run build

# Start with PM2 (if using SvelteKit with Node adapter)
pm2 start npm --name "portfolio" -- start
pm2 save
pm2 startup
```

3. **Nginx Configuration:**
```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        root /var/www/portfolio/build;
        try_files $uri $uri/ /index.html;
        
        # Cache static assets
        location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
            expires 1y;
            add_header Cache-Control "public, immutable";
        }
    }
}
```

## 🔧 Build Optimizations

### 1. Environment Variables

Create `.env.production`:
```env
VITE_API_URL=https://api.yourdomain.com
VITE_CONTACT_EMAIL=your-email@example.com
VITE_GA_TRACKING_ID=G-XXXXXXXXXX
```

### 2. Vite Configuration

Update `vite.config.ts`:
```ts
import { defineConfig } from 'vite';
import { sveltekit } from '@sveltejs/kit/vite';

export default defineConfig({
  plugins: [sveltekit()],
  build: {
    minify: 'terser',
    terserOptions: {
      compress: {
        drop_console: true,
        drop_debugger: true
      }
    },
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['svelte'],
        }
      }
    }
  },
  define: {
    __APP_VERSION__: JSON.stringify(process.env.npm_package_version)
  }
});
```

### 3. Performance Optimization

**Image Optimization:**
```bash
# Install image optimization tools
npm install -D @sveltejs/enhanced-img
```

**Bundle Analysis:**
```bash
# Analyze bundle size
npm install -D rollup-plugin-visualizer
npm run build
# Check dist/stats.html
```

## 📊 Analytics & Monitoring

### 1. Google Analytics

Add to `app.html`:
```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### 2. Performance Monitoring

**Web Vitals:**
```bash
npm install web-vitals
```

```js
// src/lib/analytics.js
import { getCLS, getFID, getFCP, getLCP, getTTFB } from 'web-vitals';

function sendToAnalytics(metric) {
  gtag('event', metric.name, {
    value: Math.round(metric.name === 'CLS' ? metric.value * 1000 : metric.value),
    event_category: 'Web Vitals',
    event_label: metric.id,
    non_interaction: true,
  });
}

getCLS(sendToAnalytics);
getFID(sendToAnalytics);
getFCP(sendToAnalytics);
getLCP(sendToAnalytics);
getTTFB(sendToAnalytics);
```

## 🔒 Security Headers

### 1. Security Headers Configuration

For Vercel, create `vercel.json`:
```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        },
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "Referrer-Policy",
          "value": "strict-origin-when-cross-origin"
        },
        {
          "key": "Content-Security-Policy",
          "value": "default-src 'self'; script-src 'self' 'unsafe-inline' https://www.googletagmanager.com; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; img-src 'self' data: https:; connect-src 'self' https://www.google-analytics.com;"
        }
      ]
    }
  ]
}
```

## 🔍 SEO Optimization

### 1. Sitemap Generation

Create `src/routes/sitemap.xml/+server.ts`:
```ts
export async function GET() {
  const sitemap = `<?xml version="1.0" encoding="UTF-8"?>
    <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
      <url>
        <loc>https://yourdomain.com/</loc>
        <lastmod>${new Date().toISOString()}</lastmod>
        <priority>1.0</priority>
      </url>
    </urlset>`;

  return new Response(sitemap, {
    headers: {
      'Content-Type': 'application/xml'
    }
  });
}
```

### 2. Robots.txt

Create `static/robots.txt`:
```
User-agent: *
Allow: /

Sitemap: https://yourdomain.com/sitemap.xml
```

## 📱 PWA Configuration

### 1. Service Worker

Install PWA plugin:
```bash
npm install -D @vite-pwa/sveltekit
```

Update `vite.config.ts`:
```ts
import { SvelteKitPWA } from '@vite-pwa/sveltekit';

export default defineConfig({
  plugins: [
    sveltekit(),
    SvelteKitPWA({
      registerType: 'autoUpdate',
      workbox: {
        globPatterns: ['**/*.{js,css,html,ico,png,svg}']
      },
      manifest: {
        name: 'Samarth Patel - Portfolio',
        short_name: 'Portfolio',
        description: 'Software Engineer Portfolio',
        theme_color: '#3b82f6',
        background_color: '#ffffff',
        display: 'standalone',
        icons: [
          {
            src: '/pwa-192x192.png',
            sizes: '192x192',
            type: 'image/png'
          },
          {
            src: '/pwa-512x512.png',
            sizes: '512x512',
            type: 'image/png'
          }
        ]
      }
    })
  ]
});
```

## 🚀 Performance Checklist

Before deployment, ensure:

- [ ] Images are optimized (WebP format, proper sizing)
- [ ] Unused CSS is purged
- [ ] JavaScript is minified
- [ ] Bundle size is analyzed and optimized
- [ ] SEO meta tags are complete
- [ ] Security headers are configured
- [ ] Analytics are implemented
- [ ] Performance monitoring is set up
- [ ] All links are working
- [ ] Mobile responsiveness is tested
- [ ] Accessibility audit is passed
- [ ] Lighthouse score is optimized (90+ in all categories)

## 🔧 Troubleshooting

### Common Issues:

1. **Build Fails:**
   - Check TypeScript errors
   - Verify all imports exist
   - Check Tailwind configuration

2. **Images Not Loading:**
   - Use proper paths (relative to `static/`)
   - Check image formats and sizes

3. **Fonts Not Loading:**
   - Verify font imports in CSS
   - Check CORS headers for external fonts

4. **Dark Mode Issues:**
   - Ensure localStorage is available
   - Check theme toggle implementation

### Performance Issues:

1. **Slow Loading:**
   - Optimize images
   - Enable compression
   - Use CDN for static assets

2. **Large Bundle Size:**
   - Analyze bundle with rollup-plugin-visualizer
   - Implement code splitting
   - Remove unused dependencies

This deployment guide should help you successfully deploy your portfolio to any platform while ensuring optimal performance and security.
