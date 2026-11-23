# 給協作 AI（Claude、Codex）的說明

## 網站結構
- 單一檔案 `index.html`，純 HTML／CSS／JavaScript，沒有建置步驟；推到 `main` 分支後由 GitHub Pages 自動發布。
- `.nojekyll` 讓 GitHub Pages 直接發布檔案，不要刪。
- 頁面切換用網址的 `#` 片段：`#home`、`#works`、`#work-<id>`，頁尾聯絡區是 `#contact`。
- 右上角有亮暗切換鈕，選擇記在 localStorage 的 `yy-theme`（和 `plan/` 共用，同網域）；沒選過就跟著系統。深色配色寫在 `:root[data-theme=dark]` 和 `@media (prefers-color-scheme:dark)` 兩處，要一起改。
- 頁尾有「網站更新」日期（`<time datetime="…">`），改網站內容時記得一起更新。

## 新增作品
作品資料集中在 `index.html` 裡的 `<script type="application/json" id="works-data">`，是一個陣列，一件作品一筆，新的放最前面：

```json
{
  "id": "英文小寫加連字號，不可重複",
  "title": "作品名稱",
  "cat": "教學網站｜師資培訓｜教案設計｜喜劇｜表演｜教學現場｜採訪與創作｜研究與設計",
  "date": "2026-11",
  "cover": "封面圖片路徑，沒有就留空字串",
  "summary": "一兩句說明，顯示在作品卡片上",
  "role": "羊羊負責的部分",
  "for": "對象或合作單位",
  "body": [["h", "小標題"], ["p", "段落"], ["ul", ["條列一", "條列二"]]],
  "link": {"text": "連結文字", "url": "https://..."}
}
```

- `cat` 使用既有分類。新增分類時也加進 `const CAT` 陣列，這裡決定篩選按鈕的順序。
- 有封面時，以 `coverInfo` 物件記錄 `alt`、`caption`、`width`、`height`。段落中可放 `["photo", {"src":"images/…","alt":"…","caption":"…","width":1200,"height":800}]`。
- YouTube 影片使用 `video` 物件，填入原頻道的影片 `id`、`title`、`caption`，需要指定起點可加秒數 `start`。內文也支援 `["video", {…}]`。播放器按下播放後才載入，另有原站觀看連結。
- 沒有外部連結時 `link` 寫 `null`。
- 圖片放在 `images/` 資料夾，用相對路徑引用（例如 `images/chem-site.jpg`），先壓到寬 1600px 以內。

## 人生計劃 `plan/`
- `plan/index.html` 是羊羊私人用的專案推進板，同樣是單一檔案、沒有建置步驟。資料結構與注意事項寫在檔案開頭的註解。
- 這個檔案是公開的：不要把任何私人專案、待辦、回顧內容寫進程式碼，預設資料只能放通用的新手範例。
- 使用者的資料存在瀏覽器 localStorage（鍵 `yy-lifeplan-v1`），選用的同步存在使用者自己帳號的秘密 Gist；改資料格式時要讓舊資料還能讀（`normalize()`）。
- 作品集首頁不要連到 `plan/`。

## 內容原則
- 只放羊羊確認可以公開的作品與文字；不確定的先問。
- 不放 Email、電話等私人聯絡方式，除非羊羊指定公開用的聯絡方式。2026-11-23 羊羊指定公開：姓名、Email、手機、LINE ID，放在頁尾聯絡區；其他私人資料仍不放。
- 不放可辨識學生正臉的照片，除非已取得同意。
- 改完在手機寬度（390px）和筆電寬度（1366px）各看一次，確認沒有水平捲軸、主控台沒有錯誤。
