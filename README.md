# DS-LA-reviewer · 实验动物学导论复习助手

> 基于 DeepSeek API 的《实验动物学导论》复习客户端。教材全文、书末例题与四种复习模式内置在本地，所有模式默认开启联网搜索交叉验证。包含 Web、Android WebView 壳层和 iOS 单页版。

> 非 DeepSeek 官方产品。教材内容由用户提供，版权归原权利人；公开分发前请自行取得授权。

- 技能仓库：[MoicLoi/LNUTCM-LabAnimalIntro-Skill](https://github.com/MoicLoi/LNUTCM-LabAnimalIntro-Skill)
- 软件仓库：[MoicLoi/deepseek-web-mobile](https://github.com/MoicLoi/deepseek-web-mobile)

![模拟练习模式](docs/screenshots/ds-la-practice.png)

## 教材与知识库

- 《实验动物学导论》约 **27.1 万字**，7 章 46 节，附录一至七。
- 书末**附录七 例题**：6 道单选题 + 4 道判断题，含答案、解析、答案速查与易错点。
- **新题库 · 填空题**：10 道填空题（100 分），含标准答案与解析，可在练习模式选择。
- 构建时把教材拆成约 **618 个检索片段**，按章节/节标注；提问时用中文 2–4 字组合做本地关键词召回，把命中的片段注入系统提示词。
- 练习/出题模式额外注入教材目录与书末例题，作为题型和难度基准。
- 教材片段优先；联网搜索只做交叉验证，冲突时明确标注。

## 四种模式

### 查阅模式

按章节查概念、机制、标准与比较。回答包含：直接结论、教材依据（章节/节）、联网交叉验证、复习提示或易混点。教材片段不足时会明确说明，不用网络内容冒充教材原文。

### 出题模式

按用户指定的章节、主题或片段生成自测题。默认 5 题，题型参考书末例题（单选题、判断题），可加入名词解释/简答。每题附答案、解析、教材依据；超纲题标注「拓展」。

### 片段练习模式

先让用户选题型（单选题、判断题、简答题、混合题），默认参考书末例题。用户选定后一次只出 1 题；作答后判分、给正确答案、解析、教材依据和易错点，再问是否继续。

### 模拟练习模式

先让用户选题型；默认按书末例题组一套 **6 道单选 + 4 道判断，共 100 分** 的模拟卷，建议 30 分钟；选填空题则使用新题库 10 道题，每题 10 分。先只出题，用户提交后统一批改：总分、逐题对错、解析、教材依据、薄弱章节与复习建议。

> 练习模式的第一问会直接显示在欢迎页；用户也可以直接输入题型。若第一条消息已经说明题型，模型不会重复提问。

## 联网搜索

所有模式默认开启 `deepseek_web_search`，用于核对现行标准、术语、数据与教材表述差异。用户仍可在输入框上方手动关闭。

## 快速开始（Web）

环境：Node.js 22.12+、pnpm。

```bash
pnpm install
pnpm dev
```

打开 `http://localhost:8090`，在接入页填入 DeepSeek API Key。

生产构建：

```bash
pnpm build
# 输出在 dist/
```

`dist/` 可以直接部署到静态服务器。

## Android

项目包含 Capacitor Android 工程（`android/`）。

```bash
pnpm install
pnpm android:sync
pnpm android:open
```

直接构建 Debug APK：

```bash
pnpm android:apk
# android/app/build/outputs/apk/debug/app-debug.apk
```

`applicationId`：`com.dstuido.lnutcmlai`。

要求：

- JDK 21
- Android SDK Platform 36、Build Tools 36
- Android WebView 83+（已在 API 30 / WebView 83 模拟器验证；建议使用系统最新 WebView）

## iOS 单页版

- 文件：[ios/deepseek-studio.html](ios/deepseek-studio.html)
- 说明：[ios/README.md](ios/README.md)

单文件约 900KB，教材数据已内联，无需构建和外部依赖。用 Safari 打开后「分享 → 添加到主屏幕」即可。建议使用 HTTPS 托管；直接 `file://` 打开时 Safari 可能限制 `localStorage` 与跨域请求。

## 数据与隐私

- API Key、模式、上下文设置保存在浏览器/设备本地。
- 会话与附件保存在 IndexedDB；教材检索片段在本地内存中计算，不上传。
- 所有模型请求直接发送到 `https://api.deepseek.com`。
- 清除浏览器数据会同时删除本地会话和 API Key。
- 若面向公众提供服务，请自行完成教材授权、内容安全、模型备案与 AI 生成内容标识等合规义务。

## 已知限制

- 教材由照片转写、校对而来，仍可能有 OCR/排版残留错误；以纸质教材与现行国家标准为准。
- 检索是本地关键词召回，不是语义向量检索；问到目录外的细节时可能召回不足。
- 练习模式依赖模型按提示词生成题目，题量与难度可能波动；重要考试请人工复核。
- Android 壳层未集成安全存储，API Key 仍保存在 WebView 的 localStorage。
- 不支持非 DeepSeek 的 OpenAI 兼容端点。

## 目录

```text
src/
  services/
    knowledge/        教材检索包与召回
    modes.ts          四种模式、系统提示词
    chat/             会话、请求、Markdown 导出
  components/
    session/          欢迎页、练习第一问、分享
    modes/            模式条与模式选择
    settings/         设置、API Key、提示词
ios/                  iOS 单文件版（内联教材）
android/              Capacitor Android 壳层
scripts/              教材抽取与发布打包脚本
```

## 发布包

```bash
pnpm build
pnpm android:sync
cd android && gradle assembleDebug && cd ..
pnpm release:package
```

产物在 `release/`：`ds-la-reviewer-v2.0.1-github-release.zip`、源码、Web、iOS、Android APK 与校验文件。详细步骤见 [docs/GITHUB_RELEASE.md](docs/GITHUB_RELEASE.md)。

## 许可与致谢

- 客户端代码基于 [deepseek-ai/chat-demo](https://github.com/deepseek-ai/chat-demo)（MIT）改造，保留原始 `LICENSE`。
- 《实验动物学导论》教材内容版权归原作者/出版方所有；本项目仅用于用户本地复习，不构成教材再出版。
- DeepSeek 名称与相关商标归深度求索公司所有；本项目不代表官方背书。
