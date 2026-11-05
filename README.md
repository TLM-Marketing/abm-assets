# ABM assets

Public image and video files referenced from PathFactory personalization CSVs. Nothing else
belongs here: no documents, no data, no state files. Layout:

```
<client-slug>/<campaign>/<segment>-<field-merge>.<png|jpg|webp|gif|svg|mp4|webm>
```

Files are published with `publish_asset.py` from the ABM Experience skill, which refuses anything
that is not a media file. The `images-only` check on every push fails the build if a non-media
file lands here anyway. The raw URL of a file is
`https://raw.githubusercontent.com/TLM-Marketing/abm-assets/main/<path>`.

Everything in this repository is visible to anyone on the internet. Only upload images cleared
for a public landing page.

## After the first push (repository owner, once)

1. Settings > Branches > add a rule for `main` with "Require status checks to pass" and pick
   `images-only`.
2. Settings > Code security > enable "Push protection" under secret scanning.
3. Open `https://raw.githubusercontent.com/TLM-Marketing/abm-assets/main/_test/brightreel-test-hero.webp`
   in a browser: if the image shows, the hosting works and the `_test/` folder can be deleted.
