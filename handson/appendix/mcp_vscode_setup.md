# VS CodeでのMCPサーバー利用準備

ここでは、VS Code (Visual Studio Code) を例に、MCPサーバーを利用するためのセットアップ手順をまとめています。

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
3. `GitHub Copilot Chat` を選択し、「インストール」をクリック。

---

### Step 2: Copilotにサインインしてライセンスを有効化する

1. VS Code左下のアカウントアイコン、またはCopilotサイドバーをクリック。
2. 「Sign in to GitHub」を選び、ブラウザーで認証フローを完了する。
3. VS Code側に戻り、Copilot Chatが利用可能な状態（`Signed in as ...` 表示）になっていることを確認。

> ここまででVS CodeからGitHub Copilotが使えるようになりました。次のステップからMCPサーバーを使えるようにしていきます。

---

### Step 3: Copilot Chatをエージェントモードにする

1. VS Codeのタイトルバーにある Copilot アイコンをクリックして、Copilot Chatを開きます。
2. Copilot Chatボックスのポップアップメニューから「Agent」を選択します。

> Copilotの設定は完了です。CopilotからMCPサーバーを使える準備が整いました。

## まとめ

- GitHub Copilot Chat拡張機能をインストールする
- GitHubアカウントでサインインする
- Copilot Chatをエージェントモードに切り替える

この3点を満たせば、VS CodeからMCPサーバーを利用するための準備は完了です。

---

[← 前へ：MCPサーバーとは](02_mcp_overview.md)  | [目次](../README.md) | [次へ：MCPサーバーを触ってみよう →](03_mcp_handson.md)
