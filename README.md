# 獵魔女團：環境淨化戰

一款以「環境教育題庫」為核心的網頁答題遊戲。玩家選擇角色後，在限時挑戰中回答環境知識題目，累積分數與連擊，適合用於課堂活動、校園環境教育競賽或自主練習。

## 目前穩定版

**v16：GitHub CSV 自動載入版**

本版已移除 Google Apps Script / GAS 依賴，改由主程式直接讀取 GitHub Pages 同層的 `questions.csv` 題庫檔案。

```text
index.html
questions.csv
```

只要兩個檔案放在同一層，開啟網頁後就會自動載入題庫。

## 專案特色

- 開啟網頁後自動載入 `questions.csv`
- 不需要 Google Apps Script
- 不需要 API 授權
- 不會跳 Google 權限請求
- 支援 5 分鐘、30 分鐘、1 小時遊戲時間
- 支援大量題庫，目前 v1 題庫約 5688 題
- 題目答完後會重新洗牌，時間內可持續作答
- 保留角色選擇、分數、連擊、排行榜與遊戲視覺效果
- 題庫讀取失敗時，會保留內建備援題庫

## 檔案結構

```text
/
├─ index.html        # 遊戲主程式
├─ questions.csv     # 題庫檔案，必須與 index.html 同一層
├─ README.md         # 專案說明
└─ CHANGELOG.md      # 版本歷程
```

## GitHub Pages 部署方式

1. 建立或進入 GitHub Repository。
2. 上傳 `index.html` 與 `questions.csv`。
3. 確認兩個檔案在同一層，不要放進不同資料夾。
4. 到 Repository 的 `Settings`。
5. 進入 `Pages`。
6. Source 選擇主要分支，例如 `main`。
7. Folder 選擇 `/root`。
8. 儲存後等待 GitHub Pages 產生網址。
9. 用無痕視窗開啟網址測試。

## 題庫格式

`questions.csv` 第一列必須是欄位名稱：

```csv
級別,題目,選項1,選項2,選項3,選項4,答案,解析
```

範例：

```csv
初級,資源回收的 3R 中，Reduce 是什麼意思？,減少使用,重複使用,回收利用,隨便丟棄,1,Reduce 是減少使用。
```

## 欄位說明

| 欄位 | 說明 |
|---|---|
| 級別 | 題目難度或關卡分類 |
| 題目 | 題目文字 |
| 選項1 | 第一個選項 |
| 選項2 | 第二個選項 |
| 選項3 | 第三個選項 |
| 選項4 | 第四個選項 |
| 答案 | 正確答案，可填 `1`、`2`、`3`、`4`，也可填 `A`、`B`、`C`、`D` |
| 解析 | 答案說明，目前主要供題庫保存與後續功能擴充 |

## 題目級別建議

可依遊戲關卡使用以下名稱：

| 遊戲關卡 | 題庫級別 |
|---|---|
| 惡魔來襲 | 初級 |
| 魂潮入侵 | 中級 |
| 惡魔攻襲 | 高級 |
| 惡魔將強襲 | 中高級 |

## 更新題庫方式

只需要更新 GitHub 上的：

```text
questions.csv
```

不需要修改 `index.html`。

建議流程：

1. 在 Excel 或 Google 試算表整理題庫。
2. 匯出為 CSV。
3. 檔名改成 `questions.csv`。
4. 上傳覆蓋 GitHub Repository 中的舊檔。
5. 等待 GitHub Pages 更新。
6. 用無痕視窗重新整理測試。

## 常見問題

### 1. 為什麼直接雙擊 index.html 可能不能讀題庫？

部分瀏覽器會擋本機檔案的 `fetch()` 讀取。請以上傳到 GitHub Pages 後測試為準。

### 2. 為什麼 GitHub 更新後網頁還是舊題庫？

可能是瀏覽器快取或 GitHub Pages 還沒更新。建議：

- 用無痕視窗測試
- 按 `Ctrl + F5` 強制重新整理
- 等待 1 到 5 分鐘後再測

### 3. 題庫讀不到怎麼辦？

請檢查：

- `questions.csv` 是否與 `index.html` 同一層
- 檔名是否完全正確，包含小寫與複數 `questions.csv`
- CSV 第一列欄位是否正確
- 答案欄是否填 `1~4` 或 `A~D`

### 4. 還需要 Apps Script 嗎？

不需要。v16 已改為 GitHub CSV 直讀版。

## 建議維護原則

- 穩定版固定使用 `index.html` + `questions.csv`
- 題庫更新只動 `questions.csv`
- 若要新增功能，先另存新版，例如 `aiv17_xxx.html`
- 不要同時混用 GAS、Google Sheet API 與 GitHub CSV，以免除錯複雜化

## 授權與使用

本專案主要供教學、課堂活動與環境教育推廣使用。若公開分享，建議註明題庫來源與維護者。
