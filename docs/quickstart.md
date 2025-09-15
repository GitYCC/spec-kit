# 快速入門指南

本指南將幫助你使用 Spec Kit 開始 Spec-Driven Development。

> 新功能：所有自動化 script 現在都提供 Bash（`.sh`）和 PowerShell（`.ps1`）兩種變體。`specify` CLI 會根據作業系統自動選擇，除非你傳遞 `--script sh|ps`。

## 4 步驟流程

### 1. 安裝 Specify

根據你使用的 coding agent 來初始化你的專案：

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

明確選擇 script 類型（可選）：
```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME> --script ps  # 強制 PowerShell
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME> --script sh  # 強制 POSIX shell
```

### 2. 建立 Spec

使用 `/specify` 指令來描述你想要建構的內容。專注於**什麼**和**為什麼**，而非技術 stack。

```bash
/specify Build an application that can help me organize my photos in separate photo albums. Albums are grouped by date and can be re-organized by dragging and dropping on the main page. Albums are never in other nested albums. Within each album, photos are previewed in a tile-like interface.
```

### 3. 建立技術實作計畫

使用 `/plan` 指令來提供你的技術 stack 和架構選擇。

```bash
/plan The application uses Vite with minimal number of libraries. Use vanilla HTML, CSS, and JavaScript as much as possible. Images are not uploaded anywhere and metadata is stored in a local SQLite database.
```

### 4. 分解並實作

使用 `/tasks` 來建立可執行的任務清單，然後請你的 agent 實作該功能。

## 詳細範例：建構 Taskify

以下是建構團隊生產力平台的完整範例：

### 步驟 1：使用 `/specify` 定義需求

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

### 步驟 2：精練規格文件

在初始規格文件建立後，澄清任何遺漏的需求：

```text
For each sample project or project that you create there should be a variable number of tasks between 5 and 15
tasks for each one randomly distributed into different states of completion. Make sure that there's at least
one task in each stage of completion.
```

同時驗證規格文件檢查清單：

```text
Read the review and acceptance checklist, and check off each item in the checklist if the feature spec meets the criteria. Leave it empty if it does not.
```

### 步驟 3：使用 `/plan` 產生技術計畫

明確說明你的技術 stack 和技術需求：

```text
We are going to generate this using .NET Aspire, using Postgres as the database. The frontend should use
Blazor server with drag-and-drop task boards, real-time updates. There should be a REST API created with a projects API,
tasks API, and a notifications API.
```

### 步驟 4：驗證並實作

讓你的 AI agent 審核實作計畫：

```text
Now I want you to go and audit the implementation plan and the implementation detail files.
Read through it with an eye on determining whether or not there is a sequence of tasks that you need
to be doing that are obvious from reading this. Because I don't know if there's enough here.
```

最後，實作解決方案：

```text
implement specs/002-create-taskify/plan.md
```

## 關鍵原則

- **明確說明**你要建構什麼以及為什麼
- **不要在規格文件階段專注於技術 stack**
- **在實作之前這代式精練**你的規格文件
- **在開始編碼前驗證**計畫
- **讓 AI agent 處理**實作細節

## 下一步

- 閱讀完整的方法論以獲取深入指導
- 查看 repository 中更多範例
- 在 GitHub 上探索原始碼
