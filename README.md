<div align="center">
    <img src="./media/logo_small.webp"/>
    <h1>🌱 Spec Kit</h1>
    <h3><em>更快速地建構高品質軟體。</em></h3>
</div>

<p align="center">
    <strong>透過 Spec-Driven Development 的協助，讓組織能夠專注於產品情境，而非撰寫同質化程式碼。</strong>
</p>

[![Release](https://github.com/github/spec-kit/actions/workflows/release.yml/badge.svg)](https://github.com/github/spec-kit/actions/workflows/release.yml)

---

## 目錄

- [🤔 什麼是 Spec-Driven Development？](#-什麼是-spec-driven-development)
- [⚡ 開始使用](#-開始使用)
- [📽️ 影片概覽](#️-影片概覽)
- [🔧 Specify CLI Reference](#-specify-cli-reference)
- [📚 核心理念](#-核心理念)
- [🌟 開發階段](#-開發階段)
- [🎯 實驗目標](#-實驗目標)
- [🔧 前置需求](#-前置需求)
- [📖 深入了解](#-深入了解)
- [📋 詳細流程](#-詳細流程)
- [🔍 疑難排解](#-疑難排解)
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
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

### 2. 建立 spec

使用 **`/specify`** 指令來描述你想要建構的內容。專注於**什麼**和**為什麼**，而非技術 stack。

```bash
/specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.
```

### 3. 建立技術實作計畫

使用 **`/plan`** 指令來提供你的技術 stack 和架構選擇。

```bash
/plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.
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
Develop Taskify, a team productivity platform. It should allow users to create projects, add team members,
assign tasks, comment and move tasks between boards in Kanban style. In this initial phase for this feature,
let's call it "Create Taskify," let's have multiple users but the users will be declared ahead of time, predefined.
I want five users in two different categories, one product manager and four engineers. Let's create three
different sample projects. Let's have the standard Kanban columns for the status of each task, such as "To Do,"
"In Progress," "In Review," and "Done." There will be no login for this application as this is just the very
first testing thing to ensure that our basic features are set up. For each task in the UI for a task card,
you should be able to change the current status of the task between the different columns in the Kanban work board.
You should be able to leave an unlimited number of comments for a particular card. You should be able to, from that task
card, assign one of the valid users. When you first launch Taskify, it's going to give you a list of the five users to pick
from. There will be no password required. When you click on a user, you go into the main view, which displays the list of
projects. When you click on a project, you open the Kanban board for that project. You're going to see the columns.
You'll be able to drag and drop cards back and forth between different columns. You will see any cards that are
assigned to you, the currently logged in user, in a different color from all the other ones, so you can quickly
see yours. You can edit any comments that you make, but you can't edit comments that other people made. You can
delete any comments that you made, but you can't delete comments anybody else made.
```

After this prompt is entered, you should see Claude Code kick off the planning and spec drafting process. Claude Code will also trigger some of the built-in scripts to set up the repository.

Once this step is completed, you should have a new branch created (e.g., `001-create-taskify`), as well as a new specification in the `specs/001-create-taskify` directory.

The produced specification should contain a set of user stories and functional requirements, as defined in the template.

At this stage, your project folder contents should resemble the following:

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

### **STEP 2:** Functional specification clarification

With the baseline specification created, you can go ahead and clarify any of the requirements that were not captured properly within the first shot attempt. For example, you could use a prompt like this within the same Claude Code session:

```text
For each sample project or project that you create there should be a variable number of tasks between 5 and 15
tasks for each one randomly distributed into different states of completion. Make sure that there's at least
one task in each stage of completion.
```

You should also ask Claude Code to validate the **Review & Acceptance Checklist**, checking off the things that are validated/pass the requirements, and leave the ones that are not unchecked. The following prompt can be used:

```text
Read the review and acceptance checklist, and check off each item in the checklist if the feature spec meets the criteria. Leave it empty if it does not.
```

It's important to use the interaction with Claude Code as an opportunity to clarify and ask questions around the specification - **do not treat its first attempt as final**.

### **STEP 3:** Generate a plan

You can now be specific about the tech stack and other technical requirements. You can use the `/plan` command that is built into the project template with a prompt like this:

```text
We are going to generate this using .NET Aspire, using Postgres as the database. The frontend should use
Blazor server with drag-and-drop task boards, real-time updates. There should be a REST API created with a projects API,
tasks API, and a notifications API.
```

The output of this step will include a number of implementation detail documents, with your directory tree resembling this:

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

Check the `research.md` document to ensure that the right tech stack is used, based on your instructions. You can ask Claude Code to refine it if any of the components stand out, or even have it check the locally-installed version of the platform/framework you want to use (e.g., .NET).

Additionally, you might want to ask Claude Code to research details about the chosen tech stack if it's something that is rapidly changing (e.g., .NET Aspire, JS frameworks), with a prompt like this:

```text
I want you to go through the implementation plan and implementation details, looking for areas that could
benefit from additional research as .NET Aspire is a rapidly changing library. For those areas that you identify that
require further research, I want you to update the research document with additional details about the specific
versions that we are going to be using in this Taskify application and spawn parallel research tasks to clarify
any details using research from the web.
```

During this process, you might find that Claude Code gets stuck researching the wrong thing - you can help nudge it in the right direction with a prompt like this:

```text
I think we need to break this down into a series of steps. First, identify a list of tasks
that you would need to do during implementation that you're not sure of or would benefit
from further research. Write down a list of those tasks. And then for each one of these tasks,
I want you to spin up a separate research task so that the net results is we are researching
all of those very specific tasks in parallel. What I saw you doing was it looks like you were
researching .NET Aspire in general and I don't think that's gonna do much for us in this case.
That's way too untargeted research. The research needs to help you solve a specific targeted question.
```

>[!NOTE]
>Claude Code might be over-eager and add components that you did not ask for. Ask it to clarify the rationale and the source of the change.

### **STEP 4:** Have Claude Code validate the plan

With the plan in place, you should have Claude Code run through it to make sure that there are no missing pieces. You can use a prompt like this:

```text
Now I want you to go and audit the implementation plan and the implementation detail files.
Read through it with an eye on determining whether or not there is a sequence of tasks that you need
to be doing that are obvious from reading this. Because I don't know if there's enough here. For example,
when I look at the core implementation, it would be useful to reference the appropriate places in the implementation
details where it can find the information as it walks through each step in the core implementation or in the refinement.
```

This helps refine the implementation plan and helps you avoid potential blind spots that Claude Code missed in its planning cycle. Once the initial refinement pass is complete, ask Claude Code to go through the checklist once more before you can get to the implementation.

You can also ask Claude Code (if you have the [GitHub CLI](https://docs.github.com/en/github-cli/github-cli) installed) to go ahead and create a pull request from your current branch to `main` with a detailed description, to make sure that the effort is properly tracked.

>[!NOTE]
>Before you have the agent implement it, it's also worth prompting Claude Code to cross-check the details to see if there are any over-engineered pieces (remember - it can be over-eager). If over-engineered components or decisions exist, you can ask Claude Code to resolve them. Ensure that Claude Code follows the [constitution](base/memory/constitution.md) as the foundational piece that it must adhere to when establishing the plan.

### STEP 5: Implementation

Once ready, instruct Claude Code to implement your solution (example path included):

```text
implement specs/002-create-taskify/plan.md
```

Claude Code will spring into action and will start creating the implementation.

>[!IMPORTANT]
>Claude Code will execute local CLI commands (such as `dotnet`) - make sure you have them installed on your machine.

Once the implementation step is done, ask Claude Code to try to run the application and resolve any emerging build errors. If the application runs, but there are _runtime errors_ that are not directly available to Claude Code through CLI logs (e.g., errors rendered in browser logs), copy and paste the error in Claude Code and have it attempt to resolve it.

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

如需支援，請開啟 [GitHub issue](https://github.com/github/spec-kit/issues/new)。我們歡迎 bug 報告、功能請求，以及關於使用 Spec-Driven Development 的問題。

## 🙏 致謝

本專案大量受到 [John Lam](https://github.com/jflam) 的工作與研究影響並基於其之上。

## 📄 授權條款

本專案依據 MIT 開源授權條款授權。請參閱 [LICENSE](./LICENSE) 檔案以獲取完整條款。
