# assets/

`index.html` looks for a headshot at:

```
assets/headshot.jpg
```

(referenced at `index.html:474`). If the file isn't present, the `onerror`
handler on that `<img>` automatically swaps it for a "VL" monogram avatar, so
the site works fine with this folder empty — the photo is optional polish,
not a requirement.

To add a headshot:
1. Drop a photo in here named exactly `headshot.jpg`.
2. Use a square (1:1) crop, at least 300×300px, reasonably compressed
   (this is a single-file site with no image pipeline — keep it under ~200KB).
3. Reload the page — no code changes needed.
