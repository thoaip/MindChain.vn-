# Handoff

## State
MindChain.vn (static HTML, repo thoaip/MindChain.vn-, branch main) is done and LIVE at https://thoaip.github.io/MindChain.vn- via GitHub Pages. Last commit `1e49840` + `023cb89` (onboarding doc). Full VI localization, AI-education pivot, real photos in assets/images/real, hero 3-photo collage, instructor team, AI course packages ("Liên hệ báo giá"), Vision/Mission, 6 real news items. Working tree clean. Sibling project TVWeb (Next.js, repo thoaip/TVWeb) is GitHub-source-only (no Netlify, run local), clean at `c22aefb`.

## Next
1. Optional: connect custom domain mindchain.vn (DNS + CNAME file).
2. Optional: rename homepage "Cảm nhận" section → "Sự kiện & Hội thảo" (now shows a real seminar poster).
3. Swap any remaining template placeholder images as real assets arrive.

## Context
- All edits/overrides go in the injected `<style>` block in each .html `<head>` (search `.mc-member`) — never hand-edit `assets/css/style.css`.
- CRITICAL: do NOT re-enable SplitType per-char on headings in `main.js` (breaks Vietnamese words); titleAnimation now uses a whole-title `gsap.from` fade. Bump `main.js?v=` cache-bust on any JS change.
- Optimize new images with sharp (~50-180KB). Verify deploys with `?v=<ts>` cache-bust.
- See docs/ONBOARDING.md for full guide.
