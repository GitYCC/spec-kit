# 章程更新檢查清單

修正章程（`/memory/constitution.md`）時，請確保所有相依文件都已更新以保持一致性。

## 需要更新的 Template

### 新增/修改任何條文時：
- [ ] `/templates/plan-template.md` - 更新章程檢查部分
- [ ] `/templates/spec-template.md` - 如果需求/範圍受到影響則更新
- [ ] `/templates/tasks-template.md` - 如果需要新的任務類型則更新
- [ ] `/.claude/commands/plan.md` - 如果規劃流程變更則更新
- [ ] `/.claude/commands/tasks.md` - 如果任務產生受到影響則更新
- [ ] `/CLAUDE.md` - 更新運行時開發指導方針

### 條文特定更新：

#### 第一條（Library-First）：
- [ ] 確保 template 強調 library 建立
- [ ] 更新 CLI 指令範例
- [ ] 新增 llms.txt 文件需求

#### 第二條（CLI Interface）：
- [ ] 更新 template 中的 CLI flag 需求
- [ ] 新增文字 I/O 協議提醒

#### 第三條（Test-First）：
- [ ] 更新所有 template 中的測試順序
- [ ] 強調 TDD 需求
- [ ] 新增測試審批關卡

#### 第四條（Integration Testing）：
- [ ] 列出整合測試觸發條件
- [ ] 更新測試類型優先順序
- [ ] 新增真實相依性需求

#### 第五條（Observability）：
- [ ] 新增日誌記錄需求到 template
- [ ] 包含多層日誌串流
- [ ] 更新效能監控部分

#### 第六條（Versioning）：
- [ ] 新增版本遞增提醒
- [ ] 包含 breaking change 程序
- [ ] 更新遷移需求

#### 第七條（Simplicity）：
- [ ] 更新專案數量限制
- [ ] 新增模式禁止範例
- [ ] 包含 YAGNI 提醒

## 驗證步驟

1. **提交章程變更前：**
   - [ ] 所有 template 都參考新需求
   - [ ] 範例已更新以符合新規則
   - [ ] 文件間無矛盾

2. **更新 template 後：**
   - [ ] 執行範例實作計畫
   - [ ] 驗證所有章程需求都已處理
   - [ ] 檢查 template 是否為自包含的（無需章程即可閱讀）

3. **版本追蹤：**
   - [ ] 更新章程版本號
   - [ ] 在 template footer 中標註版本
   - [ ] 新增修正案到章程歷史

## 常見遺漏

注意這些經常被遺忘的更新：
- 指令文件（`/commands/*.md`）
- Template 中的檢查清單項目
- 範例程式碼/指令
- 特定領域變體（web vs mobile vs CLI）
- 文件間的交叉參照

## Template 同步狀態

上次同步檢查：2025-07-16
- 章程版本：2.1.1
- Template 對齊：❌（缺少 versioning、observability 細節）

---

*此檢查清單確保章程的原則在所有專案文件中得到一致應用。*