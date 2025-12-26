# NodeGuaBot（NodeSeek AI吃瓜助手）

NodeSeek（`https://www.nodeseek.com/`）Tampermonkey 用户脚本：自动抓取楼层并生成「时间线 / 争议点 / 立场对照」吃瓜总结，支持继续追问对话（OpenAI-compatible 流式输出）。

## 安装

1. 安装浏览器扩展 Tampermonkey
2. 新建脚本，把 `NodeGuaBot.user.js` 的内容粘贴进去保存

## 使用

1. 打开任意 NodeSeek 帖子页，例如 `https://www.nodeseek.com/post-559140-1`
2. 右下角点击「瓜」打开面板
3. 先到「设置」填写 `API URL / API Key / Model`（可点「测试 API」确认可用）
4. 切到「总结」确认页码范围（默认 `1` 到 `总页数`；自动探测）
   - 若显示「总页数：未知」，可手动输入页码范围
5. 点击「开始总结」
6. 切到「对话」基于总结继续追问

面板位置/大小、以及每个帖子的总结与对话会自动保存；切换分页或换帖子后再次打开会自动恢复。

## 设置（API）

脚本使用 **Chat Completions**（`/v1/chat/completions`）并开启 `stream: true`。

- `API URL`：完整请求地址，例如：
  - OpenAI 官方：`https://api.openai.com/v1/chat/completions`
  - 其他 OpenAI-compatible 网关：填你的网关地址（同样是 `/v1/chat/completions`）
- `API Key（Bearer）`：例如 `sk-...`
- `Model`：例如 `gpt-4o-mini` / `deepseek-chat` 等（按你的服务端实际支持为准）
- `多模态发送图片（image_url）`：开启后会把帖子中的图片作为图片输入发给模型（需要模型支持图片输入；不支持会自动降级为仅发送图片链接）
- `提示词`：可分别微调「总结」与「对话」的 system prompt
