# 📓 OneNote Explorer

透過 Microsoft Graph API 搜尋您的 OneNote 筆記，部署在 GitHub Pages 上，不需要後端伺服器。

## ✨ 功能

- 🔐 Microsoft 帳號登入（MSAL）
- 🔍 關鍵字搜尋筆記標題
- 📅 起始日期篩選
- 📋 除錯日誌面板
- 📱 RWD 響應式設計

---

## 🚀 部署步驟

### 1. Fork 或上傳此 Repo

將這個資料夾上傳到您的 GitHub。

### 2. 開啟 GitHub Pages

進入 Repo → **Settings → Pages**  
Source 選 `Deploy from a branch` → Branch: `main` → `/root` → **Save**

您的網址會是：
```
https://<您的GitHub帳號>.github.io/<Repo名稱>/
```

### 3. 設定 Azure App（必做！）

前往 [Azure Portal](https://portal.azure.com) → 應用程式註冊 → 選擇您的 App：

**① 驗證頁面 → 重新導向 URI**  
加入您的 GitHub Pages 網址（結尾要有 `/`）：
```
https://<您的GitHub帳號>.github.io/<Repo名稱>/
```

**② API 權限** 確認包含：
| 權限 | 類型 |
|------|------|
| `User.Read` | 委派 |
| `Notes.Read` | 委派 |

**③ 若為學校/公司帳號**，需點「授與管理員同意」。

---

## 🔑 關於 Client ID 的安全性

> **Client ID 不是秘密，公開在程式碼裡完全沒問題。**

此工具使用的是 MSAL **Public Client** 流程（純前端 SPA），微軟的設計就是讓 Client ID 公開。  
真正需要保密的 `Client Secret` 在本工具中完全用不到，也不會出現在程式碼裡。

---

## 🛠 使用說明

1. 開啟網頁，點右上角 ⚙️ 填入您的 **Client ID** → 儲存
2. 點「🔐 登入 Microsoft」
3. 輸入關鍵字 → 點「🔎 搜尋筆記」
4. 點擊結果卡片即可在瀏覽器開啟該筆記

> **搜尋模式說明：**  
> 商業/教育帳號：Graph API `$search` 全文搜尋  
> 個人帳號：自動切換為「抓取最近 200 筆 → 標題篩選」模式

---

## 🐛 常見問題

| 問題 | 解決方式 |
|------|---------|
| 登入後跳回空白頁 | Azure Portal 的重新導向 URI 是否與網址完全一致（含尾部 `/`）？ |
| 403 錯誤 | Notes.Read 權限未授與，或學校帳號需要管理員同意 |
| 彈出視窗被封鎖 | 允許此網站的彈出視窗 |
| 搜尋不到結果 | 個人帳號改用標題篩選，請確認關鍵字與筆記標題相符 |

---

## 📄 License

MIT — 自由使用與修改
