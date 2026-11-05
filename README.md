# pocdownload — Vercel static site

Pure-black landing page + direct binary download route.

## Structure

```
pocdownload/
├── public/
│   ├── index.html            # black landing page (served at /)
│   └── file/
│       └── poc.exe           # ← UPLOAD YOUR poc.exe HERE
└── vercel.json               # rewrite rule: /poc.exe → /file/poc.exe
```

## Deploy

1. Drop your `poc.exe` into `public/file/`
2. Push to GitHub (or import the folder into Vercel)
3. In Vercel:
   - Framework Preset: **Other**
   - Root Directory: `pocdownload`
   - Build Command: *(leave empty)*
   - Output Directory: `public`
4. Deploy

## Routes after deploy

| URL                              | Serves                 |
| -------------------------------- | ---------------------- |
| `https://pocdownload.vercel.app/`         | `public/index.html`    |
| `https://pocdownload.vercel.app/poc.exe`  | `public/file/poc.exe`  |

The `vercel.json` rewrite makes `/poc.exe` resolve to the file stored
inside `/file/`, and the matching `headers` block forces the browser to
download the file (Content-Disposition: attachment) instead of trying
to render it.

## Notes

- `cleanUrls: true` strips `.html` extensions.
- `noindex, nofollow` is set on the landing page — search engines ignore it.
- If you rename the file, update both `public/file/poc.exe` AND the
  `vercel.json` rewrite destination.
