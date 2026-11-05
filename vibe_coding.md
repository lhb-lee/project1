# 期中考vibe coding 說明

> 專案實例：逢甲大學大二影展專題介紹《新中城，城中心》乙七 —— 翻轉臺中東協廣場刻板印象
> 作者：李弘博 ｜ 更新日期：2026 年 11 月 05 日

本專案展示如何運用 Vibe Coding（直覺式語意開發）指令，引導 AI 產出符合業界標準的前端程式碼。透過清楚定義「架構、視覺風格、功能限制」，一次達成完整 SEO 優化、CSS Grid 網格系統排版，以及 RWD 響應式設計（手持裝置完整顯示資訊）。

## 核心 Vibe Coding 指令模板

以下是開發本專案時使用的核心 Prompt 指令結構，可直接複製並替換專案主題：

```text
【角色與任務】
請扮演資深前端工程師，幫我製作專題介紹網頁「《新中城，城中心》影展企劃書：乙七」。

【視覺氛圍 (Vibe)】
- 配色採用東協旗幟核心色：皇家藍 (#0033A0)、東協紅 (#EE1C25)、稻穗黃 (#FFD100)。
- 導覽列採用膠囊狀圓角按鈕 (border-radius: 999px)，具備 Hover 變色效果。

【必備技術規格】
1. 完整 SEO 與語意化架構：
   - <head> 包含完整 meta description、robots 與 Open Graph (og:title, og:description, og:type, og:locale) 標籤。
   - 使用 HTML5 語意化標籤：<header>, <nav>, <main>, <article>, <section>, <aside>, <figure>, <footer>。
   - 加入 aria-label 與表格 scope 屬性，提升無障礙體驗與搜尋引擎理解度。

2. Grid System 網格系統與版面配置：
   - 全域設定 box-sizing: border-box，主容器最大寬度 980px 置中。
   - 重點區塊（如 .tips-grid）使用 CSS Grid 進行多欄排版，讓資訊模組化呈現。

3. RWD 響應式功能（手持裝置顯示完整資訊）：
   - 設定 @media (max-width: 600px) 手機版斷點。
   - Grid 網格在手機端自動轉為單欄 (grid-template-columns: 1fr)。
   - 表格 (<table>) 與長網址 (<a>) 加上 overflow-wrap: anywhere，確保手機螢幕不破版、不產生水平捲軸。
   - 圖片與嵌入影片/地圖設為 max-width: 100%，影片維持 aspect-ratio: 16 / 9 等比例縮放。
```

---

## 三大核心技術實作重點

### 1. 完整 SEO 與語意化標籤 (`project12.html`)

在指令中明確要求 Meta 協定、Open Graph 與 HTML5 語意標籤，確保網頁在搜尋引擎與社群分享時有最佳表現：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="逢甲大學大二影展專題介紹 乙七：翻轉東協廣場刻板印象">
    <meta name="robots" content="index, follow">
    <meta property="og:type" content="article">
    <meta property="og:locale" content="zh_TW">
    <meta property="og:title" content="逢甲大學影展企劃書：乙七">
    <meta property="og:description" content="跨過一道門，看見一座城 —— 翻轉臺中東協廣場刻板印象">
    <title>《新中城，城中心》影展企劃書：乙七</title>
</head>
```

* 語意化結構：使用 `<main>`、`<article>`、`<section>`、`<aside>` 區分內容權重。
* 結構化表格：使用 `<caption>`、`<th scope="col/row">` 幫助爬蟲理解比較表數據。
* 圖片備援：`<figure>` 搭配描述性 `alt` 與 `onerror` 備用圖檔機制。

### 2. CSS Grid System 網格系統 (`project12.css`)

透過全域盒模型與 CSS Grid 控制版面結構，讓資訊排列整齊且易於維護：

```css
* {
    box-sizing: border-box;
}

body {
    max-width: 980px;
    margin: 0 auto;
    padding: 32px 24px;
}

/* 多欄網格配置 */
.tips-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 16px;
}
```

### 3. RWD 響應式設計：確保手持裝置顯示完整資訊 (`project12.css`)

針對手機等窄視窗裝置，透過自動斷行、等比例縮放與 Media Queries 斷點，解決表格撐破畫面或文字截斷的問題：

| 網頁元素 | 桌面版 (`> 600px`) | 手持裝置 (`<= 600px`) | 關鍵 CSS 語法 |
| :--- | :--- | :--- | :--- |
| 整體版面 (`body`) | 內距 `32px 24px`、字級 `17px` | 內距 `16px 12px`、字級 `16px` | `@media (max-width: 600px)` |
| Grid 網格區塊 | 多欄並排顯示 | 垂直單欄呈現 | `grid-template-columns: 1fr` |
| 比較表與長網址 | 寬裕內距、完整顯示 | 緊湊內距、自動換行不截斷 | `overflow-wrap: anywhere` |
| 圖片與嵌入媒體 | 原始設定尺寸 | 依螢幕寬度 100% 等比例縮放 | `max-width: 100%`、`aspect-ratio: 16 / 9` |

```css
/* 防止表格與長網址在手機上撐破版面 */
table, a {
    overflow-wrap: anywhere;
}

img, iframe {
    display: block;
    max-width: 100%;
}

/* 手機版 RWD 斷點設定 */
@media (max-width: 600px) {
    body {
        padding: 16px 12px;
        font-size: 16px;
    }

    header, section, aside {
        padding: 20px 16px;
    }

    nav {
        padding: 18px 16px;
        border-radius: 32px;
    }

    .tips-grid {
        grid-template-columns: 1fr;
    }

    th, td {
        padding: 8px;
    }
}
```

---

## 專案檔案結構

```text
ASEAN-Square-Project/
├── css/
│   └── project12.css    # 樣式表（色彩系統、Grid 網格、RWD 斷點）
├── images/
│   └── map.jpg          # 場域實景圖片
├── project12.html       # 主網頁（SEO 標籤、語意化結構）
└── README.md            # 專案與 Vibe Coding 指令說明文件
```