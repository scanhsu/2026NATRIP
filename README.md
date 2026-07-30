# SEJZ 北美壯遊 2026 · 行程 App

SEJZ 家族美加露營車畢業旅行（2026/08/01–08/18）的手機行程 App。
單一 HTML 檔、免後端、可離線使用的 PWA，成員用手機瀏覽器開啟即可查詢整趟行程。

**正式網址：<https://scanhsu.github.io/2026NATRIP/>**

## 功能

- **今日**：出發倒數／旅程中自動顯示當天行程與明日預告、台北/太平洋/山區三地時鐘、重要提醒（夢蓮湖接駁釋票、分離票、冰原大道無訊號）
- **行程**：頂部有 **RV 路線地圖**：內嵌 Leaflet + OpenStreetMap/CARTO 圖磚（免金鑰、跟隨深淺色主題），10 個過夜點可點選看細節與導航；「▲ 步道」可加開 18 個登山口圖層、「⛰ 地形圖」切換 OpenTopoMap 等高線、「📍 我在哪」顯示自身位置（旅程中並顯示距今晚營地直線距離）；可「預載地圖」離線使用；載不到圖磚時自動改用內建 SVG 示意圖；D1–D18 每日卡片（路線、里程、住宿、電力、步道、備註），每天附整排「📍 地點」Google Maps 連結與「導航到今晚住宿」，D1/D3/D14/D15/D16 含逐時行程
- **訂位**：所有訂位代號總表，可搜尋、點一下即複製，已確認／待辦狀態一目了然
- **待辦**：出發前待辦清單依優先級分組，勾選進度存在手機本機（localStorage）
- **工具**：
  - **記帳**：USD/CAD/TWD 記帳，手動匯率自動折台幣，依類別與付款人統計
  - **行事曆提醒**：釋票、球賽、取還車、趕車等 7 個關鍵時刻（以各事件當地時間顯示），一鍵加入 Google 日曆或下載 .ics（Apple/Outlook）
  - **露營車儀表**：清水/灰水/黑水/油量手動記錄，灰黑水過 75% 提示處理
  - **照片日記**：每天一張照片＋一句話（IndexedDB 本機儲存），18 天回憶牆
  - **證件保險箱**：護照/ESTA/駕照/保單照片離線存手機，過海關快速調出
  - **位置分享**：GPS 一鍵產生 Google Maps 座標連結分享，內建常用會合點
  - **待辦同步**：匯出/匯入同步碼，全家合併勾選進度（免後端）
- **更多**：洛磯山脈 24 條步道指南（可依難度篩選）、天氣穿搭、機票、露營車、訂位風險清單、**可勾選打包清單**、**大統華採買與備餐清單**（T&T Surrey 店資訊＋57 項可勾選清單、跨境生鮮限制與防熊規則）、**西雅圖彈性候補名單**、**官方資訊網站列表**（Parks Canada／路況／天氣）、緊急聯絡（可直接撥號）
- **即時天氣**：今日頁串接 Open-Meteo（免金鑰）顯示 9 個站點 3 日預報，離線時退回快取或月均值表
- **一鍵導航**：每日行程卡與今日頁提供「導航到今晚住宿」Google Maps 路線深連結
- **離線可用**：Service Worker 快取整個 App，冰原大道無訊號路段也能開
- **可加到主畫面**：附 manifest 與 icon，手機「加入主畫面」後如原生 App 般全螢幕使用
- 深淺色主題自動跟隨系統，也可手動切換

## 使用方式（給家人）

1. 手機開啟 <https://scanhsu.github.io/2026NATRIP/>
2. 加到主畫面：iPhone 用 Safari 點分享 →「加入主畫面」；Android 用 Chrome 點選單 →「安裝應用程式」
3. 首次開啟即完成離線快取，之後沒網路也能查行程
4. **出發前記得在「行程」頁按一次「⬇ 預載地圖」**，冰原大道無訊號路段才看得到地圖

### 部署

GitHub Pages 發佈來源為 **`main` 分支的 `/ (root)`**（Settings → Pages）。
推送到 `main` 後 Pages 會自動重新建置，約 1 分鐘後生效，網址不變。

改行程的流程：從 `main` 開分支 → 修改 → 開 PR → 合併回 `main` → Pages 自動更新。
記得同時更新 `sw.js` 的 `CACHE` 版本號，成員手機才會換到新版。

## 檔案結構

| 檔案 | 說明 |
|---|---|
| `index.html` | 整個 App（HTML/CSS/JS、Leaflet 1.9.4 與行程資料皆內嵌，無外部 CDN） |
| `manifest.webmanifest` | PWA 資訊（名稱、icon、主題色） |
| `sw.js` | Service Worker（離線快取；`sejz-tiles-v1` 存放預載地圖圖磚，換版不清除） |
| `icon-192.png` / `icon-512.png` | App icon |

## 更新行程資料

行程內容內嵌在 `index.html` 的 `<script>` 區塊，依序為 `DAYS`（每日行程）、`TIMELINES`（逐時細部）、`BOOKINGS`（訂位）、`TODOS`（待辦）、`TRAILS` / `TRAILTIPS`（步道）、`WEATHER`、`PACKING`、`RISKS`、`FLIGHT`、`RV`，以及 `GEO`（天氣站點）、`STAYNAV`（導航目的地）、`CALEV`（行事曆事件，時間為 UTC）。改完後更新 `sw.js` 內 `CACHE` 版本號（如 `sejz-natrip-v2`）讓成員手機自動換新版。

## 資料版本

目前對應「定案版每日行程表」**第 10 版**（2026/07/30a）。

- **第 10 版**：加入洗衣計畫——D5 Parks Canada 營地無洗衣設施警示、D6 洗衣①（Jasper Coin Clean）、D10 洗衣②（Banff Cascade Coin，全程最佳窗口）、D12 Revelstoke 備援、D15 民宿收尾；待辦插入 4 項（確認民宿洗衣機、洗衣硬幣 CAD 60、洗衣片自備、防水臟衣袋＋速乾衣）。
- **第 9 版**：D1 加入派克市場美食巡禮（The Crumpet Shop／初代星巴克 1912 Pike Place／Beecher's／Hellenika，備選 Cafe Hagen；Starbucks Reserve Roastery 移入西雅圖彈性候補）；D4 採買地點由 Walmart/Costco 改為大統華 T&T Surrey；新增「西雅圖彈性候補」（Ooink／Hot Cakes／Dué Cucina）；記帳新增「哥哥」付款人以配合 CAD$150 財務長任務。
- **第 8 版**：住宿全確認——EVEN Hotels（D1-2）、Hotel Belmont（D3）、民宿 Mount Pleasant（D14-15）；D4 Kamloops 改 Costco／Silver Sage 二選一；D7 營地改 Waterfowl／Icefields Ctr 彈性；D12 改 Golden Skybridge 09:00 早鳥（07:00 拔營）；D16 不住宿；D15 補本拿比 Wong 家聯絡資料。
- **第 7 版**：D1 寬鬆版時間軸、D2 上午改西雅圖水族館、D16 飛行博物館移入（保留 05:45 叫車 + 入境預檢）。

D3、D14、D15 依使用者指示**維持原版行程**：D3 早班巴士 13:00 出發 + FlyOver Canada + 煤氣鎮蒸氣鐘、D14 史丹利公園海堤單車 + Yaletown 晚餐、D15 固蘭湖島 + 本拿比朋友聚會。

## 地圖

地圖用 [Leaflet](https://leafletjs.com/)（BSD-2-Clause，已內嵌）搭配 [CARTO](https://carto.com/attributions) 的 OpenStreetMap 圖磚與 [OpenTopoMap](https://opentopomap.org) 地形圖，全部免費且不需 API 金鑰。圖磚在執行時載入，因此需網路；按「預載地圖」可把路線範圍 zoom 5–9 的圖磚（約 190 塊）存進 Cache Storage，冰原大道無訊號時仍可瀏覽。圖磚載入失敗時會自動改用內建的 SVG 路線示意圖，離線也不會空白。
