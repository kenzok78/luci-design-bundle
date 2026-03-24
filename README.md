# LuCI Design Bundle

This repository bundles two OpenWrt LuCI projects into one tree:

- `luci-theme-design`
- `luci-app-design-config`

Integration instructions: `OPENWRT_INTEGRATION.md`

## Included Fixes

### luci-theme-design

- Fixed Lua menu URL query handling bug in `header.htm` (`k.query` -> `nnode.query`).
- Replaced unsafe JSON parsing (`eval`) with `JSON.parse` in theme XHR helper.
- Improved JSON `Content-Type` matching to support `application/json; charset=utf-8`.
- Hardened menu matching logic in `script.js`:
  - escaped regex input,
  - replaced array `for...in` with index loop,
  - added null-safe href checks.

### luci-app-design-config

- Added explicit `nixio.fs` require in controller and used local `fs` accessor.
- Removed invalid debug write (`/tmp/aaa`) from form handler.
- Limited UCI writes to intended keys only: `mode`, `navbar`, `navbar_proxy`.
- Added auto-create fallback for missing `design` `global` section.
- Added safe defaults for first-run configs:
  - `mode=normal`
  - `navbar=display`
  - `navbar_proxy=shadowsocksr`
- Fixed README release link typo (`hhttps://` -> `https://`).

## Layout

```
.
├── luci-theme-design/
└── luci-app-design-config/
```
