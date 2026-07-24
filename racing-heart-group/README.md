# Racing Heart Group — website

Single-page marketing site for Racing Heart Group (PTY) LTD, built as one
self-contained `index.html`. No build step, no dependencies — open the file
in a browser or drop the folder on any static host.

## Media

### Hero video — done

`assets/hero.mp4` is the Bio-Separator Toilet System explainer (3:11),
transcoded from the original `IMG_3046.mov`. The source was **HEVC/H.265 in a
QuickTime container**, which Chrome and Firefox cannot play, so it was
re-encoded to H.264 High\@4.0 + AAC-LC — supported by every current browser —
with `+faststart` so playback begins before the file finishes downloading.
`assets/hero-poster.jpg` is the title card, shown before play.

The source is only 568x320, so it is soft on large or high-DPI screens. The
hero frame renders it at roughly its native width, which is about as good as
it gets. If a higher-resolution master exists, re-encode with the same
settings and drop it in:

```sh
ffmpeg -i MASTER.mov -c:v libx264 -preset slow -crf 21 -pix_fmt yuv420p \
  -profile:v high -level 4.0 -c:a aac -b:a 128k -movflags +faststart hero.mp4
```

### Gallery — still placeholders

The six tiles use generated placeholder graphics. Replace them by dropping
photos at `assets/gallery/01.jpg` … `06.jpg` and pointing each
`.gallery__item img` `src` at its file.

Keep the `alt` text and `.gallery__cap` captions accurate to whatever photo
you swap in — they describe the image to screen readers and drive the
lightbox caption.

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
