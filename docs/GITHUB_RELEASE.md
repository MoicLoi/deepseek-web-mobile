# 发布到 GitHub Releases

项目名：`ds-la-reviewer`  
版本：`v2.0.1`

## 1. 生成发布资产

先确保 Web 与 Android 已构建：

```bash
pnpm install
pnpm build
pnpm android:sync
cd android
gradle assembleDebug
cd ..
```

然后生成 GitHub 发布包：

```bash
pnpm release:package
# 或
python scripts/package_release.py
```

产物在 `release/`：

```text
ds-la-reviewer-v2.0.1-github-release.zip   # 完整包（推荐）
ds-la-reviewer-v2.0.1-source.zip           # 源码
ds-la-reviewer-v2.0.1-web.zip              # 静态 Web
ds-la-reviewer-v2.0.1-ios.zip              # iOS 单页版
ds-la-reviewer-v2.0.1-android-debug.apk    # Android Debug APK
SHA256SUMS.txt
SHA256SUMS-all.txt
```

`release/` 已在 `.gitignore` 中忽略，不会把二进制打进源码仓库。

## 2. 创建 GitHub 仓库

在 GitHub 新建空仓库 `ds-la-reviewer`，然后：

```bash
git remote add origin https://github.com/<你的账号>/ds-la-reviewer.git
git push -u origin main
```

## 3. 打标签

```bash
git tag -a v2.0.1 -m "ds-la-reviewer v2.0.1"
git push origin v2.0.1
```

## 4. 创建 Release

在 GitHub 仓库页面：

1. 打开 **Releases → Draft a new release**
2. 选择标签 `v2.0.1`
3. 标题填 `ds-la-reviewer v2.0.1`
4. 描述复制 [RELEASE_NOTES_v2.0.1.md](RELEASE_NOTES_v2.0.1.md)
5. 上传 `release/` 下的五个发布资产
6. 发布

如果本机安装了 GitHub CLI：

```bash
gh release create v2.0.1 release/* \
  --title "ds-la-reviewer v2.0.1" \
  --notes-file docs/RELEASE_NOTES_v2.0.1.md
```

## 备注

- 项目名统一为 `ds-la-reviewer`；仓库名、`package.json` 与发布资产文件名保持一致。
- APK 为 Debug 签名，适合侧载测试；上架应用商店需要配置 release keystore。
- iOS 单页版必须托管在 HTTPS 站点上，直接 `file://` 打开可能受 Safari 的存储与跨域限制。
