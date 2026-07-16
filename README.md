# 足跡地球儀 · PWA 版（iPhone 直接讀相簿）

單一個 `index.html`。iPhone Safari 開啟 → 按「選照片」→ 從相簿挑帶定位的照片 →
前端讀 GPS → 標到 3D 地球上。加到主畫面就像一個 App，重開會記得上次的足跡。

**不需要 Mac、不需要開發者帳號、不需要編譯、不需要上架。**

---

## 為什麼要「上傳到網站」才能在手機用

iPhone 要「加到主畫面」並穩定運作，需要一個網址（https）。以下三種免費作法擇一，
把整個 `pwa/` 資料夾（其實只有 index.html）放上去即可。

### 方式 A：Netlify Drop（最快，免註冊登入也能試）
1. 電腦瀏覽器開 https://app.netlify.com/drop
2. 把 `pwa` 資料夾**直接拖進網頁**。
3. 幾秒後得到一個網址，例如 `https://xxxx.netlify.app`。
4. iPhone Safari 開那個網址即可。

### 方式 B：GitHub Pages（想長期保存）
1. 建一個 repo，把 `index.html` 傳上去。
2. Settings → Pages → Source 選 `main` 分支 → 存檔。
3. 得到 `https://你的帳號.github.io/repo名/`。

### 方式 C：Cloudflare Pages / Vercel
同理，拖資料夾或連 GitHub 部署，都會給 https 網址。

---

## 在 iPhone 上使用

1. Safari 打開你的網址。
2. 按底部「＋ 選照片」，從相簿選照片（可多選）。
3. 有 GPS 的會標上地球；沒定位的會自動略過（會顯示略過幾張）。
4. 點地球上的光點 → 跳出照片縮圖 + 地名 + 日期。
5. **加到主畫面**：Safari 分享鈕 → 「加入主畫面」→ 之後從桌面圖示全螢幕開啟。

資料存在手機本機（IndexedDB），重開 App 會自動載回，不會上傳到任何伺服器。

---

## ⚠️ 唯一要你親自驗證的事：iOS 會不會把 GPS 拔掉

這是路線 1 事先無法確定、**只能用你的真實照片在 iPhone 上實測**的一點：

- iOS 從相簿透過網頁選照片時，**有時基於隱私會移除 GPS**。
- 若你選了明明有定位的照片，卻一直顯示「N 張無定位」，就是被拔掉了。

**若真的被拔掉的救援方案：**
- 改走「電腦建檔」：用同資料夾裡的 `build_globe.py` 在電腦產生 `globe.html`
  （電腦端讀 EXIF 不受此限制），再同步到手機看。
- 或改走原生 App（需雲端 build + 開發者帳號），用 PhotoKit 直接拿座標，不受此限。

---

## 小提醒
- 函式庫（Three.js / Globe.gl / exifr）走 CDN，使用時需要網路。
- 地球貼圖 `earth-8k.jpg`（8192×4096, 2.3MB）隨 repo 一起提供，首次載入後會被瀏覽器快取。
- 一次選太多張（上千）會較慢且佔記憶體，建議分批。
- HEIC（iPhone 原生格式）在 iPhone Safari 可正常解碼縮圖。

## 致謝 / 授權

地球貼圖 `earth-8k.jpg` 來自 **[Solar System Scope](https://www.solarsystemscope.com/textures/)**，
授權 **[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)**，本專案已調整其亮度以符合介面色調。

地形起伏貼圖來自 [three-globe](https://github.com/vasturiano/three-globe) 範例資源。
地名反查使用 [OpenStreetMap Nominatim](https://nominatim.openstreetmap.org/)（© OpenStreetMap contributors, ODbL）。
