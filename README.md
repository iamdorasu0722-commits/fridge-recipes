# 🍳 冰箱食譜

輸入手邊的食材，馬上找到能做的家常料理。純靜態網站（HTML／CSS／JavaScript），不需要後端，也不需要建置步驟。

## 專案結構

```
fridge-recipes/
├── index.html        頁面結構
├── assets/
│   ├── style.css     樣式（含深色模式）
│   └── app.js        食譜資料與配對邏輯
├── _headers          Cloudflare 快取與安全標頭
├── .gitignore
└── README.md
```

## 本機預覽

直接用瀏覽器開啟 `index.html`，或在資料夾內執行：

```bash
python3 -m http.server 8000
```

然後開啟 http://localhost:8000

## 上傳到 GitHub

```bash
cd fridge-recipes
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/<你的帳號>/fridge-recipes.git
git push -u origin main
```

（需先在 GitHub 建立同名的空白儲存庫，不要勾選 README。）

## 部署到 Cloudflare Pages

1. Cloudflare 後台 → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**。
2. 選擇 `fridge-recipes` 儲存庫。
3. 建置設定：
   - Framework preset：**None**
   - Build command：**留空**
   - Build output directory：**`/`**（或留空）
4. 按 **Save and Deploy**。之後每次 push 到 `main` 都會自動重新部署。

## 新增食譜

編輯 `assets/app.js` 最上方的 `R` 陣列，照現有格式加一筆：

```js
{n:"料理名稱", e:"🍳", t:15, d:"簡單",
 i:[["主要食材","份量"]],   // 必備食材（用來配對）
 o:[["選用食材","份量"]],   // 可省略的食材
 s:["步驟一","步驟二"],
 tip:"小撇步"}
```

食材名稱要與 `Q`（常見食材清單）一致；別名（例如「蕃茄」→「番茄」）加在 `AL` 物件裡。

## 備註

- 已選食材存在瀏覽器的 localStorage，只在使用者自己的裝置上。
- 預設家裡都有鹽、油、醬油、糖、胡椒，不計入缺少的食材。
- 字型使用 Google Fonts 的 Noto Sans TC；離線時會改用系統字型。
