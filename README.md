# gui-for-singbox-pkgbuild

个人维护的 [GUI.for.SingBox](https://github.com/GUI-for-Cores/GUI.for.SingBox) 的 Arch Linux PKGBUILD，fork 自 [AUR `gui-for-singbox`](https://aur.archlinux.org/packages/gui-for-singbox)。

**⚠️ 这不是 AUR 官方包，仅供个人使用。** 如果你想用社区维护的版本，请直接通过 `yay -S gui-for-singbox` 安装。

## 为什么有这个仓库

上游 AUR 包维护不及时（截至 2026-03-11 已标记 out-of-date），且存在以下问题：

- 动态获取 `latest` 二进制导致 source 不可复现、checksum 频繁失效
- 未正确解压 zip 包（`package()` 直接 install 一个不存在的文件名）
- 图标安装到 `/opt` 非标准路径，.desktop 引用无效
- 多语言提示存在拼写错误、locale 匹配过于严格
- 版本更新滞后于上游 release

此 fork 专注于个人使用场景下的定制化调整，不替代 AUR 社区版本。

## 安装

```bash
# 首次使用：clone 并构建安装
git clone https://github.com/Akitora-R/gui-for-singbox-pkgbuild.git
cd gui-for-singbox-pkgbuild
makepkg -si

# 之后更新：一行搞定
cd gui-for-singbox-pkgbuild && git pull && makepkg -si
```

也可以写成 alias（追加到 `~/.bashrc` 或 `~/.zshrc`）：

```bash
alias singbox-up='cd ~/aur/gui-for-singbox-pkgbuild && git pull && makepkg -si'
```

**注意：** 不支持通过 `yay -S` 直接从本仓库安装。yay 的 `-S` 只查询 AUR 数据库，不走 GitHub 直链。

## 更新 PKGBUILD

当上游 [GUI.for.SingBox](https://github.com/GUI-for-Cores/GUI.for.SingBox/releases) 发布新版本时：

```bash
# 1. 修改 pkgver
vim PKGBUILD

# 2. 更新校验和（二进制 zip 使用 SKIP，仅更新 .desktop 和 .install 的 checksum）
updpkgsums

# 3. 本地构建测试
makepkg -si

# 4. 推送更新
git commit -am "bump to x.x.x"
git push
```

## 与 AUR 原版的差异

- 固定版本号（非动态 `latest`），source URL 可复现
- 二进制 zip 校验和设为 `SKIP`，避免每次版本更新时 checksum 失效
- 图标安装至 `/usr/share/pixmaps/`（符合 XDG 标准）
- 修复 .install 中的拼写错误（`youUSER`/`youGROUP`）和 locale 通配匹配
- 所有 shell 变量添加引号，通过 shellcheck

## 依赖

| 依赖 | 说明 |
|------|------|
| `glibc` | C 运行时（动态链接） |
| `webkit2gtk-4.1` | Wails WebView 渲染后端 |

> `jq` / `curl` 未列入 depends：应用内部使用 Go 的 `encoding/json` 和 `net/http`，不调用外部命令。

## 上游信息

- **项目**: [GUI.for.SingBox](https://github.com/GUI-for-Cores/GUI.for.SingBox)
- **描述**: Modern, lightweight desktop app built with Wails (Go) and Vue 3
- **许可证**: GPL-3.0

## 许可

本仓库中 PKGBUILD 及配套文件遵循与原 AUR 包相同的惯例。上游软件使用 GPL-3.0。
