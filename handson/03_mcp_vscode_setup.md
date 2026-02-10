# 3. MCPサーバーの利用方法

ここでは、VS Code (Visual Studio Code) を例に、任意のMCPサーバーを使えるようにする方法を紹介します。

## VS CodeでMCPサーバーを呼び出す準備
### このページの目的

- VS CodeとGitHub CopilotでMCPサーバーを呼び出す準備を整える

---

### 前提条件

- GitHubアカウント
- Visual Studio Code バージョン 1.99 以降
- GitHub Copilotへのアクセス権

---

### Step 1: GitHub Copilot Chat拡張機能のインストール

1. VS Code左側の「拡張機能」（四角形アイコン）を開く。
2. 検索ボックスに `GitHub Copilot` と入力。
3. `GitHub copilot Chat` を選択し、「インストール」をクリック。

---

### Step 2: Copilotにサインインしてライセンスを有効化する

1. VS Code左下のアカウントアイコン、またはCopilotサイドバーをクリック。
2. 「Sign in to GitHub」を選び、ブラウザーで認証フローを完了する。
3. VS Code側に戻り、Copilot Chatが利用可能な状態（`Signed in as ...` 表示）になっていることを確認。

> ここまででVScodeからCopilotが使えるようになりました。次のステップからMCPサーバーを使えるようにしていきます。

---

### Step 3: Copilot Chatをエージェントモードにする

1. VS Codeのタイトルバーにある Copilot アイコンをクリックして、Copilot Chatを開きます。

2. Copilot Chatボックスのポップアップメニューから「Agent」を選択します。

> Copilotの設定は完了です。CopilotからMCPサーバーを使える準備が整いました。


### Step 4: `mcp.json` を作成する
MCPサーバーを使うには、設定ファイル`mcp.json`に追記します。

**MCPサーバーをユーザー設定として自身のVScode全体で使用したい場合：**
1. `Cmd+Shift+P`でコマンドパレットを開く。
2. 「MCP: Open User Configuration」を実行。
3. `~/Library/Application Support/Code/User/mcp.json`が作成される。


**MCPサーバーをワークスペース設定としてリポジトリ単位で使用したい場合：**
1. ハンズオン用のVS Codeワークスペースを開く。
2. プロジェクト直下に`.vscode` フォルダーが無ければ作成し、その中に `mcp.json` を新規作成。
3. まずは空の `servers` オブジェクトを用意する。

```json
{
  "servers": {}
}
```

- 以降、PlaywrightやMarkItDown、駅すぱあと API MCPサーバーなどの設定をこの `servers` 配下に追記します。

---

## まとめ

- GitHub Copilot Chat拡張機能のインストールとGitHubアカウントへのサインインが、MCPサーバーを利用するための前提条件です。
- `mcp.json` の `servers` 配下にサーバー定義を追記していくのが基本フローです。

---

[← 前へ：MCPサーバーとは](02_mcp_overview.md) | [目次](../README.md) | [次へ：MCPサーバーハンズオン →](03_mcp_handson.md)
