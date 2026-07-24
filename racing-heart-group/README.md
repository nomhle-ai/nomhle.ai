# Racing Heart Group — website

Single-page marketing site for Racing Heart Group (PTY) LTD, built as one
self-contained `index.html`. No build step, no dependencies — open the file
in a browser or drop the folder on any static host.

## Adding your media

The hero video and the gallery ship with placeholder graphics. Replace them:

| Slot | Drop the file at | Then |
| --- | --- | --- |
| Hero video | `assets/hero.mp4` (and optionally `assets/hero.webm`) | Replace the `poster` data-URI on the `<video>` with `assets/hero-poster.jpg` |
| Gallery photos | `assets/gallery/01.jpg` … `06.jpg` | Point each `.gallery__item img` `src` at its file |

Keep the `alt` text and `.gallery__cap` captions accurate to whatever photo
you swap in — they describe the image to screen readers and drive the
lightbox caption.

Prefer a YouTube/Vimeo embed instead? Swap the `<video>` element inside
`.hero__media` for the provider's `<iframe>`; the surrounding frame and
caption styling still apply.

## Contact form

The form currently validates and shows a confirmation state, but **does not
send anything** — there is no backend. To receive real enquiries, point it at
a form endpoint (Formspree, Netlify Forms, Web3Forms, etc.):

```html
<form id="contact-form" action="https://your-endpoint" method="POST">
```

and remove the `e.preventDefault()` branch in the inline script, or post via
`fetch` and keep the existing success panel.

## Structure

Nav · Hero (copy + video + stats) · Technology · How It Works · Installation ·
Gallery · Benefits · Projects · Contact · Footer

Design tokens (colours, fonts, spacing) live in the `:root` block at the top
of the `<style>` element — change the accent colour in one place with
`--accent`.
