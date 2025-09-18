# YTlinktoiframe

# YouTube 連結 ➜ iframe 產生器

一個給記者／編輯在 **手機或桌機** 上快速把 YouTube 連結轉成可嵌入 `<iframe>` 的小工具。以 **Bootstrap 5** 打造，單一 HTML 檔即可使用，支援時間戳、播放清單、`shorts`，並提供複製／貼上／清除與即時預覽。

---

## ✨ 功能特色

* **多連結格式支援**：`watch?v=...`、`youtu.be/...`、`shorts/...`、以及播放清單 `list=...`。
* **時間戳支援**：`?t=90`、`?t=1m30s`、`&start=45` 皆可解析為秒數。
* **一鍵產生 iframe**：輸入（或貼上）連結 → 立即產生可貼進 CMS 的 `<iframe>` 程式碼。
* **即時預覽**：右側卡片可立即看到嵌入效果。
* **複製／貼上／清除**：

  * 「**貼上**」按鈕在 **「YouTube 網址」標題** 右側，會嘗試讀取剪貼簿並自動產生預覽。
  * 「**複製**」按鈕在 **「輸出程式碼」** 標題右側，一鍵複製產出的 `<iframe>`。
  * 「**清除**」按鈕可快速清空輸入與預覽。
* **進階設定（預設收合）**：

  * 自訂寬／高，或勾選 **響應式（16:9）** 包裹（Bootstrap `.ratio-16x9`）。
  * 切換 **autoplay**、**mute**、**controls**、**rel=0**。
* **貼心提示**：所有關鍵動作（複製成功、貼上權限不足等）皆以 **Bootstrap Toast** 顯示於右下角。
* **鍵盤快捷**：在網址輸入框按 **Enter** 直接產生。

---

## 📦 專案結構

本工具為單檔案專案：

```
index.html  # 含 Bootstrap CDN、UI 與所有邏輯
```

無需建置流程，直接打開 `index.html` 即可使用。

> 依賴：Bootstrap 5.3（CDN），無額外套件。

---

## 🚀 快速開始

1. 下載或複製本專案到你的電腦。
2. 雙擊開啟 `index.html`（或以任何靜態伺服器提供）。
3. 貼上 YouTube 連結，按「產生」，複製下方程式碼貼到你的 CMS／後臺即可。

> 若要部署到 GitHub Pages：將 `index.html` 放在 repo 根目錄，於 GitHub 開啟 Pages（Branch: `main` / 根目錄）。

---

## 🧭 使用說明

1. **輸入 YouTube 連結**（或點標題右側 **貼上** 由剪貼簿帶入）。
2. 按 **產生**，右側即時預覽會更新，並在下方輸出區顯示 `<iframe>` 程式碼。
3. 需要進階控制時，展開 **進階設定**：

   * **寬度／高度**：預設 `560×315`。
   * **響應式**：勾選時，會以 `<div class="ratio ratio-16x9">` 包裹 `<iframe>`，適合 RWD。
   * **自動播放（autoplay）**：行動裝置通常需要同時 **靜音（mute）** 才會允許自動播放。
   * **靜音（mute）**：與 `autoplay` 常搭配使用。
   * **控制列（controls）**：可隱藏或顯示播放控制列。
   * **rel=0**：僅顯示**同頻道**的相關影片（註：YouTube 規則變更後，無法完全關閉相關影片）。
4. 按 **複製** 將輸出程式碼複製到剪貼簿。

---

## 🔗 支援的連結格式

* `https://www.youtube.com/watch?v=VIDEO_ID`
* `https://youtu.be/VIDEO_ID`
* `https://www.youtube.com/shorts/VIDEO_ID`
* 播放清單：`https://www.youtube.com/playlist?list=PLAYLIST_ID` 或 `watch?v=...&list=...`
* **時間戳**：

  * `?t=90`、`?t=1m30s`、`&start=45` → 皆會轉為 `start=秒數`

> 產生的影片嵌入 URL 形式：
>
> * 影片：`https://www.youtube.com/embed/VIDEO_ID?...`
> * 清單：`https://www.youtube.com/embed/videoseries?list=PLAYLIST_ID...`

---

## 🧩 產出範例

```html
<iframe width="560" height="315" src="https://www.youtube.com/embed/amlJDZd_iew?start=90" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
```

若勾選 **響應式（16:9）**，外層還會包：

```html
<div class="ratio ratio-16x9">
  <!-- 上述 iframe 放在這裡 -->
</div>
```

---

## ⚠️ 瀏覽器與權限注意事項

* **讀取剪貼簿**（貼上按鈕）需要 **HTTPS** 網站或 `localhost`，且需使用者觸發動作。
* 某些瀏覽器（特別是 iOS Safari）對剪貼簿權限較嚴格，無法直接讀取時，系統會跳出 Toast 提示你改用手動貼上。
* **自動播放** 常見限制：行動裝置通常需 **同時靜音** 才可自動播放。
* **rel=0 行為**（YouTube 規則，2018 之後）：無法完全關閉相關影片，只會限制為「同頻道」的相關影片。

---

## 🔧 自訂與擴充

* **預設參數**：可在 `buildEmbedUrl()` 內調整預設 query 參數，例如固定加上 `modestbranding=1`、`playsinline=1`。
* **允許權限**：`<iframe allow="...">` 目前包含 `autoplay`、`encrypted-media`、`picture-in-picture` 等常用權限，若有特別需求可自行增減。
* **按鈕版位**：

  * 「貼上」按鈕已置於「YouTube 網址」標題右側。
  * 「複製」按鈕置於「輸出程式碼」標題右側。
  * 若想改成圖示按鈕或 Tooltip，可直接調整對應按鈕樣式與屬性。

---

## 🧱 已知限制

* 不支援 **會員影片**、**年齡限制** 或需要登入授權的內容（YouTube 本身不允許嵌入或會顯示受限）。
* 若網址格式不標準、或短網址經過額外跳轉，可能須先在瀏覽器中開啟後再複製分享連結。

---

## 🤝 貢獻

Issue／PR 歡迎協作：

* 改善網址解析（例如更完整的 `shorts` 變體、時間戳解析）。
* 增加更多參數切換（`modestbranding`、`playsinline`、`loop`、`playlist` 等）。
* i18n 語系切換（目前為繁體中文）。

---

## 📝 授權

MIT License

---

## 🗒️ 版本紀錄（Changelog）

* **v1.4**：把「貼上」移到「YouTube 網址」標題右邊；輸入列只保留清除／產生。
* **v1.3**：新增「貼上」與「清除」按鈕；貼上可自動判斷並產生預覽。
* **v1.2**：進階設定改為預設收合；整合完整參數（寬高、RWD、autoplay、mute、rel、controls）。
* **v1.1**：複製成功以 Toast 提示（2 秒自動關閉）。
* **v1.0**：初版：貼上 YouTube 連結 → 產生 `<iframe>`，含即時預覽。
