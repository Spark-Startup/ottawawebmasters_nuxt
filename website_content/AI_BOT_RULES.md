
# AI Bot & Web Project Rules & Best Practices

## 📚 Introduction
This document outlines the essential rules, standards, and best practices for developing AI bots and web projects in this repository. It is intended for all contributors—developers, designers, and automation engineers. These guidelines ensure high-quality, maintainable, ethical, and performant solutions.

> **Note:** These rules are living guidelines. Propose improvements via pull request as best practices evolve.


## 🎯 Core Principles
- **Performance First:** Prioritize page speed and user experience in every decision.
- **Accessibility Always:** WCAG 2.1 AA compliance is mandatory.
- **SEO Optimized:** Ensure search engine visibility.
- **Code Consistency:** Follow established patterns and standards.
- **Test Coverage:** All functions must have corresponding tests.
- **Modern Standards:** Use ES6+ modules and SSR-first approach.
- **Ethical AI:** Ensure responsible, transparent, and privacy-respecting AI/automation.
## 🤖 AI & Automation Rules

### Core AI Ethics
- **Prompt Design:** Write clear, unambiguous prompts for AI bots. Document prompt logic and expected outcomes.
- **Data Privacy:** Never expose sensitive or personal data in prompts, logs, or outputs. Follow [GDPR](https://gdpr.eu/) and [PIPEDA](https://www.priv.gc.ca/en/) guidelines.
- **Bias Mitigation:** Regularly review AI outputs for bias or inappropriate content. Use diverse datasets and document known limitations.
- **Transparency:** Clearly indicate when users are interacting with an AI or automated system.
- **Human Oversight:** Provide escalation paths for users to reach a human when needed.

### AI Implementation Standards
- **Error Handling:** Implement graceful fallbacks when AI services are unavailable.
- **Rate Limiting:** Implement proper throttling to prevent API abuse.
- **Caching:** Cache AI responses where appropriate to reduce costs and latency.
- **Monitoring:** Track AI performance, costs, and usage patterns.
- **Logging:** Log AI/automation actions for traceability, but never log sensitive data.


## 🚀 Performance & Page Speed


### Critical Requirements
- **Core Web Vitals:**
  - LCP (Largest Contentful Paint) < 2.5s
  - INP (Interaction to Next Paint) < 200ms (replacing FID)
  - CLS (Cumulative Layout Shift) < 0.1
- **Bundle Size:** JavaScript bundles < 200KB gzipped per route.
- **Image Optimization:** Use WebP/AVIF formats, lazy loading, responsive images.
- **Critical CSS:** Inline critical styles < 14KB, defer non-critical CSS.
- **Font Loading:** Use `font-display: swap` and preload critical fonts.
- **Resource Hints:** Use `preload`, `prefetch`, and `dns-prefetch` strategically.


### Implementation Rules
- Use tree-shaking to eliminate unused code.
- Use dynamic imports for route-based code splitting.
- Enable Nuxt's built-in performance optimizations.
- Minimize third-party scripts and monitor their impact.
- Use service workers for caching strategies ([MDN Guide](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)).


## ♿ Accessibility Standards


### WCAG 2.1 AA Compliance
- **Keyboard Navigation:** All interactive elements accessible via keyboard.
- **Screen Reader Support:** Proper ARIA labels and semantic HTML.
- **Color Contrast:** Minimum 4.5:1 for normal text, 3:1 for large text.
- **Focus Management:** Visible focus indicators and logical tab order.
- **Alternative Text:** Descriptive alt text for all images.


### Implementation Requirements
- Use semantic HTML5 elements (`<nav>`, `<main>`, `<section>`, etc.).
- Implement skip links for main content.
- Ensure form labels are properly associated.
- Test with screen readers (NVDA, JAWS, VoiceOver).
- Validate with [axe-core](https://www.deque.com/axe/) accessibility testing.


## 🔍 SEO Optimization


### Technical SEO
- **Meta Tags:** Unique title and description for each page.
- **Structured Data:** JSON-LD schema markup where applicable.
- **Open Graph:** Social media preview optimization.
- **XML Sitemap:** Auto-generated and submitted to search engines.
- **Robots.txt:** Proper crawling directives.


### Content SEO
- **Heading Structure:** Logical H1-H6 hierarchy.
- **Internal Linking:** Strategic linking between related pages.
- **URL Structure:** Clean, descriptive URLs.
- **Page Speed:** Fast loading times boost rankings.
- **Mobile-First:** Responsive design and mobile optimization.


### Nuxt-Specific SEO
```js
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
- **ES6+ Only:** Use modern JavaScript features exclusively.
- **Module System:** ES6 imports/exports only, no CommonJS.
- **Async/Await:** Prefer over Promise chains.
- **Arrow Functions:** Use for consistency unless `this` binding required.
- **Destructuring:** Use object/array destructuring where appropriate.


### Vue/Nuxt Patterns
- **Composition API:** Use `<script setup>` syntax.
- **Auto-imports:** Leverage Nuxt's auto-import system.
- **Component Naming:** PascalCase for components, kebab-case for files.
- **Props/Emits:** Explicit typing with TypeScript.
- **State Management:** Use Pinia for complex state.


### File Structure
```text
/
├── components/
│   ├── ui/           # Reusable UI components (buttons, inputs, etc.)
│   ├── layout/       # Layout components (header, footer, sidebar)
│   └── feature/      # Feature-specific components
├── composables/      # Reusable composition functions
├── content/          # Content files (markdown, JSON)
├── pages/            # File-based routing
├── plugins/          # Nuxt plugins
├── server/           # Server-side code (API routes, middleware)
├── stores/           # Pinia stores for state management
├── types/            # TypeScript type definitions
└── utils/            # Utility functions and helpers
```


## 🧪 Testing Requirements


### Coverage Standards
- **Unit Tests:** 80% minimum code coverage.
- **Component Tests:** All Vue components must have tests.
- **E2E Tests:** Critical user journeys covered.
- **Accessibility Tests:** Automated a11y testing integrated.


### Testing Stack
- **Unit Testing:** [Vitest](https://vitest.dev/) for fast unit tests.
- **Component Testing:** [Vue Test Utils](https://test-utils.vuejs.org/) + [Testing Library](https://testing-library.com/).
- **E2E Testing:** [Playwright](https://playwright.dev/) for cross-browser testing.
- **Visual Testing:** [Chromatic](https://www.chromatic.com/) or similar for UI regression.


### Test Structure
```js
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
- **Universal Mode:** Enable SSR by default.
- **Hydration:** Ensure smooth client-side hydration.
- **Meta Tags:** Server-rendered for SEO benefits.
- **Data Fetching:** Use `$fetch` and `useFetch` composables.


### SSR Best Practices
- Avoid browser-only APIs in SSR context.
- Use `process.client` checks when necessary.
- Implement proper error handling for SSR failures.
- Optimize for both server and client performance.


### Data Fetching Patterns
```js
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
- **Utility-First:** Use [Tailwind CSS](https://tailwindcss.com/) for consistent spacing/colors.
- **Component Styles:** Scoped styles for component-specific CSS.
- **CSS Modules:** For complex component styling.
- **Custom Properties:** Use CSS variables for theming.


### Responsive Design
- **Mobile-First:** Design for mobile, enhance for desktop.
- **Breakpoints:** Consistent breakpoint system.
- **Flexible Layouts:** Use CSS Grid and Flexbox.
- **Touch Targets:** Minimum 44px for interactive elements.


## 🔧 Development Workflow


### Code Quality Tools
- **ESLint:** Automated code linting.
- **Prettier:** Code formatting.
- **TypeScript:** Type checking.
- **Husky:** Git hooks for pre-commit checks.


### Git Workflow
- **Conventional Commits:** Structured commit messages ([Conventional Commits](https://www.conventionalcommits.org/)).
- **Branch Naming:** `feature/`, `bugfix/`, `hotfix/` prefixes.
- **Pull Requests:** Required for all changes.
- **Code Review:** Mandatory peer review.


### Performance Monitoring
- **Lighthouse CI:** Automated performance testing.
- **Bundle Analysis:** Regular bundle size monitoring.
- **Core Web Vitals:** Continuous monitoring in production.
- **Error Tracking:** Implement error monitoring ([Sentry](https://sentry.io/), etc.).


## 📝 Documentation Requirements


### Code Documentation
- **JSDoc:** Document all functions and complex logic.
- **README:** Keep project README up to date.
- **API Documentation:** Document all API endpoints.
- **Component Docs:** Document props, events, and usage.


### Change Documentation
- **Changelog:** Maintain detailed changelog following [Keep a Changelog](https://keepachangelog.com/) format.
- **Migration Guides:** Document breaking changes with step-by-step upgrade instructions.
- **Architecture Decisions:** Record significant technical decisions ([ADR Guide](https://adr.github.io/)).
- **Performance Metrics:** Document performance benchmarks and improvements.

---

## 🔒 Security Guidelines

### Code Security
- **Input Validation:** Validate all user inputs on both client and server.
- **XSS Prevention:** Use proper escaping and Content Security Policy.
- **CSRF Protection:** Implement CSRF tokens for state-changing operations.
- **Environment Variables:** Never commit secrets; use `.env` files and proper secret management.
- **Dependencies:** Regularly audit and update dependencies for security vulnerabilities.

### API Security
- **Authentication:** Implement proper JWT or session-based authentication.
- **Authorization:** Verify user permissions for each protected resource.
- **Rate Limiting:** Implement API rate limiting to prevent abuse.
- **HTTPS Only:** Enforce HTTPS in production environments.

## 🤝 Contributing & Proposing Changes

### Before Contributing
- Read these rules thoroughly before contributing.
- Check existing issues and PRs to avoid duplication.
- Set up the development environment according to project README.

### Contribution Process
- Fork the repository and create a feature branch.
- Follow conventional commit messages.
- Ensure all tests pass and meet coverage requirements.
- Update documentation for any new features or changes.
- Submit PR with clear description and rationale.

### Code Review Process
- All PRs require peer review before merging.
- Address review feedback promptly and professionally.
- Maintain discussion in PR comments for transparency.

---

**Remember:** These rules are living guidelines. Update them as the project evolves and new best practices emerge.