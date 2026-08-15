# NocturneSVG

A single-file interception web proxy built on [Scramjet](https://github.com/MercuryWorkshop/scramjet),
styled to match the main **Nocturne** theme (midnight palette, Inter, lavender accent, aurora backdrop).
Pure static — no backend to host. Drop it on GitHub Pages / jsDelivr and go.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The proxy page. All paths are relative, so it works from any location. |
| `proxy.svg` | The same page wrapped in `<svg><foreignObject>` — a browser renders it as full HTML from a `.svg` URL. |
| `sw.js` | Service worker that routes requests through the Scramjet controller. |
| `scj/` | Scramjet engine bundle (`scj.js`) and WASM (`scj.wasm`). |
| `controller/` | Scramjet controller inject script. |

## Deploying on jsDelivr

Push to a public GitHub repo, then link to either:

```
https://cdn.jsdelivr.net/gh/<owner>/<repo>@<branch>/index.html
https://cdn.jsdelivr.net/gh/<owner>/<repo>@<branch>/proxy.svg
```

The service worker registers within the file's own directory, and the engine, WASM,
controller, and `sw.js` all resolve relatively from that same path.

## Notes

- Transport uses a WISP server (`wss://nocturne.lol/wisp/`) — the network tunnel every
  interception proxy needs. Swap it in the `LibcurlClient` config inside `index.html` /
  `proxy.svg` to point elsewhere.
- Service workers require an `https` (or `localhost`) origin — opening the file over
  `file://` will fail with a `null` origin. jsDelivr / GitHub Pages serve over `https`.
- `Ctrl + Shift + Z` exits the proxied frame overlay.
