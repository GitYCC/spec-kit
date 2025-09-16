# Implementation Plan: [FEATURE]

<!-- VARIANT:sh - Run `/scripts/bash/update-agent-context.sh __AGENT__` for your AI assistant -->
<!-- VARIANT:ps - Run `/scripts/powershell/update-agent-context.ps1 -AgentType __AGENT__` for your AI assistant -->

**Branch**: `[###-feature-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Feature specification from `/specs/[###-feature-name]/spec.md`

## 執行流程（/plan 指令範圍）
```
1. Load feature spec from Input path
   → If not found: ERROR "No feature spec at {path}"
2. Fill Technical Context (scan for NEEDS CLARIFICATION)
   → Detect Project Type from context (web=frontend+backend, mobile=app+api)
   → Set Structure Decision based on project type
3. Evaluate Constitution Check section below
   → If violations exist: Document in Complexity Tracking
   → If no justification possible: ERROR "Simplify approach first"
   → Update Progress Tracking: Initial Constitution Check
4. Execute Phase 0 → research.md
   → If NEEDS CLARIFICATION remain: ERROR "Resolve unknowns"
5. Execute Phase 1 → contracts, data-model.md, quickstart.md, agent-specific template file (e.g., `CLAUDE.md` for Claude Code, `.github/copilot-instructions.md` for GitHub Copilot, or `GEMINI.md` for Gemini CLI).
6. Re-evaluate Constitution Check section
   → If new violations: Refactor design, return to Phase 1
   → Update Progress Tracking: Post-Design Constitution Check
7. Plan Phase 2 → Describe task generation approach (DO NOT create tasks.md)
8. STOP - Ready for /tasks command
```

**重要**：/plan 指令在步驟 7 結束。第 2-4 階段由其他指令執行：
- 第 2 階段：/tasks 指令建立 tasks.md
- 第 3-4 階段：實作執行（手動或透過工具）

## 摘要
[從功能規格中提取：主要需求 + 研究中的技術方法]

## 技術背景
**程式語言/版本**：[例如，Python 3.11、Swift 5.9、Rust 1.75 或 NEEDS CLARIFICATION]
**主要相依性**：[例如，FastAPI、UIKit、LLVM 或 NEEDS CLARIFICATION]
**儲存**：[如果適用，例如，PostgreSQL、CoreData、檔案 或 N/A]
**測試**：[例如，pytest、XCTest、cargo test 或 NEEDS CLARIFICATION]
**目標平台**：[例如，Linux server、iOS 15+、WASM 或 NEEDS CLARIFICATION]
**專案類型**：[single/web/mobile - 決定原始碼結構]
**效能目標**：[領域特定，例如，1000 req/s、1000萬行/秒、60 fps 或 NEEDS CLARIFICATION]
**約束**：[領域特定，例如，<200ms p95、<100MB 記憶體、離線支援 或 NEEDS CLARIFICATION]
**規模/範圍**：[領域特定，例如，1萬使用者、100萬 LOC、50 個畫面 或 NEEDS CLARIFICATION]

## Constitution Check
*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

**簡單性**：
- 專案：[#] (最多 3 個 - 例如，api、cli、tests)
- 直接使用 framework？（不用 wrapper 類別）
- 單一資料模型？（除非序列化不同，否則不用 DTO）
- 避免模式？（沒有證明需要就不用 Repository/UoW）

**架構**：
- 每個功能都作為 library？（不直接寫 app 程式碼）
- Library 清單：[每個的名稱 + 目的]
- 每個 library 的 CLI：[帶有 --help/--version/--format 的指令]
- Library 文件：規劃使用 llms.txt 格式？

**測試（不可協商）**：
- 強制執行 RED-GREEN-Refactor 循環？（測試必須先失敗）
- Git 提交顯示測試在實作之前？
- 順序：Contract→Integration→E2E→Unit 嚴格遵循？
- 使用真實相依性？（實際資料庫，不是 mock）
- 整合測試用於：新 library、契約變更、共享 schema？
- 禁止：測試前實作、跳過 RED 階段

**可觀測性**：
- 包含結構化日誌記錄？
- Frontend 日誌 → backend？（統一串流）
- 錯誤背景足夠？

**版本控制**：
- 已指定版本號？（MAJOR.MINOR.BUILD）
- 每次變更都增加 BUILD？
- 處理 breaking change？（並行測試、遷移計畫）

## 專案結構

### 文件（此功能）
```
specs/[###-feature]/
├── plan.md              # 此檔案 (/plan 指令輸出)
├── research.md          # 第 0 階段輸出 (/plan 指令)
├── data-model.md        # 第 1 階段輸出 (/plan 指令)
├── quickstart.md        # 第 1 階段輸出 (/plan 指令)
├── contracts/           # 第 1 階段輸出 (/plan 指令)
└── tasks.md             # 第 2 階段輸出 (/tasks 指令 - 不由 /plan 建立)
```

### 原始碼（repository 根目錄）
```
# 選項 1：單一專案（預設）
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# 選項 2：Web 應用程式（當偵測到 "frontend" + "backend" 時）
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# 選項 3：Mobile + API（當偵測到 "iOS/Android" 時）
api/
└── [same as backend above]

ios/ or android/
└── [platform-specific structure]
```

**結構決策**：[預設為選項 1，除非技術背景指示為 web/mobile app]

## 第 0 階段：大綱與研究
1. **從上方技術背景中提取未知問題**：
   - 每個 NEEDS CLARIFICATION → 研究任務
   - 每個相依性 → 最佳實務任務
   - 每個整合 → 模式任務

2. **生成並派遣研究 agent**：
   ```
   為技術背景中的每個未知問題：
     任務："為 {feature context} 研究 {unknown}"
   為每個技術選擇：
     任務："在 {domain} 中找到 {tech} 的最佳實務"
   ```

3. **在 `research.md` 中統整研究結果**，使用格式：
   - 決策：[選擇什麼]
   - 理由：[為什麼選擇]
   - 考慮的替代方案：[還評估了什麼]

**輸出**：research.md，所有 NEEDS CLARIFICATION 都已解決

## 第 1 階段：設計與契約
*先決條件：research.md 完成*

1. **從功能規格中提取實體** → `data-model.md`：
   - 實體名稱、欄位、關係
   - 從需求中提取驗證規則
   - 狀態轉換（如果適用）

2. **從功能需求生成 API 契約**：
   - 每個使用者動作 → endpoint
   - 使用標準 REST/GraphQL 模式
   - 輸出 OpenAPI/GraphQL schema 到 `/contracts/`

3. **從契約生成契約測試**：
   - 每個 endpoint 一個測試檔案
   - 斷言 request/response schema
   - 測試必須失敗（尚無實作）

4. **從使用者故事中提取測試情境**：
   - 每個故事 → 整合測試情境
   - Quickstart 測試 = 故事驗證步驟

5. **遞增更新 agent 檔案**（O(1) 操作）：
   VARIANT-INJECT
   - 如果存在：僅從當前計畫中新增新技術
   - 保留標記間的手動新增內容
   - 更新最近變更（保留最後 3 個）
   - 保持在 150 行以下以提高 token 效率
   - 輸出到 repository 根目錄

**輸出**：data-model.md、/contracts/*、失敗的測試、quickstart.md、agent 特定檔案

## 第 2 階段：任務規劃方法
*此節描述 /tasks 指令將執行的作業 - 在 /plan 期間不要執行*

**任務生成策略**：
- 載入 `/templates/tasks-template.md` 作為基礎
- 從第 1 階段設計文件生成任務（contracts、data model、quickstart）
- 每個 contract → contract 測試任務 [P]
- 每個實體 → 模型建立任務 [P]
- 每個使用者故事 → 整合測試任務
- 讓測試通過的實作任務

**排序策略**：
- TDD 順序：測試在實作之前
- 相依性順序：模型在服務之前，服務在 UI 之前
- 標記 [P] 進行並行執行（獨立檔案）

**預估輸出**：tasks.md 中 25-30 個編號、排序的任務

**重要**：此階段由 /tasks 指令執行，不是由 /plan 執行

## 第 3+ 階段：未來實作
*這些階段超出 /plan 指令的範圍*

**第 3 階段**：任務執行（/tasks 指令建立 tasks.md）
**第 4 階段**：實作（遵循章程原則執行 tasks.md）
**第 5 階段**：驗證（運行測試、執行 quickstart.md、效能驗證）

## 複雜度追蹤
*僅在章程檢查有必須被証明的違反時填寫*

| 違反 | 為什麼需要 | 拒絕簡單替代方案的原因 |
|-----------|------------|-------------------------------------|
| [例如，第 4 個專案] | [當前需求] | [為什麼 3 個專案不夠] |
| [例如，Repository 模式] | [特定問題] | [為什麼直接 DB 存取不夠] |


## 進度追蹤
*此檢查清單在執行流程中更新*

**階段狀態**：
- [ ] 第 0 階段：研究完成 (/plan 指令)
- [ ] 第 1 階段：設計完成 (/plan 指令)
- [ ] 第 2 階段：任務規劃完成 (/plan 指令 - 僅描述方法)
- [ ] 第 3 階段：任務已生成 (/tasks 指令)
- [ ] 第 4 階段：實作完成
- [ ] 第 5 階段：驗證通過

**關卡狀態**：
- [ ] 初始章程檢查：通過
- [ ] 設計後章程檢查：通過
- [ ] 所有 NEEDS CLARIFICATION 已解決
- [ ] 複雜度偏差已記錄

---
*基於章程 v2.1.1 - 參見 `/memory/constitution.md`*