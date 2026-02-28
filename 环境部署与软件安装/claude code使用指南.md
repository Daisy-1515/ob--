


# https://claudecode.tangshuang.net/

# 榨干 Claude Code 的 16 个实用小技巧（高端玩法，建议收藏！）

这几年 AI 编程工具越来越火，尤其是 Cursor、Claude Code 这种终端级 AI 编程助手，用好了真的能让程序员开发效率直接起飞。但很多同学用 AI 写代码，常常卡在“不会提问”、“不会拆需求”、“不会控制上下文”，只会傻傻提问。以下是高效利用 Claude Code 搞定开发的实用技巧。

---

## 1. 把你的需求说具体点

别再说：“修复这个漏洞”这么笼统的指令，尽量把你的需求说具体点。

错误示例：修复这个漏洞

正确示例：

> 修复用户登录时不输入密码出现的空指针错误

---

## 2. 把复杂的需求分步执行

- **小任务**：可以一次性把需求发给 AI，一次性出结果，效率更高。
    
- **大需求**：如果实现流程较长，建议拆解成小步骤。
    

**示例拆解**：

1. 给用户 API 创建一个新接口；
    
2. 给请求的字段添加必要的验证；
    
3. 编写这个接口的测试用例。
    

**原因**：AI 上下文有限制，代码量或记忆太长可能导致输出不全甚至被截断。分步最安全，每一步完成后都可以先 review/测试，再进行下一步。

---

## 3. 先理解项目代码再开动

在修改代码之前，先让 Claude 理解你的代码，这样才能更精准、高效地辅助开发和优化。

**常用指令**：

- 分析一下数据库表结构；
    
- 这个应用中的错误是如何处理的？
    

---

## 4. 学会用快捷键，节省时间

熟练使用快捷键可以大幅提升效率：

- 输入 `/`：查看所有斜杠命令。
    
- **上下方向键**：查看命令历史。
    
- **Tab 键**：进行命令快速补全。
    
- **Option + Enter**：换行。
    
- **Ctrl + C**：退出终端等。
    

---

## 5. 使用免授权模式

Claude Code 经常会在执行任务中途停下来请求授权，严重影响效率。可以使用参数启动“免授权模式”。

**启动命令**：

Bash

```
claude --dangerously-skip-permissions
```

_[图片描述：终端显示黄色的 WARNING 警告信息，提示该模式将允许容器无限制地访问互联网和执行命令，需要用户确认]_

确认后，终端下方会出现黄色的 **Bypassing Permissions** 提示，之后所有操作都不再需要手动授权。

进阶技巧（设置别名）：

为了避免每次输入长命令，可以设置 alias 别名（建议写入个人环境配置文件中永久生效）：

Bash

```
alias claude='claude --dangerously-skip-permissions'
```

---

## 6. 激活深度思考模式

可以使用 `think` 关键词来激活不同级别的深度思考模式：

`think` < `think hard` < `think harder` < `ultrathink`

- **注意**：级别越高，消耗的思考预算越多，`ultrathink` 最贵。
    
- **建议**：Max 套餐用户可尝试 `ultrathink`，否则请注意钱包。
    

**示例**：

```
1+1 ? ultrathink
```

_[图片描述：终端显示计算消耗成本，$0.0619，耗时 2分7.8秒]_

---

## 7. 输错指令，随时打断它工作

如果在 Claude Code 工作时发现命令描述错误，或者想让它停止，只需按 **ESC 键** 即可。

_[图片描述：终端显示 "Interrupted by user"（已被用户打断）]_

---

## 8. 发送图片处理

Claude Code 支持在命令行中发送图片并进行处理。

操作方法：

把图片粘贴到终端（Mac 使用 Ctrl + V 而不是 Command + V），并附带提示词。

**示例指令**：

- `[图片] 这个按钮样式错乱了，请修复`
    
- `这个图片显示了什么？`
    
- `这是错误的截图，是什么原因导致的？`
    
- `请根据这个图片的设计模型设计网页`
    

---

## 9. 恢复历史会话

Claude Code 提供两种方式恢复对话：

**非交互模式下（启动前）**：

- `claude --continue` 或 `claude -c`：自动继续最近的对话，无需提示。
    
- `claude --resume` 或 `claude -r`：显示历史对话选择器。
    

**交互模式下（会话中）**：

- 使用 `/resume` 命令恢复历史会话。
    

_[图片描述：终端显示历史会话列表，包含时间、消息摘要，用户可通过上下键选择要恢复的会话]_

---

## 10. 记忆管理

### 记忆文件介绍

Claude Code 提供三种记忆位置：

|**记忆类型**|**文件位置**|**用途说明**|**使用示例**|
|---|---|---|---|
|**项目记忆 (共享)**|`/CLAUDE.md`|项目团队共享的指令|项目架构、编码规范、常用工作流程|
|**用户记忆 (全局)**|`~/.claude/CLAUDE.md`|用于所有项目的个人偏好|代码风格偏好、个人工具快捷方式|
|**项目记忆 (本地)**|`/CLAUDE.local.md`|(已废弃)|你的沙箱地址、测试数据偏好等|

`CLAUDE.md` 类似于 Cursor 的 rules 文件，但更强大，可以包含常用 bash 命令、核心文件说明、代码风格指南等。Claude Code 启动时会从当前目录向上递归读取这些文件。

### 编辑记忆文件

使用 `/memory` 命令可在系统编辑器中打开记忆文件进行编辑。

_[图片描述：终端显示 Select memory to edit 菜单，列出 Project memory 和 User memory 供选择]_

**技巧**：在用户级记忆文件中添加“每次请用中文回答我”，之后所有交互都会默认使用中文。

---

## 11. 和 Git 进行交互

在 Claude Code 中，Git 操作可以变成对话形式，无需记忆繁琐命令。

**常用自然语言指令**：

- `我修改了哪些文件` -> 自动执行 `git status`。
    
- `用合理描述性信息提交我的更改` -> 自动执行 `git add` 和 `git commit`，并自动生成 Commit Message。
    
- `推送本分支到远程` -> 自动执行 `git push`。
    
- `创建一个新分支: feature/test` -> 自动执行 `git checkout -b`。
    
- `删除本分支并切换到 master 分支` -> 自动切换并删除分支。
    

---

## 12. 和 Linux 交互

可以把它当作 Linux 智能助手，无需记忆复杂参数。

**交互模式示例**：

> `列出行数最多的前3个 .java 文件`

Claude 会自动生成并执行复杂的 `find` / `xargs` / `wc` / `sort` / `head` 组合命令。

**非交互模式示例**：

> claude -p "列出行数最多的前3个 .java 文件"
> 
> （执行一次命令，列出结果后退出）

---

## 13. 模型切换

目前支持 **Claude Opus** 与 **Claude Sonnet** 两个模型。

**切换命令**：

Bash

```
/model
```

- **默认**：Claude Sonnet 3.5 (原文写作 Sonnet 4，可能是笔误或特定版本称呼)，推荐使用，体验与 Opus 差别不大但便宜很多（计费倍率仅为 1/5）。
    
- **注意**：只有 Max 用户支持切换到 Opus，Pro 用户仅支持 Sonnet。
    

---

## 14. 查看消耗情况

简单查看：

在会话中使用 /cost 命令。

[图片描述：显示 Total cost, Duration, Code changes, Token usage 等统计信息]

详细报表工具 (ccusage)：

官方推荐安装 ccusage 工具查看详细报表。

安装：

Bash

```
sudo npm install -g ccusage
```

查看日报表：

Bash

```
ccusage
```

_[图片描述：表格显示日期、模型、Input/Output Token 数及对应成本]_

查看特定日期：ccusage -s 20250701

实时查看：ccusage blocks --live

_注：Pro / Max 订阅用户按月计费，无需太关注单次消耗，但超过限额会不可用。_

---

## 15. 上下文压缩

Claude Code 提供 `/compact` 命令来手动压缩上下文。

**命令**：

Bash

```
/compact [可选的摘要指令]
```

作用：清除对话历史记录，但保留上下文中的摘要。

使用场景：

- 减少 Token 使用量。
    
- 虽然系统默认在上下文超过 95% 时自动压缩，但建议在上下文变大时定期手动执行。
    
- 配合 `clear` 命令重置上下文。
    

_[图片描述：终端右下角显示 Context left until auto-compact: 39%，提示剩余空间]_

---

## 16. 自定义快捷命令

你可以创建自定义命令来快速执行特定的 Prompt 或任务。

**语法**：`/<prefix>:<command-name> (arguments)`

**配置说明**：

- **用户级命令**：存放在 `~/.claude/commands`，前缀 `/user:`，所有项目可用。
    
- **项目级命令**：存放在当前项目 `.claude/commands`，前缀 `/project:`，仅当前项目可用。
    
- 支持 `$ARGUMENTS` 占位符。
    

**实战示例 1：项目性能分析**

1. 创建目录：`mkdir -p .claude/commands`
    
2. 创建命令文件 `optimize.md`，内容为："分析这个项目的性能，并提出三个具体的优化建议。"
    
3. 使用命令：`/project:optimize`
    

**实战示例 2：一键提交推送**

1. 创建命令文件 `~/.claude/commands/push.md`
    
2. 内容："用合理描述性信息提交所有变更文件，然后推送到远程仓库。"
    
3. 使用命令：`/user:push`


基于您上传的四张图片，整理了 Claude Code 的所有指令、原始说明及中文对照翻译如下：

### Claude Code 指令清单 (Command List)

| **指令 (Command)**                   | **英文说明 (Description)**                                                                                        | **中文对照 (Translation)**                   |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| **/add-dir**                       | Add a new working directory                                                                                   | 添加一个新的工作目录                               |
| **/agents**                        | Manage agent configurations                                                                                   | 管理 Agent（智能体）配置                          |
| **/clear** (reset, new)            | Clear conversation history and free up context                                                                | 清除对话历史记录并释放上下文空间                         |
| **/compact**                       | Clear conversation history but keep a summary in context. Optional: /compact [instructions for summarization] | 清除对话历史，但在上下文中保留摘要。可选：`/compact [摘要说明]`   |
| **/config** (theme)                | Open config panel                                                                                             | 打开配置面板                                   |
| **/context**                       | Visualize current context usage as a colored grid                                                             | 以彩色网格形式可视化当前上下文的使用情况                     |
| **/cost**                          | Show the total cost and duration of the current session                                                       | 显示当前会话的总成本和持续时间                          |
| **/doctor**                        | Diagnose and verify your Claude Code installation and settings                                                | 诊断并验证您的 Claude Code 安装和设置                |
| **/exit** (quit)                   | Exit the REPL                                                                                                 | 退出交互式终端（REPL）                            |
| **/export**                        | Export the current conversation to a file or clipboard                                                        | 将当前对话导出为文件或复制到剪贴板                        |
| **/help**                          | Show help and available commands                                                                              | 显示帮助信息和可用指令                              |
| **/hooks**                         | Manage hook configurations for tool events                                                                    | 管理工具事件的 Hook（钩子）配置                       |
| **/ide**                           | Manage IDE integrations and show status                                                                       | 管理 IDE 集成并显示状态                           |
| **/init**                          | Initialize a new CLAUDE.md file with codebase documentation                                                   | 初始化一个新的 `CLAUDE.md` 文件，包含代码库文档           |
| **/install-github-app**            | Set up Claude GitHub Actions for a repository                                                                 | 为仓库设置 Claude GitHub Actions              |
| **/login**                         | Switch Anthropic accounts                                                                                     | 切换 Anthropic 账号                          |
| **/logout**                        | Sign out from your Anthropic account                                                                          | 登出当前的 Anthropic 账号                       |
| **/mcp**                           | Manage MCP servers                                                                                            | 管理 MCP (Model Context Protocol) 服务器      |
| **/memory**                        | Edit Claude memory files                                                                                      | 编辑 Claude 的记忆文件                          |
| **/migrate-installer**             | Migrate from global npm installation to local installation                                                    | 从全局 npm 安装迁移到本地安装                        |
| **/model**                         | Set the AI model for Claude Code                                                                              | 设置 Claude Code 使用的 AI 模型                 |
| **/output-style**                  | Set the output style directly or from a selection menu                                                        | 直接设置输出样式或从菜单中选择                          |
| **/permissions** (allowed-tools)   | Manage allow & deny tool permission rules                                                                     | 管理工具的允许与拒绝权限规则                           |
| **/plugin** (plugins, marketplace) | Manage Claude Code plugins                                                                                    | 管理 Claude Code 插件                        |
| **/pr-comments**                   | Get comments from a GitHub pull request                                                                       | 获取 GitHub Pull Request (PR) 中的评论         |
| **/release-notes**                 | View release notes                                                                                            | 查看版本发布说明                                 |
| **/resume**                        | Resume a conversation                                                                                         | 恢复之前的对话                                  |
| **/review**                        | Review a pull request                                                                                         | 审查 Pull Request (PR)                     |
| **/rewind** (checkpoint)           | Restore the code and/or conversation to a previous point                                                      | 将代码和/或对话回滚（恢复）到之前的某个时间点                  |
| **/security-review**               | Complete a security review of the pending changes on the current branch                                       | 对当前分支上待处理的更改完成一次安全审查                     |
| **/status**                        | Show Claude Code status including version, model, account, API connectivity, and tool statuses                | 显示 Claude Code 状态，包括版本、模型、账号、API 连接和工具状态 |
| **/statusline**                    | Set up Claude Code's status line UI                                                                           | 设置 Claude Code 的状态栏界面                    |
| **/stickers**                      | Order Claude Code stickers                                                                                    | 订购 Claude Code 贴纸                        |
| **/tasks** (bashes)                | List and manage background tasks                                                                              | 列出并管理后台任务                                |
| **/terminal-setup**                | Install Shift+Enter key binding for newlines                                                                  | 安装 `Shift+Enter` 快捷键用于换行                 |
| **/todos**                         | List current todo items                                                                                       | 列出当前的待办事项 (Todo)                         |
| **/upgrade**                       | Upgrade to Max for higher rate limits and more Opus                                                           | 升级到 Max 计划以获得更高的速率限制和更多 Opus 模型使用额度      |
| **/usage**                         | Show plan usage limits                                                                                        | 显示套餐使用限额                                 |
| **/vim**                           | Toggle between Vim and Normal editing modes                                                                   | 在 Vim 编辑模式和普通编辑模式之间切换                    |

# 模板

## Claude Code 最佳实践：CLAUDE.md 分层架构与工作流
#### 1. 核心理念：为什么需要分层架构？

CLAUDE.md 的作用：

它是每次会话自动注入上下文的“入职手册”，赋予无状态 LLM 对项目的认知 。

痛点：

如果将所有配置（如 Nginx、Webpack、MCP 调用）都塞进主文件，会导致上下文过载，影响模型专注度 。

灵感来源：

借鉴 Skills 的“渐进式披露”设计——主入口仅保留精简描述与触发条件，详细内容分散在子文档中按需加载 。

#### 2. 目录结构模板

Bash

```
.claude/
├── CLAUDE.md            # Core principles (~60 lines)
└── docs/
    ├── nginx.md         # Task-specific documentation
    ├── dev-server.md
    ├── mcp-*.md         # MCP tool references
    └── ...
```



#### 3. 分层架构的优势

1. **上下文清爽**：主文件仅约 60 行，专注于通用信息（环境、技术栈、风格、索引）。具体细节（如 Nginx SNI 分流）隔离在子文档中，只有在相关任务触发时才被读取 。
    
2. **迭代便捷**：新增功能只需添加子文档并在索引表中增加一行，无需改动主文件，避免主文件变成“补丁堆”。
    
3. **关注点分离**：完全不相关的逻辑（如 Nginx 配置与 Codex MCP 调用）被物理隔离，易于维护 。
    

#### 4. 实践经验与 Tips

- **保持精简**：主文件控制在 60 行以内 。
    
- **绝对路径**：文档引用必须使用绝对路径（如 `/root/.claude/docs/nginx.md`），避免 Claude 在不同工作目录下找不到文件 。
    
- **子文档自包含**：每个子文档应能独立阅读，不依赖主文件上下文 。
    

#### 5. CLAUDE.md 完整模板参考

以下是作者实际使用的配置，包含 VPS 环境、技术栈、代码哲学及三方协作流程 。

Markdown

```
# VPS 开发环境

## 基本信息
| 项目 | 值 |
|------|-----|
| OS | Debian 13 (trixie) |
| CPU | 2 vCPU |
| RAM | 2 GB |
| Disk | 15 GB |
| IPv4 | ** |
| 域名 | ** |

轻量无图形 root 开发环境。

## 技术栈
- 容器: docker compose
- Python: uv

## 代码哲学
避免 AI slop，写人类会写的代码：
- 不加多余注释，保持文件风格一致
- 不加异常的防御性检查 / try-catch（尤其在已验证路径）
- 不用 `any` 绕过类型问题
- 精简高效，仅做针对性改动

## 工作原则
1. **语义理解**: 以 serena 为基础工具，符号级代码操作优于文本搜索
2. **三方协作**: codex 审查逻辑/定位 bug，gemini 设计前端 UI
3. **交流语言**: 与用户中文，与 codex/gemini 英文

## 三方协作流程
  需求分析
  → 告知 codex/gemini 原始需求 + 初始思路
  → 迭代讨论
  ↓
  编码前
  → 向 codex(后端) 或 gemini(前端) 索要代码原型
  ↓
  实施
  → 以原型为参考重写为生产级代码
  ↓
  完成后
  → codex review 代码改动

  **注意**: codex/gemini 仅供参考，保持独立思考和质疑。

## 文档索引
| 主题 | 路径 | 说明 |
|------|------|------|
| Nginx | `/root/.claude/docs/nginx.md` | SNI 分流架构 |
| 开发服务器 | `/root/.claude/docs/dev-server.md` | ** |
| Codex | `/root/.claude/docs/mcp-codex.md` | 后端/逻辑/Debug |
| Gemini | `/root/.claude/docs/mcp-gemini.md` | 前端/UI/规划 |
| Serena | `/root/.claude/docs/mcp-serena.md` | LSP 符号级操作 |
| Chrome | `/root/.claude/docs/mcp-chrome.md` | 浏览器自动化 |
| 前端部署 | `/root/.claude/docs/frontend-deploy.md` | React/Vite 构 |
```

# 安装指南
这是一个为您整理的、专门针对 **Obsidian** 优化的 Markdown 格式。

您可以直接复制下面的内容，在 Obsidian 中新建一篇笔记粘贴即可。我使用了 Obsidian 支持的 **Callouts (警告/提示框)**、**代码块**和**元数据 (Frontmatter)** 格式，以便于您建立索引和阅读。

---



```

curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo bash -
sudo apt-get update
sudo apt-get install -y nodejs
node --version
```


### macOS 系统

推荐使用 Homebrew 安装：

Bash

```
# 1. 安装 Xcode 命令行工具 (如已安装可跳过)
sudo xcode-select --install

# 2. 安装 Homebrew (如已安装可跳过)
/bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"

# 3. 安装 Node.js
brew install node

# 4. 验证版本
node --version
```

### Windows 系统

_请前往 Node.js 官网下载安装包或使用 `winget install OpenJS.NodeJS`，安装后在终端验证 `node --version` 即可。_

---

## 2. 安装 Claude Code CLI

使用 npm 全局安装：

Bash

```
npm install -g @anthropic-ai/claude-code
```

验证安装是否成功：

Bash

```
claude --version
# 输出版本号即代表成功
```

---

## 3. API 凭据配置

在使用前需要配置身份验证。

1. **获取 Token**：登录 [Anthropic 开发者平台](https://console.anthropic.com/)，在 "API Keys" 页面生成。
    
    - 复制以 `sk-` 开头的 Key。
        
    - _建议：使用不限额度的 Token 以避免中断。_
        
2. **准备中转地址** (可选)：如果您使用国内中转服务，请准备好 `ANTHROPIC_BASE_URL`。
    

---

## 4. 快速启动与首次交互

### 单次运行 (临时环境变量)

在项目根目录下执行：

Bash

```
cd your-project-folder

# 替换为您的实际 Key 和 URL
export ANTHROPIC_AUTH_TOKEN=sk-xxxxxxxxxxxxxxxx
export ANTHROPIC_BASE_URL=https://您的中转API地址

# 启动 Claude
claude
```

### 首次运行交互向导

第一次启动时，CLI 会引导进行以下配置：

- [ ] **选择主题** (Select Theme) → 按 `Enter`
    
- [ ] **安全须知** (Safety Review) → 阅读并确认 `Enter`
    
- [ ] **Terminal 配置** → 默认即可 `Enter`
    
- [ ] **工作目录授权** → 确认授权 `Enter`
    

---

## 5. 进阶：持久化环境变量 (推荐)

为避免每次都要输入 export 命令，建议写入 Shell 配置文件。

> [!TIP] 应该修改哪个文件？
> 
> - **macOS/Linux (Bash)**: 修改 `~/.bash_profile` 或 `~/.bashrc`
>     
> - **macOS (Zsh)**: 修改 `~/.zshrc` (较新版 macOS 默认)
>     

请将以下内容添加到您的配置文件末尾：

Bash

```
# Claude Code Configuration
export ANTHROPIC_AUTH_TOKEN=sk-您的真实Token
export ANTHROPIC_BASE_URL=https://您的API地址
```

**快速写入命令 (复制即可用)：**

Bash

```
# Zsh 用户 (macOS 默认)
echo -e '\nexport ANTHROPIC_AUTH_TOKEN=sk-...' >> ~/.zshrc
echo -e '\nexport ANTHROPIC_BASE_URL=https://你的API地址' >> ~/.zshrc
source ~/.zshrc

# Bash 用户
echo -e '\nexport ANTHROPIC_AUTH_TOKEN=sk-...' >> ~/.bashrc
echo -e '\nexport ANTHROPIC_BASE_URL=https://你的API地址' >> ~/.bashrc
source ~/.bashrc
```

配置完成后，您只需进入项目目录输入 `claude` 即可直接使用。

---

## 6. 扩展资源

> [!INFO] 关注更新
> 
> 建议关注官方 GitHub 仓库以获取最新功能：@anthropic-ai/claude-code

```

### 💡 如何在 Obsidian 中使用：
1.  **复制**上面的代码块内容。
2.  在 Obsidian 中按下 `Ctrl+N` (或 `Cmd+N`) 新建笔记。
3.  **粘贴**内容。
4.  (可选) 如果您安装了 *Templater* 或 *Dataview* 插件，顶部的 YAML Frontmatter (`---` 包裹的部分) 将自动被识别，方便您后续通过标签检索。
```