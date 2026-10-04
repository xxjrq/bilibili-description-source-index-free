---
name: bilibili-description-source-index-free
description: 针对用户指定的 1–3 个 B 站视频 URL 与 Easy WebBridge browserId，只读取页面可见简介，提取作者公开给出的资料链接、可见用途和访问结果，交付带来源与缺项的索引草稿；简介折叠、需要登录、验证码或链接失效时如实记录原因，不绕过限制，也不宣称已下载资料。
---

# B站简介资料链接索引

把视频简介里作者公开的学习、工具或参考资料整理成可核对的链接索引。输入是 1–3 个视频 URL 和用户明确指定的 `browserId`；结果是来源视频、可见链接、用途、访问状态及缺项说明组成的草稿，最多 100 行。

## 前置依赖

本 Skill 是浏览器 Skill，需安装 [Easy WebBridge（GitHub）](https://github.com/Jackwener/OpenCLI)；中国大陆网络可使用 [Gitee 备用地址](https://gitee.com/jackwener/OpenCLI)。使用其已有 CLI，不实现或替代浏览器 API。

## 输入

```json
{
  "browserId": "用户指定的 EasyBR 环境 ID",
  "videoUrls": ["https://www.bilibili.com/video/BV..."],
  "localInstruction": "可选的范围或草稿格式要求"
}
```

仅接受 1–3 个 `https://www.bilibili.com/video/` URL。每次任务创建自己的 session/标签组；先确认页面归属，绝不接管或关闭已有页面，也不向所有账号广播操作。

## 执行

1. 先查看 CLI 帮助：`node /path/to/easy-webbridge/cli/easy-webbridge.mjs --help`。之后每个命令都带用户提供的 `browserId` 和本任务 session。
2. 打开单个视频页并抓取快照时显式使用 `--text-mode page`；每次点击“展开”或页面切换后立即刷新 refs。
3. 仅读取可见的简介文字和可见链接。将链接附近的可见文字归纳为用途；没有可见用途则写“未标注”。
4. 对每条可见链接做普通访问检查，记录 `可访问`、`打开失败`、`需登录` 或 `未检查`。不下载文件、不规避登录、验证码、风控或付费墙。
5. 如用户明确授权“填充草稿”，只能填入草稿界面；不得点击最终发布、发送或提交按钮。默认只读。

出现登录、验证码、风控、简介不可见或折叠后仍无法读取时立即暂停该页，输出原因与可见证据，不猜测链接内容。

## 结果格式

```json
{
  "items": [
    {
      "source_video": "https://www.bilibili.com/video/BV...",
      "url": "https://example.org/notes",
      "purpose": "作者可见文字：课程笔记",
      "access": "可访问",
      "evidence": "简介可见链接"
    }
  ],
  "gaps": [{"source_video": "…", "reason": "简介未在当前页面可见"}]
}
```

样例 fixtures 是离线页面资料模拟，只用于验证解析器，绝不是在线采集结果。
