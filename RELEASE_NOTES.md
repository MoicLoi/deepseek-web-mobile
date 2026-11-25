# DS-LA-reviewer v2.0.0

实验动物学导论复习助手。项目名：`ds-la-reviewer`。

## 版本亮点

- **教材内置**：集成用户提供的《实验动物学导论》约 27.1 万字、7 章 46 节、附录一至七；书末附录七的 6 道单选题 + 4 道判断题一并收录。
- **本地检索**：正文拆成约 618 个带章节/节标注的片段；提问时按中文 2–4 字组合召回，把命中片段注入系统提示词。
- **四种复习模式**：查阅、出题、片段练习、模拟练习。
- **练习第一问**：片段/模拟练习先让用户选题型；默认参考书末例题：6 单选 + 4 判断，共 100 分。若用户第一条消息已说明题型，模型直接开始，不重复提问。
- **全模式联网交叉验证**：默认开启 `deepseek_web_search`，教材优先、网络补充，冲突时标注。
- **完整客户端**：流式回复、思考、来源引用、会话分支、提示词编辑、上下文窗口、历史导入导出。
- **单轮 / 整段 .md 导出**：通过系统分享面板发送到其他 App；不支持分享时自动下载。
- **Android / iOS**：Android Debug APK（`applicationId: com.dstuido.lnutcmlai`，versionName 2.0.0）+ iOS 单页版（教材数据内联，单文件约 900KB）。
- **技能仓库**：`photo-book-to-ebook` 技能发布在 `MoicLoi/LNUTCM-LabAnimalIntro-Skill`；本软件是其分支产品。

## 发布资产

| 文件 | 用途 |
| --- | --- |
| `ds-la-reviewer-v2.0.0-github-release.zip` | 完整包（Web + iOS + Android APK + 源码） |
| `ds-la-reviewer-v2.0.0-source.zip` | 干净源码 |
| `ds-la-reviewer-v2.0.0-web.zip` | 静态 Web |
| `ds-la-reviewer-v2.0.0-ios.zip` | iOS 单页版 |
| `ds-la-reviewer-v2.0.0-android-debug.apk` | Android Debug APK |
| `SHA256SUMS.txt` | 资产校验 |

## 安装

- **Web**：解压 web 包，部署到 HTTPS 静态站点。
- **Android**：安装 APK；首次打开必须填入 DeepSeek API Key。
- **iOS**：解压 iOS 包，将 `index.html` 部署到 HTTPS 站点，Safari 打开后添加到主屏幕。

## 验证

- `pnpm lint` / `pnpm type` / `pnpm build` 通过。
- 教材检索：查询「无菌动物饲养在什么环境」命中「隔离环境」片段，请求 system 中包含教材片段。
- 四种模式与练习第一问在 390×844 视口验证。
- 联网搜索默认开启，请求 tools 同时包含 `deepseek_read_url` 与 `deepseek_web_search`。
- Android APK 构建通过；iOS 单页教材数据解析 618 个片段。

## 已知限制

- 教材由照片转写、校对而来，仍可能有 OCR/排版残留错误；以纸质教材与现行标准为准。
- 本地检索是关键词召回，不是语义向量检索。
- 练习题目由模型生成，题量与难度可能波动；重要考试请人工复核。
- 教材版权归原权利人；公开分发前请自行取得授权。

## 许可

- 客户端代码基于 [deepseek-ai/chat-demo](https://github.com/deepseek-ai/chat-demo)（MIT）。
- 非 DeepSeek 官方产品；DeepSeek 名称与商标归深度求索公司所有。
