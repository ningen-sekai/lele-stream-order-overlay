# Stream Orders — scrolling channel-point ticker

Viewers redeem a channel-point reward and type a message ("order"); it scrolls
across a full-width bar right-to-left as a continuous crawl and fades out at the
edges. Shows `Name → their text`.

- One file, `index.html`. No build step.
- **The bar is hidden until someone redeems**, fades in with their order, and fades
  back out once nothing is left to show.
- Each order crosses the bar **once**. Multiple redemptions chain one after another,
  in order; when the last one clears, the bar fades away.
- Uses the **same Twitch app** as the Lost Meter overlay (Client ID is baked in).

## See it now (no setup)
**Double-click `index.html`** → it opens in preview mode. Press **T** a few times to
watch orders crawl across. Hotkeys: **T** test · **R** clear · **S** settings · **C** connect.

## Connect it to Twitch
1. **Reward:** in the streamer's Creator Dashboard, make a Channel-Points reward with
   **"Require viewer to enter text" turned ON**, and put the word **order** in its
   name (e.g. `Give Lele an order`). Affiliate/Partner required.
2. **Host it** (Twitch login needs an https/localhost URL — a `file://` page can't log
   in). GitHub Pages is easiest; see the Lost Meter README for the exact steps.
3. **Add the redirect URL:** in your existing Twitch app at dev.twitch.tv/console,
   add this page's hosted URL to the app's **OAuth Redirect URLs** list (an app can
   have several). It must match the page URL exactly.
4. Open the hosted page → **⚙ / press S** → confirm the reward filter → **Connect to
   Twitch** → the streamer logs in with their account → dot turns green.
5. Add the same URL to OBS as a **Browser Source**. Make it **1920 × 1080** (full
   canvas) — the bar is a fixed-height strip that anchors itself (bottom by default;
   set Top/Center in the panel). Adjust **Bar height** and **Position** in ⚙.

## Configure by URL

```
index.html?reward=order&speed=100&name=1&accent=54D2FF
```

| Param | Meaning | Default |
|-------|---------|---------|
| `clientId` | Twitch app Client ID | (baked in) |
| `reward` | reward-title text to match (`any` = all) | `order` |
| `speed` | crawl speed, px/sec | `100` |
| `maxlen` | max characters shown per order | `200` |
| `height` | bar height in px | `64` |
| `pos` | bar position: `bottom`, `top`, `center` | `bottom` |
| `name` | `1` show submitter name, `0` hide | `1` |
| `accent` | hex accent color (no `#`) | `54D2FF` |
| `idle` | faint text shown when no orders | (blank) |
| `preview` | force the dark preview backdrop | off |

Panel settings save in the browser; URL params override them.

## Notes
- Browser tokens last ~4h — reconnect at the start of each stream (in OBS: right-click
  the source → Interact → Connect).
- The bar is a fixed-height, full-width strip that anchors itself within the source, so
  a normal 1920×1080 browser source works — the bar sits at the bottom (or top/center).
