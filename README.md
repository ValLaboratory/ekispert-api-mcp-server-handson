# 駅すぱあと API MCPサーバー ハンズオン

## 概要

このハンズオンでは、MCP（Model Context Protocol）の基礎を学び、実際にMCPサーバーを動かしながら、[駅すぱあと API MCPサーバー](https://github.com/ValLaboratory/ekispert-api-mcp-server-docs)の活用方法を体験します。

**所要時間**: 約90分

## 目次

### イントロダクション（5分）

ハンズオンの目的と全体の流れを説明します。

### [1. 生成AI時代とAIエージェントの基礎](handson/01_ai_agent_basics.md)（10分）

生成AIの普及状況とAIエージェントの概念を理解し、MCPサーバーが必要な背景を学びます。

- 生成AI/LLMの普及と現状
- AIエージェントとは
- MCPの必要性

### [2. MCPサーバーとは](handson/02_mcp_overview.md)（20分）

MCP（Model Context Protocol）の基礎を理解し、MCPサーバーとMCPクライアントの関係、実際の活用例を学びます。

- MCP（Model Context Protocol）の定義と必要性
- MCPサーバーとMCPクライアントの役割と関係
- MCPの通信方式（stdio方式とStreamable HTTP方式）
- MCPサーバーが提供する機能（Tool、Resource、Prompt）
- 公式およびコミュニティのMCPサーバー活用例
- 駅すぱあと API MCPサーバーの位置づけ

**付録資料**: [付録：MCPサーバーのセキュリティガイド](handson/appendix/mcp_security.md)

### [3. MCPサーバーを触ってみよう](handson/03_mcp_handson.md)（40分）

stdio方式とStreamable HTTP方式の両方のMCPサーバーを実際に体験します。

**3-0. [VS CodeでのMCPサーバー利用準備](handson/03_mcp_vscode_setup.md)（10分）**
- GitHub Copilot Chat拡張機能のインストール
- Copilotへのサインインとライセンスの有効化
- Copilot Chatをエージェントモードにする
- `mcp.json` の設定方法

**3-1. stdio方式のMCPサーバーを体験する（15分）**
- Playwright MCPサーバーの設定とハンズオン
  - 駅すぱあと公式サイトの操作
  - 経路検索ページでのフォーム操作

**3-2. Streamable HTTP方式のMCPサーバーを体験する（15分）**
- 駅すぱあと API MCPサーバーの設定とハンズオン
  - 基本的な経路探索
  - 駅情報の取得
  - 探索条件を指定した応用操作

**3-3. 便利なMCPサーバーの紹介**
- Slack MCP Server
- MarkItDown MCP Server
- Atlassian MCP Server

**3-4. MCPサーバーの探し方**
- MCP Registryサービスの活用
- セキュリティを考慮したサーバー選択

### まとめ・質疑応答（15分）

## 付録

### [付録：MCPサーバーのセキュリティガイド](handson/appendix/mcp_security.md)

MCPサーバーを安全に利用するための詳細なガイドです。ハンズオンの時間内では扱いませんが、実際の業務で活用する際に参考にしてください。

- プロンプトインジェクション攻撃の詳細と対策
- ツール汚染攻撃の仕組みと防御方法
- ラグプル攻撃の検出と対処
- 安全な設定の実装例
- 参考資料とコミュニティリソース
