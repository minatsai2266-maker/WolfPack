# 公會佈達站：上線設定說明

網站本體放在 **GitHub Pages**（免費），資料和管理員登入放在 **Firebase**（免費方案就夠用）。
成員打開網址就能看公告、報名，不需要註冊。

檔案：
- `index.html`：整個網站
- `firestore.rules`：資料庫權限（誰能看、誰能改）

---

## 第一步：建立 Firebase 專案（約 10 分鐘）

1. 用 Google 帳號登入 https://console.firebase.google.com ，按「建立專案」，名稱隨意（例如 `guild-board`），Google Analytics 可以關掉。
2. 左側「建構 → Authentication」→「開始使用」→ 登入方式選 **電子郵件/密碼** → 啟用 → 儲存。
3. 左側「建構 → Firestore Database」→「建立資料庫」→ 位置選 `asia-east1`（台灣）→ 選「以正式版模式啟動」。
4. Firestore 頁面上方點「規則」，把 `firestore.rules` 的內容整份貼上，**把 `OWNER@example.com` 改成妳的 Email（全小寫）**，按「發布」。
5. 專案首頁按 `</>`（網頁應用程式）圖示新增一個 Web App，名稱隨意，不用勾 Hosting。
   畫面會出現一段 `const firebaseConfig = { apiKey: ..., ... }`，把這段複製下來給我（這段是公開的設定，不是密碼，可以放心貼）。

## 第二步：建立 GitHub 儲存庫

1. 到 https://github.com/new 建一個 **Public** 的 repository，名稱例如 `guild-board`，按 Create。
2. 告訴我 repository 名稱，並確認 Claude 有權限存取（https://github.com/apps/claude/installations/select_target ）。
3. 我把檔案推上去後，到 repository 的「Settings → Pages」，Source 選 `Deploy from a branch`、Branch 選 `main` / `(root)`，按 Save。
   幾分鐘後網址會是 `https://你的帳號.github.io/guild-board/`。
4. 回到 Firebase「Authentication → 設定 → 已授權網域」，新增 `你的帳號.github.io`。

## 第三步：設定最高管理員

1. 打開網站 → 右上「管理員登入」→「第一次使用？設定密碼」，用妳在規則裡填的 Email 設密碼。
2. 到信箱點驗證連結（也看看垃圾郵件匣），回網站按「我已經驗證了」。
3. 上方會多一個「⚙ 管理員設定」分頁，在這裡輸入其他管理員的 Email 新增。
4. 其他管理員一樣用「第一次使用？設定密碼」→ 驗證信 → 登入就能編輯。

---

## 使用說明

- **公告頁**：可以新增多則公告，可設「置頂」。
- **標裝限制／人員名單／敵人警誡名單**：各是一整頁內容，管理員按「編輯這頁」修改，可設頁面底色。
- **各項補助商品報名**：管理員新增報名項目（可設截止日、開關報名），成員填角色名稱和備註就能報名；管理員可以移除報名、下載 CSV 名單（Excel 可開）。
- **編輯器**：字體、字體大小、文字顏色／底色（調色盤圖示）、表格、圖片、連結、對齊、清單等。
  - 「上傳圖片」按鈕會自動把照片縮小，建議用它；每則內容的圖片總量建議在 3～5 張內（資料庫單筆上限約 1MB）。
  - 也可以用「圖片」按鈕貼上圖片網址，網址圖片不佔空間。

## 費用

Firebase 免費方案（Spark）每天 5 萬次讀取、2 萬次寫入，公會規模的網站用不完，不需綁信用卡。GitHub Pages 免費。
