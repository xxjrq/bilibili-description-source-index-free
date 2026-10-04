# B站简介资料链接索引

把指定 B 站视频简介中作者公开的学习与工具资料，整理成可核对的链接清单。你提供 1–3 个视频 URL 和 `browserId`；Skill 交付每条链接的来源、可见用途、可访问状态，以及无法读取或打开时的原因，不会假称资料已经下载。

![B站简介资料链接索引推广图](assets/promo.png)

## 安装

```bash
npx skills add xxjrq/bilibili-description-source-index-free
```

这是浏览器 Skill。安装 [Easy WebBridge（GitHub）](https://github.com/Jackwener/OpenCLI)，或使用 [Gitee 备用地址](https://gitee.com/jackwener/OpenCLI)。运行时由用户提供 `browserId`；一项任务只管理自己的 session 和标签组，不接管已有页面。

## 输入与结果

输入：一个 Easy WebBridge `browserId`、1–3 个 B站视频 URL，以及可选的本地整理要求。

结果：JSON/表格草稿，包含 `source_video`、`url`、`purpose`、`access`、`evidence`，并在 `gaps` 中记录简介不可见、需登录或链接打不开等原因。默认只读；若授权填充草稿，也绝不点击最终发布或发送。

只处理网页可见内容。遇到登录、验证码或风控会停止并如实记录，不绕过限制。单次最多 100 行；更多内容需分批。

## 本地验证

```bash
node scripts/self-test.mjs
```

fixtures 是离线页面资料模拟，验证的是解析和失败记录，不代表在线采集。

## 来源与许可

浏览器适配的业务用途参考 [OpenCLI](https://github.com/jackwener/OpenCLI) 与其 [B站适配说明](https://github.com/jackwener/OpenCLI/blob/main/docs/adapters/browser/bilibili.md)，未复制其实现或源码。本仓库以 [MIT License](LICENSE) 发布。
