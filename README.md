# 🚀 OpenAI / ChatGPT 全自动注册机 & Token 提取器

![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![curl_cffi](https://img.shields.io/badge/curl__cffi-Chrome%20120-success.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

这是一个高度现代化的 OpenAI 自动化注册脚本。本项目不仅实现了全自动化的 ChatGPT 账号注册流程，还集成了对 OpenAI 最新反爬机制（Sentinel）的绕过方案，并能够通过拦截原生 OAuth2 授权流，直接为你提取出最核心的 `access_token` 和 `refresh_token`。

## ✨ 核心特性

* 📧 **全自动邮箱对接**：内置 `mail.tm` 临时邮箱 API 接口，动态获取可用域名，自动轮询并提取验证码。
* 🛡️ **无视 TLS 指纹检测**：底层全面采用 `curl_cffi`，完美伪装 Chrome 120 浏览器指纹，有效绕过 Cloudflare 盾和基础网络拦截。
* 🔑 **突破 Sentinel 风控**：针对 OpenAI 最新的机器验证机制，在关键请求前自动向 `sentinel.openai.com` 申请并携带合规的防护 Token (`authorize_continue` & `oauth_create_account`)。
* 🚀 **深度 Token 提取 (OAuth2 PKCE)**：自动生成状态码和挑战码 (Code Challenge)，模拟真实用户环境选择默认工作区 (Workspace)，并通过拦截底层的跳转重定向，强行提取出包括 `access_token` 和 `refresh_token` 在内的完整授权配置。
* 📁 **结构化资产管理**：注册成功后，自动在本地创建 `tokens` 文件夹，将完整的 Token 信息保存为 JSON 文件，并将明文账密按 `账号----密码` 格式追加保存。

## 📷 截图
<details>
<summary>📸 点击查看截图</summary>
<br>
   
![Screenshot](Screenshot_2026-03-18-01-16-05-39_84d3000e3f4017145260f7618db1d683.jpg)

</details>

## 🛠️ 环境准备与安装

1. **环境要求**：需要 Python 3.8 或更高版本。
2. **克隆项目**：
   ```bash
   git clone https://github.com/你的用户名/你的项目名.git
   cd 你的项目名
   ```
3. **安装依赖**：
   本项目高度依赖 `curl_cffi` 库，请使用 pip 进行安装：
   ```bash
   pip install curl_cffi
   ```

## 💻 使用说明

脚本提供了极其简单的命令行调用方式，支持无限循环注册和代理配置。

### 1. 基础运行 (无限循环注册)
脚本默认会一直循环运行，每次注册完成后随机休息 5-15 秒，适合挂机批量生成。
```bash
python chatgpt.py
```

### 2. 单次运行测试 (`--once`)
如果你只想测试注册一个账号，请带上 `--once` 参数：
```bash
python chatgpt.py --once
```

### 3. 配置本地代理 (`--proxy`)
由于 OpenAI 对网络环境有严格要求，你可以直接通过命令行传入代理地址（支持 HTTP/HTTPS/SOCKS5）：
```bash
python chatgpt.py --proxy "http://127.0.0.1:7890"

# 或搭配单次运行：
python chatgpt.py --once --proxy "http://127.0.0.1:7890"
```

## 📂 产出文件说明

注册成功的账号数据会自动保存在脚本同级目录的 `tokens/` 文件夹下：

* `accounts.txt`：汇总保存所有的账号密码，格式为 `email----password`，方便直接复制到第三方发卡平台或客户端使用。
* `token_[email]_[timestamp].json`：详细的授权文件，包含您的 `access_token`、`refresh_token`、`id_token` 以及过期时间等底层通讯秘钥。

## ⚠️ 免责声明 (Disclaimer)

1. 本项目代码仅供**编程学习与学术研究**（如探讨 OAuth2 授权机制、TLS 指纹安全及对抗技术）使用。
2. 请勿将本项目用于任何非法用途、大规模恶意注册或违反平台服务条款（TOS）的商业行为。
3. OpenAI 的接口风控策略经常变动，不保证代码的永久可用性。因使用本脚本带来的任何封号风险或法律纠纷，由使用者自行承担，与开发者无关。

---
*If you find this project helpful, please consider giving it a ⭐!*
