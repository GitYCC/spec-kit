---
description: 從自然語言功能描述建立或更新功能規格說明。
scripts:
  sh: scripts/bash/create-new-feature.sh --json "{ARGS}"
  ps: scripts/powershell/create-new-feature.ps1 -Json "{ARGS}"
---

給定作為參數提供的功能描述，執行以下操作：

1. 從 repo 根目錄執行 script `{SCRIPT}` 並解析其 JSON 輸出以取得 BRANCH_NAME 和 SPEC_FILE。所有檔案路徑必須是絕對路徑。
2. 載入 `templates/spec-template.md` 以了解必需的節段。
3. 使用 template 結構將規格說明寫入 SPEC_FILE，用從功能描述（參數）中提取的具體細節替換占位符，同時保持節段順序和標題。
4. 報告完成情況，包括分支名稱、規格檔案路徑和下一階段的準備情況。

注意：Script 在寫入前建立並切換到新分支並初始化規格檔案。
