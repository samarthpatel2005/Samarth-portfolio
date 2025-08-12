# Samarth Patel - Portfolio Website

A modern, responsive portfolio website built with SvelteKit and Tailwind CSS, showcasing expertise in full-stack development, cloud architecture, and modern web technologies.

## 🚀 Features

- **Responsive Design**: Optimized for all devices and screen sizes
- **Dark Mode**: System preference detection with manual toggle
- **Smooth Animations**: Intersection Observer API for scroll-triggered animations
- **Accessibility**: WCAG compliant with keyboard navigation and screen reader support
- **SEO Optimized**: Meta tags, semantic HTML, and performance optimized
- **Modern Stack**: SvelteKit, TypeScript, and Tailwind CSS

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
- **Deployment**: Vercel (recommended)

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ 
- npm or yarn

### Installation

1. Clone the repository:
```bash
git clone https://github.com/samarthpatel/portfolio.git
cd portfolio
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open http://localhost:5173 in your browser

## 📝 Customization

### Personal Information

Update the following files with your information:

1. **Hero Section** (`src/lib/Hero.svelte`):
   - Name and title
   - Profile description
   - Profile image/initials

2. **Contact Information** (`src/lib/CallToAction.svelte` & `src/lib/Footer.svelte`):
   - Email address
   - Social media links
   - Contact methods

3. **Projects** (`src/lib/Projects.svelte`):
   - Replace with your actual projects
   - Update GitHub/demo links
   - Add project screenshots

4. **SEO Meta Tags** (`src/App.svelte`):
   - Update title, description, and keywords
   - Add your domain for Open Graph tags

### Styling

- **Colors**: Modify the color palette in `tailwind.config.js`
- **Fonts**: Update font imports in `src/app.css`
- **Animations**: Customize animation timings and effects in component styles

## 🌐 Deployment

### Vercel (Recommended)

1. Push your code to GitHub
2. Connect your repository to Vercel
3. Deploy with zero configuration

### Alternative Platforms

- **Netlify**: Add `npm run build` as build command
- **AWS Amplify**: Configure build settings for SvelteKit
- **GitHub Pages**: Use SvelteKit static adapter

### Build for Production

```bash
npm run build
```

## ♿ Accessibility Features

- Semantic HTML structure
- ARIA labels and descriptions
- Keyboard navigation support
- Screen reader compatible
- High contrast color scheme
- Focus indicators
- Skip navigation links

## 🔧 Performance Optimizations

- **Image Optimization**: Lazy loading and responsive images
- **Code Splitting**: Automatic with SvelteKit
- **CSS Purging**: Tailwind removes unused styles
- **Preloading**: Critical resources preloaded
- **Compression**: Gzip/Brotli compression enabled

## 📱 Responsive Design

- **Mobile First**: Designed for mobile devices first
- **Breakpoints**: sm (640px), md (768px), lg (1024px), xl (1280px)
- **Touch Friendly**: Optimized for touch interactions
- **Fast Loading**: Optimized for slower mobile connections

## 🔍 SEO Best Practices

- **Meta Tags**: Comprehensive meta tag implementation
- **Structured Data**: Schema.org markup for better search results
- **Sitemap**: Auto-generated sitemap for search engines
- **Performance**: Lighthouse score optimized
- **Social Sharing**: Open Graph and Twitter Card support

## 📧 Contact Form Integration

To add a working contact form, integrate with:

- **Formspree**: Simple form backend
- **Netlify Forms**: Built-in form handling
- **EmailJS**: Client-side email service
- **SendGrid**: Professional email API

Example Formspree integration:
```html
<form action="https://formspree.io/f/your-form-id" method="POST">
  <!-- form fields -->
</form>
```

## 🚀 Performance Tips

1. **Optimize Images**: Use WebP format and proper sizing
2. **Minimize JavaScript**: Remove unused dependencies
3. **Enable Compression**: Configure server compression
4. **Use CDN**: Serve static assets from CDN
5. **Monitor Performance**: Use Lighthouse and WebPageTest

## 📦 Building Components

When creating new components:

1. Use TypeScript for type safety
2. Implement proper accessibility attributes
3. Add responsive design considerations
4. Include loading states and error handling
5. Test across different devices and browsers

## 🔧 Environment Variables

Create a `.env` file for sensitive data:

```env
VITE_CONTACT_EMAIL=your-email@example.com
VITE_GITHUB_USERNAME=your-github-username
VITE_LINKEDIN_URL=your-linkedin-url
```

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📞 Support

For questions or support:
- Email: samarth@example.com
- GitHub Issues: [Create an issue](https://github.com/samarthpatel/portfolio/issues)
- LinkedIn: [Connect with me](https://linkedin.com/in/samarthpatel)

---

Made with ❤️ using SvelteKit and Tailwind CSS

**Why `global.d.ts` instead of `compilerOptions.types` inside `jsconfig.json` or `tsconfig.json`?**

Setting `compilerOptions.types` shuts out all other types not explicitly listed in the configuration. Using triple-slash references keeps the default TypeScript setting of accepting type information from the entire workspace, while also adding `svelte` and `vite/client` type information.

**Why include `.vscode/extensions.json`?**

Other templates indirectly recommend extensions via the README, but this file allows VS Code to prompt the user to install the recommended extension upon opening the project.

**Why enable `allowJs` in the TS template?**

While `allowJs: false` would indeed prevent the use of `.js` files in the project, it does not prevent the use of JavaScript syntax in `.svelte` files. In addition, it would force `checkJs: false`, bringing the worst of both worlds: not being able to guarantee the entire codebase is TypeScript, and also having worse typechecking for the existing JavaScript. In addition, there are valid use cases in which a mixed codebase may be relevant.

**Why is HMR not preserving my local component state?**

HMR state preservation comes with a number of gotchas! It has been disabled by default in both `svelte-hmr` and `@sveltejs/vite-plugin-svelte` due to its often surprising behavior. You can read the details [here](https://github.com/rixo/svelte-hmr#svelte-hmr).

If you have state that's important to retain within a component, consider creating an external store which would not be replaced by HMR.

```ts
// store.ts
// An extremely simple external store
import { writable } from 'svelte/store'
export default writable(0)
```
