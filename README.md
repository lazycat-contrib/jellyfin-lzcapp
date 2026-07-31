# Jellyfin for LazyCat

[Jellyfin](https://jellyfin.org) 的 LazyCat LPK v2 打包项目，支持多实例部署。

## 应用配置

- 包名：`community.lazycat.app.jellyfin`
- 当前应用版本：`10.11.11`
- 运行镜像：`docker.1ms.run/jellyfin/jellyfin:10.11.11`
- 架构：`amd64`
- 配置目录：`/lzcapp/var/config`
- 缓存目录：`/lzcapp/cache`
- 主媒体目录：安装时选择，默认 `Media`，挂载到 `/media`
- 第二媒体目录：安装时选择，默认 `Media2`，只读挂载到 `/media2`
- 自定义字体目录：安装时选择，默认 `Fonts`，只读挂载到 `/usr/local/share/fonts/custom`

首次启动后使用 Jellyfin 自带的初始化向导创建管理员、设置语言并添加媒体库。本项目不包含密码或文件选择注入。

> 安全提示：为兼容 Jellyfin 原生客户端和 UDP 自动发现，应用接口允许客户端直接访问。安装后请立即完成管理员初始化，不要让未初始化的实例长时间运行。

## 本地构建

```bash
lzc-cli project release -o dist/application.lpk
lzc-cli lpk info dist/application.lpk
```

## 自动发布

GitHub Actions 跟踪上游 `jellyfin/jellyfin` 的稳定版本，生成带版本号的 GitHub Release LPK，并且只发布到喵喵私有应用商店。当前运行镜像固定为 `10.11.11`，通过 1ms 镜像地址直接交付，不会复制到懒猫镜像仓库，也不会发布到懒猫官方商店。

仓库使用以下 GitHub Secrets：

- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID`（可选）
- `PRIVATE_STORE_GROUP_CODES`（可选）
