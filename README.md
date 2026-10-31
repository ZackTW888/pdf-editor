# 秉軒老師的 PDF 工具箱

純靜態網站（單一 `index.html`），所有 PDF 處理都在使用者的瀏覽器內完成，不需要後端。

工具：合併、分割、刪除頁面、擷取頁面、整理頁面、旋轉、壓縮、圖片轉 PDF、PDF 轉圖片、PDF 轉文字、加入浮水印、加入頁碼。

函式庫由 cdnjs 載入：pdf-lib 1.17.1、pdf.js 3.11.174、JSZip 3.10.1。

## 部署（GitHub ＋ Vercel）

1. Vercel → Add New → Project，匯入這個 repo。
2. Framework Preset 選 **Other**，Build Command 與 Output Directory 留空。
3. 按 Deploy。之後推到 `main` 會自動重新部署，其他分支會產生預覽網址。

## 本機預覽

```bash
python3 -m http.server 8000
```
