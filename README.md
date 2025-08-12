# Samarth Patel - Portfolio Website

🚀 **Live Site**: [samarthpatel.me](https://samarthpatel.me)

A modern, responsive portfolio website built with SvelteKit, TypeScript, and Tailwind CSS. Features custom animations, dark/light mode toggle, and a tech-themed design.

## 🌟 Features

- **Responsive Design**: Optimized for all devices and screen sizes
- **Light/Dark Mode**: System preference detection with manual toggle
- **Smooth Animations**: Intersection Observer API for scroll-triggered animations
- **Modern Tech Stack**: SvelteKit, TypeScript, and Tailwind CSS
- **Custom Logo**: Tech-themed branding with circuit patterns
- **SEO Optimized**: Meta tags, semantic HTML, and performance optimized

## 📋 Sections

1. **Hero Section**: Introduction with call-to-action buttons
2. **Expertise**: Technical skills and specializations
3. **Projects**: Featured work and portfolio showcase
4. **Tech Stack**: Technologies and tools used
5. **Contact**: Call-to-action with contact information

## 🛠️ Tech Stack

- **Framework**: SvelteKit
- **Styling**: Tailwind CSS
- **Language**: TypeScript
- **Build Tool**: Vite
- **Deployment**: Vercel
- **Version Control**: Git & GitHub

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/samarthpatel2005/Samarth-portfolio.git
cd Samarth-portfolio

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## 📱 Features in Detail

### 🎨 Design System
- **Custom Logo**: Tech-themed SVG logo with circuit patterns and code symbols
- **Color Scheme**: Purple and blue gradient theme with excellent contrast
- **Typography**: Modern, clean fonts optimized for readability
- **Icons**: Consistent iconography throughout the interface

### ⚡ Performance
- **Lazy Loading**: Images and components load on demand
- **Code Splitting**: Optimized bundle sizes with Vite
- **SEO**: Comprehensive meta tags, semantic HTML, sitemap
- **Accessibility**: WCAG compliant design with proper contrast ratios

### 📱 Responsive Design
- **Mobile First**: Designed for mobile, enhanced for desktop
- **Breakpoints**: Tailored layouts for all screen sizes
- **Touch Friendly**: Optimized for touch interactions and gestures

## 🔧 Development

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Git

### Local Development
1. **Clone the repository**:
   ```bash
   git clone https://github.com/samarthpatel2005/Samarth-portfolio.git
   cd Samarth-portfolio
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Start development server**:
   ```bash
   npm run dev
   ```

4. **Open browser**: Navigate to [http://localhost:5173](http://localhost:5173)

### Build Commands
```bash
# Development
npm run dev          # Start dev server with hot reload

# Production
npm run build        # Build for production
npm run preview      # Preview production build locally

# Linting & Formatting
npm run lint         # Run ESLint
npm run format       # Format code with Prettier
```

## 🚀 Deployment

This project is configured for easy deployment on multiple platforms:

### Vercel (Recommended)
```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Set custom domain in Vercel dashboard
```

### Other Platforms
See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed instructions including:
- Netlify deployment
- GitHub Pages setup
- Self-hosted options
- Performance optimization

## 📊 Performance Metrics

- **Lighthouse Score**: 95+ in all categories
- **Core Web Vitals**: Optimized for LCP, FID, CLS
- **Bundle Size**: < 200KB gzipped
- **Image Optimization**: WebP format, responsive sizing

## 🎯 Project Structure

```
src/
├── lib/
│   ├── Navigation.svelte      # Main navigation with logo
│   ├── Hero.svelte           # Landing section
│   ├── Expertise.svelte      # Skills overview
│   ├── Projects.svelte       # Portfolio showcase
│   ├── TechStack.svelte      # Technology cards
│   ├── CallToAction.svelte   # Contact section
│   ├── Footer.svelte         # Site footer
│   └── utils/
│       ├── animations.ts     # Scroll animations
│       └── constants.ts      # Site constants
├── App.svelte               # Main app component
├── main.ts                  # Application entry point
└── app.css                  # Global styles

public/
├── logo.svg                 # Custom tech logo
├── favicon.svg              # Site favicon
└── profile.jpg              # Profile image
```

## 🔧 Customization

### Updating Content
- **Personal Info**: Edit `src/lib/utils/constants.ts`
- **Projects**: Modify `src/lib/Projects.svelte`
- **Skills**: Update `src/lib/TechStack.svelte`
- **Colors**: Customize `tailwind.config.js`

### Adding New Sections
1. Create new component in `src/lib/`
2. Import in `App.svelte`
3. Add navigation link in `Navigation.svelte`

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes
4. Commit: `git commit -m 'Add feature'`
5. Push: `git push origin feature-name`
6. Submit a pull request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🔗 Links

- **Live Website**: [samarthpatel.me](https://samarthpatel.me)
- **GitHub Repository**: [Samarth-portfolio](https://github.com/samarthpatel2005/Samarth-portfolio)
- **Deployment Guide**: [DEPLOYMENT.md](./DEPLOYMENT.md)

## 📧 Contact

- **Portfolio**: [samarthpatel.me](https://samarthpatel.me)
- **GitHub**: [@samarthpatel2005](https://github.com/samarthpatel2005)

---

**Built with ❤️ by Samarth Patel using SvelteKit & Tailwind CSS**
