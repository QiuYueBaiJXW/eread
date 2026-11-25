# 有益阅读（eread）

NAS 私人电子书库，手机和网页都能读。

**书架**：按刊名成组、继续阅读、阅读统计与每日目标，支持 EPUB / PDF / TXT / MOBI / AZW3 / FB2，阅读器字号/行距/四档主题、翻页与滑动、自动阅读、目录/书签/划线批注，进度按账号同步。

**书城**：OPDS 书源自己添加，搜书下载直接进书库。

**文章**：微信文章一键保存（只存链接，点开读原文），按公众号分组、可收藏；RSS 订阅自动拉新。

## 部署方式

### Docker（推荐，任何 NAS / 服务器 / 云主机都能用）

镜像：[`ghcr.io/qiuyuebaijxw/ebook-go`](https://github.com/users/QiuYueBaiJXW/packages/container/package/ebook-go)（公开，无需登录即可拉取）

```bash
docker run -d --name eread --restart unless-stopped \
  -p 9020:9020 \
  -e TZ=Asia/Shanghai \
  -e EREAD_PASSWORD=你自己的密码 \
  -e TRIM_DATA_ACCESSIBLE_PATHS=/books \
  -v ./data:/data \
  -v /你的书库:/books \
  ghcr.io/qiuyuebaijxw/ebook-go:latest
```

或用 docker compose（本仓库自带 `docker-compose.yml`）：

```bash
docker compose up -d
```

- 打开 `http://你的服务器 IP:9020`，用 `admin` + 你设置的 `EREAD_PASSWORD` 登录。
- 多用户：在网页“我的”→“用户管理”里加人，每人独立密码；进度、书签、划线、收藏、统计、文章、RSS 按账号隔离，书库共用。
- 书库目录必须读写挂载：上传和书城下载都直接写书库根目录。
- 数据在 `./data`（账号、阅读记录、文章、RSS），备份它即可。

### 飞牛 fnOS（FPK）

- 在飞牛应用商店内搜索有益阅读，下载安装。
- 在 [Releases](https://github.com/QiuYueBaiJXW/eread/releases) 里下载 `eread-3.2.5-arm64.fpk`，飞牛应用中心 → 手动安装 → 上传安装。

- 仅支持 ARM64 机型；x86 机型请用 Docker 版。
- 安装后在飞牛桌面打开，或访问 `https://你的域名/app/eread`，用飞牛账号登录，无需另外设密码。

### iOS 客户端

原生客户端已上架外区 App Store，国区App store暂不考虑上架。

## 说明

- 服务端免费；iOS 客户端基础功能免费，会员功能收费。
- 本仓库仅为分发页，不含源码。
