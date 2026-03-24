# LuCI Design Bundle

本仓库将两个 OpenWrt LuCI 项目整合到一个目录中：

- `luci-theme-design`
- `luci-app-design-config`

集成说明：`OPENWRT_INTEGRATION.md`

## 包含的修复

### luci-theme-design

<small>

- 修复了 `header.htm` 中 Lua 菜单 URL 查询处理 bug（`k.query` -> `nnode.query`）。
- 在主题 XHR 帮助器中用安全的 JSON 解析（`JSON.parse`）替换了不安全的 `eval` 解析。
- 改进了 JSON `Content-Type` 匹配，支持 `application/json; charset=utf-8`。
- 加强了 `script.js` 中的菜单匹配逻辑：
  - 转义了正则输入
  - 用索引循环替换了数组 `for...in`
  - 添加了空值安全的 href 检查

</small>

### luci-app-design-config

<small>

- 在控制器中添加了显式的 `nixio.fs` require，并使用本地 `fs` 访问器。
- 从表单处理程序中移除了无效的调试写入（`/tmp/aaa`）。
- 限制 UCI 写入仅限预期键：`mode`、`navbar`、`navbar_proxy`。
- 为缺失的 `design` `global` 节添加了自动创建回退。
- 为首次运行配置添加了安全默认值：
  - `mode=normal`
  - `navbar=display`
  - `navbar_proxy=shadowsocksr`
- 修复了 README 发布链接拼写错误（`hhttps://` -> `https://`）。

</small>

## 目录结构

```
.
├── luci-theme-design/
└── luci-app-design-config/
```
