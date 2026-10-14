# 塞唄 Sideby

先塞塞看，再下單。網址：https://pengwho.com/sideby/

看收納盒放進 IKEA BILLY、KALLAX 等櫃子時，每層怎麼擺、能不能疊、要買幾個，並附上實拍照片、影片與購買連結。

## 新增商品（在網站上直接做，不用改程式）

1. 打開 https://pengwho.com/sideby/#lab （手機、電腦都可以）。
2. 第一次使用時，在「發佈到網站」填 GitHub 金鑰，勾「記在這台裝置上」。
3. **新增收納盒**：在「收納盒」欄位填尺寸，3D 會即時顯示擺法。確認後往下到「發佈到網站」：
   - 「要儲存的盒子」選「新增一個盒子」
   - 貼上蝦皮分潤連結，選擇照片或短影片，或貼 YouTube 連結
   - 按「儲存盒子」
4. **新增推薦組合**：在「推薦組合」選櫃子，每一層選要放的盒子（或放書／空著），可以先按「在 3D 預覽」，再按「儲存組合」。
5. 大約 1 分鐘後網站就會更新。

要補連結或照片時，在「要儲存的盒子」選既有的盒子，資料會自動帶入，改完再按一次儲存。

### 照片與影片

- 照片會自動縮到最長邊 1600px 再上傳，手機直接拍的照片就能用。
- 短影片上限 25 MB，存在 repo 的 `media/` 資料夾。
- **影片建議放 YouTube（特別是 Shorts）再貼連結**：不佔 repo 空間、所有手機都能播，而且 YouTube 和蝦皮有合作的購物聯盟計畫，同一支影片在 YouTube 上也能賺分潤。
- iPhone 拍的 `.mov` 在部分 Android 手機上播不出來，這也是建議放 YouTube 的原因。

### 建立 GitHub 金鑰（只要做一次）

1. 打開 https://github.com/settings/personal-access-tokens/new
2. Token name 填 `sideby`，Expiration 選一年。
3. Repository access 選 **Only select repositories**，只勾 `pengwho/sideby`。
4. Permissions → Repository permissions → **Contents** 設成 **Read and write**。
5. 按 Generate token，複製 `github_pat_` 開頭的字串，貼到網站的金鑰欄位。

這個金鑰只能改 sideby 這個 repo，而且只存在你自己的瀏覽器裡，不會被上傳。萬一外流，到 GitHub 設定頁刪掉重建即可。

## 檔案結構

```
index.html     頁面、3D 模擬、測試模式與發佈功能
catalog.json   櫃子、收納盒、推薦組合的資料（網站的發佈功能會自動更新）
media/         上傳的照片與影片
```

## catalog.json 欄位（需要手動修改時參考）

收納盒 `boxes`：

| 欄位 | 意思 |
|---|---|
| tw / td | 上緣外尺寸 寬 / 深 |
| bw / bd | 底部外尺寸 寬 / 深（上寬下窄的盒子會比上緣小） |
| h | 盒身高度（不含蓋） |
| hasLid / lw / ld / lh | 有沒有蓋子、蓋子寬 / 深 / 高 |
| lidOn | 放進櫃子時是否蓋著 |
| stack / nest | 可否堆疊、疊放時底部卡進下層蓋子的深度 |
| links | `shopee`、`coupang` 分潤連結，留空會顯示「連結待補」 |
| media | `{"type":"image","src":"media/x.jpg"}`、`{"type":"video","src":"media/x.mp4"}`、`{"type":"youtube","id":"影片ID"}` |
| verified | 自己實際買來放過就填 true |

推薦組合 `combos`：`levels` 由上往下列出每層放哪個盒子 id，`null` 代表放書或空著；`media` 放這組的實拍照片或影片。

## 本機預覽

```
python3 -m http.server 8000
```

打開 http://localhost:8000 。
