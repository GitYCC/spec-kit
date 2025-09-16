# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## 格式：`[ID] [P?] Description`
- **[P]**：可以並行執行（不同檔案，無相依性）
- 在描述中包含精確的檔案路徑

## 路徑約定
- **單一專案**：repository 根目錄的 `src/`、`tests/`
- **Web app**：`backend/src/`、`frontend/src/`
- **Mobile**：`api/src/`、`ios/src/` 或 `android/src/`
- 以下顯示的路徑假設為單一專案 - 根據 plan.md 結構調整

## 第 3.1 階段：設定
- [ ] T001 按照實作計畫建立專案結構
- [ ] T002 使用 [程式語言] 初始化專案與 [framework] 相依性
- [ ] T003 [P] 設定 linting 和格式化工具

## 第 3.2 階段：測試優先 (TDD) ⚠️ 必須在 3.3 之前完成
**關鍵**：這些測試必須撰寫且必須在任何實作之前失敗
- [ ] T004 [P] 在 tests/contract/test_users_post.py 中對 POST /api/users 進行契約測試
- [ ] T005 [P] 在 tests/contract/test_users_get.py 中對 GET /api/users/{id} 進行契約測試
- [ ] T006 [P] 在 tests/integration/test_registration.py 中進行使用者註冊整合測試
- [ ] T007 [P] 在 tests/integration/test_auth.py 中進行認證流程整合測試

## 第 3.3 階段：核心實作（僅在測試失敗後）
- [ ] T008 [P] 在 src/models/user.py 中建立 User 模型
- [ ] T009 [P] 在 src/services/user_service.py 中建立 UserService CRUD
- [ ] T010 [P] 在 src/cli/user_commands.py 中建立 CLI --create-user
- [ ] T011 POST /api/users endpoint
- [ ] T012 GET /api/users/{id} endpoint
- [ ] T013 輸入驗證
- [ ] T014 錯誤處理和日誌記錄

## 第 3.4 階段：整合
- [ ] T015 連接 UserService 到 DB
- [ ] T016 Auth middleware
- [ ] T017 Request/response 日誌記錄
- [ ] T018 CORS 和安全標頭

## 第 3.5 階段：精製
- [ ] T019 [P] 在 tests/unit/test_validation.py 中進行驗證的單元測試
- [ ] T020 效能測試 (<200ms)
- [ ] T021 [P] 更新 docs/api.md
- [ ] T022 移除重複
- [ ] T023 執行 manual-testing.md

## 相依性
- 測試 (T004-T007) 在實作 (T008-T014) 之前
- T008 阻擋 T009、T015
- T016 阻擋 T018
- 實作在精製 (T019-T023) 之前

## 並行範例
```
# 一起啟動 T004-T007：
Task: "在 tests/contract/test_users_post.py 中對 POST /api/users 進行契約測試"
Task: "在 tests/contract/test_users_get.py 中對 GET /api/users/{id} 進行契約測試"
Task: "在 tests/integration/test_registration.py 中進行註冊整合測試"
Task: "在 tests/integration/test_auth.py 中進行認證整合測試"
```

## 注意事項
- [P] 任務 = 不同檔案，無相依性
- 在實作前驗證測試失敗
- 每個任務後提交
- 避免：模糊任務、相同檔案衝突

## 任務生成規則
*在 main() 執行期間應用*

1. **從契約**：
   - 每個契約檔案 → 契約測試任務 [P]
   - 每個 endpoint → 實作任務
   
2. **從資料模型**：
   - 每個實體 → 模型建立任務 [P]
   - 關係 → 服務層任務
   
3. **從使用者故事**：
   - 每個故事 → 整合測試 [P]
   - Quickstart 情境 → 驗證任務

4. **排序**：
   - 設定 → 測試 → 模型 → 服務 → Endpoint → 精製
   - 相依性阻擋並行執行

## 驗證檢查清單
*關卡：在返回前由 main() 檢查*

- [ ] 所有契約都有相應的測試
- [ ] 所有實體都有模型任務
- [ ] 所有測試都在實作之前
- [ ] 並行任務真正獨立
- [ ] 每個任務指定精確的檔案路徑
- [ ] 沒有任務修改與其他 [P] 任務相同的檔案