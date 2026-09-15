# Bayside Home Builders — Google Ads landing page (static)

Static HTML. No build step, no framework, no dependencies.

## Structure

```
.nojekyll                          empty file — stops GitHub's Jekyll processing
CNAME                              offers.baysidehomebuilders.com
index.html                         redirect to the landing page
home-renovation-phoenix/index.html the landing page
thank-you/index.html               form fallback destination + conversion page
assets/                            11 WebP images (~420 KB total)
```

## Deploy to GitHub Pages

1. Create a public repo and commit everything in this folder at the repo root.
2. Settings → Pages → Source: "Deploy from a branch" → `main` / `/ (root)`.
3. At your DNS host add a CNAME record: host `offers`, value `USERNAME.github.io`.
4. Settings → Pages → Custom domain → `offers.baysidehomebuilders.com` → Save.
5. Wait for the certificate, then check **Enforce HTTPS**.

Final URL for the ad: `https://offers.baysidehomebuilders.com/home-renovation-phoenix/`

> The CNAME file assumes `baysidehomebuilders.com`. If the ads still display
> `azbaysidehomeimprovement.com`, change CNAME to a subdomain of that domain
> instead — Google Ads requires the display URL domain to match the final URL.

## Before spending money

- [ ] **Activate FormSubmit.** Submit the form once from the live URL. FormSubmit
      emails `sales@baysidehi.net` an activation link; until someone clicks it,
      no lead is delivered. Test again after activating.
- [ ] **Replace the three video testimonial names.** Search for
      `Homeowner name TBD` (3 occurrences).
- [ ] **Add conversion tracking.** Paste the Google Ads gtag snippet in `<head>`.
      The page already fires `gtag('event','conversion', …)` on form success and
      on every `tel:` click, and pushes `lead_form_submit` / `call_click` to
      `dataLayer` if you use GTM. No code change needed, just the tag.
- [ ] Check `_next` in the form points at the live thank-you URL (currently
      `https://offers.baysidehomebuilders.com/thank-you/`). This only matters for
      the no-JS fallback path; the normal path shows the inline success panel.
- [ ] Run PageSpeed Insights on mobile.

## Notes

- `noindex, follow` is set deliberately so this page never competes with the
  main site organically. Do not remove it.
- Fonts load from Google Fonts. To remove that third-party request, self-host
  the three families in `assets/` and swap the `<link>` for an `@font-face` block.
- Asset paths are relative (`../assets/…`), so the page works at the subdomain
  root, at a repo subpath, and opened straight off disk.
- Images are compressed WebP. If you replace any, keep the `width`/`height`
  attributes accurate — they prevent layout shift.
- Cost figures are deliberately absent from this page. The "What shapes your
  estimate" section answers the price question without publishing numbers.
