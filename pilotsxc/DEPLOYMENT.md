# Deployment Guide

Website StudentsxCEOs siap untuk deployment ke berbagai platform. Berikut adalah panduan lengkap untuk deployment ke GitHub Pages, Vercel, dan platform lainnya.

## 🚀 Platform yang Didukung

### 1. GitHub Pages (Recommended)
- ✅ Free hosting
- ✅ Custom domain support
- ✅ HTTPS otomatis
- ✅ CI/CD dengan GitHub Actions

### 2. Vercel (Recommended)
- ✅ Free hosting
- ✅ Global CDN
- ✅ Custom domain
- ✅ Analytics
- ✅ Preview deployments

### 3. Netlify
- ✅ Free hosting
- ✅ Form handling
- ✅ Split testing
- ✅ Edge functions

### 4. Firebase Hosting
- ✅ Free hosting
- ✅ Global CDN
- ✅ SSL certificates
- ✅ Custom domain

---

## 📋 Persiapan Sebelum Deployment

### 1. Pastikan Semua File Siap
```bash
# Structure yang harus ada:
pilotsxc/
├── index.html              # Main file
├── styles.css              # Styling
├── scroll-animations.js    # Animations
├── package.json            # Dependencies
├── README.md               # Documentation
├── .gitignore              # Git ignore file
├── .nojekyll               # GitHub Pages
├── vercel.json             # Vercel config
├── .github/workflows/deploy.yml  # GitHub Actions
├── media/                  # Images
├── sponsor/                # Partner logos
└── medpar/                 # Media partner logos
```

### 2. Test Website Lokal
```bash
# Install dependencies
npm install

# Start development server
npm start

# Test semua halaman:
# - http://localhost:3000/
# - http://localhost:3000/about
# - http://localhost:3000/community
# - http://localhost:3000/support
# - http://localhost:3000/contact
```

---

## 🎯 Deployment ke GitHub Pages

### Method 1: GitHub Actions (Recommended)

1. **Push ke GitHub**
```bash
git init
git add .
git commit -m "Initial commit - StudentsxCEOs Website"
git branch -M main
git remote add origin https://github.com/username/studentsxceos-website.git
git push -u origin main
```

2. **Enable GitHub Pages**
- Go to repository Settings → Pages
- Source: Deploy from a branch
- Branch: main
- Folder: / (root)
- Save

3. **GitHub Actions akan otomatis deploy**
- Tunggu beberapa menit
- Website akan tersedia di: `https://username.github.io/studentsxceos-website`

### Method 2: Manual Upload

1. **Build website** (tidak perlu build untuk static website)
2. **Upload files** ke GitHub repository
3. **Configure GitHub Pages** seperti di atas

---

## ⚡ Deployment ke Vercel

### Method 1: CLI (Recommended)

1. **Install Vercel CLI**
```bash
npm i -g vercel
```

2. **Login ke Vercel**
```bash
vercel login
```

3. **Deploy**
```bash
vercel --prod
```

4. **Follow prompts** untuk setup project

### Method 2: Vercel Dashboard

1. **Go to [vercel.com](https://vercel.com)**
2. **Sign up/Login**
3. **Import Git Repository**
4. **Connect GitHub repository**
5. **Configure settings:**
   - Framework Preset: Other
   - Root Directory: ./
   - Build Command: (kosongkan)
   - Output Directory: ./
   - Install Command: `npm install`

6. **Deploy**

### Method 3: GitHub Integration

1. **Install Vercel GitHub App**
2. **Connect repository**
3. **Auto-deploy on push to main**

---

## 🌐 Deployment ke Netlify

### Method 1: Drag & Drop

1. **Compress project folder**
```bash
# Create zip file (exclude node_modules)
zip -r studentsxceos-website.zip . -x "node_modules/*"
```

2. **Go to [netlify.com](https://netlify.com)**
3. **Drag & drop zip file**
4. **Deploy**

### Method 2: Git Integration

1. **Connect GitHub repository**
2. **Configure settings:**
   - Build command: (kosongkan)
   - Publish directory: ./
   - Node version: 18

3. **Deploy**

---

## 🔥 Deployment ke Firebase Hosting

### 1. Install Firebase CLI
```bash
npm install -g firebase-tools
```

### 2. Login Firebase
```bash
firebase login
```

### 3. Initialize Firebase
```bash
firebase init hosting
```

### 4. Configure firebase.json
```json
{
  "hosting": {
    "public": ".",
    "ignore": [
      "firebase.json",
      "**/.*",
      "node_modules/**"
    ],
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ]
  }
}
```

### 5. Deploy
```bash
firebase deploy
```

---

## ⚙️ Konfigurasi Custom Domain

### GitHub Pages
1. **Go to repository Settings → Pages**
2. **Add custom domain**
3. **Configure DNS records**
4. **Enable HTTPS**

### Vercel
1. **Go to project dashboard**
2. **Settings → Domains**
3. **Add custom domain**
4. **Configure DNS**
5. **Auto SSL**

### Netlify
1. **Site settings → Domain management**
2. **Add custom domain**
3. **Configure DNS**
4. **Force HTTPS**

---

## 🔍 Troubleshooting

### Common Issues

#### 1. 404 Errors pada SPA Routes
**Solution**: Pastikan routing configuration benar
- GitHub Pages: `.github/workflows/deploy.yml`
- Vercel: `vercel.json`
- Netlify: `_redirects` file

#### 2. CSS/JS tidak loading
**Solution**: Check file paths dan relative URLs
```html
<!-- Use relative paths -->
<link rel="stylesheet" href="styles.css">
<script src="scroll-animations.js"></script>
```

#### 3. Images tidak muncul
**Solution**: Pastikan folder assets di-upload
```bash
# Check structure
media/
sponsor/
medpar/
```

#### 4. Slow loading
**Solution**: Optimize images dan enable caching
```json
// vercel.json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, immutable"
        }
      ]
    }
  ]
}
```

---

## 📊 Performance Optimization

### 1. Image Optimization
- Compress images sebelum upload
- Use WebP format jika possible
- Lazy loading untuk gambar besar

### 2. CSS Optimization
- Minimize CSS files
- Remove unused CSS
- Use CSS custom properties

### 3. JavaScript Optimization
- Minify JavaScript files
- Remove unused code
- Use async/defer untuk scripts

### 4. Enable Caching
```json
// vercel.json headers
{
  "headers": [
    {
      "source": "/static/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, immutable"
        }
      ]
    }
  ]
}
```

---

## 🚀 Best Practices

### 1. Environment Variables
```bash
# .env.local untuk development
VITE_API_URL=http://localhost:3000
```

### 2. Error Handling
```javascript
// Add error handling for navigation
window.addEventListener('error', (e) => {
  console.error('Navigation error:', e);
});
```

### 3. Analytics
- Google Analytics
- Vercel Analytics
- Netlify Analytics

### 4. SEO Optimization
```html
<!-- Add meta tags -->
<meta name="description" content="StudentsxCEOs - Leadership accelerator">
<meta property="og:title" content="StudentsxCEOs">
<meta property="og:description" content="Leadership accelerator">
<meta property="og:image" content="https://yourdomain.com/media/logo.png">
```

---

## 📞 Support

Jika mengalami masalah selama deployment:

1. **Check logs** di deployment platform
2. **Test locally** terlebih dahulu
3. **Check file structure** dan permissions
4. **Review configuration files**
5. **Contact platform support** jika perlu

---

**Happy Deploying! 🎉**

Website StudentsxCEOs siap go live dengan performa optimal di platform mana pun!