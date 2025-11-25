# Git 扩展与工具

## VS Code 内置 Git 功能

VS Code 提供了强大的 Git 支持，无需安装额外插件即可完成大部分 Git 操作。

### Source Control 视图

点击左侧活动栏的 **Source Control** 图标（或按 `Ctrl+Shift+G`），可以看到**CHANGES**: 显示所有未提交的文件更改

**CHANGES** 栏目中有 **Code Review** 按钮， 可以调用copilot检查未提交的代码，并提出意见（类似于Github的merge信息）。

**CHANGES** 栏目下有 **Changes** 子栏目，可以点击文件对比更改内容，选择丢弃更改或者提交至暂存区，然后直接输入commit的信息，实现无终端git操作。

另外还有 **GRAPH** 栏目， 提供可视化的git log。点击具体commit可以显示每次提交的内容，栏目中存在一系列按钮，支持远端管理操作。

### 核心功能

可以直接通过按钮完成 Git 操作，无需使用终端命令。

- **生成 Commit Message**: 在 CHANGES 栏目点击图标，调用 Copilot 根据代码变更自动生成提交信息
- **Diff 查看**: 点击文件名可并排对比修改前后的差异
- **部分暂存**: 在 Diff 视图中右键选中代码行，选择 **"Stage Selected Ranges"** 可只暂存部分修改
- **Timeline 视图**: 在文件资源管理器底部显示当前文件的 Git 历史记录
- **分支管理**: 左下角显示当前分支名，点击可快速切换或创建分支

## 推荐 Git 插件

### 1. Git Graph

**功能**: 提供可视化的 Git 提交历史图，清晰展示分支和合并关系。

**安装与使用**:
1. 在 **Extensions** 中搜索并安装 **Git Graph**
2. 安装后，在 **Source Control** 视图的 **CHANGES** 栏目上方会出现 **View Git Graph** 按钮
3. 点击按钮打开图形化界面

**核心功能**:
- 可视化查看所有分支的提交历史和拓扑结构
- 右键提交可进行 **Cherry-pick**、**Revert**、**Reset** 等高级操作
- 直接在图中创建、删除、合并分支
- 点击提交节点查看详细信息和文件变更列表

**使用技巧**:
- 支持搜索提交记录（按作者、消息、SHA 等）
- 可以自定义显示的分支和日期范围


### 2. GitLens

**功能**: 最强大的 Git 增强工具，提供代码归属、历史追踪等高级功能。

**安装与使用**:
1. 在 **Extensions** 中搜索并安装 **GitLens**
2. 安装后，**Source Control** 视图中会出现 **GITLENS** 栏目
3. **GITLENS** 栏目，可用于管理提交内容和生成提交信息，比如branch按钮可以对比不同branch的区别，remote可以管理不同的远端仓库。
4. **CHANGES** 栏目出现 **GitLens** 按钮，可以结合Copilot自动生成Commit Message，并且比较Commits产生的所有更改。

**核心功能**:
- **Inline Blame**: 在代码行末实时显示最后修改者和时间（可在设置中开关）
- **File History**: 查看文件的完整修改历史和每次变更内容
- **Hovers**: 鼠标悬停在代码上显示详细的 commit 信息、作者和变更时间
- **Compare**: 比较不同提交、分支、工作区之间的差异
- **Repositories 视图**: 可视化所有分支的 commit 记录和文件更改
- **Remotes 管理**: 管理和查看远程仓库连接
- **生成 Commit Message**: 在 **CHANGES** 栏目点击 **GitLens** 按钮，根据代码变更自动生成提交信息（需要 Copilot）

**使用技巧**:
- 点击代码行末的 blame 信息可快速跳转到对应 commit
- 使用命令面板（`Ctrl+Shift+P`）搜索 "GitLens" 查看所有可用命令
- 在设置中搜索 "GitLens" 可自定义显示方式和行为


### 3. Conventional Commits

**功能**: 帮助生成符合 Conventional Commits 规范的提交消息，提升项目提交历史的可读性。

**安装与配置**:

1. **安装插件**
   - 在 **Extensions** 中搜索并安装 **"Conventional Commits"**（推荐 `vivaxy.vscode-conventional-commits`）

2. **自定义配置（可选）**
   - 在 `settings.json` 中添加自定义 scope 列表：

   ```jsonc
   {
     // 自定义 scope 列表
     "conventionalCommits.scopes": [
       "ex1",
       "ex2",
       "p1"
       // 添加其他 scope
     ]
   }
   ```

**使用方式**:

1. **方法一**: 打开命令面板（`Ctrl+Shift+P` 或 `Cmd+Shift+P`），输入 **"Conventional Commits"**，按 `Enter`
2. **方法二**: 在 **Source Control** 视图中，点击提交消息输入框旁的 **圆圈符号**
3. 在弹出的快速选择窗口中依次选择或填写：
   - **Type**: 提交类型（如 `feat`、`fix`、`docs` 等）
   - **Scope**: 影响范围（可选）
   - **Emoji**: 表情符号（可选）
   - **Subject**: 简短描述

插件会自动生成符合规范的提交消息，例如：`feat(auth): add login feature`

**常用 Type 类型**:
- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档更新
- `style`: 代码格式调整
- `refactor`: 代码重构
- `test`: 测试相关
- `chore`: 构建/工具链相关
