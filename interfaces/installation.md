# 安装与授权

模块签名清单可用 requires 声明依赖，例如 `[{"kind":"plugin","id":"cloud115","minVersion":"1.8.0"}]`。kind 可取 plugin 或 component。最低版本使用三个十进制版本段。调用权限通过 calls、components、domains、fileRead 等单独声明。

在线安装先 POST /api/v1/market/{kind}/{id}/preview，再将返回的 digest 原样传入 If-Match，POST 至同路径的 install。本地 ZIP 先 POST /api/v1/plugins/preview，再带着返回的 release 和同一 ZIP POST /api/v1/plugins。两者都向管理员展示完整计划，按依赖顺序安装，已安装的兼容依赖可以复用。

公开插件省略 license。需要授权的插件填写 `{"license":{"url":"https://开发者域名/授权页面","publicKey":"Base64 编码的 Ed25519 公钥"}}`。安装后在插件设置读取本机安装 ID 并访问该地址，取得并导入签名凭证。授权站点由开发者运营。

授权凭证字段为 module、host、expires 和 signature。expires 为截止 Unix 秒，0 表示长期。签名消息为 UTF-8 编码的 `TIDE-LICENSE-1\0模块ID\0安装ID\0截止秒数`，其中 \0 表示单个零字节。signature 是 Ed25519 签名的标准 Base64。GET /api/v1/plugins/{id}/license 查看状态，PUT 同一路径导入凭证。两者均使用宿主管理身份。本机安装 ID 随数据卷保存。

组件的正式下载、架构、字节数和 SHA-256 见索引。安装后插件通过其声明的具名能力调用。文件型能力同时要求插件拥有宿主文件读取权限。组件接口目录给出各动作的参数、返回结构和示例。
