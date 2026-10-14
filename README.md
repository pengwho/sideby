# 塞唄 Sideby

先塞塞看，再下單。網址：https://pengwho.com/sideby/

看收納盒放進 IKEA BILLY、KALLAX 等櫃子時，每層怎麼擺、能不能疊、要買幾個，並附上實拍照片與購買連結。

## 檔案結構

```
index.html     頁面與 3D 模擬（平常不用改）
catalog.json   櫃子、收納盒、推薦組合的資料（新增商品改這裡）
images/        實拍照片
.nojekyll      讓 GitHub Pages 直接發佈靜態檔案
```

## 新增一個收納盒

1. 量尺寸（單位公分，量最寬處，提把、卡扣也要算）：上緣寬深、底部寬深、盒高、蓋子寬深高。
2. 照片放進 `images/`，檔名用英文，例如 `images/tote-01.jpg`（建議寬 1200px 以內）。
3. 在 `catalog.json` 的 `boxes` 加一筆：

```json
"tote2": {
  "name": "某某整理箱 L",
  "tw": 36, "td": 25, "bw": 33, "bd": 22, "h": 13,
  "hasLid": true, "lw": 36.5, "ld": 25.5, "lh": 1.5, "lidOn": true,
  "stack": true, "nest": 0.8,
  "photos": ["images/tote-01.jpg"],
  "links": { "shopee": "https://s.shopee.tw/xxxx", "coupang": "" },
  "verified": true
}
```

| 欄位 | 意思 |
|---|---|
| tw / td | 上緣外尺寸 寬 / 深 |
| bw / bd | 底部外尺寸 寬 / 深（上寬下窄的盒子會比上緣小） |
| h | 盒身高度（不含蓋） |
| hasLid / lw / ld / lh | 有沒有蓋子、蓋子寬 / 深 / 高 |
| lidOn | 放進櫃子時是否蓋著 |
| stack / nest | 可否堆疊、疊放時底部卡進下層蓋子的深度 |
| links | 分潤連結，留空會顯示「連結待補」 |
| verified | 自己實際買來放過就填 true |

## 新增一個推薦組合

在 `combos` 加一筆，`levels` 由上往下列出每層放哪個盒子，`null` 代表放書或空著：

```json
{
  "id": "billy80-tote2",
  "title": "整理箱放滿整櫃",
  "cabinet": "billy80",
  "levels": ["tote2", "tote2", "tote2", "tote2", "tote2", "tote2"],
  "note": "一句話說明這個組合適合誰。"
}
```

層高跟預設櫃子不同時，可以加 `"hs": [26, 28, 30, 32, 34, 38]` 覆蓋。

## 先在測試模式試擺

網址後面加 `#lab` 進入測試模式，自由輸入尺寸。試好後按「複製組合資料」，把複製到的 `box` 和 `combo` 分別貼進 `catalog.json`，再補上名稱、照片和連結。

## 本機預覽

頁面用 `fetch` 讀 `catalog.json`，直接雙擊 index.html 會讀不到，請開本機伺服器：

```
python3 -m http.server 8000
```

然後打開 http://localhost:8000 。

## 發佈

改完 commit 並 push 到 `main`，GitHub Pages 約一分鐘後自動更新。
