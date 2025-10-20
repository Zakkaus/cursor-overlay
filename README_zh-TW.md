# Cursor Overlay for Gentoo

[English](README.md) | **繁體中文**

一個非官方的 Gentoo overlay,提供最新版本的 [Cursor](https://cursor.com/) AI 驅動程式碼編輯器。

## 🎯 關於

Cursor 是一款革命性的 AI 驅動程式碼編輯器,提供智慧程式碼補全、AI 對話、程式碼生成等功能。這個 overlay 旨在為 Gentoo 使用者提供最新版本的 Cursor,而官方 `gentoo-zh` 倉庫通常會落後於最新發布。

### ✨ 主要特色

- **🚀 最新版本**: 追蹤 Cursor 官方發布,快速更新
- **🔧 完整整合**: 原生 Gentoo 套件管理,完整系統整合
- **🎨 USE flags**: 靈活的功能配置 (Wayland、EGL 等)
- **🌏 多語言**: 支援繁體中文、簡體中文、英文等 30+ 種語言
- **🔐 安全**: 使用官方下載源,校驗完整性

## 📦 目前版本

- **最新版本**: `app-editors/cursor-1.7.52`
- **支援架構**: `amd64` (x86_64), `arm64` (aarch64)
- **Electron 版本**: 34.5.8
- **Node.js 版本**: 132.0.6834.210

## 🚀 安裝方式

### 方法 1: 使用 eselect-repository (推薦)

這是最簡單且推薦的方式:

```bash
# 1. 添加 overlay
sudo eselect repository add cursor-overlay git https://github.com/Zakkaus/cursor-overlay.git

# 2. 同步 overlay
sudo emerge --sync cursor-overlay

# 3. 接受測試關鍵字 (如果您使用穩定系統)
echo "app-editors/cursor ~amd64" | sudo tee /etc/portage/package.accept_keywords/cursor

# 4. 安裝 Cursor
sudo emerge -av app-editors/cursor
```

### 方法 2: 手動安裝

如果您想要更多控制:

```bash
# 1. 克隆倉庫
sudo git clone https://github.com/Zakkaus/cursor-overlay.git /var/db/repos/cursor-overlay

# 2. 添加到 repos.conf
sudo tee /etc/portage/repos.conf/cursor-overlay.conf << 'EOF'
[cursor-overlay]
location = /var/db/repos/cursor-overlay
sync-type = git
sync-uri = https://github.com/Zakkaus/cursor-overlay.git
auto-sync = yes
EOF

# 3. 同步並安裝
sudo emerge --sync cursor-overlay
echo "app-editors/cursor ~amd64" | sudo tee /etc/portage/package.accept_keywords/cursor
sudo emerge -av app-editors/cursor
```

## 🔧 進階配置

### USE Flags 說明

Cursor ebuild 提供以下 USE flags:

| USE Flag | 預設 | 說明 |
|----------|------|------|
| `egl` | ✅ 啟用 | 啟用 EGL 支援以獲得更好的圖形效能 |
| `wayland` | ✅ 啟用 | 啟用 Wayland 原生支援 (推薦 Wayland 使用者) |
| `kerberos` | ❌ 停用 | 啟用 Kerberos 驗證支援 (企業環境) |

### 自訂 USE Flags

如果您想自訂功能:

```bash
# 啟用 Wayland 和 EGL,停用 Kerberos (預設配置)
echo "app-editors/cursor wayland egl -kerberos" | sudo tee /etc/portage/package.use/cursor

# 只啟用 EGL,不使用 Wayland
echo "app-editors/cursor egl -wayland -kerberos" | sudo tee /etc/portage/package.use/cursor

# 啟用所有功能 (企業環境)
echo "app-editors/cursor wayland egl kerberos" | sudo tee /etc/portage/package.use/cursor
```

### 語言支援 (L10N)

預設已包含繁體中文 (`zh-TW`) 和簡體中文 (`zh-CN`)。如果您想自訂語言:

```bash
# 只保留繁體中文和英文
echo "app-editors/cursor L10N: zh-TW en-GB" | sudo tee -a /etc/portage/package.use/cursor

# 添加日文和韓文
echo "app-editors/cursor L10N: zh-TW ja ko" | sudo tee -a /etc/portage/package.use/cursor
```

支援的語言:
- 中文: `zh-CN` (簡體), `zh-TW` (繁體)
- 英文: `en-GB`
- 日文: `ja`
- 韓文: `ko`
- 以及 30+ 種其他語言

## 🔄 更新 Cursor

更新到最新版本非常簡單:

```bash
# 方式 1: 更新所有套件 (推薦)
sudo emerge --sync
sudo emerge -uDNav @world

# 方式 2: 只更新 Cursor
sudo emerge --sync cursor-overlay
sudo emerge -u app-editors/cursor
```

## 💻 使用方式

安裝完成後,您可以通過多種方式啟動 Cursor:

### 命令列

```bash
# 啟動 Cursor
cursor

# 開啟當前目錄
cursor .

# 開啟特定檔案
cursor /path/to/file.py

# 開啟特定資料夾
cursor ~/Projects/my-project

# 查看版本
cursor --version

# 查看幫助
cursor --help
```

### 圖形介面

在應用程式選單中搜尋 "Cursor" 即可啟動。

### 桌面整合

Cursor 會自動註冊為以下檔案類型的預設編輯器:
- 純文字檔案
- 程式碼檔案 (`.py`, `.js`, `.ts`, `.cpp` 等)
- 專案資料夾

## 🛠️ 疑難排解

### 問題: 無法啟動 Cursor

**解決方案**:
```bash
# 檢查安裝
which cursor
cursor --version

# 如果使用 Wayland,確保已啟用 wayland USE flag
emerge -pv cursor | grep wayland

# 嘗試使用 X11 強制啟動 (如果 Wayland 有問題)
cursor --disable-wayland
```

### 問題: 中文輸入法不工作

**解決方案**:
```bash
# 確保啟用了 Wayland IME 支援
# Cursor 會自動使用 --enable-wayland-ime 標誌

# 或手動啟動
cursor --enable-wayland-ime
```

### 問題: 顯示效能不佳

**解決方案**:
```bash
# 確保啟用 EGL
emerge -pv cursor | grep egl

# 如果沒有啟用,重新編譯
echo "app-editors/cursor egl" | sudo tee /etc/portage/package.use/cursor
sudo emerge -av app-editors/cursor
```

### 問題: 更新後無法啟動

**解決方案**:
```bash
# 清理舊版本
sudo emerge -c

# 重新安裝
sudo emerge -av app-editors/cursor
```

## 📝 解除安裝

如果您想移除 Cursor:

```bash
# 1. 移除套件
sudo emerge -C app-editors/cursor

# 2. (可選) 移除 overlay
sudo eselect repository remove cursor-overlay

# 3. (可選) 清理配置
sudo rm /etc/portage/package.accept_keywords/cursor
sudo rm /etc/portage/package.use/cursor
```

## 🐛 問題回報與貢獻

### 回報問題

發現 bug 或有功能建議?請在 [GitHub Issues](https://github.com/Zakkaus/cursor-overlay/issues) 回報。

回報時請提供:
- Gentoo 版本和架構 (`uname -a`)
- Cursor 版本 (`cursor --version`)
- 錯誤訊息和日誌
- 重現步驟

### 貢獻程式碼

歡迎貢獻!請參閱 [CONTRIBUTING.md](CONTRIBUTING.md) 了解詳情。

快速開始:
1. Fork 這個倉庫
2. 建立功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交變更 (`git commit -m 'Add amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 開啟 Pull Request

## 📚 相關資源

### Cursor 官方

- **官方網站**: https://cursor.com/
- **文件**: https://docs.cursor.com/
- **GitHub**: https://github.com/getcursor/cursor (社群)
- **Discord**: https://discord.gg/cursor

### Gentoo 資源

- **Gentoo 官方**: https://www.gentoo.org/
- **Gentoo Wiki**: https://wiki.gentoo.org/
- **Overlays 指南**: https://wiki.gentoo.org/wiki/Overlay
- **ebuild 開發**: https://devmanual.gentoo.org/

### 其他 Cursor Overlay

- **gentoo-zh**: https://github.com/microcai/gentoo-zh (官方中文 overlay)

## ⚠️ 免責聲明

這是一個**非官方** overlay,不隸屬於 Cursor 或 Anysphere Inc.。

- Cursor 是 Anysphere Inc. 的專有軟體
- 此 overlay 僅提供安裝 ebuild,不包含 Cursor 本體
- 使用 Cursor 需遵守其[使用條款](https://cursor.com/terms)
- 此 overlay 依照 MIT 授權釋出

## 📜 授權

### Overlay 授權

此 overlay (ebuild 腳本和設定檔) 採用 **MIT License**。

詳見 [LICENSE](LICENSE) 檔案。

### Cursor 軟體授權

Cursor 應用程式本身為專有軟體:
- 版權所有 © Anysphere Inc.
- 使用受 Cursor [使用條款](https://cursor.com/terms) 約束
- 詳情請訪問 https://cursor.com/

## 🙏 致謝

- 感謝 [gentoo-zh](https://github.com/microcai/gentoo-zh) 提供的原始 ebuild 參考
- 感謝 Cursor 團隊開發出色的 AI 程式碼編輯器
- 感謝所有貢獻者和使用者的支援

## 📞 聯絡方式

- **維護者**: [Zakkaus](https://github.com/Zakkaus)
- **電子郵件**: zakkauu@gmail.com
- **GitHub**: https://github.com/Zakkaus/cursor-overlay
- **問題追蹤**: https://github.com/Zakkaus/cursor-overlay/issues

---

**喜歡這個 overlay?** 給個 ⭐️ Star 吧!

**有問題?** 開個 [Issue](https://github.com/Zakkaus/cursor-overlay/issues/new)!

**想貢獻?** 提交 [Pull Request](https://github.com/Zakkaus/cursor-overlay/pulls)!
