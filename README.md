<div align="center">
    <img src="./media/logo_small.webp"/>
    <h1>🌱 Spec Kit</h1>
    <h3><em>更快速地建構高品質軟體。</em></h3>
</div>

<p align="center">
    <strong>透過 Spec-Driven Development 的協助，讓組織能夠專注於產品情境，而非撰寫同質化程式碼。</strong>
</p>

[![Release](https://github.com/GitYCC/spec-kit/actions/workflows/release.yml/badge.svg)](https://github.com/GitYCC/spec-kit/actions/workflows/release.yml)

---

## 目錄

- [目錄](#目錄)
- [🤔 什麼是 Spec-Driven Development？](#-什麼是-spec-driven-development)
- [⚡ 開始使用](#-開始使用)
  - [1. 安裝 Specify](#1-安裝-specify)
  - [2. 建立 spec](#2-建立-spec)
  - [3. 建立技術實作計畫](#3-建立技術實作計畫)
  - [4. 分解並實作](#4-分解並實作)
- [📽️ 影片概覽](#️-影片概覽)
- [🔧 Specify CLI Reference](#-specify-cli-reference)
  - [指令](#指令)
  - [`specify init` 參數與選項](#specify-init-參數與選項)
  - [範例](#範例)
- [📚 核心理念](#-核心理念)
- [🌟 開發階段](#-開發階段)
- [🎯 實驗目標](#-實驗目標)
  - [技術獨立性](#技術獨立性)
  - [企業限制](#企業限制)
  - [以使用者為中心的開發](#以使用者為中心的開發)
  - [創意與順代式流程](#創意與順代式流程)
- [🔧 前置需求](#-前置需求)
- [📖 深入了解](#-深入了解)
- [📋 詳細流程](#-詳細流程)
  - [**步驟 1：** 啟動專案](#步驟-1-啟動專案)
  - [**步驟 2：** 功能規格澄清](#步驟-2-功能規格澄清)
  - [**步驟 3：** 產生計畫](#步驟-3-產生計畫)
  - [**步驟 4：** 讓 Claude Code 驗證計畫](#步驟-4-讓-claude-code-驗證計畫)
  - [步驟 5：實作](#步驟-5實作)
- [🔍 疑難排解](#-疑難排解)
  - [Linux 上的 Git Credential Manager](#linux-上的-git-credential-manager)
- [👥 維護者](#-維護者)
- [💬 支援](#-支援)
- [🙏 致謝](#-致謝)
- [📄 授權條款](#-授權條款)

## 🤔 什麼是 Spec-Driven Development？

Spec-Driven Development **顛覆了**傳統軟體開發的做法。數十年來，程式碼一直是王道——規格文件只是我們建立後，在開始「真正工作」撰寫程式碼時就丟棄的鷹架。Spec-Driven Development 改變了這一切：**規格變成可執行的**，直接產生可運作的實作，而不僅僅是指導實作。

## ⚡ 開始使用

### 1. 安裝 Specify

根據你使用的 coding agent 來初始化專案：

```bash
uvx --from git+https://github.com/GitYCC/spec-kit.git specify init <PROJECT_NAME>
```

### 2. 建立 spec

使用 **`/specify`** 指令來描述你想要建構的內容。專注於**什麼**和**為什麼**，而非技術 stack。

```bash
/specify 建立一個應用程式，可以幫助我將照片整理到不同的相簿中。相簿按日期分組，並且可以在主頁面上透過拖拉的方式重新排列。相簿永遠不會巢狀在其他相簿內。在每個相簿中，照片會以瓷磚式介面預覽顯示。
```

### 3. 建立技術實作計畫

使用 **`/plan`** 指令來提供你的技術 stack 和架構選擇。

```bash
/plan 這個應用程式使用 Vite 並搭配最少數量的程式庫。盡可能使用原生的 HTML、CSS 和 JavaScript。圖片不會上傳到任何地方，元數據會儲存在本地的 SQLite 資料庫中。
```

### 4. 分解並實作

使用 **`/tasks`** 來建立可執行的任務清單，然後請你的 agent 實作該功能。

詳細的逐步指引請參閱我們的[完整指南](./spec-driven.md)。

## 📽️ 影片概覽

想看 Spec Kit 的實際操作嗎？觀看我們的[影片概覽](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)！

[![Spec Kit video header](/media/spec-kit-video-header.jpg)](https://www.youtube.com/watch?v=a9eR1xsfvHg&pp=0gcJCckJAYcqIYzv)

## 🔧 Specify CLI Reference

`specify` 指令支援以下選項：

### 指令

| 指令     | 描述                                                    |
|-------------|----------------------------------------------------------------|
| `init`      | 從最新樣板初始化新的 Specify 專案      |
| `check`     | 檢查已安裝的工具 (`git`, `claude`, `gemini`, `code`/`code-insiders`, `cursor-agent`) |

### `specify init` 參數與選項

| 參數/選項        | 類型     | 描述                                                                  |
|------------------------|----------|------------------------------------------------------------------------------|
| `<project-name>`       | 參數 | 新專案目錄的名稱（使用 `--here` 時可選）            |
| `--ai`                 | 選項   | 要使用的 AI 助手：`claude`、`gemini`、`copilot` 或 `cursor`             |
| `--script`             | 選項   | 要使用的 script 變體：`sh` (bash/zsh) 或 `ps` (PowerShell)                 |
| `--ignore-agent-tools` | 旗標     | 跳過對於 AI agent 工具（如 Claude Code）的檢查                             |
| `--no-git`             | 旗標     | 跳過 git repository 初始化                                          |
| `--here`               | 旗標     | 在目前目錄初始化專案，而非建立新目錄   |
| `--skip-tls`           | 旗標     | 跳過 SSL/TLS 驗證（不建議）                                 |
| `--debug`              | 旗標     | 啟用詳細的 debug 輸出以供問題排除                            |

### 範例

```bash
# 基本專案初始化
specify init my-project

# 使用特定 AI 助手初始化
specify init my-project --ai claude

# 使用 Cursor 支援初始化
specify init my-project --ai cursor

# 使用 PowerShell scripts 初始化（Windows/跨平台）
specify init my-project --ai copilot --script ps

# 在目前目錄初始化
specify init --here --ai copilot

# 跳過 git 初始化
specify init my-project --ai gemini --no-git

# 啟用 debug 輸出以供問題排除
specify init my-project --ai claude --debug

# 檢查系統需求
specify check
```

## 📚 核心理念

Spec-Driven Development 是一個結構化的流程，強調：

- **意圖驅動的開發**，其中規格在「_怎麼做_」之前先定義「_做什麼_」
- **豐富的規格建立**，使用保障與組織原則
- **多步驟精練**，而非從提示一次生成程式碼
- **重度依賴**進階 AI 模型的規格解釋能力

## 🌟 開發階段

| 階段 | 重點 | 主要活動 |
|-------|-------|----------------|
| **0-to-1 Development**（「Greenfield」） | 從頭開始產生 | <ul><li>從高層級需求開始</li><li>產生規格</li><li>規劃實作步驟</li><li>建構生產就緒的應用程式</li></ul> |
| **創意探索** | 平行實作 | <ul><li>探索多元化解方案</li><li>支援多種技術 stack 與架構</li><li>實驗 UX 模式</li></ul> |
| **頁代式增強**（「Brownfield」） | Brownfield 現代化 | <ul><li>預代式增加功能</li><li>現代化遺留系統</li><li>適應流程</li></ul> |

## 🎯 實驗目標

我們的研究與實驗主要重點：

### 技術獨立性

- 使用多元化技術 stack 建立應用程式
- 驗證 Spec-Driven Development 是一個不網於特定技術、程式語言或 framework 的流程這個假說

### 企業限制

- 展示關鍵任務應用程式開發
- 納入組織限制（雲端提供商、技術 stack、工程實踐）
- 支援企業設計系統與合規需求

### 以使用者為中心的開發

- 為不同使用者群體與偏好建構應用程式
- 支援各種開發方式（從 vibe-coding 到 AI-native 開發）

### 創意與順代式流程

- 驗證平行實作探索的概念
- 提供健全的頁代式功能開發工作流程
- 擴展流程以處理升級與現代化任務

## 🔧 前置需求

- **Linux/macOS**（或 Windows 上的 WSL2）
- AI coding agent：[Claude Code](https://www.anthropic.com/claude-code)、[GitHub Copilot](https://code.visualstudio.com/)、[Gemini CLI](https://github.com/google-gemini/gemini-cli) 或 [Cursor](https://cursor.sh/)
- [uv](https://docs.astral.sh/uv/) 用於 package 管理
- [Python 3.11+](https://www.python.org/downloads/)
- [Git](https://git-scm.com/downloads)

## 📖 深入了解

- **[完整的 Spec-Driven Development 方法論](./spec-driven.md)** - 深入探討完整流程
- **[詳細演示](#-詳細流程)** - 逐步實作指南

---

## 📋 詳細流程

<details>
<summary>點擊展開詳細的逐步演示</summary>

你可以使用 Specify CLI 來啟動你的專案，這將在你的環境中帶入所需的成品。執行：

```bash
specify init <project_name>
```

或在目前目錄初始化：

```bash
specify init --here
```

![Specify CLI bootstrapping a new project in the terminal](./media/specify_cli.gif)

你將被提示選擇你正在使用的 AI agent。你也可以在終端機中主動指定：

```bash
specify init <project_name> --ai claude
specify init <project_name> --ai gemini
specify init <project_name> --ai copilot
# 或在目前目錄：
specify init --here --ai claude
```

CLI 將檢查你是否已安裝 Claude Code 或 Gemini CLI。如果沒有，或者你偏好不檢查正確工具而直接取得樣板，請在你的指令中使用 `--ignore-agent-tools`：

```bash
specify init <project_name> --ai claude --ignore-agent-tools
```

### **步驟 1：** 啟動專案

前往專案資料夾並執行你的 AI agent。在我們的範例中，我們使用 `claude`。

![Bootstrapping Claude Code environment](./media/bootstrap-claude-code.gif)

如果你看到 `/specify`、`/plan` 和 `/tasks` 指令可用，就表示設定正確。

第一步應該是建立新的專案鷹架。使用 `/specify` 指令，然後提供你想要開發的專案的具體需求。

>[!IMPORTANT]
>盡可能明確地說明你試圖建構的_是什麼_和_為什麼_。**此時不要專注於技術 stack**。

範例提示：

```text
開發 Taskify，一個團隊生產力平台。它應該允許使用者建立專案、新增團隊成員、指派任務、留言，
並以 Kanban 風格在看板之間移動任務。在這個功能的初始階段，我們稱之為「Create Taskify」，
讓我們設定多個使用者，但使用者將提前宣告、預先定義。我希望有五個使用者分為兩個不同類別，
一個產品經理和四個工程師。讓我們建立三個不同的範例專案。每個任務的狀態應該有標準的 Kanban 欄位，
例如「待辦」、「進行中」、「審核中」和「完成」。此應用程式不會有登入功能，因為這只是確保我們基本功能
設定正確的第一個測試。對於 UI 中的每個任務卡片，你應該能夠在 Kanban 工作看板的不同欄位之間
更改任務的目前狀態。你應該能夠為特定卡片留下無限數量的留言。你應該能夠從該任務卡片指派
有效使用者之一。當你第一次啟動 Taskify 時，它會給你一個五個使用者的清單供選擇。
不需要密碼。當你點擊使用者時，你會進入主檢視，顯示專案清單。當你點擊專案時，
你會開啟該專案的 Kanban 看板。你會看到欄位。你能夠在不同欄位之間拖拉卡片。
你會看到指派給你（目前登入的使用者）的任何卡片以不同顏色顯示，以便你能夠快速辨識你的卡片。
你可以編輯你製作的任何留言，但不能編輯其他人製作的留言。你可以刪除你製作的任何留言，
但不能刪除其他人製作的留言。
```

輸入此提示後，你應該會看到 Claude Code 啟動規劃和規格起草流程。Claude Code 也會觸發一些內建的 scripts 來設定 repository。

完成此步驟後，你應該會有一個新建立的分支（例如 `001-create-taskify`），以及在 `specs/001-create-taskify` 目錄中的新規格。

產生的規格應該包含一套使用者故事和功能需求，如樣板中定義的那樣。

在此階段，你的專案資料夾內容應該類似於以下內容：

```text
├── memory
│	 ├── constitution.md
│	 └── constitution_update_checklist.md
├── scripts
│	 ├── check-task-prerequisites.sh
│	 ├── common.sh
│	 ├── create-new-feature.sh
│	 ├── get-feature-paths.sh
│	 ├── setup-plan.sh
│	 └── update-claude-md.sh
├── specs
│	 └── 001-create-taskify
│	     └── spec.md
└── templates
    ├── plan-template.md
    ├── spec-template.md
    └── tasks-template.md
```

### **步驟 2：** 功能規格澄清

建立基本規格後，你可以進一步澄清在第一次嘗試中沒有正確捕捉到的任何需求。例如，你可以在同一個 Claude Code 會話中使用這樣的提示：

```text
對於你建立的每個範例專案，應該有 5 到 15 個任務，隨機分佈在不同的完成狀態中。確保每個完成階段至少有一個任務。
```

你也應該要求 Claude Code 驗證**審核與接受清單**，勾選通過驗證/符合需求的項目，未符合的項目則保持未勾選。可以使用以下提示：

```text
閱讀審核與接受清單，如果功能規格符合清單中的條件，請勾選該項目。如果不符合，則保留空白。
```

重要的是，要利用與 Claude Code 的互動作為澄清規格相關問題的機會——**不要將它的第一次嘗試視為最終版本**。

### **步驟 3：** 產生計畫

現在你可以具體說明技術 stack 和其他技術需求。你可以使用專案樣板內建的 `/plan` 指令，搭配這樣的提示：

```text
我們將使用 .NET Aspire 來產生這個應用程式，使用 Postgres 作為資料庫。前端應該使用 Blazor server，具備拖拉式任務看板和即時更新功能。應該建立一個 REST API，包含專案 API、任務 API 和通知 API。
```

此步驟的輸出將包含多個實作細節文件，你的目錄樹將類似於：

```text
.
├── CLAUDE.md
├── memory
│	 ├── constitution.md
│	 └── constitution_update_checklist.md
├── scripts
│	 ├── check-task-prerequisites.sh
│	 ├── common.sh
│	 ├── create-new-feature.sh
│	 ├── get-feature-paths.sh
│	 ├── setup-plan.sh
│	 └── update-claude-md.sh
├── specs
│	 └── 001-create-taskify
│	     ├── contracts
│	     │	 ├── api-spec.json
│	     │	 └── signalr-spec.md
│	     ├── data-model.md
│	     ├── plan.md
│	     ├── quickstart.md
│	     ├── research.md
│	     └── spec.md
└── templates
    ├── CLAUDE-template.md
    ├── plan-template.md
    ├── spec-template.md
    └── tasks-template.md
```

檢查 `research.md` 文件，確保根據你的指示使用了正確的技術 stack。如果任何元件看起來突出，你可以要求 Claude Code 精煉它，甚至讓它檢查你想使用的平台/框架的本地安裝版本（例如 .NET）。

此外，如果所選的技術 stack 是快速變化的技術（例如 .NET Aspire、JS 框架），你可能會想要求 Claude Code 研究相關細節，可以使用這樣的提示：

```text
我希望你檢視實作計畫和實作細節，尋找可能需要額外研究的領域，因為 .NET Aspire 是一個快速變化的函式庫。對於你識別出需要進一步研究的領域，我希望你使用我們將在這個 Taskify 應用程式中使用的特定版本的額外細節來更新研究文件，並啟動平行研究任務來透過網路研究澄清任何細節。
```

在此過程中，你可能會發現 Claude Code 卡在研究錯誤的事物上——你可以用這樣的提示幫助引導它往正確方向：

```text
我認為我們需要將此分解為一系列步驟。首先，識別一個在實作過程中你不確定或會受益於進一步研究的任務清單。寫下這些任務的清單。然後對於每一個任務，我希望你啟動一個獨立的研究任務，這樣我們就能平行研究所有這些非常具體的任務。我看到你在做的是似乎在研究一般的 .NET Aspire，我認為這在這種情況下對我們沒有太大幫助。那太過於無目標的研究。研究需要幫助你解決特定的目標問題。
```

>[!NOTE]
>Claude Code 可能會過於積極並添加你沒有要求的元件。要求它澄清理由和變更的來源。

### **步驟 4：** 讓 Claude Code 驗證計畫

計畫就緒後，你應該讓 Claude Code 檢視一遍，確保沒有遺漏的部分。你可以使用這樣的提示：

```text
現在我希望你去審核實作計畫和實作細節檔案。在閱讀時，請專注於確定是否有一系列明顯需要執行的任務。因為我不確定這裡是否有足夠的資訊。例如，當我查看核心實作時，如果能在實作細節中參考適當的地方，讓它在執行核心實作或精煉的每個步驟時能找到資訊，這會很有用。
```

這有助於精煉實作計畫，並幫助你避免 Claude Code 在規劃週期中遺漏的潛在盲點。初步精煉完成後，在進入實作階段前，請 Claude Code 再次檢視清單。

你也可以要求 Claude Code（如果你已安裝 [GitHub CLI](https://docs.github.com/en/github-cli/github-cli)）從目前分支到 `main` 建立一個詳細描述的 pull request，以確保工作得到適當追蹤。

>[!NOTE]
>在讓 agent 實作之前，也值得提示 Claude Code 交叉檢查細節，看看是否有任何過度設計的部分（記住——它可能會過於積極）。如果存在過度設計的元件或決策，你可以要求 Claude Code 解決它們。確保 Claude Code 在建立計畫時遵循 [constitution](base/memory/constitution.md) 作為必須遵守的基礎原則。

### 步驟 5：實作

準備就緒後，指示 Claude Code 實作你的解決方案（包含範例路徑）：

```text
implement specs/002-create-taskify/plan.md
```

Claude Code 將立即開始行動並開始建立實作。

>[!IMPORTANT]
>Claude Code 將執行本地 CLI 指令（例如 `dotnet`）——請確保你的機器上已安裝這些指令。

實作步驟完成後，要求 Claude Code 嘗試執行應用程式並解決任何出現的建置錯誤。如果應用程式可以執行，但存在 Claude Code 無法透過 CLI 日誌直接取得的 _執行時錯誤_（例如，在瀏覽器日誌中呈現的錯誤），請將錯誤複製並貼上到 Claude Code 中，讓它嘗試解決。

</details>

---

## 🔍 疑難排解

### Linux 上的 Git Credential Manager

如果你在 Linux 上遇到 Git 認證問題，你可以安裝 Git Credential Manager：

```bash
#!/usr/bin/env bash
set -e
echo "Downloading Git Credential Manager v2.6.1..."
wget https://github.com/git-ecosystem/git-credential-manager/releases/download/v2.6.1/gcm-linux_amd64.2.6.1.deb
echo "Installing Git Credential Manager..."
sudo dpkg -i gcm-linux_amd64.2.6.1.deb
echo "Configuring Git to use GCM..."
git config --global credential.helper manager
echo "Cleaning up..."
rm gcm-linux_amd64.2.6.1.deb
```

## 👥 維護者

- Den Delimarsky ([@localden](https://github.com/localden))
- John Lam ([@jflam](https://github.com/jflam))

## 💬 支援

如需支援，請開啟 [GitHub issue](https://github.com/GitYCC/spec-kit/issues/new)。我們歡迎 bug 報告、功能請求，以及關於使用 Spec-Driven Development 的問題。

## 🙏 致謝

本專案大量受到 [John Lam](https://github.com/jflam) 的工作與研究影響並基於其之上。

## 📄 授權條款

本專案依據 MIT 開源授權條款授權。請參閱 [LICENSE](./LICENSE) 檔案以獲取完整條款。
