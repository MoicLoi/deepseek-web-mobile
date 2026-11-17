# deepseek-web-moblie
首个可发布版本。项目名：`deepseek-web-mobile`；应用显示名：**DeepSeek Studio**。

## 版本亮点

- **强制接入 DeepSeek API**：无游客模式、无跳过按钮，`GET /models` 校验通过后才进入。
- **六种创作模式**：闲聊、RP、恋爱（RP 分支）、小说、实验记录、文献查找。
- **上下文管理特化**：默认只携带最近 12 轮，可切换 6 / 12 / 24 轮或完整上下文；系统提示词自动注入上下文策略。
- **可编辑提示词**：每种模式内置精简提示词，设置中可预览、保存、恢复内置。
- **完整 Web 客户端**：流式回复、深度思考、智能搜索、链接阅读、来源引用、文件上传、语音输入、朗读、Mermaid / KaTeX、多会话、历史导入导出。
- **Android 壳层**：Capacitor WebView、品牌启动图、自适应图标、状态栏配色、录音权限。Debug APK 可直接安装。
- **iOS 单页版**：单个 HTML，无构建、无依赖；包含同样的强制接入、六种模式、上下文窗口、提示词编辑、SSE 流式回复、深浅色与安全区适配。
- **本地优先**：API Key、对话、设置仅保存在本机浏览器 / WebView。

## 发布资产

| 文件                                              | 用途                                          |
| ----------------------------------------------- | ------------------------------------------- |
| `deepseek-web-mobile-v1.0.0-github-release.zip` | 推荐下载：Web + iOS + Android APK + 源码的完整发布包     |
| `deepseek-web-mobile-v1.0.0-source.zip`         | 干净源码（不含 `node_modules`、构建产物、APK）            |
| `deepseek-web-mobile-v1.0.0-web.zip`            | 构建后的静态 Web，解压到任意静态站点即可                      |
| `deepseek-web-mobile-v1.0.0-ios.zip`            | iOS 单页版：`index.html` + 使用说明                 |
| `deepseek-web-mobile-v1.0.0-android-debug.apk`  | Android Debug APK（包名 `com.deepseek.studio`） |
| `SHA256SUMS.txt`                                | 资产 SHA-256 校验                               |

## 安装与使用

### Web

解压 `deepseek-web-mobile-v1.0.0-web.zip`，部署到 HTTPS 静态站点，打开后输入 DeepSeek API Key。

### Android

安装 `deepseek-web-mobile-v1.0.0-android-debug.apk`。首次打开会停留在全屏接入页，必须填入 DeepSeek API Key。

> 这是 Debug 签名 APK，适合测试与侧载；上架商店需要自行配置 release 签名。

### iOS

解压 `deepseek-web-mobile-v1.0.0-ios.zip`，将 `index.html` 部署到 HTTPS 静态空间，Safari 打开后「分享 → 添加到主屏幕」。

> 直接 `file://` 打开时 Safari 可能限制 `localStorage` 与跨域请求，建议使用 HTTPS 托管。

## 验证

- `pnpm lint`：0 warnings / 0 errors
- `pnpm type`：通过
- `pnpm build`：通过
- Android Debug APK：`assembleDebug` 通过，并在 Android 11 / API 30 模拟器安装运行
- iOS 单页版：在 390×844 移动视口验证接入页、模式选择、设置、Mock SSE 流式渲染、Markdown、来源卡片与深色主题
- 未使用真实 API Key 发起真实计费对话；接口协议沿用 DeepSeek 官方 chat-demo

## 已知限制

- 上下文管理是客户端滑动窗口 + 提示词约束，不含服务端摘要或向量记忆。
- 没有自建后端；依赖 DeepSeek API 的浏览器 CORS 策略与账户额度。
- Android 壳层的 API Key 仍保存在 WebView `localStorage`，未接入 Android Keystore。
- iOS 单页版不含文件上传、语音、朗读、Mermaid / KaTeX。
- 不支持非 DeepSeek 的 OpenAI 兼容端点。

## 许可与致谢

- 基于 [deepseek-ai/chat-demo](https://github.com/deepseek-ai/chat-demo)（MIT）改造，保留原始 `LICENSE`。
- 非 DeepSeek 官方产品；DeepSeek 名称与相关商标归深度求索公司所有。
