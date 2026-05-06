# 📒 學習筆記整理 — 上架說明

## 上架 GitHub Pages（5 分鐘）

### 步驟一：建立 GitHub Repository

1. 前往 https://github.com/new
2. Repository name 填 `notes-app`（或任何名稱）
3. 選 **Public**
4. 點「Create repository」

### 步驟二：上傳檔案

**方法 A — 直接在網頁上傳（最簡單）**
1. 進入剛建立的 repo
2. 點「uploading an existing file」
3. 把 `index.html` 拖進去
4. 點「Commit changes」

**方法 B — 用 git**
```bash
git init
git add index.html
git commit -m "init"
git remote add origin https://github.com/你的帳號/notes-app.git
git push -u origin main
```

### 步驟三：開啟 GitHub Pages

1. 進入 repo → Settings → Pages
2. Source 選「Deploy from a branch」
3. Branch 選「main」，資料夾選「/ (root)」
4. 點 Save

幾分鐘後網址會是：
`https://你的帳號.github.io/notes-app/`

---

## 設定 Firebase（跨裝置同步）

### 建立 Firebase 專案

1. 前往 https://console.firebase.google.com
2. 新增專案（名稱例如 `my-notes`）
3. 進入專案 → Firestore Database → 建立資料庫（測試模式）
4. 點左上「⚙ 專案設定」→「你的應用程式」→「新增 Web 應用程式」
5. 複製 `firebaseConfig` 裡的 `apiKey`、`projectId`、`appId`

### 在網站上填入設定

1. 打開你的筆記網站
2. 點右上角「🔥 Firebase」按鈕
3. 填入 API Key、Project ID、App ID
4. 點「儲存並連線」

設定只存在你的瀏覽器，不會上傳到 GitHub。

### Firestore 安全規則（建議設定）

Firebase Console → Firestore → 規則，貼上：

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /notes/{document} {
      allow read, write: if true;
    }
  }
}
```

---

## 注意事項

- **未設定 Firebase** → 筆記存在瀏覽器 localStorage，換裝置會不見
- **設定 Firebase 後** → 自動同步到雲端，任何裝置都能看到
- Firebase 設定存在 localStorage，不會被推到 GitHub，安全沒問題
