# 隱私權政策 / Privacy Policy

**酷澎分潤連結產生器 (Coupang Partners Link Generator)**

最後更新：2026 年 5 月

## 中文

### 我們收集的資訊

本擴充功能**不收集任何個人資料**，也不會將任何資料傳送到我們的伺服器（事實上我們沒有伺服器）。

唯一儲存的資料：
- 你在「設定」頁面填入的 Coupang Partners API 憑證（Access Key / Secret Key / Sub ID / 市場別）
- 這些資料只儲存在你瀏覽器的 `chrome.storage.sync` 內，由 Chrome 加密保存並隨你的 Google 帳號同步到你的其他裝置（如果你有開啟 Chrome 同步）

### 資料如何被使用

當你在酷澎頁面按下「產生分潤網址」時，本擴充功能會：

1. 讀取當前分頁的網址
2. 用你的 API 憑證對 `https://api-gateway.tw.coupang.com`（或備援 host）發送請求，由酷澎官方產生分潤連結
3. 把長/短網址顯示給你，方便你複製

**所有 API 通訊都是直接從你的瀏覽器發到酷澎的伺服器，不經過任何第三方。**

### 我們不會做的事

- 不收集瀏覽歷史
- 不收集個人身分資料
- 不追蹤你產生的連結
- 不將你的憑證傳送到第三方
- 不在任何分析平台埋追蹤碼
- 不出售任何資料

### 資料刪除

你可以隨時：
- 在擴充功能設定頁按「清除」清掉所有儲存的資料
- 或在 `chrome://extensions` 移除擴充功能（會自動清除所有相關資料）

### 第三方服務

本擴充功能僅與以下網域通訊：
- `*.coupang.com` — 酷澎官方 API 與網站
- `*.coupa.ng` — 酷澎短網址服務

### 聯絡

如果有任何隱私相關疑慮，請透過 Chrome Web Store 商品頁的「支援」連結回報。

---

## English

### Information We Collect

This extension **does not collect any personal data** and does not transmit any data to our servers (in fact, we don't have any servers).

The only data stored:
- Your Coupang Partners API credentials (Access Key, Secret Key, Sub ID, market) which you enter on the Settings page
- These are stored only in your browser's `chrome.storage.sync`, encrypted by Chrome, and synced to your other devices via your Google account if you have Chrome sync enabled

### How Data Is Used

When you click "Generate Affiliate Link" on a Coupang page, this extension will:

1. Read the current tab's URL
2. Send a request to `https://api-gateway.tw.coupang.com` (or fallback hosts) using your API credentials, asking Coupang to generate the affiliate link
3. Display the long and short URLs for you to copy

**All API communication is direct from your browser to Coupang's servers, with no third party involved.**

### What We Do Not Do

- We do not collect browsing history
- We do not collect personally identifiable information
- We do not track which links you generate
- We do not transmit your credentials to any third party
- We do not embed any analytics tracking
- We do not sell any data

### Data Deletion

At any time, you can:
- Click "Clear" on the Settings page to remove all stored data
- Or remove the extension from `chrome://extensions` (this automatically clears all related data)

### Third-Party Services

This extension only communicates with the following domains:
- `*.coupang.com` — Coupang's official API and websites
- `*.coupa.ng` — Coupang's URL shortener

### Contact

For any privacy-related concerns, please reach out via the "Support" link on the Chrome Web Store listing.
