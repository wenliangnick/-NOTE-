# AGENTS.md - 大學統計學：機率分布筆記（單頁式網站規範）

## 1. 專案目的 (Project Purpose)
本專案是一個可持續擴充的「大學統計學：機率分布筆記」單頁式（Single-Page）靜態網站，託管於 GitHub Pages。
所有總覽目錄與個別分布的完整筆記（定義、統計量、性質與推導）皆整合於同一個 `index.html` 檔案中。AI 只需根據本規範，就能持續往 `index.html` 中擴充新的機率分布卡片，並維持全站版面、配色與數學符號的高度一致。

## 2. 專案檔案結構與技術限制 (File Structure & Tech Stack)
- **檔案清單**：全專案僅維護兩個核心檔案，**嚴禁額外建立多餘的 `.html`、`.css` 或 `.js` 檔案**：
  1. `AGENTS.md`：本專案開發規範書。
  2. `index.html`：包含完整 `<style>` 樣式、`<script>` 篩選邏輯與所有分布內容的唯一網頁。
- **技術規範**：純原生 HTML5、CSS3、Vanilla JavaScript，不依賴任何前端框架（React/Vue）或打包工具。
- **數學公式渲染**：統一使用 **MathJax 3** CDN，行內公式用 `$ ... $`，獨立區塊公式用 `$$ ... $$`。
- **視覺風格**：學術極簡風（Academic Minimalism）。離散型分布使用深海藍（`#1e3a8a`），連續型分布使用森林綠（`#065f46`）。

## 3. 單一分布卡片標準結構 (Distribution Card Template)
每當在 `index.html` 的 `<main id="notes-list">` 內新增一個機率分布時，**必須使用 `<article class="dist-card" data-type="discrete|continuous">` 包裝**，且內部必須嚴格包含以下 6 個標準區塊（順序不可調動）：

1. **卡片標頭 (`<div class="card-header">`)**：
   - 分類標籤（`<span class="badge badge-discrete">離散型</span>` 或 `<span class="badge badge-continuous">連續型</span>`）
   - 中文名稱與英文名稱（`<h2>`）
   - 標準記號（例如：$X \sim \text{Bin}(n, p)$）
2. **直觀意義與應用場景**：
   - 白話說明該分布「在計算什麼」及常見統計應用情境。
3. **核心定義與函數 (`<div class="formula-box">`)**：
   - 參數空間（Parameter Space）與支撐集（Support）。
   - 機率質量函數（PMF）或機率密度函數（PDF）。
   - 累積分布函數（CDF）。
4. **核心統計量摘要表 (`<table class="stats-table">`)**：
   - 必須列出：**期望值 $E[X]$**、**變異數 $\text{Var}(X)$**、**動差母函數 (MGF) $M_X(t)$**。
5. **關鍵性質與定理**：
   - 可加性、無記憶性、或與其他分布的極限／近似關係。
6. **重點推導過程 (`<details class="derivation-box">`)**：
   - 使用 `<details>` 折疊區塊呈現至少一項核心推導（如期望值、變異數、MGF 或無記憶性證明），保持頁面版面清爽且支援點擊展開閱讀。

## 4. AI 新增與修改規則 (AI Rules)
1. **目錄同步更新**：在 `<main id="notes-list">` 新增 `<article>` 時，必須同步在頂部 `<nav class="quick-nav">` 中新增對應的錨點連結（`<a href="#dist-id">`），確保點擊目錄可直接跳轉至該分布。
2. **符號一致性**：全站統一使用 $E[X]$（期望值）、$\text{Var}(X)$（變異數）、$p_X(x)$（PMF）、$f_X(x)$（PDF）、$F_X(x)$（CDF）。
3. **資料整合原則**：當使用者提供課堂講義（如 `Statistics_I.pdf`）或 Wiki 筆記時，AI 需將內容拆解並填入上述 6 個標準區塊；若原始筆記缺少 MGF 或推導步驟，AI 應主動補齊嚴謹的數學推導。