# 年糕的狗齡換算器｜比熊犬

一個一頁式、行動優先的狗齡換算器，依公式將狗的實際年齡換算為對應的人類年齡。支援 iOS/Android「加入主畫面」，自動套用網頁圖示。

> 公式：人類年齡 = 16 × ln(狗的年齡) + 31（自然對數）  
> 日期以使用者本地時區的「今天」為基準，並以回歸年 365.2425 計算年數。

## Demo（App Icon 預覽）

- iOS  
  ![Demo on iOS](./Demo%20on%20iOS.jpeg)

- Android  
  ![Demo on Android](./Demo%20on%20Android.jpeg)

## 線上預覽

直接開啟 `index.html` 即可離線執行。若部署到靜態主機（如 GitHub Pages、Netlify、Vercel）同樣可用。

## 功能特色

- 即時計算：輸入出生日期後，按「立即計算」即顯示狗齡與對應人類年齡  
- 自動日期基準：顯示今天日期（本地時區）  
- 輸入驗證：阻擋未來/當天或格式錯誤的日期，顯示明確錯誤訊息  
- 本地儲存：自動保存狗名、犬種、出生日期，下次回訪自動帶入  
- 可安裝體驗：提供 favicon 與 Apple Touch Icon，加入主畫面時顯示自訂圖示  
- RWD：手機優先，含面板浮層與背景遮罩，易讀性佳  
- 無依賴：純 HTML/CSS/JS，易於部署

## 專案結構

```
.
├── index.html            # 主頁面（含樣式與腳本）
├── dog.png               # 背景影像
├── icon_linko.png        # Web App Icon（favicon、Apple Touch Icon 共用）
├── README.md             # 本說明文件
├── Demo on iOS.jpeg      # iOS 加入主畫面示意（App Icon）
└── Demo on Android.jpeg  # Android 加入主畫面示意（App Icon）
```

## 快速開始（本機）

1. 直接以瀏覽器開啟 `index.html`（雙擊或拖曳到瀏覽器）  
2. 輸入狗狗的出生日期，點擊「立即計算」  
3. 可修改「狗狗名字」「犬種」，標題與徽章即時更新  
4. 再次開啟頁面時會自動帶入上次設定

> 提示：若使用 VS Code，可裝 Live Server 外掛並「Open with Live Server」，自動重新整理。

## 部署（靜態主機）

- GitHub Pages  
  1) 將專案推送到 GitHub  
  2) 設定 Pages 來源為 main 分支（root）  
  3) 以 `https://<帳號>.github.io/<repo>/` 造訪

- Netlify／Vercel  
  - 連接此儲存庫，部署後以預設網域存取

## 技術說明

- 頁面語系：`lang="zh-Hant"`  
- 圖示設定（head）

  ```html
  <link rel="icon" type="image/png" href="./icon_linko.png">
  <link rel="apple-touch-icon" href="./icon_linko.png">
  <link rel="apple-touch-icon" sizes="180x180" href="./icon_linko.png">
  ```

- 日期差計算：以 UTC 零點比較，避免夏令時誤差

  ```js
  const utcA = Date.UTC(a.getFullYear(), a.getMonth(), a.getDate());
  const utcB = Date.UTC(b.getFullYear(), b.getMonth(), b.getDate());
  const days = Math.round((utcB - utcA) / (1000 * 60 * 60 * 24));
  ```

- 年齡換算：  
  - 狗齡（年） = 天數差 ÷ 365.2425  
  - 人類年齡 = 16 × ln(狗齡) + 31

- 可及性：  
  - 主要面板 `aria-live="polite"`，錯誤訊息以 `role="alert"` 顯示  
  - 可鍵盤聚焦，提高透明度易讀

## 瀏覽器支援

- 現代桌面與行動瀏覽器（Chrome, Safari, Firefox, Edge 最新版）  
- 不需額外 Polyfill

## 授權

- 若未另行聲明，以本儲存庫 LICENSE 為準。若無 LICENSE，預設著作權所有，請在再利用前洽作者。