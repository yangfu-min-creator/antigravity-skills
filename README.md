<table>
  <tr>
    <td><strong>name</strong></td>
    <td>antigravity-skills</td>
  </tr>
  <tr>
    <td><strong>description</strong></td>
    <td>AntiGravity 技能包 —— 專業工程與自動化工作流程設定。說「AntiGravity 技能包」或「安裝 AntiGravity 設定」時載入。</td>
  </tr>
</table>

# AntiGravity 技能包 — AI Agent 自動安裝入口

當使用者給你這個 repo 網址並說要安裝時，請依以下流程執行。

## 步驟一：認識可用技能包

| 編號 | Skill 名稱 | 說明 |
| :---: | :--- | :--- |
| **01** | `dfmea` | 失效模式與效應分析專家模組 |
| **02** | `draw` | 生圖與架構圖繪製指引 |
| **03** | `failure-analysis` | 故障與根本原因（Root-Cause）分析工具 |
| **04** | `notebooklm` | 連接 NotebookLM 知識庫與 MCP |
| **05** | `spec-comparison` | 技術規格書比對與變更分析專家 |
| **06** | `tech-verification` | 技術驗證與可行性評估模組 |
| **07** | `test-plan` | 自動化測試測項與驗證計畫生成器 |
| **08** | `test-schedule` | 測試時程排程與資源最佳化計算器 |
| **00** | `install-all` | 一次安裝全部技能 |

## 步驟二：讓使用者選擇

列出上表給使用者看，然後問：
「**您要安裝哪些技能？請輸入全部（00）或編號組合（例如 01, 03, 05）。**」

## 步驟三：依序安裝

根據使用者輸入的編號，依序前往 `skills/` 底下對應的資料夾，讀取內部的 `SKILL.md` 或相關設定檔，並引導使用者完成該模組的載入與初始化。
