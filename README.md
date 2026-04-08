<!-- omit in toc -->
# Nemoclaw

<!-- omit in toc -->
## Table of contents

- [Document](#document)
- [Contribute](#contribute)
  - [定期同步上游](#定期同步上游)
  - [日常開發流程](#日常開發流程)
- [Prerequisite](#prerequisite)
  - [開發環境（跑測試 / lint / build）](#開發環境跑測試--lint--build)
  - [執行 App（啟動 OpenClaw agent sandbox）](#執行-app啟動-openclaw-agent-sandbox)
- [Setup](#setup)
  - [Step 1：安裝 Ollama 與拉取模型](#step-1安裝-ollama-與拉取模型)
  - [Step 2：安裝 OpenShell](#step-2安裝-openshell)
  - [Step 3：安裝 npm 依賴並讓 CLI 可用](#step-3安裝-npm-依賴並讓-cli-可用)
  - [Step 4：執行 onboard](#step-4執行-onboard)
  - [Step 5：連線到 sandbox](#step-5連線到-sandbox)
- [Reference](#reference)

## Document

- [NVIDIA / NemoClaw - README.md](./nvidia-nemoclaw.md)

## Contribute

本專案 fork 自 `NVIDIA/NemoClaw`，`origin/main` 作為上游鏡像，會不定期透過 GitHub Sync fork 更新。開發完成後經 `release-NAME` 測試驗收，再合併至 `main-NAME`。

```mermaid
flowchart TD
    U["NVIDIA/NemoClaw (main)"]
    OM["origin/main (上游鏡像)"]
    D["dev-NAME"]
    R["release-NAME (穩定測試區)"]
    M["main-NAME (正式發佈區)"]
    A["編輯檔案"] --> B["/commit"] --> D
    U -->|"GitHub Sync fork"| OM
    OM -->|"git merge origin/main"| D
    D -->|"PR 1：push & Pull Request"| R
    R -->|"PR 2：驗收通過後 Pull Request"| M
```

### 定期同步上游

```bash
# 1. 至 GitHub 點 Sync fork，更新 origin/main
# 2. 在 dev-NAME 執行
git fetch origin
git merge origin/main
```

### 日常開發流程

```bash
# 1. 編輯檔案後 commit
/commit

# 2. push 至個人 fork
git push origin dev-NAME

# 3. 至 GitHub 建立 PR 1，將 dev-NAME 合併至 release-NAME（測試驗收）

# 4. 驗收通過後，建立 PR 2，將 release-NAME 合併至 main-NAME
```

## Prerequisite

### 開發環境（跑測試 / lint / build）

| 項目 | 最低版本 |
|------|----------|
| Node.js | 22.16+ |
| npm | 10+ |
| Docker | 任意支援版本，需正在運行 |
| uv | 任意版本（Python 依賴管理） |
| Python | 3.11+（blueprint 與文件建置用） |

```bash
npm install
cd nemoclaw && npm install && npm run build && cd ..
cd nemoclaw-blueprint && uv sync && cd ..
```

### 執行 App（啟動 OpenClaw agent sandbox）

除上述開發環境外，還需要：

| 項目 | 說明 |
|------|------|
| OpenShell | NVIDIA agent runtime，透過安裝腳本取得 |
| CPU / RAM / Disk | 最低 4 vCPU / 8 GB RAM / 20 GB 磁碟空間 |
| Container runtime | Linux 上使用 Docker 或 Podman |

```bash
# 安裝後透過 onboard 引導建立 sandbox
node bin/nemoclaw.js onboard
```

## Setup

### Step 1：安裝 Ollama 與拉取模型

```bash
# 安裝 Ollama
curl -fsSL https://ollama.com/install.sh | sh

# 啟動服務（若未自動啟動）
ollama serve &

# 拉取 qwen3.5:27b 模型（約 17 GB）
ollama pull qwen3.5:27b
```

> **記憶體提示**：`qwen3.5:27b` 需要約 17 GB RAM。若記憶體不足，可改用 `qwen3.5:9b`（6.6 GB）或 `qwen3.5:4b`（3.4 GB）。

### Step 2：安裝 OpenShell

```bash
bash scripts/install-openshell.sh
```

確認安裝成功：

```bash
openshell --version
```

### Step 3：安裝 npm 依賴並讓 CLI 可用

> **注意**：`npm install` 的 `prepare` 腳本會移除 devDependency，需加 `--ignore-scripts`。

```bash
# 安裝全部依賴（跳過 prepare 腳本）
npm install --ignore-scripts

# 手動補做 CLI build
npx tsc -p tsconfig.src.json

# 讓 nemoclaw 指令全域可用
npm link
```

確認：

```bash
nemoclaw --version
```

### Step 4：執行 onboard

```bash
nemoclaw onboard
```

引導過程中選擇 inference provider 時：

| 項目 | 填入值 |
|------|--------|
| Provider | Ollama (local) |
| URL | `http://localhost:11434` |
| Model | `qwen3.5:27b` |

### Step 5：連線到 sandbox

```bash
nemoclaw my-assistant connect
```

進入 sandbox shell 後，開啟 TUI 與 agent 對話：

```bash
openclaw tui
```

## Reference

- GitHub
  - [NVIDIA / NemoClaw](https://github.com/NVIDIA/NemoClaw)
  - [openclaw / openclaw](https://github.com/openclaw/openclaw)
