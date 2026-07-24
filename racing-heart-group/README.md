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

### Gallery — done

Five site photographs in `assets/gallery/`, ordered as an installation
narrative: chamber being fitted, chamber set and connected, completed
installation, municipal site visit, and a resident with her new toilet.

Each exists at two widths — `NN.jpg` (800px) for the tiles and `NN@2x.jpg`
(1600px) for retina and the lightbox — selected via `srcset`. The camera
originals were 3–4 MB each; the whole set is now about 2 MB.

**All EXIF was stripped during processing.** Three of the originals carried
GPS coordinates, which would have published the exact location of the
beneficiaries' homes. If you add more photos, strip metadata the same way:

```sh
ffmpeg -i ORIGINAL.jpg -map_metadata -1 \
  -vf "scale='if(gt(iw,ih),1600,-2)':'if(gt(iw,ih),-2,1600)'" -q:v 4 NN@2x.jpg
```

`-map_metadata -1` is what removes the GPS. Do not skip it.

Tiles crop to 4:3; `.gallery__item--low` and `--high` bias that crop toward
the subject on portrait sources. The lightbox always shows the full frame.
Keep `alt` text and `.gallery__cap` captions accurate to the photo — they
describe the image to screen readers and drive the lightbox caption.

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
