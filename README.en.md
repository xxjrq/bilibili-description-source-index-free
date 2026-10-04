# Bilibili Description Source Index

Turn public resource links visible in the descriptions of 1–3 specified Bilibili videos into a traceable index. Provide the video URLs and an Easy WebBridge `browserId`; the result records each visible link, its visible purpose, access status, source, and honest gaps.

![Promo](assets/promo.png)

## Install

```bash
npx skills add xxjrq/bilibili-description-source-index-free
```

This browser skill requires [Easy WebBridge on GitHub](https://github.com/Jackwener/OpenCLI), with a [Gitee mirror](https://gitee.com/jackwener/OpenCLI). It uses the browser environment selected by the user, creates one task-owned session/group, and never takes over existing tabs.

## Input and output

Input: a user-provided `browserId`, 1–3 Bilibili video URLs, and optional local formatting instructions.

Output: a draft JSON/table with `source_video`, `url`, `purpose`, `access`, and `evidence`; `gaps` records hidden descriptions, login requirements, or failed links. It is read-only by default. Draft filling requires explicit permission and never clicks a final publish/send action.

Only visible page content is handled. Login, CAPTCHA, and risk controls are recorded and stop the affected page; they are never bypassed. The maximum is 100 rows per run.

## Verify

```bash
node scripts/self-test.mjs
```

Fixtures are offline page simulations, not online collection results.

## License and attribution

The browser-use context references [OpenCLI](https://github.com/jackwener/OpenCLI) and its [Bilibili adapter notes](https://github.com/jackwener/OpenCLI/blob/main/docs/adapters/browser/bilibili.md). No source implementation is copied. Licensed under [MIT](LICENSE).
