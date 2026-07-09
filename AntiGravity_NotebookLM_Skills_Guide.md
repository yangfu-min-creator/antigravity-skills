# Anti-Gravity 懶人包：NotebookLM 連接與自動化文件生成設定

> 版本：v2.1 (精簡優化版)
> 更新日期：2026-07-09
> 語系偏好：繁體中文（Taiwan）

這份懶人包的目標，是讓 Anti-Gravity 使用者能安全連接 NotebookLM，並建立自動化生成專業 Word 規格書與 Excel 數據報表的能力。

本文件只放可公開教學的設定流程，不放任何個人 NotebookLM 清單、筆記本 ID、研究報告、生成圖片、帳號 token 或測試專案。

---

## 先備條件

- [ ] 已安裝 Anti-Gravity 或可使用 MCP 的 AI 編碼助理
- [ ] 已安裝 Git 與 GitHub CLI（`gh`）
- [ ] 已安裝 Python 或 `uv`（用於運行 NotebookLM MCP 與 Python 文件生成套件）
- [ ] 已安裝 Node.js / npm（若使用 Node-based 轉換工具）
- [ ] 有 Google 帳號，可登入 NotebookLM

Windows 快速檢查：
```powershell
git --version
python --version
pip --version
一、連接 NotebookLM重點原則NotebookLM 登入應走瀏覽器 OAuth 授權。不要複製 cookie、token，也不要把 NotebookLM 匯出的 notebooks.json 或筆記本 ID 清單放進公開 repo。安裝 NotebookLM MCP CLI建議優先用 uv 安裝：PowerShelluv tool install notebooklm-mcp-cli
nlm --version
如果沒有 uv，再用 pip：PowerShellpip install notebooklm-mcp-cli
nlm --version
重新登入 Google 帳號若曾經登入錯帳號，先登出再重新 OAuth：PowerShellnlm logout
nlm login
nlm login 會開啟瀏覽器，請在瀏覽器選擇正確的 Google 帳號完成授權。驗證：PowerShell$env:PYTHONIOENCODING = "utf-8"  # 防止 Windows 環境編碼錯誤
nlm doctor
nlm list
註冊 MCP不要直接套用 OpenCode 的 opencode.json，請依 Anti-Gravity 實際產品 UI 或設定檔路徑進行通用註冊：JSON{
  "mcp": {
    "notebooklm": {
      "type": "local",
      "command": ["nlm", "mcp"],
      "enabled": true
    }
  }
}
二、Word 與 Excel 檔案自動化生成規範當使用者要求生成報告（Word）或數據清單（Excel）時，AI 應具備自動調用環境中的 Python 套件（如 python-docx、openpyxl）或透過特定指令直接產出實體檔案的能力。1. Excel (.xlsx) 生成規範結構化矩陣：所有生成的 Excel 必須包含明確的標題列（Header）、資料列與邊框，禁止產出無排版的裸文字。視覺美化：標題列一律使用深藍色系（如 #1F497D）填充並搭配白色粗體字；資料列採用灰白相間（Zebra Stripes）提升閱讀性。程式執行範例（AI 於背景或透過 Terminal 執行）：Pythonimport openpyxl
from openpyxl.styles import Font, PatternFill
wb = openpyxl.Workbook()
ws = wb.active
ws.title = "NotebookLM 知識庫矩陣"
# 寫入數據與套用樣式...
wb.save("NotebookLM_Data_Matrix.xlsx")
2. Word (.docx) 生成規範嚴格排版：產出的文件必須具備清晰的階層（標題 1、標題 2、內文），內文一律採用「左右對齊」，重要步驟使用 Code Block 或 Callout 區塊框起。內容範疇：主要用於輸出從 NotebookLM 萃取出的深度分析報告、系統規格書或操作指南。建議的 ANTIGRAVITY.md 範本Markdown# <專案名稱> - ANTIGRAVITY.md

## 專案入口
專案名稱：
主要工作目錄：
Outputs 目錄：./outputs/  (所有生成的 Word/Excel 均存放於此)

## 工作規則
- 回應使用繁體中文。
- 涉及檔案操作時回報完整產出位置。
- 固定經由 NotebookLM MCP 同步外部知識庫。
- 任務結束時，若涉及複雜數據或長文本，必須主動詢問使用者是否自動生成對應的 Excel 矩陣或 Word 規格書。

## 不要做
- 不要 commit API key、token、密碼。
- 不要 commit NotebookLM 個人匯出清單或筆記本 ID 清單。
- 產出 Excel 時，禁止出現欄寬不足導致文字被遮擋（###）的情況。
完成回報格式Markdown## Anti-Gravity 懶人包設定完成

- NotebookLM：已登入 / 待 OAuth / 失敗
- Word/Excel 生成環境：Python 套件已就緒 / 缺套件 / 未測試
- 規則檔：ANTIGRAVITY.md 已建立 / 已更新
- 下一步：
常見問題問題解法NotebookLM 登入到錯帳號nlm logout 後重新 nlm loginWindows 顯示編碼錯誤設定 $env:PYTHONIOENCODING = "utf-8" 後重試生成的 Excel 打開格式混亂確保程式中有調用 openpyxl 的 Alignment 與 PatternFill 進行美化AI 無法直接生成 Word 檔案檢查環境中是否遺漏 pip install python-docx更新紀錄日期版本更新內容2026-07-09v2.1移除「開工/收工/新專案初始化」章節，使文件核心更聚焦於 NotebookLM 整合與文件自動化生成機制。