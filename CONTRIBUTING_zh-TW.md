# 貢獻指南

[English](CONTRIBUTING.md) | **繁體中文**

感謝您考慮為 Cursor Overlay 做出貢獻!本文檔提供了貢獻流程和最佳實踐的指南。

## 📋 目錄

- [行為準則](#行為準則)
- [如何貢獻](#如何貢獻)
- [開發流程](#開發流程)
- [更新 Cursor 版本](#更新-cursor-版本)
- [測試變更](#測試變更)
- [提交 Pull Request](#提交-pull-request)
- [編碼規範](#編碼規範)

## 📜 行為準則

本專案採用友好、包容的環境。參與時請:

- 使用友善和包容的語言
- 尊重不同的觀點和經驗
- 優雅地接受建設性批評
- 專注於對社群最有利的事情
- 對其他社群成員表示同理心

## 🤝 如何貢獻

### 回報 Bug

發現 bug 時,請在 [GitHub Issues](https://github.com/Zakkaus/cursor-overlay/issues) 建立問題報告,包含:

1. **清晰的標題**: 簡潔描述問題
2. **環境資訊**:
   ```bash
   uname -a
   emerge --info
   cursor --version
   ```
3. **重現步驟**: 詳細的步驟說明
4. **預期行為**: 應該發生什麼
5. **實際行為**: 實際發生什麼
6. **錯誤日誌**: 相關的錯誤訊息

### 建議功能

對於功能建議:

1. 在 [GitHub Issues](https://github.com/Zakkaus/cursor-overlay/issues) 開啟功能請求
2. 清楚描述功能和其用途
3. 說明為什麼這個功能對 overlay 有用
4. 如果可能,提供實作建議

### 改進文檔

文檔改進非常歡迎!

- 修正拼寫錯誤或語法錯誤
- 改善說明的清晰度
- 添加更多範例
- 翻譯文檔為其他語言

## 🔧 開發流程

### 設定開發環境

1. **Fork 倉庫**:
   ```bash
   # 在 GitHub 上點擊 "Fork" 按鈕
   ```

2. **克隆您的 fork**:
   ```bash
   git clone git@github.com:YOUR_USERNAME/cursor-overlay.git
   cd cursor-overlay
   ```

3. **添加上游 remote**:
   ```bash
   git remote add upstream https://github.com/Zakkaus/cursor-overlay.git
   ```

4. **安裝為本地 overlay**:
   ```bash
   sudo ln -s "$(pwd)" /var/db/repos/cursor-overlay
   
   # 或添加到 repos.conf
   sudo tee /etc/portage/repos.conf/cursor-overlay.conf << EOF
   [cursor-overlay]
   location = $(pwd)
   EOF
   ```

### 建立功能分支

```bash
# 更新您的 main 分支
git checkout main
git pull upstream main

# 建立新分支
git checkout -b feature/your-feature-name
```

## 🔄 更新 Cursor 版本

當 Cursor 發布新版本時,按照以下步驟更新 ebuild:

### 1. 檢查新版本

訪問 [Cursor 下載頁面](https://cursor.com/download) 或檢查 GitHub releases。

### 2. 獲取新的 BUILD_ID

```bash
# 新版本的下載連結通常遵循此格式:
# https://downloads.cursor.com/production/{BUILD_ID}/linux/x64/Cursor-{VERSION}-x86_64.AppImage

# 例如,對於 1.7.52 版本,您可以使用瀏覽器開發者工具
# 或查看下載頁面的網路請求來找到 BUILD_ID
```

### 3. 複製並修改 ebuild

```bash
cd app-editors/cursor

# 複製現有 ebuild
cp cursor-1.7.52.ebuild cursor-1.8.0.ebuild

# 編輯新 ebuild
vim cursor-1.8.0.ebuild
```

### 4. 更新 BUILD_ID

在新 ebuild 中更新 `BUILD_ID` 變數:

```bash
BUILD_ID="新的_BUILD_ID_在這裡"
```

### 5. 驗證下載連結

測試下載連結是否有效:

```bash
# amd64
BUILD_ID="您的_BUILD_ID"
VERSION="1.8.0"
curl -I "https://downloads.cursor.com/production/${BUILD_ID}/linux/x64/Cursor-${VERSION}-x86_64.AppImage"

# arm64
curl -I "https://downloads.cursor.com/production/${BUILD_ID}/linux/arm64/Cursor-${VERSION}-aarch64.AppImage"
```

應該會回應 `HTTP/2 200` (成功) 或 `HTTP/2 302` (重新導向到有效檔案)。

### 6. 生成 Manifest

```bash
cd /path/to/cursor-overlay
sudo ebuild app-editors/cursor/cursor-1.8.0.ebuild manifest
```

這會下載 AppImages 並生成校驗和。

### 7. 測試安裝

```bash
# 如果已安裝舊版本,先移除
sudo emerge -C app-editors/cursor

# 安裝新版本
sudo emerge -av =app-editors/cursor-1.8.0

# 驗證
cursor --version
```

### 8. 清理舊版本 (可選)

如果新版本運作正常,您可以移除舊的 ebuild:

```bash
cd app-editors/cursor
rm cursor-1.7.52.ebuild
# 記得更新 Manifest
sudo ebuild cursor-1.8.0.ebuild manifest
```

## 🧪 測試變更

在提交之前,請徹底測試您的變更:

### 1. 語法檢查

```bash
# 檢查 ebuild 語法
repoman manifest
```

### 2. 安裝測試

```bash
# 完全移除並重新安裝
sudo emerge -C app-editors/cursor
sudo emerge -av app-editors/cursor
```

### 3. 功能測試

- ✅ 應用程式啟動
- ✅ 命令列選項運作 (`cursor --version`, `cursor .`)
- ✅ 桌面整合 (圖示、選單項目)
- ✅ Wayland/X11 支援 (如啟用)
- ✅ 中文輸入法 (如適用)
- ✅ AI 功能運作正常

### 4. 不同配置測試

```bash
# 測試不同的 USE flags
echo "app-editors/cursor -wayland" >> /etc/portage/package.use/cursor
sudo emerge -av app-editors/cursor

echo "app-editors/cursor wayland kerberos" >> /etc/portage/package.use/cursor
sudo emerge -av app-editors/cursor
```

## 📤 提交 Pull Request

### 1. 提交變更

```bash
# 暫存變更
git add app-editors/cursor/

# 提交並附帶清晰的訊息
git commit -m "feat: Update Cursor to version 1.8.0"

# 或修正 bug
git commit -m "fix: Correct BUILD_ID for Cursor 1.7.52"
```

### 提交訊息規範

使用 [Conventional Commits](https://www.conventionalcommits.org/) 格式:

- `feat:` - 新功能 (例如新版本)
- `fix:` - Bug 修正
- `docs:` - 文檔變更
- `refactor:` - 程式碼重構
- `test:` - 添加測試
- `chore:` - 維護任務

範例:
```
feat: Update Cursor to version 1.8.0

- Update BUILD_ID to latest release
- Verify download links for amd64 and arm64
- Generate new Manifest with checksums
- Test installation on Wayland and X11
```

### 2. 推送到您的 Fork

```bash
git push origin feature/your-feature-name
```

### 3. 建立 Pull Request

1. 訪問您在 GitHub 上的 fork
2. 點擊 "Pull Request" 按鈕
3. 填寫 PR 模板:
   - **標題**: 簡潔描述變更
   - **描述**: 詳細說明變更內容和原因
   - **測試**: 描述如何測試變更
   - **截圖**: 如適用,附上截圖

### 4. 程式碼審查

- 回應審查者的意見
- 根據建議進行修改
- 推送更新 (會自動更新 PR)

## 📝 編碼規範

### Ebuild 風格

遵循 [Gentoo 開發手冊](https://devmanual.gentoo.org/) 的規範:

1. **縮排**: 使用 Tab 縮排,不使用空格
2. **變數**: 使用大寫命名 (例如 `BUILD_ID`)
3. **引號**: 變數使用雙引號 `"${VAR}"`
4. **註解**: 添加清晰的註解說明複雜邏輯

範例:
```bash
# 正確 ✅
src_install() {
	insinto /opt/cursor
	doins -r *
}

# 錯誤 ❌ (使用空格縮排)
src_install() {
    insinto /opt/cursor
    doins -r *
}
```

### metadata.xml 風格

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE pkgmetadata SYSTEM "https://www.gentoo.org/dtd/metadata.dtd">
<pkgmetadata>
	<maintainer type="person">
		<email>maintainer@example.com</email>
		<name>Your Name</name>
	</maintainer>
	<use>
		<flag name="wayland">Enable Wayland support</flag>
	</use>
</pkgmetadata>
```

### 文檔風格

- 使用清晰、簡潔的語言
- 包含程式碼範例
- 為命令添加註解
- 保持格式一致

## 🎯 優先事項

目前歡迎的貢獻:

1. **🔥 高優先**:
   - 更新 Cursor 到最新版本
   - 修正 bug 和安裝問題
   - 改善文檔清晰度

2. **📚 中優先**:
   - 添加更多語言翻譯
   - 改善 USE flags 說明
   - 添加疑難排解指南

3. **💡 低優先**:
   - 程式碼重構
   - 自動化腳本
   - 額外範例

## ❓ 問題?

如果您有任何問題:

1. 查看 [README.md](README.md) 和現有文檔
2. 搜尋現有的 [Issues](https://github.com/Zakkaus/cursor-overlay/issues)
3. 在 GitHub 上開啟新的 Issue
4. 聯絡維護者: zakkauu@gmail.com

## 🙏 感謝

感謝您對 Cursor Overlay 的貢獻!每個貢獻,無論大小,都有助於讓 Gentoo 社群更加完善。

---

**準備好貢獻了嗎?** [Fork 這個倉庫](https://github.com/Zakkaus/cursor-overlay/fork) 並開始吧!
