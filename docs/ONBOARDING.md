# MindChain.vn — Onboarding & Handoff Guide

> Hand-written from the build session (no knowledge-graph). Last commit at handoff: `1e49840`.

## 1. Project Overview
- **What:** Marketing website for **MindChain** (Công ty Cổ phần Chuỗi Tư Duy / MINDCHAIN JSC.), an AI technology & education brand, **a member unit of Tinh Vân Group**.
- **Type:** **Static HTML site** (no build step). Adapted from the *Inotek* "home-8 / AI Agency" HTML template.
- **Stack:** HTML5 + Bootstrap 5.3 + GSAP (ScrollTrigger/ScrollSmoother) + Swiper + AOS + jQuery. Fonts: **Manrope + Noto Sans**.
- **Brand color:** tech blue `#1053f3` (+ orange `#ff9d10`). Dark theme.
- **Repo:** https://github.com/thoaip/MindChain.vn-  (branch `main`)
- **Live:** https://thoaip.github.io/MindChain.vn-/ (GitHub Pages, source = `main` / root)
- **Contact in site:** hotline `0886 206 116`, `info@mindchain.vn`, *Số 37, Ngõ 97 Triều Khúc, P. Thanh Xuân Nam, Q. Thanh Xuân, Hà Nội*, YouTube `@mindchainacademy2583`.

## 2. How to Run / Deploy
```bash
# Local preview (any static server)
python -m http.server 8099    # -> http://localhost:8099
# or just open index.html
```
**Deploy:** push to `main` → GitHub Pages rebuilds automatically (~1–2 min). No build/CI.

## 3. Architecture / File Map
```
index.html              # Homepage (hero collage, services, solutions, choose, industries,
                        #   projects, team band, testimonials, news, footer)
about.html              # Về MindChain (about, Vision/Mission, instructor team)
service.html            # Dịch vụ AI (services + AI course/service packages)
contact.html            # Liên hệ (form, address, map)
service-details.html    # Service detail template page
assets/
  css/style.css         # Template stylesheet (large, compiled from sass/). DO NOT hand-edit;
                        #   override via the injected <style> block in each .html <head>.
  js/main.js            # Template behaviors (sliders, counters, title animation, sticky header)
  js/*.js               # gsap, ScrollTrigger, swiper, aos, lenis, jquery, split-type, etc.
  images/brand/         # mindchain-logo.svg, product logos (ae/bizdx/tvis/libol/kitano/...),
                        #   partners/ (tinhvan, accenture, r3, dainam, blockchainvn)
  images/real/          # REAL MindChain photos (hero-group, hero-books, students-lab, lab-demo,
                        #   seminar, aptech-ai, teacher-*, cert1-3, seminar-tester, ...)
  images/news/          # news1-6.jpg (real event thumbnails)
```

### Per-page custom CSS
Each page has an **injected `<style>` block** at the end of `<head>` (search `.mc-member`). It holds all our overrides: logo size, heading word-break, `.hero-collage`, hero subtext max-width, photo-background dimming, testimonial poster styling. **Add new overrides here**, not in `style.css`.

## 4. Key Concepts & Conventions
- **Content was localized to Vietnamese + pivoted to AI** from the English template via Python find/replace scripts (kept in `D:\TDX\mc_*.py`). For small edits, edit the HTML directly; for bulk text, a script is easier.
- **Vietnamese text must be NFC** (precomposed). The files already are.
- **Images:** optimize with `sharp` (we used the TVWeb project's `node_modules`) to ~50–180 KB before committing. Real photos live in `assets/images/real/`.
- **Logos:** main logo = `assets/images/brand/mindchain-logo.svg` (subtitle "Powered by Tinhvan Group", dimmed). Product/partner logos under `assets/images/brand/`.

## 5. ⚠️ Complexity Hotspots & Gotchas
1. **Title animation / Vietnamese word-break (CRITICAL).** `main.js → titleAnimation()` originally used **SplitType `types:'chars'`**, turning every heading character into an `inline-block` → Vietnamese words ("tương", "số") broke mid-word on wrap. **Fixed** by replacing the SplitType call with a whole-title `gsap.from(...)` fade. **Do NOT reintroduce per-character SplitType/SplitText on headings.** A global safety rule `h1..h5,.sec-title{word-break:normal!important}` is also in the injected CSS.
2. **Browser/CDN caching of `main.js`.** When you change `main.js`, **bump the cache-bust query** on every page: `src="assets/js/main.js?v=YYYYMMDDx"`. Otherwise users keep the old JS.
3. **`style.css` is huge & compiled** — never hand-edit; always override in the page `<style>` block with a specific selector (use `!important` to beat the template's runtime-injected styles, e.g. split-type / hero `counter-info{left:-140px}`).
4. **Template floating stat cards** (hero `counter-info` "60+", social-proof "30+") were designed for the old robot art; they fight the new photo collage. We currently keep them; re-positioning needs care (a prior attempt overlapped them — was reverted).
5. **Many template images are dimension placeholders** (e.g. `newsletter/img01.webp` shows "151x195"). Replace with real assets as needed.
6. **GitHub Pages cache** ~10 min on the CDN; verify deploys with `?v=<timestamp>` cache-busting in curl/browser.

## 6. Known TODO / Backlog
- Founder portraits: not shown (no labeled headshots) — team section uses **instructors by domain** instead.
- Optional: connect custom domain `mindchain.vn` (add DNS + `CNAME` file).
- Optional: rename "Cảm nhận" section → "Sự kiện & Hội thảo" (now shows a real seminar poster).
