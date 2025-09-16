---
description: 使用計畫 template 執行實作規劃工作流程以生成設計物件。
scripts:
  sh: scripts/bash/setup-plan.sh --json
  ps: scripts/powershell/setup-plan.ps1 -Json
---

給定作為參數提供的實作細節，執行以下操作：

1. 從 repo 根目錄執行 `{SCRIPT}` 並解析 JSON 以取得 FEATURE_SPEC、IMPL_PLAN、SPECS_DIR、BRANCH。所有未來的檔案路徑必須是絕對路徑。
2. 讀取並分析功能規格說明以了解：
   - 功能需求和使用者故事
   - 功能性和非功能性需求（功能需求回答「做什麼」，非功能需求回答「做多好」）
   - 成功標準和接受標準
   - 任何提及的技術約束或相依性

3. 讀取 `/memory/constitution.md` 的章程以了解章程需求。

4. 執行實作計畫 template：
   - 載入 `/templates/plan-template.md`（已複製到 IMPL_PLAN 路徑）
   - 將 Input 路徑設定為 FEATURE_SPEC
   - 執行執行流程（main）函數步驟 1-10
   - Template 是自包含且可執行的
   - 遵循指定的錯誤處理和關卡檢查
   - 讓 template 在 $SPECS_DIR 中指導物件生成：
     * 第 0 階段生成 research.md
     * 第 1 階段生成 data-model.md、contracts/、quickstart.md
     * 第 2 階段生成 tasks.md
   - 將參數中的使用者提供細節結合到技術背景中：{ARGS}
   - 完成每個階段時更新進度追蹤

5. 驗證執行完成：
   - 檢查進度追蹤顯示所有階段完成
   - 確保所有必需的物件都已生成
   - 確認執行中無 ERROR 狀態

6. 報告結果，包括分支名稱、檔案路徑和生成的物件。

所有檔案操作都使用帶有 repository 根目錄的絕對路徑以避免路徑問題。
