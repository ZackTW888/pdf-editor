# 秉軒老師的 PDF 工具箱

靜態網站（單一 `index.html`），共 34 個工具。除了「AI 智慧工具」之外，所有處理都在使用者的瀏覽器內完成，檔案不會上傳。

## 工具

| 分類 | 工具 |
|---|---|
| 整理 PDF | 合併、分割、刪除頁面、擷取頁面、整理頁面、掃描成 PDF（相機／照片） |
| 優化 PDF | 壓縮、修復 PDF、OCR 文字辨識 |
| 轉成 PDF | 圖片、Word、PowerPoint、Excel、HTML 轉 PDF |
| 從 PDF 轉出 | PDF 轉圖片、Word、PowerPoint、Excel、PDF/A、純文字 |
| 編輯 PDF | 旋轉、頁碼、浮水印、裁切、編輯 PDF（文字／圖形／手繪／圖片）、填寫表單 |
| 安全與簽署 | 解除密碼、加密保護、簽名、塗黑遮蔽、比較 PDF |
| AI 智慧工具 | AI 摘要、AI 翻譯、PDF 轉 Markdown |

函式庫：
- 啟動時由 cdnjs 載入：pdf-lib 1.17.1、pdf.js 3.11.174、JSZip 3.10.1。
- 用到時才由 jsDelivr 載入：tesseract.js（OCR）、qpdf-wasm（加密／解密／修復）、mammoth（Word）、SheetJS（Excel）、html2canvas、PptxGenJS。

## AI 功能設定（選用）

「AI 摘要」和「AI 翻譯」會把 PDF 的文字送到 `api/ai.js`（Vercel Serverless Function），再由它呼叫 Claude API。

在 Vercel 專案的 Settings → Environment Variables 加入：

| 變數 | 說明 |
|---|---|
| `ANTHROPIC_API_KEY` | 必填，Claude API 金鑰 |
| `AI_MODEL` | 選填，預設 `claude-opus-5-5` |
| `AI_ALLOWED_ORIGINS` | 選填，允許呼叫的網域（逗號分隔），預設只允許同網域 |

沒有設定金鑰時，網站會改用 Chrome 內建的 AI（Translator／Summarizer API），只在支援的 Chrome 版本可用。

「PDF 轉 Markdown」不需要 AI，完全在本機處理。

## 已知限制

- Word／PPT／Excel／HTML 轉 PDF 預設產生圖片式 PDF（文字不可選取）。要可選取的文字，可以改用「列印」模式，透過瀏覽器另存 PDF。
- PowerPoint 的圖表與 SmartArt 不會被轉出。
- 舊版 .doc／.ppt 不支援，請先另存為 .docx／.pptx（Excel 支援 .xlsx、.xls、.csv、.ods）。
- 簽名是視覺簽名（圖片），不是數位憑證簽章。
- PDF/A 輸出符合 PDF/A-2b 的結構要求，但沒有用 veraPDF 驗證過。
- OCR 品質取決於掃描清晰度。
- 塗黑遮蔽會把受影響的頁面轉成圖片，以確保底下文字被真正移除。

## 部署（GitHub ＋ Vercel）

1. Vercel → Add New → Project，匯入這個 repo。
2. Framework Preset 選 **Other**，Build Command 與 Output Directory 留空。
3. （選用）加入上面的 AI 環境變數。
4. 按 Deploy。之後推到 `main` 會自動重新部署，其他分支會產生預覽網址。

## 本機預覽

```bash
python3 -m http.server 8000
```

本機預覽時 AI 端點不存在，AI 工具會改用 Chrome 內建 AI。要在本機測試 AI 端點，請用 `vercel dev`。
