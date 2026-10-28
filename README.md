# 企业微信问答网页

这是一个简单的网页聊天入口：用户输入问题，网页将问题发送给 n8n，并显示返回的答案。

## 项目状态

- 已有单页聊天界面，支持点击发送和回车发送。
- 仓库只包含前端页面；没有 n8n 工作流、模型配置或知识库。
- 已配置 n8n Cloud Webhook；当前接口可用性和线上部署状态尚未验证。
- 页面标题为“企业微信问答”，但仓库中没有企业微信登录或消息回调代码。

## 文件结构

```text
index.html       网页、样式和请求逻辑
README.md        用途与使用说明
MAINTENANCE.md   维护、排查和待核实事项
.gitignore       本机临时文件忽略规则
```

## 本地查看

本项目不需要安装前端依赖或构建工具。可以直接用浏览器打开 index.html 查看界面。

测试接口时，建议在本目录启动静态文件服务。例如本机已安装 Python 3 时：

```sh
python3 -m http.server 8000
```

然后访问 http://localhost:8000。接口能否回答还取决于网络、n8n 工作流状态以及跨域配置。

## 请求与返回约定

页面向 index.html 中 N8N_WEBHOOK_URL 指定的地址发送 POST JSON：

```json
{"question": "你的问题"}
```

预期返回：

```json
{"answer": "回答内容"}
```

## 部署与配置

将 index.html 放在支持静态网页的托管服务上即可提供界面。仓库元数据表明已启用 GitHub Pages，但当前发布源、访问地址和运行情况仍需在仓库 Settings → Pages 核实。

替换后端入口时，修改 index.html 中的 N8N_WEBHOOK_URL。浏览器里的地址和代码对访问者可见，不要在页面中加入模型 API 密钥或其他私密凭据。

完整操作和故障排查见 [维护说明](MAINTENANCE.md)。

## 相关仓库导航

| 仓库 | 用途 |
| --- | --- |
| [n8n-chat-page](https://github.com/Totin143/n8n-chat-page) | 企业微信问答网页，将问题发送给 n8n |
| [totin143.github.io](https://github.com/Totin143/totin143.github.io) | GitHub Pages 仓库，目前只存放验证文件 |
| [wechat-verify](https://github.com/Totin143/wechat-verify) | 验证文件仓库，登记了 Vercel 网址 |

三个仓库之间的实际部署依赖尚未核实，不能仅凭名称认定后两个互相替代。
