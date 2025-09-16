# Feature Specification: [FEATURE NAME]

**Feature Branch**: `[###-feature-name]`  
**Created**: [DATE]  
**Status**: Draft  
**Input**: User description: "$ARGUMENTS"

## Execution Flow (main)
```
1. Parse user description from Input
   → If empty: ERROR "No feature description provided"
2. Extract key concepts from description
   → Identify: actors, actions, data, constraints
3. For each unclear aspect:
   → Mark with [NEEDS CLARIFICATION: specific question]
4. Fill User Scenarios & Testing section
   → If no clear user flow: ERROR "Cannot determine user scenarios"
5. Generate Functional Requirements
   → Each requirement must be testable
   → Mark ambiguous requirements
6. Identify Key Entities (if data involved)
7. Run Review Checklist
   → If any [NEEDS CLARIFICATION]: WARN "Spec has uncertainties"
   → If implementation details found: ERROR "Remove tech details"
8. Return: SUCCESS (spec ready for planning)
```

---

## ⚡ 快速指南
- ✅ 專注於使用者需要什麼以及為什麼
- ❌ 避免如何實作（不談技術堆疊、API、程式碼結構）
- 👥 為業務利益關係人而寫，不是為開發者

### 節段需求
- **必填節段**：每個功能都必須完成
- **選填節段**：僅在與功能相關時包含
- 當節段不適用時，完全刪除（不要留作 "N/A"）

### 為 AI 生成
從使用者提示建立此規格時：
1. **標記所有模糊之處**：對於任何您需要假設的事項，使用 [NEEDS CLARIFICATION: 具體問題]
2. **不要猜測**：如果提示沒有指定某事（例如，「登入系統」但沒有認證方法），就標記它
3. **像測試者一樣思考**：每個模糊的需求都應該在「可測試且明確」檢查清單項目中失敗
4. **常見不完整指定的領域**：
   - 使用者類型和權限
   - 資料保存/刪除政策
   - 效能目標和規模
   - 錯誤處理行為
   - 整合需求
   - 安全/合規需求

---

## 使用者情境與測試 *(必填)*

### 主要使用者故事
[用白話描述主要使用者旅程]

### 接受情境
1. **Given** [初始狀態]，**When** [動作]，**Then** [預期結果]
2. **Given** [初始狀態]，**When** [動作]，**Then** [預期結果]

### 邊界情況
- 當 [邊界條件] 時會發生什麼？
- 系統如何處理 [錯誤情境]？

## 需求 *(必填)*

### 功能需求
- **FR-001**：系統必須 [特定能力，例如：「允許使用者建立帳戶」]
- **FR-002**：系統必須 [特定能力，例如：「驗證電子郵件地址」]
- **FR-003**：使用者必須能夠 [關鍵互動，例如：「重設密碼」]
- **FR-004**：系統必須 [資料需求，例如：「保存使用者偏好設定」]
- **FR-005**：系統必須 [行為，例如：「記錄所有安全事件」]

*標記不明確需求的範例：*
- **FR-006**：系統必須透過 [NEEDS CLARIFICATION: 認證方法未指定 - email/password, SSO, OAuth?] 驗證使用者
- **FR-007**：系統必須保存使用者資料 [NEEDS CLARIFICATION: 未指定保存期限]

### 關鍵實體 *(如果功能涉及資料則包含)*
- **[實體 1]**：[代表什麼，不包含實作的關鍵屬性]
- **[實體 2]**：[代表什麼，與其他實體的關係]

---

## 審查與接受檢查清單
*關卡：在 main() 執行期間運行的自動檢查*

### 內容品質
- [ ] 無實作細節（程式語言、framework、API）
- [ ] 專注於使用者價值和業務需求
- [ ] 為非技術利益關係人撰寫
- [ ] 所有必填節段已完成

### 需求完整性
- [ ] 無 [NEEDS CLARIFICATION] 標記殘留
- [ ] 需求是可測試和明確的
- [ ] 成功標準是可衡量的
- [ ] 範圍有明確界限
- [ ] 已識別相依性和假設

---

## 執行狀態
*在處理期間由 main() 更新*

- [ ] 使用者描述已解析
- [ ] 關鍵概念已提取
- [ ] 模糊之處已標記
- [ ] 使用者情境已定義
- [ ] 需求已生成
- [ ] 實體已識別
- [ ] 審查檢查清單已通過

---
