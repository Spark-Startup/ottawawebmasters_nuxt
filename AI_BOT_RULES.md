# AI Bot Development Rules & Best Practices

## 🎯 Core Principles
- **Performance First**: Every decision must consider page speed and user experience
- **Accessibility Always**: WCAG 2.1 AA compliance is mandatory
- **SEO Optimized**: Search engine visibility is essential
- **Code Consistency**: Follow established patterns and standards
- **Test Coverage**: All functions must have corresponding tests
- **Modern Standards**: ES6+ modules only, SSR-first approach

## 🚀 Performance & Page Speed

### Critical Requirements
- **Core Web Vitals**:
  - LCP (Largest Contentful Paint) < 2.5s
  - FID (First Input Delay) < 100ms
  - CLS (Cumulative Layout Shift) < 0.1
- **Bundle Size**: Keep JavaScript bundles < 200KB gzipped
- **Image Optimization**: Use WebP/AVIF formats, lazy loading
- **Critical CSS**: Inline critical styles, defer non-critical CSS
- **Font Loading**: Use `font-display: swap` and preload critical fonts

### Implementation Rules
- Implement tree-shaking for unused code elimination
- Use dynamic imports for route-based code splitting
- Enable Nuxt's built-in performance optimizations
- Minimize third-party scripts and track their impact
- Use service workers for caching strategies

## ♿ Accessibility Standards

### WCAG 2.1 AA Compliance
- **Keyboard Navigation**: All interactive elements accessible via keyboard
- **Screen Reader Support**: Proper ARIA labels and semantic HTML
- **Color Contrast**: Minimum 4.5:1 ratio for normal text, 3:1 for large text
- **Focus Management**: Visible focus indicators and logical tab order
- **Alternative Text**: Descriptive alt text for all images

### Implementation Requirements
- Use semantic HTML5 elements (`<nav>`, `<main>`, `<section>`, etc.)
- Implement skip links for main content
- Ensure form labels are properly associated
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Validate with axe-core accessibility testing

## 🔍 SEO Optimization

### Technical SEO
- **Meta Tags**: Unique title and description for each page
- **Structured Data**: JSON-LD schema markup where applicable
- **Open Graph**: Social media preview optimization
- **XML Sitemap**: Auto-generated and submitted to search engines
- **Robots.txt**: Proper crawling directives

### Content SEO
- **Heading Structure**: Logical H1-H6 hierarchy
- **Internal Linking**: Strategic linking between related pages
- **URL Structure**: Clean, descriptive URLs
- **Page Speed**: Fast loading times boost rankings
- **Mobile-First**: Responsive design and mobile optimization

### Nuxt-Specific SEO
```javascript
// Use Nuxt SEO module for automated optimization
export default defineNuxtConfig({
  modules: ['@nuxtjs/seo'],
  seo: {
    baseURL: 'https://yoursite.com'
  }
})
```

## 💻 Code Consistency Rules

### JavaScript/TypeScript Standards
- **ES6+ Only**: Use modern JavaScript features exclusively
- **Module System**: ES6 imports/exports only, no CommonJS
- **Async/Await**: Prefer over Promise chains
- **Arrow Functions**: Use for consistency unless `this` binding required
- **Destructuring**: Use object/array destructuring where appropriate

### Vue/Nuxt Patterns
- **Composition API**: Use `<script setup>` syntax
- **Auto-imports**: Leverage Nuxt's auto-import system
- **Component Naming**: PascalCase for components, kebab-case for files
- **Props/Emits**: Explicit typing with TypeScript
- **State Management**: Use Pinia for complex state

### File Structure
```
/
├── components/
│   ├── UI/          # Reusable UI components
│   ├── Layout/      # Layout components
│   └── Feature/     # Feature-specific components
├── composables/     # Reusable composition functions
├── pages/          # File-based routing
├── server/         # Server-side code
├── types/          # TypeScript type definitions
└── utils/          # Utility functions
```

## 🧪 Testing Requirements

### Coverage Standards
- **Unit Tests**: 80% minimum code coverage
- **Component Tests**: All Vue components must have tests
- **E2E Tests**: Critical user journeys covered
- **Accessibility Tests**: Automated a11y testing integrated

### Testing Stack
- **Unit Testing**: Vitest for fast unit tests
- **Component Testing**: Vue Test Utils + Testing Library
- **E2E Testing**: Playwright for cross-browser testing
- **Visual Testing**: Chromatic or similar for UI regression

### Test Structure
```javascript
// components/MyComponent.spec.ts
import { describe, it, expect } from 'vitest'
import { mount } from '@vue/test-utils'
import MyComponent from './MyComponent.vue'

describe('MyComponent', () => {
  it('renders correctly', () => {
    const wrapper = mount(MyComponent)
    expect(wrapper.text()).toContain('Expected content')
  })
})
```

## 🏗️ SSR (Server-Side Rendering) Rules

### Nuxt SSR Configuration
- **Universal Mode**: Enable SSR by default
- **Hydration**: Ensure smooth client-side hydration
- **Meta Tags**: Server-rendered for SEO benefits
- **Data Fetching**: Use `$fetch` and `useFetch` composables

### SSR Best Practices
- Avoid browser-only APIs in SSR context
- Use `process.client` checks when necessary
- Implement proper error handling for SSR failures
- Optimize for both server and client performance

### Data Fetching Patterns
```javascript
// pages/index.vue
<script setup>
// SSR-friendly data fetching
const { data: posts } = await $fetch('/api/posts')

// Client-side hydration safe
const { data: user } = await useFetch('/api/user', {
  server: false // Client-only if needed
})
</script>
```

## 🎨 Styling Guidelines

### CSS Architecture
- **Utility-First**: Use Tailwind CSS for consistent spacing/colors
- **Component Styles**: Scoped styles for component-specific CSS
- **CSS Modules**: For complex component styling
- **Custom Properties**: Use CSS variables for theming

### Responsive Design
- **Mobile-First**: Design for mobile, enhance for desktop
- **Breakpoints**: Consistent breakpoint system
- **Flexible Layouts**: Use CSS Grid and Flexbox
- **Touch Targets**: Minimum 44px for interactive elements

## 🔧 Development Workflow

### Code Quality Tools
- **ESLint**: Automated code linting
- **Prettier**: Code formatting
- **TypeScript**: Type checking
- **Husky**: Git hooks for pre-commit checks

### Git Workflow
- **Conventional Commits**: Structured commit messages
- **Branch Naming**: `feature/`, `bugfix/`, `hotfix/` prefixes
- **Pull Requests**: Required for all changes
- **Code Review**: Mandatory peer review

### Performance Monitoring
- **Lighthouse CI**: Automated performance testing
- **Bundle Analysis**: Regular bundle size monitoring
- **Core Web Vitals**: Continuous monitoring in production
- **Error Tracking**: Implement error monitoring (Sentry, etc.)

## 📝 Documentation Requirements

### Code Documentation
- **JSDoc**: Document all functions and complex logic
- **README**: Keep project README up to date
- **API Documentation**: Document all API endpoints
- **Component Docs**: Document props, events, and usage

### Change Documentation
- **Changelog**: Maintain detailed changelog
- **Migration Guides**: Document breaking changes
- **Architecture Decisions**: Record significant technical decisions

---

**Remember**: These rules are living guidelines. Update them as the project evolves and new best practices emerge.