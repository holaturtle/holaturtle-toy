# 版本歷程

## v16.0.0 - GitHub CSV 自動載入版

**狀態：目前穩定版**

### 新增

- 開啟網頁後自動讀取同層 `questions.csv`。
- 題庫載入期間，開始按鈕會顯示「題庫載入中」。
- 題庫成功載入後，才允許玩家開始任務。
- 後台題庫路徑預設為 `questions.csv`。

### 調整

- 主資料來源改為 GitHub Pages 同層 CSV。
- 保留內建備援題庫，避免題庫讀取失敗時整個遊戲中斷。
- 保留 v9 既有遊戲功能，例如角色選擇、限時挑戰、分數、連擊、排行榜視覺與手動 CSV 上傳。

### 移除 / 停用

- 不再依賴 Google Apps Script。
- 不再使用 GAS JSONP。
- 不再自動呼叫 Google Sheet 備援。
- 不再出現 Google 權限請求。

---

## v15.0.0 - GitHub CSV 無 GAS 版

### 新增

- 將題庫來源改為 `questions.csv`。
- 支援 GitHub Pages 直接讀取 CSV。
- 提供 `index.html` + `questions.csv` 的部署結構。

### 調整

- 後台「從 Google 表單載入題庫」改為「從 GitHub 題庫載入」。
- 題庫欄位統一為：

```csv
級別,題目,選項1,選項2,選項3,選項4,答案,解析
```

### 解決

- 避免 GAS 授權錯誤。
- 避免 Apps Script 部署權限問題。
- 避免 JSONP failed 導致遊戲題庫無法載入。

---

## v1 題庫 - questions.csv

### 新增

- 將 `ghost_hunter_library.csv` 轉換為遊戲可讀的 v1 題庫格式。
- 輸出檔名：`questions.csv`。
- 另輸出相容檔名：`question.csv`。

### 題庫資訊

- 欄位：`級別, 題目, 選項1, 選項2, 選項3, 選項4, 答案, 解析`
- 有效題數：約 5688 題
- 編碼：UTF-8 BOM
- 答案格式：支援 `1~4` 或 `A~D`

---

## v14.0.0 - API 單次請求防權限跳窗版

### 調整

- 開頁只請求原本 Apps Script API 一次。
- 避免開頁自動載入與按 START 時重複打 API。
- 停用 Google Sheets GViz 自動備援讀取。

### 解決

- 降低重複請求 API 的機率。
- 降低 Google 權限請求跳出的機率。

### 限制

- 若 Apps Script Web App 部署權限設定錯誤，仍可能無法正常讀取題庫。

---

## v13.0.0 - API 預設自動載入版

### 新增

- 開啟網頁後預設嘗試載入 Apps Script API 題庫。
- 若 API 失敗，嘗試使用 Google Sheets GViz 備援讀取。

### 問題

- 在部分環境中，GViz 或 Apps Script 可能觸發 Google 權限請求。
- 若 Apps Script 部署權限不正確，前端會出現 `GAS JSONP failed`。

---

## v12.0.0 - API fallback 無彈窗版

### 新增

- 加入 Apps Script API 讀取題庫。
- 加入 JSONP 讀取邏輯。
- 加入 Google Sheets GViz 備援讀取。
- API 失敗時保留目前題庫，不再跳錯誤提示。

### 已知問題

- 如果 Apps Script 權限或部署設定不正確，仍會讀取失敗。
- 若瀏覽器或 Google 權限流程介入，可能造成使用者端困惑。

---

## v9 - 遊戲功能保留基礎版

### 已知保留功能

- 角色選擇
- 玩家代號輸入
- 限時答題
- 分數與連擊
- 排行榜畫面
- 手動 CSV 上傳
- AI 出題區塊
- 視覺特效與舞台背景

### 備註

v9 的完整修改細節目前資料不足，無法確認；後續版本皆以「保留 v9 功能」為主要原則進行調整。

---

## v8 - Time Attack 版

### 已知功能

- 遊戲標題顯示為 Time Attack 版本。
- 具備限時答題模式。
- 題目會在時間內持續出現。

### 備註

v8 的完整修改細節目前資料不足，無法確認。

---

# 維護策略

目前建議固定使用：

```text
v16.0.0
index.html
questions.csv
```

後續如果要新增功能，建議從 v16 分支另存：

```text
aiv17_功能名稱.html
```

避免再回到 GAS / Apps Script 授權流程，除非確定需要雲端即時同步。
