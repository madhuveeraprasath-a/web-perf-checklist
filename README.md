# web-perf-checklist

A practical frontend performance checklist with scripts and tools for auditing FCP, LCP, bundle size, and script loading. Based on real-world optimizations that reduced login page FCP from 12s → 2.5s.

## Checklist

### Script Loading
- [ ] Defer non-critical third-party scripts
- [ ] Use `async` / `defer` attributes appropriately
- [ ] Audit Module Federation remotes — only load what's needed on each route
- [ ] Remove unused polyfills
- [ ] Tree-shake large dependencies

### Bundle Size
- [ ] Analyze bundle with `next-bundle-analyzer` or `webpack-bundle-analyzer`
- [ ] Code-split by route
- [ ] Lazy-load heavy components with `React.lazy` + `Suspense`
- [ ] Replace heavy libraries with lighter alternatives

### Images
- [ ] Use `next/image` or equivalent for automatic optimization
- [ ] Serve WebP/AVIF formats
- [ ] Set explicit `width` and `height` to prevent layout shifts
- [ ] Lazy-load below-fold images

### Fonts
- [ ] Use `font-display: swap`
- [ ] Preload critical fonts
- [ ] Self-host fonts to avoid render-blocking

### Core Web Vitals
- [ ] FCP < 1.8s
- [ ] LCP < 2.5s
- [ ] CLS < 0.1
- [ ] INP < 200ms

### Caching
- [ ] Set correct `Cache-Control` headers on static assets
- [ ] Use content hashing for cache busting
- [ ] Enable CDN for static assets

## Scripts

**Audit all scripts on a page:**
```bash
node scripts/audit-scripts.js https://yoursite.com
```

**Bundle size report:**
```bash
npm run analyze
```

**Lighthouse CI:**
```bash
npm run lighthouse -- --url https://yoursite.com
```

## Real-World Results

| Metric | Before | After | Improvement |
|---|---|---|---|
| First Contentful Paint | 12–13s | ~2.5s | ~5x faster |
| JS Transfer Size | 23.4 MB | 6.1 MB | −74% |
| Decoded JS Size | 76.9 MB | 19.6 MB | −75% |
| Scripts on load | 59 | ~10 | −83% |

**Approach:** Identified 59 unnecessary Module Federation scripts loading eagerly on the login page. Deferred them using dynamic imports — users now see the login UI in ~2.5s instead of 12–13s.

## Tools Used

- Chrome DevTools Performance panel
- Chrome DevTools MCP — automated performance profiling
- Lighthouse
- webpack-bundle-analyzer
- `web-vitals` npm package

## License

MIT
