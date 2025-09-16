---
description: 根據可用的設計物件為功能生成可執行、相依性排序的 tasks.md。
scripts:
  sh: scripts/bash/check-task-prerequisites.sh --json
  ps: scripts/powershell/check-task-prerequisites.ps1 -Json
---

給定作為參數提供的背景，執行以下操作：

1. 從 repo 根目錄執行 `{SCRIPT}` 並解析 FEATURE_DIR 和 AVAILABLE_DOCS 清單。所有路徑必須是絕對路徑。
2. 載入並分析可用的設計文件：
   - 總是讀取 plan.md 以取得 tech stack 和 library
   - 如果存在：讀取 data-model.md 以取得 Entities
   - 如果存在：讀取 contracts/ 以取得 API endpoint
   - 如果存在：讀取 research.md 以取得技術決策
   - 如果存在：讀取 quickstart.md 以取得測試情境

   注意：不是所有專案都有所有文件。例如：
   - CLI 工具可能沒有 contracts/
   - 簡單的 library 可能不需要 data-model.md
   - 根據可用的內容生成任務

3. 遵循 template 生成任務：
   - 使用 `/templates/tasks-template.md` 作為基礎
   - 用以下內容為基礎的實際任務替換範例任務：
     * **設定任務**：Project init, dependencies, linting
     * **測試任務 [P]**：One per contract, one per integration scenario
     * **核心任務**：One per entity, service, CLI command, endpoint
     * **整合任務**：DB connections, middleware, logging
     * **精製任務 [P]**：Unit tests, performance, docs

4. 任務生成規則：
   - Each contract file → contract test task marked [P]
   - Each entity in data-model → model creation task marked [P]
   - Each endpoint → implementation task (not parallel if shared files)
   - Each user story → integration test marked [P]
   - Different files = can be parallel [P]
   - Same file = sequential (no [P])

5. 按相依性排序任務：
   - 設定在所有其他之前
   - 測試在實作之前 (TDD)
   - Models 在服務之前
   - 服務在 endpoint 之前
   - 核心在整合之前
   - 所有都在精製之前

6. 包含並行執行範例：
   - Group [P] tasks that can run together
   - 顯示實際的 Task agent 指令

7. 建立 FEATURE_DIR/tasks.md，包含：
   - 從實作計畫中的正確功能名稱
   - 編號任務 (T001, T002, 等)
   - 每個任務的明確檔案路徑
   - 相依性說明
   - 並行執行指導

任務生成的背景：{ARGS}

tasks.md 應該可以立即執行 - 每個任務必須具體到足以讓 LLM 在沒有額外背景的情況下完成它。
