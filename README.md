<!-- Copyright © 2026 CV SATRIA TEKNOLOGI. All rights reserved. (cvsatriateknologi.com) -->

# 500 Error Page — Kinetic Typography

A self-contained `500.html` built with HTML, CSS and GSAP 3.12.5 (from cdnjs).

## Why a single file
An error page gets served from whatever URL failed (for example `/shop/cart/42`), often while the app server is unhealthy. Relative `css/`/`js/` paths would break, so all CSS and JS is inlined. GSAP and Google Fonts are the only external requests, and the page still works without them: everything stays visible, with no animation and system fonts.

## Customize
| What | Where |
|---|---|
| Logo | `.logo-slot` in the header. Replace the placeholder `<span>` with an `<img>` (use an absolute path) or an inline `<svg>`. The box is about 168×48 px. |
| Status page link | `.pill` `href` in the header |
| Help center link | footer `<nav>` |
| Support email | `data-support` link in the details card. The reference, time and URL are added to the email automatically. |
| Brand colors | `:root` tokens: `--accent`, `--signal`, `--bg`, `--ink` |

## Reference ID — important
By default the page **generates a reference ID in the browser**. That ID does **not** exist in your server logs. To make it useful to support, have your server render the real request/trace ID:

```html
<code data-ref data-server="true">req_8f3a…</code>
```

## Motion
- Intro: the numerals rise while their variable `wght`/`wdth` axes "inflate", the headline reveals word by word, and the content cascades in.
- Numerals react to pointer proximity, and breathe in a wave when the pointer is idle or on touch screens.
- Occasional RGB-split glitch on a single numeral.
- Background marquees speed up and skew with pointer or scroll velocity.
- Magnetic buttons (mouse/trackpad only).
- `prefers-reduced-motion: reduce` turns all of this off.

## Server wiring (examples)
- **Nginx:** `error_page 500 502 503 504 /500.html; location = /500.html { root /var/www/errors; internal; }`
- **Laravel:** copy the file to `resources/views/errors/500.blade.php`. Escape any `@` signs as `@@` if you add Blade directives.
