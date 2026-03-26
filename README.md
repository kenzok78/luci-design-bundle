# luci-design-bundle

适用于 OpenWrt/Lede 的 LuCI Design 主题及配置插件。

## 简介

本仓库整合了 Design 主题及其配置插件，方便 One-Key 部署：

- **luci-theme-design**: 移动端优化的沉浸式 LuCI 主题
- **luci-app-design-config**: Design 主题配置插件

## 功能特性

### luci-theme-design

- **移动端优化**: 响应式布局，适合手机端作为 WebApp 使用
- **沉浸式体验**: 简洁的登录界面，底部导航栏，类 App 操作体验
- **深色模式**: 支持深色/浅色模式，支持系统自动切换
- **主题配置**: 支持插件式自定义主题模式
- **视觉统一**: 完善的设备图标，优化插件显示

### luci-app-design-config

- 支持更改主题深色/浅色模式
- 支持显示/隐藏导航栏
- 支持更换常用的代理图标

## 包含的修复

### luci-theme-design

- 修复了 `header.htm` 中 Lua 菜单 URL 查询处理 bug
- 用安全的 `JSON.parse` 替换了不安全的 `eval` 解析
- 改进了 JSON `Content-Type` 匹配
- 加强了菜单匹配逻辑

### luci-app-design-config

- 控制器中添加了显式的 `nixio.fs` require
- 限制 UCI 写入仅限预期键
- 添加了自动创建缺失配置的 fallback
- 修复了 README 发布链接拼写错误

## 安装

### OpenWrt Feed 方式

```bash
# 添加 feed
echo 'src-git luci_design https://github.com/kenzok78/luci-design-bundle.git' >> feeds.conf.default
./scripts/feeds update -a
./scripts/feeds install -a -p luci_design

# 编译
make package/luci-theme-design/compile V=s
make package/luci-app-design-config/compile V=s
```

### 直接编译

```bash
git clone https://github.com/kenzok78/luci-design-bundle.git package/luci-design-bundle
make menuconfig  # 选择 LuCI -> Themes -> luci-theme-design
                  # 选择 LuCI -> Applications -> luci-app-design-config
make -j$(nproc) V=s
```

## 使用说明

### 基本配置

1. 访问 OpenWrt Web 管理界面 → 系统 → Design 配置
2. 设置主题模式（正常/深色/浅色/自动）
3. 设置导航栏显示/隐藏
4. 设置导航栏代理图标
5. 保存并应用配置

### 配置说明

| 选项 | 说明 | 默认值 |
|------|------|--------|
| 主题模式 | 主题颜色模式 | normal |
| 导航栏 | 是否显示底部导航栏 | display |
| 导航栏代理 | 代理图标替换 | shadowsocksr |

## 目录结构

```
luci-design-bundle/
├── luci-theme-design/         # LuCI 主题
│   ├── luasrc/               # Lua 视图
│   ├── htdocs/               # 静态资源
│   ├── root/                 # 文件系统文件
│   └── Makefile
├── luci-app-design-config/    # LuCI 配置插件
│   ├── luasrc/               # Lua 控制器
│   ├── po/                   # 翻译文件
│   ├── root/                 # 启动脚本
│   └── Makefile
└── README.md
```

## 许可证

AGPL-3.0

## 来源

- [luci-theme-design](https://github.com/gngpp/luci-theme-design)
- [luci-app-design-config](https://github.com/gngpp/luci-app-design-config)
