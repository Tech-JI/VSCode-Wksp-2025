# AI Coding Assistants in VS Code: Copilot & Claude

## GitHub Copilot

### 1. 注册 GitHub 账号

1. 注册 [GitHub](https://github.com/) 账号（邮箱注册），可以使用交大邮箱（学生认证也需要交大邮箱作为验证）
2. 点击右上角头像，进入设置界面（Settings）
3. 在左侧列表 **Access** 中，选中 **Password and authentication**，启用 **Two-factor authentication**（进行敏感操作时需要二次验证）
4. 在手机应用市场搜索 **Authenticator**，打开并扫码（验证码每隔 30 秒刷新）
5. 在 **Billing and plans** 中选择 **Payment information**（填写真实姓名与信息，需要与学生认证信息一致，中英文都可以，注册完学生认证后可删除）
   - **Address**: 800 DongChuan Rd, Min Hang District, Shanghai, China
   - **Postal Code**: 200240
6. 选择 **Emails**，确保至少添加交大邮箱

### 2. 学生认证

1. 进行 [学生认证](http://education.github.com/discount_requests/application)（**注意必须关闭代理/VPN!** 否则成功率较低，极有可能被秒拒）
2. 填写 Application 表单
3. 提供证明：推荐打开交我办，搜索 **本科生在读证明** 和 **学生卡**，放在一起拍照上传（不要开虚拟摄像头）
4. 等待审核（最快几个小时，通常 1-3 天），注意检查邮箱
5. 访问 [GitHub Education](https://github.com/education) 确认显示紫色权益
6. 最后，手动 [订阅 GitHub Pro](https://github.com/settings/copilot/features)

### 3. VS Code 上使用 Copilot

1. 在 **Extensions** 中搜索并安装：
   - **GitHub Copilot**
   - **GitHub Copilot Chat**
2. 点击 VS Code 左下角账号按钮，登录 GitHub 账号
3. 日常使用时，可以点击右下角 Copilot 图标，关闭自动补全功能
4. **考试时务必关闭 Copilot!**


## Claude Code

点击右上角 Claude 图标即可开始使用。

### 1. 使用官方 Claude API Key（需要 Anthropic 账户）

**注意**: 官方 API 成本较高，且存在账号封禁风险，不建议新手使用。

**使用步骤**:
1. 前往 [Anthropic Console](https://console.anthropic.com/) 获取 API Key
2. 在 VS Code 中配置 API Key（见下方配置方法）
3. API Provider 选择 `anthropic`

#### 什么是 API Key？

API Key 是一串唯一的密钥（类似密码），用于验证你的身份并授权访问 AI 模型服务。通过 API Key，Claude Code 可以调用远程 AI 模型进行代码补全、对话等功能。

#### 如何获取 API Key（以智谱 AI GLM 为例）

1. 访问 [智谱 AI 开放平台](https://open.bigmodel.cn/)
2. 点击右上角 **注册/登录**，使用手机号或邮箱注册账号
3. 登录后，点击右上角头像，进入 **个人中心**
4. 在左侧菜单选择 **API Keys** 或 **密钥管理**
5. 点击 **创建新的 API Key** 或 **生成密钥**
6. 复制生成的 API Key（通常格式为 `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.xxxxxxxx`）
7. **重要**: 妥善保管 API Key，不要泄露或提交到代码仓库中

**注意**: 智谱 AI 新用户通常会赠送一定额度的免费 tokens，用完后需要充值。

### 2. 使用本地或第三方兼容 API（不需要 Claude 账号）

支持使用 OpenAI 兼容的本地模型（如 Ollama、LM Studio）或第三方服务（如 OpenRouter）。

#### 配置方法一：通过终端配置 Claude Code

**1. 安装 Node.js**（已安装可跳过）

确保 Node.js 版本 ≥ 18.0

```bash
# Ubuntu / Debian 用户
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo bash -
sudo apt-get install -y nodejs
node --version

# macOS 用户
sudo xcode-select --install
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install node
node --version
```

**2. 安装 Claude Code**

```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

**遇到权限错误？** 如果出现 `EACCES` 或权限不足错误，选择以下方案之一：

<details>
<summary><b>方案 1：使用 nvm 管理 Node.js（官方推荐）</b></summary>

nvm 是 Node.js 官方推荐的版本管理工具，完全避免权限问题：

```bash
# 安装 nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# 重新加载配置
source ~/.zshrc  # 或 source ~/.bashrc

# 安装 Node.js LTS 版本
nvm install --lts
nvm use --lts

# 安装 Claude Code
npm install -g @anthropic-ai/claude-code
```

**优点**：
- 可以轻松切换 Node.js 版本
- 完全在用户目录下，无需 sudo
- Node.js 社区最推荐的管理方式

</details>

<details>
<summary><b>方案 2：修改 npm 全局目录（推荐）</b></summary>

不需要 `sudo`，最安全的方式：

```bash
# 创建全局包目录
mkdir -p ~/.npm-global

# 设置 npm 全局路径
npm config set prefix '~/.npm-global'

# 配置 PATH（根据你的 Shell 类型选择）
# 如果使用 zsh（默认 macOS 和部分 Linux）
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# 如果使用 bash
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# 重新安装
npm install -g @anthropic-ai/claude-code
```

</details>

<details>
<summary><b>方案 3：使用 sudo（不推荐，但最快）</b></summary>

```bash
sudo npm install -g @anthropic-ai/claude-code
```

**注意**：此方法会修改系统目录，可能导致权限混乱，不建议长期使用。

</details>

**3. 初始化配置**

在项目目录下运行：

```bash
cd your-project-folder
export ANTHROPIC_AUTH_TOKEN=sk-...
export ANTHROPIC_BASE_URL=...
claude
```

**4. 首次运行配置**

依次完成以下步骤：
1. 选择你喜欢的主题，按 `Enter`
2. 确认安全须知，按 `Enter`
3. 使用默认 Terminal 配置，按 `Enter`
4. 信任工作目录，按 `Enter`

配置完成后即可开始使用！



**5. 配置环境变量（推荐）**

为避免每次重复输入，可将环境变量写入配置文件（根据你的 Shell 类型选择 `.bashrc` 或 `.zshrc`，默认为 `.bashrc`）：

```bash
# 添加环境变量到配置文件
echo 'export ANTHROPIC_AUTH_TOKEN=sk-...' >> ~/.bashrc
echo 'export ANTHROPIC_BASE_URL=...' >> ~/.bashrc
echo 'export ANTHROPIC_AUTH_TOKEN=sk-...' >> ~/.zshrc
echo 'export ANTHROPIC_BASE_URL=...' >> ~/.zshrc
```

重启终端后，直接使用：

```bash
cd your-project-folder
claude
```

即可快速启动 Claude Code，无需重复配置环境变量。


#### 配置方法二：通过设置界面

1. 打开命令面板（`Ctrl+Shift+P` 或 `Cmd+Shift+P`）
2. 搜索 **"Claude Code: Settings"** 或 **"Preferences: Open Settings (UI)"**
3. 搜索 **"Claude Code"**，找到以下设置：
   - **API Provider**: 选择
     - `anthropic`（官方 Claude API）
     - `openrouter`（第三方聚合服务）
     - `openai-compatible`（自定义/本地模型）
   - **API Key**: 填入密钥
   - **Base URL**: 使用自定义端点时填写（如 `http://localhost:11434/v1`）
   - **Model**: 指定模型名称

#### 配置方法三：直接编辑 settings.json

按 `Ctrl+Shift+P` 或 `Cmd+Shift+P`，搜索 **"Preferences: Open User Settings (JSON)"**，添加：

**使用智谱 GLM 模型**:
```json
{
  "claudeCode.apiProvider": "openai-compatible",
  "claudeCode.apiKey": "your-glm-api-key",
  "claudeCode.baseUrl": "https://open.bigmodel.cn/api/paas/v4",
  "claudeCode.model": "glm-4-plus"
}
```

**使用本地 Ollama 模型**:
```json
{
  "claudeCode.apiProvider": "openai-compatible",
  "claudeCode.apiKey": "your-key",
  "claudeCode.baseUrl": "http://localhost:11434/v1",
  "claudeCode.model": "your-model-name"
}
```