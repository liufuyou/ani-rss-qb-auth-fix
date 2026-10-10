# ani-rss-qb-auth-fix（自用）：恢复 qBittorrent 用户名 + 密码登录

ani-rss 的镜像构建。上游改用 ApiKey 鉴权后，这里把 qBittorrent 登录方式
恢复成 **用户名 + 密码**，ApiKey 仍可用（密码以 `qbt_` 开头即按 ApiKey 处理）。
其余功能跟随上游。

本仓库只存放补丁文件与构建配置，源码在构建时从上游获取。

## 说明

> - 本镜像为**个人自用**，非官方发布物，与上游项目及其作者无关。
> - 本镜像**更新可能滞后于上游**，重要更新会尽量跟进但不作保证。请自行评估后再使用。
> - 仅用于个人自测与学习，**不建议**用于生产环境或商业用途；如使用中产生任何问题，需由使用者自行承担。
> - **低调使用**：请勿在上游项目的 Issue / 讨论区 / 社群宣传、推广或询问本镜像，也不要就相关问题打扰上游作者。

## 使用

镜像每周更新一次，建议固定版本，不要用 `latest`。可用标签见本仓库 Actions 的构建记录或 GHCR 包页面：

```bash
docker pull ghcr.io/liufuyou/ani-rss-qb-auth-fix:upstream-a1b2c3d
```

`upstream-xxx` 是对应上游某个提交的固定版本，不会被覆盖；想要最新版本再用 `:latest`。

```bash
docker run -d \
  --name ani-rss \
  --network host \
  --restart always \
  -v /你的配置目录:/config \
  -v /你的下载目录:/你的下载目录 \
  ghcr.io/liufuyou/ani-rss-qb-auth-fix:upstream-a1b2c3d
```

> 配置目录挂到 `/config`。下载目录在宿主机是什么路径，容器里就挂成一样的路径。

下载器选择 **qBittorrent**，填写**用户名 + 密码**即可（无需 ApiKey）。其余用法与上游 ani-rss 相同。
