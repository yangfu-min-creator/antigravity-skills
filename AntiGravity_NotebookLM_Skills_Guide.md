# Anti-Gravity 懶人包：NotebookLM 連接與自動化文件生成設定

> 版本：v2.1
> 更新日期：2026-07-09

這份懶人包的目標，是讓使用者能安全連接 NotebookLM，並建立自動化生成專業 Word 規格書與 Excel 數據報表的能力。

---

## 一、連接 NotebookLM

### 1. 安裝 NotebookLM MCP CLI
建議優先用 uv 安裝：
uv tool install notebooklm-mcp-cli

如果沒有 uv，再用 pip：
pip install notebooklm-mcp-cli

### 2. 登入 Google 帳號
nlm logout
nlm login

### 3. 註冊 MCP 設定
在您的設定檔中加入：
{
  "mcp": {
    "notebooklm": {
      "type": "local",
      "command": ["nlm", "mcp"],
      "enabled": true
    }
  }
}

---

## 二、Word 與 Excel 自動化生成規範

當要求生成文件時，AI 應調用 Python 套件 (python-docx, openpyxl)。

### 1. Excel 生成規範
- 必須有明確標題列、資料列與邊框。
- 標題列建議深藍色填充，資料列採用灰白相間色系。

### 2. Word 生成規範
- 必須具備階層 (標題1, 標題2, 內文)。
- 內文採用左右對齊。

---

## 三、ANTIGRAVITY.md 範本

在專案根目錄建立 ANTIGRAVITY.md：

# <專案名稱> - ANTIGRAVITY.md

## 專案入口
專案名稱：
主要工作目錄：
Outputs 目錄：./outputs/

## 工作規則
- 回應使用繁體中文。
- 涉及檔案操作時回報完整產出位置。
- 固定經由 NotebookLM MCP 同步外部知識庫。
- 任務結束時，若涉及複雜數據或長文本，必須主動詢問是否自動生成 Excel 矩陣或 Word 規格書。

## 不要做
- 不要 commit API key、token、密碼。
- 不要 commit NotebookLM 個人匯出清單。
