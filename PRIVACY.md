# 隱私權政策 / Privacy Policy

**酷澎分潤連結產生器 (Coupang Partners Link Generator)**

最後更新：2026 年 10 月（v1.12.0；新增「✨ AI 文案」說明）

## 中文

### 摘要

- 本擴充功能**不收集個人資料**、不埋追蹤碼、不出售任何資料。
- 你的 Coupang Partners API 憑證**只存在你自己的瀏覽器裡**，永遠不會傳送到我們或任何第三方。授權金鑰也存在你的瀏覽器裡，只有驗證授權時會送到我們的授權伺服器（見下方「授權驗證」）。
- 本擴充功能只在兩種情況把資料送到我們的伺服器：**授權驗證**（只送金鑰與一組隨機裝置識別碼），以及**你按下 ✨AI 時**（只送目前這個商品頁上的公開商品資訊，見下方「AI 文案」）。
- 價格追蹤的歷史、截圖、文案，**全部在你自己的電腦上產生與保存**。

### 我們儲存什麼（全部都在你的裝置上）

- 你在「設定」頁填入的 Coupang Partners API 憑證（Access Key / Secret Key / Sub ID / 市場別）與授權金鑰，儲存在 `chrome.storage.sync`，由 Chrome 加密保存，並在你開啟 Chrome 同步時同步到你自己的其他裝置。
- 價格追蹤的商品清單與歷史價格、截圖工具的偏好（標貼樣式、走勢卡片的開關與位置）、你選的文案版型，儲存在 `chrome.storage.local`（**只在這台電腦，不會同步、不會上傳**）。

### 產生分潤連結時

1. 讀取當前分頁的網址
2. 用**你自己的** API 憑證向 `https://api-gateway.tw.coupang.com`（或備援 host）請求，由酷澎官方產生分潤連結
3. 把長／短網址顯示給你複製

這段通訊是直接從你的瀏覽器發到酷澎的伺服器。

### 📊 價格追蹤（你按下 ☆ 才會開始）

你在商品頁按「☆ 追蹤價格」之後，擴充功能會定期回去看那個商品現在多少錢，把價格記在你的電腦上，畫成走勢圖。

**它會連到哪裡**

只有**酷澎自己的網站與官方 API**。價格追蹤的過程**完全不經過我們的伺服器**，我們不知道你在追蹤哪些商品。

**它怎麼抓價**

1. 優先在你**已經開著的酷澎分頁**裡發出同源請求；若沒有開著的分頁，則由擴充功能在背景直接請求。
2. 這兩種方式都會**帶上你在酷澎的登入狀態（cookie）**，和你自己打開那個商品頁看到的畫面一致 —— 這也是為什麼追蹤到的是**你看到的價格**（含 WOW 會員價、已套用的優惠券價），而不是未登入的牌價。
3. 官方 Partners API 作為備援來源，同樣使用你自己的 API 憑證。

**多久一次**

- 每小時檢查一輪；同一個商品若價格沒變，最短間隔 3 小時才會新增一筆紀錄。
- 被酷澎暫時擋下時會自動退避（2／4／8 小時），不會反覆重試。
- 你也可以在儀表板手動更新（全部更新有 45 分鐘冷卻，單一商品不受限制）。

**存多久、存在哪**

每個商品最多保留 400 筆價格點，全部存在 `chrome.storage.local`（只在這台電腦）。**沒有雲端備份**：你重灌、換電腦或移除擴充功能，這些紀錄就會消失。

**取消追蹤**：在儀表板按 ✕ 即可；不追蹤就不會再去抓那個商品。

### 📸 截圖工具

- 使用 Chrome 的分頁截圖功能，只擷取**你自己框選的範圍**。
- 單價標貼、價格走勢卡片都是在你的電腦上畫到圖片裡的。
- 成品直接放進你的剪貼簿，**不會上傳到任何地方**，我們也拿不到。

### ✏️ 短文案

口語版與條列版**完全在你的電腦上運算**，使用的是商品頁上的公開資訊與內建句庫，**不連網、不傳送任何資料**。

### ✨ AI 文案（只有你按下 ✨AI 才會連線）

此功能自 v1.12.0 起提供。AI 版需要把商品資訊交給 AI 模型來寫，流程如下。

**送出什麼**

你按下 ✨AI 時，擴充功能從**目前這個商品頁**讀取公開資訊，送到我們架在 Cloudflare Workers 上的伺服器（`coupang-ai-copy.pidan0126.workers.dev`）：

- 商品標題、品牌、分類、價格、評分與評價數、「近一個月超過 N 位購買」、商品資訊表（成分、原產地、製造商、規格等）、購買數量選項與單價、配送標籤（例如免運）
- 這個商品頁的網址（**已去掉所有查詢參數**，不含你的分潤連結或 Sub ID），只用來辨認是不是同一個商品
- 授權用的數位簽章憑證（內含金鑰的單向雜湊值與隨機裝置識別碼，**不含金鑰本身**）

**不會送出**：你的 API 憑證、授權金鑰本身、分潤連結與 Sub ID、瀏覽紀錄、追蹤清單、任何個人資料。

**交給誰**

我們的伺服器先驗證授權，再把**商品資訊**轉交給 OpenAI 的 API 產生文案。轉交時會再拿掉商品網址與價格（貼文裡的價格那一行由擴充功能在你的電腦上自己加）；授權憑證只在我們的伺服器驗證，不會轉交。
依 OpenAI 公開的 API 資料政策，經由 API 傳送的資料**不會被用來訓練模型**，為了偵測濫用最多保留 30 天（法律另有要求時除外），詳見 [OpenAI 官方說明](https://developers.openai.com/api/docs/guides/your-data)。

**我們保留什麼**

- 每組授權每天用了幾次：只存授權的雜湊代號與次數，約 36 小時後自動刪除
- 產生出來的文案：快取 24 小時，讓同一個商品再按一次可以立刻出現；快取的索引是單向雜湊，不是可讀的網址
- 這兩樣都不含個人資料。連線時 Cloudflare 會看到你的 IP 位址（任何網路連線都會），我們的程式不記錄 IP。

AI 產生的文案在送到你的畫面前，會先在你的電腦上逐句檢查（療效宣稱、捏造的數字等），不合格的句子直接拿掉。

### 授權驗證

為了確認訂閱有效，擴充功能會向我們的授權伺服器（Google Apps Script，`script.google.com`）驗證你的金鑰，並取回一張有數位簽章的離線憑證（約每 24 小時一次）。傳送的內容只有：**金鑰本身、以及擴充功能自行產生的一組隨機裝置識別碼**（用來限制一組金鑰只在一台裝置使用）。不含任何個人資料，也不含你的 API 憑證，更不含你追蹤了哪些商品。

### 我們不會做的事

- 不收集瀏覽歷史
- 不收集個人身分資料
- 不追蹤你產生了哪些連結
- 不知道、也不記錄你在追蹤哪些商品
- 不上傳你的截圖
- 不將你的 API 憑證或授權金鑰傳送給任何第三方
- 不在任何分析平台埋追蹤碼
- 不出售任何資料
- 不執行任何遠端程式碼

### 資料刪除

- 在擴充功能設定頁按「清除」可清掉所有儲存在本機的資料
- 在儀表板逐一按 ✕ 可移除個別商品的追蹤
- 在 `chrome://extensions` 移除擴充功能會清除所有相關本機資料（**包含價格歷史，且無法復原**）

除了授權驗證，以及 AI 文案的使用次數與 24 小時快取（不含個人資料，時間到自動刪除）之外，我們沒有保存任何你的資料，所以沒有需要向我們申請刪除的東西。

### 第三方服務

| 網域 | 用途 | 何時會連線 |
|---|---|---|
| `*.coupang.com`、`*.coupa.ng` | 酷澎官方網站、API 與短網址 | 產生分潤連結、追蹤價格時 |
| `script.google.com`、`script.googleusercontent.com` | 我們的授權驗證伺服器（Google Apps Script） | 驗證授權（約每 24 小時一次） |
| `coupang-ai-copy.pidan0126.workers.dev` | 我們的 AI 文案伺服器（Cloudflare Workers） | 你按下 ✨AI 時 |
| `api.openai.com`（由我們的伺服器連線，不是你的瀏覽器） | 產生 AI 文案（OpenAI） | 你按下 ✨AI，且這個商品 24 小時內沒有快取時 |

除上述之外，本擴充功能不會連線到任何第三方服務。

### 聯絡

如果有任何隱私相關疑慮，請透過 Chrome Web Store 商品頁的「支援」連結，或 LINE（pidan0126）回報。

---

## English

### Summary

- This extension **does not collect personal data**, contains no analytics or tracking code, and sells no data.
- Your Coupang Partners API credentials are **stored only in your own browser** and are never sent to us or to any third party. Your licence key is also stored in your browser and is sent only to our licence server, to verify your subscription (see "Licence verification" below).
- The extension sends data to our servers in only two cases: **licence verification** (only your key and a random device identifier), and **when you click ✨AI** (only public product information from the product page you are on; see "AI post text" below).
- Price history, screenshots and post text are all **produced and stored on your own computer**.

### What we store (all on your own device)

- The Coupang Partners API credentials (Access Key, Secret Key, Sub ID, market) and licence key you enter on the Settings page, stored in `chrome.storage.sync`, encrypted by Chrome and synced to your own other devices if you have Chrome sync enabled.
- Your tracked product list and price history, screenshot preferences (label style, trend-card on/off and position) and your chosen post-text template, stored in `chrome.storage.local` (**this computer only; never synced, never uploaded**).

### When generating an affiliate link

1. Read the current tab's URL
2. Using **your own** API credentials, request an affiliate link from `https://api-gateway.tw.coupang.com` (or fallback hosts)
3. Display the long and short URLs for you to copy

This communication goes directly from your browser to Coupang's servers.

### 📊 Price tracking (starts only when you click ☆)

After you click "☆ Track price" on a product page, the extension periodically re-checks that product's price, stores it on your computer and draws a trend chart.

**Where it connects**

Only to **Coupang's own website and official API**. Price tracking **never passes through our servers**; we do not know which products you track.

**How it reads the price**

1. It prefers to issue a same-origin request from a **Coupang tab you already have open**; if none is open, the extension requests the page directly in the background.
2. Both paths **carry your Coupang login state (cookies)**, so the page seen matches what you would see yourself — which is why the tracked figure is **your price** (including WOW member pricing and applied coupons) rather than the logged-out list price.
3. The official Partners API acts as a fallback source, using your own API credentials.

**How often**

- One check per hour. For a given product, if the price is unchanged, a new data point is recorded at most once every 3 hours.
- If Coupang temporarily blocks the request, the extension backs off automatically (2/4/8 hours) rather than retrying repeatedly.
- You can also refresh manually from the dashboard (a 45-minute cooldown applies to "refresh all"; single products are not limited).

**How long, and where**

Up to 400 price points per product, all in `chrome.storage.local` (this computer only). **There is no cloud backup**: reinstalling, changing computer or removing the extension loses this history.

**To stop tracking**: click ✕ in the dashboard; the extension then stops fetching that product.

### 📸 Screenshot tool

- Uses Chrome's tab-capture feature and captures **only the area you select**.
- The unit-price label and the price-trend card are drawn into the image on your own computer.
- The result goes straight to your clipboard. It is **never uploaded**, and we never see it.

### ✏️ Post text

The conversational and bullet templates run **entirely on your computer**, using public information from the product page and a built-in phrase library. **No network access, no data sent.**

### ✨ AI post text (connects only when you click ✨AI)

Available from v1.12.0. The AI version needs to hand product information to an AI model, as follows.

**What is sent**

When you click ✨AI, the extension reads public information from **the product page you are on** and sends it to our server on Cloudflare Workers (`coupang-ai-copy.pidan0126.workers.dev`):

- Product title, brand, category, price, rating and review count, "over N bought in the past month", the product information table (ingredients, origin, manufacturer, specifications, etc.), quantity options with unit prices, and delivery labels (e.g. free shipping)
- The product page URL **with all query parameters removed** (no affiliate link, no Sub ID), used only to recognise the same product
- The digitally signed licence lease (a one-way hash of the key and a random device identifier — **not the key itself**)

**Not sent**: your API credentials, the licence key itself, affiliate links or Sub ID, browsing history, your tracked-product list, or any personal data.

**Who receives it**

Our server verifies the licence, then forwards the **product information** to the OpenAI API to write the text. The product URL and price are removed before forwarding (the price line in the post is added by the extension on your own computer); the licence lease is verified on our server only and never forwarded.
Under OpenAI's published API data policy, data sent through the API **is not used to train models** and is retained for up to 30 days for abuse monitoring (unless longer retention is required by law); see [OpenAI's documentation](https://developers.openai.com/api/docs/guides/your-data).

**What we keep**

- How many times each licence used the feature today: only a hashed licence identifier and a count, deleted automatically after about 36 hours
- The generated text: cached for 24 hours so that clicking again on the same product is instant; the cache is indexed by a one-way hash, not a readable URL
- Neither contains personal data. Cloudflare sees your IP address when you connect (as with any network connection); our code does not record it.

Before AI text reaches your screen, it is checked line by line on your own computer (health claims, invented numbers and so on), and any line that fails is removed.

### Licence verification

To confirm your subscription is valid, the extension verifies your key against our licence server (Google Apps Script, `script.google.com`) and receives a digitally signed offline lease, roughly once every 24 hours. Only two things are sent: **the key itself and a random device identifier generated by the extension** (used to limit one key to one device). No personal data, no API credentials, and nothing about which products you track.

### What we do not do

- We do not collect browsing history
- We do not collect personally identifiable information
- We do not track which links you generate
- We do not know or record which products you track
- We do not upload your screenshots
- We do not send your API credentials or licence key to any third party
- We do not embed analytics or tracking
- We do not sell any data
- We do not execute remote code

### Data deletion

- Click "Clear" on the Settings page to remove all locally stored data
- Click ✕ in the dashboard to stop tracking an individual product
- Removing the extension at `chrome://extensions` clears all related local data (**including price history, irreversibly**)

Apart from licence verification, and the AI feature's usage counter and 24-hour cache (no personal data, deleted automatically), we keep no data about you, so there is nothing to request deletion of from us.

### Third-party services

| Domain | Purpose | When contacted |
|---|---|---|
| `*.coupang.com`, `*.coupa.ng` | Coupang's official website, API and URL shortener | Generating affiliate links, price tracking |
| `script.google.com`, `script.googleusercontent.com` | Our licence verification server (Google Apps Script) | Licence checks (about once every 24 hours) |
| `coupang-ai-copy.pidan0126.workers.dev` | Our AI post-text server (Cloudflare Workers) | When you click ✨AI |
| `api.openai.com` (contacted by our server, not by your browser) | Writing AI post text (OpenAI) | When you click ✨AI and the product has no cached result from the last 24 hours |

The extension contacts no third-party services other than those listed above.

### Contact

For privacy-related concerns, please use the "Support" link on the Chrome Web Store listing, or LINE (pidan0126).
