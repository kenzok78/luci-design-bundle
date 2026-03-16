# OpenWrt Integration Guide

This repository contains two LuCI packages under subdirectories:

- `luci-theme-design`
- `luci-app-design-config`

Use one of the following methods to integrate into your OpenWrt build tree.

## Method 1: Copy into local `package/`

From your OpenWrt root:

```bash
git clone https://github.com/kenzok78/luci-design-bundle.git /tmp/luci-design-bundle
mkdir -p package/luci-theme-design package/luci-app-design-config
cp -a /tmp/luci-design-bundle/luci-theme-design/. package/luci-theme-design/
cp -a /tmp/luci-design-bundle/luci-app-design-config/. package/luci-app-design-config/
```

Then run:

```bash
make menuconfig
```

Enable:

- `LuCI -> Themes -> luci-theme-design`
- `LuCI -> Applications -> luci-app-design-config`

Build:

```bash
make package/luci-theme-design/compile V=s
make package/luci-app-design-config/compile V=s
```

## Method 2: Use a custom feed

Add to `feeds.conf.default` (or `feeds.conf`):

```text
src-git luci_design_bundle https://github.com/kenzok78/luci-design-bundle.git
```

Update and install feeds:

```bash
./scripts/feeds update luci_design_bundle
./scripts/feeds install -a -p luci_design_bundle
```

Then select packages in `make menuconfig` and build normally.

## Runtime requirements

- `luci-app-design-config` expects `luci-theme-design` static assets at:
  - `/www/luci-static/design/css/style.css`
- Install order recommendation:
  1. `luci-theme-design`
  2. `luci-app-design-config`

## Post-install checks (on router)

```bash
uci show design
ls -l /www/luci-static/design/css/style.css
/etc/init.d/uhttpd restart
```

In LuCI:

1. Set Theme to `Design`
2. Open `System -> Design Config`
3. Save `Theme mode`, `Navigation bar`, `Navigation bar proxy`
4. Refresh and confirm settings persist
