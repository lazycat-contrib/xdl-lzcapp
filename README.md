# XDL 懒猫微服打包

上游：https://github.com/missuo/xdl （GPL-3.0，分支 feat/go-rewrite）

X(Twitter) 媒体批量下载器：任务队列、订阅、HTTP API 与 MCP。

## 打包说明

- 镜像：`ghcr.io/missuo/xdl`（headless 服务端，`xdl serve`），由 [ca-x/lazycat-github-action](https://github.com/ca-x/lazycat-github-action) 镜像模式自动同步
- HTTP API（47333）走 upstreams，对外提供 API / MCP / Chrome 扩展连接端点
- 设置向导参数：
  - `auth_token`（secret）：x.com 的 auth_token Cookie，下载必需
  - `api_token`（secret）：HTTP API / MCP / Chrome 扩展的 Bearer Token
- 数据：媒体库/订阅/设置在 `/lzcapp/var/data`（容器 `/data`），下载的媒体在 `/lzcapp/var/downloads`（容器 `/downloads`）

## 使用

部署后在浏览器/CLI/Chrome 扩展中以 `https://xdl.<你的懒猫域名>` + `api_token` 连接：

```sh
XDL_API_URL=https://xdl.<域名> XDL_API_TOKEN=<api_token> xdl sub add nasa 1d
```

MCP 端点：`https://xdl.<域名>/mcp`（Bearer Token 认证）。

## 发布

workflow 定时 + 手动触发，镜像模式同步上游 release tag 并发布喵喵商店。
