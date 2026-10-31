# 中文口语练习 · Netlify 版

Dino Space Mission（恐龙太空探险）：太空背景、小恐龙伙伴、星星奖励。一页完成一段综合对话：先打招呼（你好、你好吗），再聊学校（第1课）、在做什么（第2课）和吃的（第3课），最后说再见。题目从题库里随机抽取，每次重做都不一样。AI 判断答案，任何说得通的回答都算对。

## 文件
- `public/index.html` — 网页
- `netlify/functions/chat.mjs` — 连接 AI 的后端（API 密钥只保存在这里，学生看不到）
- `netlify.toml` — Netlify 设置

## 第 1 步：申请 API 密钥
1. 打开 https://console.anthropic.com ，注册并充值少量额度。
2. 在 API Keys 页面创建一个密钥，复制下来（以 `sk-ant-` 开头）。
3. 建议在 Billing / Limits 里设置每月消费上限。

## 第 2 步：部署到 Netlify
注意：直接把文件夹**拖进 Netlify 的方式不支持后端函数**，那样 AI 对话不能用。请用下面两种方法之一。

**方法 A：GitHub（推荐，不用装软件）**
1. 在 GitHub 新建一个仓库，把这个文件夹里的所有文件上传进去（保持文件夹结构）。
2. 在 app.netlify.com 点 **Add new site → Import an existing project → GitHub**，选这个仓库，其他保持默认，点 Deploy。

**方法 B：Netlify CLI**
```
npm install -g netlify-cli
netlify login
cd kouyu-netlify
netlify deploy --prod
```

## 第 3 步：设置环境变量
在 Netlify 网站后台 **Site configuration → Environment variables** 添加：

| 名称 | 值 | 必填 |
|---|---|---|
| `ANTHROPIC_API_KEY` | 你的 API 密钥 | 是 |
| `CLASS_CODE` | 班级密码，例如 `epsom3` | 建议填写。填了以后学生第一次聊天要输入密码，防止陌生人用掉额度 |
| `ANTHROPIC_MODEL` | 默认 `claude-haiku-5-5` | 否 |

添加后到 **Deploys** 点 **Trigger deploy → Deploy site**，让设置生效。

## 使用提示
- 麦克风需要 Chrome、Edge 或 Safari，第一次使用时浏览器会询问是否允许麦克风，请点"允许"。
- 网址必须是 https（Netlify 默认就是）。
- 想加新题目：在 `public/index.html` 里找到 `POOLS`，照格式加一行（问题、拼音、英文，以及一个参考答案）。`n` 表示每轮从该组抽几题。
