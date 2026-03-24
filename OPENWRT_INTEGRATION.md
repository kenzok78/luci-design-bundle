<small>

# OpenWrt 集成指南

本仓库包含两个 LuCI 软件包，位于子目录中：

- `luci-theme-design`
- `luci-app-design-config`

使用以下方法之一集成到您的 OpenWrt 构建树。

## 方法 1：复制到本地 `package/`

在 OpenWrt 根目录下执行：

```bash
git clone https://github.com/kenzok78/luci-design-bundle.git /tmp/luci-design-bundle
mkdir -p package/luci-theme-design package/luci-app-design-config
cp -a /tmp/luci-design-bundle/luci-theme-design/. package/luci-theme-design/
cp -a /tmp/luci-design-bundle/luci-app-design-config/. package/luci-app-design-config/
```

然后运行：

```bash
make menuconfig
```

启用：

- `LuCI -> Themes -> luci-theme-design`
- `LuCI -> Applications -> luci-app-design-config`

构建：

```bash
make package/luci-theme-design/compile V=s
make package/luci-app-design-config/compile V=s
```

## 方法 2：使用自定义 feed

添加到 `feeds.conf.default`（或 `feeds.conf`）：

```text
src-git luci_design_bundle https://github.com/kenzok78/luci-design-bundle.git
```

更新并安装 feeds：

```bash
./scripts/feeds update luci_design_bundle
./scripts/feeds install -a -p luci_design_bundle
```

然后在 `make menuconfig` 中选择软件包并正常构建。

## 运行时要求

- `luci-app-design-config` 需要 `luci-theme-design` 静态资源位于：
  - `/www/luci-static/design/css/style.css`
- 安装顺序建议：
  1. `luci-theme-design`
  2. `luci-app-design-config`

## 安装后检查（在路由器上）

```bash
uci show design
ls -l /www/luci-static/design/css/style.css
/etc/init.d/uhttpd restart
```

在 LuCI 中：

1. 将主题设置为 `Design`
2. 打开 `系统 -> Design 配置`
3. 保存 `主题模式`、`导航栏`、`导航栏代理`
4. 刷新并确认设置已保存

</small>
