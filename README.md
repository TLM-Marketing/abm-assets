# ABM assets

Public image and video files referenced from PathFactory personalization CSVs. Nothing else
belongs here: no documents, no data, no state files. Layout:

```
<client-slug>/<campaign>/<segment>-<field-merge>.<png|jpg|webp|gif|svg|mp4|webm>
```

Files are published with `publish_asset.py` from the ABM Experience skill, which refuses anything
that is not a media file. The `images-only` check on every push fails the build if a non-media
file lands here anyway. The raw URL of a file is
`https://raw.githubusercontent.com/<org>/<repo>/main/<path>`.

## Renders requested from a claude.ai chat (`_inbox/`)

A claude.ai chat cannot download an image from Recraft itself, so it commits a request file
`_inbox/<client>-<campaign>-<name>.txt` with two lines, `url=https://img.recraft.ai/...` and
`path=<client>/<campaign>/<name>`. The `fetch-inbox` Action then downloads the image on GitHub,
checks it is an image from Recraft, stores it at that path with the right extension, removes the
request and commits as `github-actions[bot]`. A request that fails leaves
`_inbox/<name>.failed` with the reason. `publish_asset.py --request-url` writes the request and
waits for the file. Only `img.recraft.ai` links are accepted.

Everything in this repository is visible to anyone on the internet. Only upload images cleared
for a public landing page.
