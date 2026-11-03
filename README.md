# 潮汐官方商店

宿主读取 [签名商店索引](./index.json)。插件包同时包含发布者签名、构建器签名和加密的 QuickJS 字节码。原生组件按 Linux amd64 或 arm64 分发。

| 插件 | 能力 | 接口 |
| --- | --- | --- |
| 115 连接器 | 按账号 UUID 限速，支持 CK 与 Open 调用。扫码引导无需 UUID。 | [参数与返回值](interfaces/cloud115/operations.json) · [P115C 逐项覆盖](interfaces/cloud115/p115c-coverage.tsv) |
| 115 账号管理器 | 扫码、账号资料、私有凭据及调用句柄。安装时一并解析 115 连接器。 | [参数与返回值](interfaces/accounts115/operations.json) |

| 组件 | 能力 |
| --- | --- |
| [CD2](interfaces/cd2/operations.json) | [gRPC 方法表](interfaces/cd2/rpc.tsv)及[消息字段](interfaces/cd2/types.json.gz) |
| [通知](interfaces/notify/operations.json) | Telegram Bot、企业微信自建应用 |
| [ffprobe](interfaces/ffprobe/operations.json) | 容器与媒体流信息 |
| [ffmpeg](interfaces/ffmpeg/operations.json) | 视频预览帧 |
| [mihomo](interfaces/mihomo/operations.json) | 核心版本、路由规则校验 |
| [图像处理](interfaces/image/operations.json) | 图片信息与缩略图 |
| [光盘读取](interfaces/optical/operations.json) | ISO 9660 镜像与映射光驱的目录遍历、文件分块读取 |

[插件统计接口](interfaces/statistics.json)由宿主统一提供。当前两款 115 插件可在所有受支持的 NAS 上安装并启用。宿主也支持开发者签发的离线授权，详见[安装与授权契约](interfaces/installation.md)。

自有发行包位于 packages。FFmpeg、ffprobe 和 mihomo 使用签名索引中固定版本的上游发行地址与 SHA-256。[FFmpeg 发行渠道](https://github.com/eugeneware/ffmpeg-static/releases/tag/b6.1.1) · [mihomo 发行渠道](https://github.com/MetaCubeX/mihomo/releases/tag/v1.19.33)
