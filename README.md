# 尋光者 · 資源下載站

IG 私訊關鍵字回覆用的免費資源下載頁（GitHub Pages 靜態站）。

## 網址

`https://<ORG名稱>.github.io/seeklight-downloads/`

PDF 直連：`https://<ORG名稱>.github.io/seeklight-downloads/files/7天內耗自救清單.pdf`

## 加新檔案

1. 把 PDF 放進 `files/`
2. 編輯 `index.html`，複製一組 `.item` 區塊改檔名／頁數／大小
3. `git add -A && git commit -m "add: 檔名" && git push`

⚠️ **已發佈的檔名不要改**——自動回覆和舊貼文都指著它。改版就覆蓋同一個檔名。

## 隱私設定（重要）

本 repo 的 commit 身分已在本機設成 `SeekLight <seeklight@users.noreply.github.com>`，
不含本名。**新 clone 到別台機器時要重設**：

```bash
git config user.name "SeekLight"
git config user.email "seeklight@users.noreply.github.com"
```

另需在 GitHub 網頁確認：Settings → Emails 勾選 "Keep my email address private"
與 "Block command line pushes that expose my email"。

## PDF 壓縮

用 qpdf 無損壓縮（字型與可點連結都保留）：

```bash
qpdf --recompress-flate --compression-level=9 --object-streams=generate in.pdf out.pdf
```

驗證（⚠️ 壓縮後物件流會被壓，直接 grep 抓不到字型，必須先解壓再驗）：

```bash
qpdf --show-npages out.pdf
qpdf --stream-data=uncompress out.pdf - | grep -ao '/FontName */[A-Za-z0-9+-]*' | sort -u
qpdf --stream-data=uncompress out.pdf - | grep -ao '/URI *([^)]*)'   # 可點連結還在嗎
```
