# 3. MCPサーバーを触ってみよう
ここでは、ハンズオン形式でMCPサーバーについて学習します。stdio方式とStreamable HTTP方式の両方を体験し、実際にMCPサーバーを利用できるようになることを目指します。

## このセクションの目的

- stdio方式とStreamable HTTP方式の特徴と利点を体験を通じて理解する
- Playwright MCPサーバーを VS Code から利用できるようにする
- 「駅すぱあと API MCPサーバー」を VS Code から利用できるようにする
- 実務で活用できる便利なMCPサーバーを知る
- MCP Registryサービスの使い方を理解し、自分に適したMCPサーバーを探せるようになる

---

## MCPサーバーの通信方式について

MCPサーバーの通信方式（stdio方式・Streamable HTTP方式）については、[前のセクション](02_mcp_overview.md)で詳しく説明しています。詳細はそちらを参照してください。

----

## 3-1. stdio方式のMCPサーバー

### Playwright MCPサーバー

Playwright MCPサーバーは、ブラウザをAIエージェントから直接操作するためのサーバーです。
[GitHub MCP Registry](https://github.com/mcp) （GitHubが管理・運営しているレジストリ）を通じて、簡単にインストールできます。

| 項目 | 内容 |
|------|------|
| 目的 | AIエージェントにブラウザ操作（ページ遷移・操作・スクリーンショット）を担わせる |
| プロンプト例 | 「Googleで「駅すぱあと」を検索してスクリーンショットを撮って」 |
| インパクト | Webスクレイピング、フォーム入力、ビジュアル検証など従来手作業だったタスクを自動化 |

**事前準備チェック**

- インターネット経由でGitHubにアクセスできる
- VS CodeでGitHub Copilotのチャットが使える
Node.js 22以降（LTS版推奨）
  - Node.jsをインストールしていない場合はHomebrew等でNode.js（npx同梱）を入れてください。
    ```sh
    brew install node@22
    ```

**Step 1: GitHub MCPレジストリを開く**

GitHub MCP Registryから [Playwright MCP](https://github.com/mcp/microsoft/playwright-mcp) のページを開きます。
「Install in VS Code」をクリックすると、VS Codeが開きPlaywright MCPサーバーのインストール画面が表示されます。

**Step 2: Playwright MCPサーバーをインストールする**

VS Codeに表示されたPlaywright MCPサーバーの詳細画面で「Install Server」を押すと、自動で設定が追加されます。

**Step 3: `mcp.json` を確認する**

VS Codeが生成した設定を `mcp.json` で確認します（例）。

```json
"servers": {
  "playwright": {
    "command": "npx",
    "args": ["@modelcontextprotocol/server-playwright"],
    "type": "stdio"
  }
}
```

**Step 4: MCPサーバーを起動する**

MCPサーバーの起動は、`mcp.json`で「Start」ボタンをクリックします。

#### ハンズオン: 「駅すぱあと」公式サイトを開いてスクリーンショットを撮る
```txt
Playwright MCPサーバーで https://ekispert.jp/ を開いて、ページタイトルと最初の見出しを読み上げ、最後にスクリーンショットを添付して
```

1. Copilot Chatの実行ログでTool呼び出しが順に行われたことを確認する
2. ブラウザが開き、「駅すぱあと」の公式サイトが開いたことを確認する
3. 応答に添付されたPNGをクリックし、トップページが想定どおり表示されているかをチェックする

#### ハンズオン: 経路検索ページでフォーム操作を試す
```
Playwrightで https://roote.ekispert.net/ を開き、出発に 東京、到着に 新宿 を入力して検索ボタンを押し、結果の最初の候補タイトルを読み上げて
```
1. Copilot Chatの実行ログでTool呼び出しを確認する
2. 回答に検索結果の概要（例: 「中央線快速で約14分です」）が記載されているかを確認する

---

## 3-2. Streamable HTTP方式のMCPサーバー

### 駅すぱあと API MCPサーバー

「[駅すぱあと API MCPサーバー](https://github.com/ValLaboratory/ekispert-api-mcp-server-docs)」は、株式会社ヴァル研究所が提供する経路検索WebAPI「駅すぱあと API」をMCP経由で呼び出せる公式サーバーです。経路探索・駅情報取得・探索条件生成といったToolを提供しており、VS Code + GitHub Copilot などのMCPクライアントから自然言語で利用できます。

#### 利用可能な機能一覧
本MCPサーバーが提供する機能（Tool）の一覧とその詳細です。新しい機能を今後も順次追加予定です。
* 駅情報取得（ekispert_api_get_stations）
* 経路探索（ekispert_api_search_routes）
* 探索条件生成（ekispert_api_generate_condition）

各Toolの使い方は後続のハンズオンで扱います。詳細仕様や最新情報は公式ドキュメントを参照してください。

**事前準備チェック**

- VS CodeとGitHub Copilot拡張がインストール済み
- 「駅すぱあと API」のアクセスキーを用意している
- ターミナルで環境変数を設定できる

**Step 1: 環境変数を設定する**

「駅すぱあと API」のアクセスキーを環境変数に登録します。

macOS / Linux の場合、ターミナルで以下を実行してください。

```bash
export EKISPERT_API_ACCESS_KEY="YOUR_ACCESS_KEY_HERE"
```

永続化したい場合は `~/.zshrc` や `~/.bashrc` に同じ行を追記し、`source ~/.zshrc` で反映させます。

設定後、`echo $EKISPERT_API_ACCESS_KEY` を実行し、アクセスキーが表示されれば設定完了です。

**Step 2: `mcp.json` に追記する**

`servers` に下記を追記します。`${env:EKISPERT_API_ACCESS_KEY}` の部分で、Step 1 で設定した環境変数からアクセスキーを取得しています。

```json
"servers": {
  "ekispert-api-mcp-server": {
    "type": "http",
    "url": "https://api-mcp.ekispert.jp/mcp",
    "headers": {
      "ekispert-api-access-key": "${env:EKISPERT_API_ACCESS_KEY}"
    }
  }
}
```

**Step 3: VS Code を再起動する**

設定を反映させるため、VS Code を完全に終了してから再度起動してください。Cmd+Q でウィンドウを閉じます。

環境変数を新しく設定した場合は、再起動後のウィンドウで作業を続けてください。リロードだけでは環境変数が反映されないことがあります。

**Step 4: MCPサーバーを起動する**

MCPサーバーの起動は、`mcp.json`で「Start」ボタンをクリックします。

#### ハンズオン: 基本的な経路探索

```text
東京駅から新宿駅への経路を教えて
```

**使用されるTool**: `ekispert_api_search_routes`

**期待する結果**

複数の経路候補、運賃、乗換回数などの情報が返ってきます。

別の区間でも試してみましょう。

```text
渋谷駅から横浜駅までの経路を教えて
```

```text
新宿駅から成田空港までの経路を教えて
```

#### ハンズオン: 駅情報を取得する

```text
東京駅の情報を教えて
```

**使用されるTool**: `ekispert_api_get_stations`

**期待する結果**

駅コード、所在地、通過路線などの情報が返ってきます。駅コードは経路探索で駅を正確に指定する際に使えます。

#### ハンズオン: 探索条件を指定した応用操作

`ekispert_api_generate_condition` を使うと、交通手段のON/OFFや優先度を細かく調整できます。自然言語で条件を伝えれば、AIが適切なパラメータを組み立てます。

```text
東京から大阪まで、新幹線を使わない経路を教えて
```

**使用されるTool**: `ekispert_api_generate_condition`（`shinkansen: "never"`）→ `ekispert_api_search_routes`

**期待する結果**

在来線、高速バス、飛行機などを利用した経路が返ってきます。

---

## 3-3. 便利なMCPサーバーの紹介

ここでは、実務で活用できる便利なMCPサーバーをいくつか紹介します。各MCPサーバーの詳細な設定方法は省略しますが、どのようなことができるのか、どんな場面で便利なのかをイメージしていただければと思います。

### Slack MCP Server

[Slack MCP Server](https://docs.slack.dev/ai/mcp-server/) は、Slack公式が提供するMCPサーバーで、AIエージェントからSlackワークスペースへ安全にアクセスできるようにします。

| 項目 | 内容 |
|------|------|
| 目的 | チーム内のコミュニケーションをAIエージェントから検索・分析・送信する |
| 主な機能 | メッセージの検索・取得・送信、ユーザー情報の管理、チャンネル検索、Canvas管理 |
| プロンプト例 | 「先週のマーケティングチャンネルで話し合われた『新製品ローンチ』に関する情報をまとめて」 |
| インパクト | チームの過去のやり取りを検索して文脈を理解したり、外部の情報をSlackに持ち込んで議論を始めたりと、チーム全体のコミュニケーションを効率化 |

### Atlassian MCP Server

[Atlassian MCP Server](https://github.com/atlassian/atlassian-mcp-server) は、Atlassian公式が提供するMCPサーバーで、Jira、Confluence、Compassの各サービスとAIエージェントを連携させます。

| 項目 | 内容 |
|------|------|
| 目的 | プロジェクト管理とドキュメント作成を自然言語で効率化する |
| 主な機能 | Jira Issueの検索・作成・更新、Confluenceページの要約・作成・検索、Compassコンポーネントの操作 |
| プロンプト例 | 「プロジェクトXの全ての未解決バグを検索して」「『要件定義』というタイトルでConfluenceページを作成して」 |
| インパクト | プロジェクト管理とドキュメント作成を自然言語で実現し、情報の検索から更新まで一貫した作業フローを構築できる |

### MarkItDown MCP Server

[MarkItDown MCP Server](https://github.com/mcp/microsoft/markitdown) は、Microsoft公式が提供するMCPサーバーで、様々なバイナリファイルをMarkdownに変換し、AIが再利用しやすいデータへ整形します。

| 項目 | 内容 |
|------|------|
| 目的 | PDF、PowerPoint、Excel、画像などのファイルをMarkdownへ変換し、AIが扱いやすい形にする |
| 主な機能 | PDF・Office文書・画像ファイルの読み込み、テキスト抽出、Markdown形式での出力 |
| プロンプト例 | 「この議事録.pdfをMarkdownに直して」「請求書.xlsxの内容を一覧にして」 |
| インパクト | 既存資料の構造化に強く、社内ナレッジ活用の足掛かりになる。OCRや文書変換を活用した業務効率化 |

---

## 3-4. MCPサーバーの探し方

世の中には多数のMCPサーバーが公開されており、目的に応じたMCPサーバーを見つけることができます。

### MCP Registryサービス

便利なMCPサーバーを探す際は、以下のレジストリサービスが参考になります。

#### Official MCP Registry

[Official MCP Registry](https://registry.modelcontextprotocol.io/) は、Anthropic社およびMCPコミュニティが運営しているレジストリサービスです。

- 幅広いカテゴリのMCPサーバーが登録されている
- コミュニティベースで様々な開発者が公開しているサーバーを探せる
- 新しく実験的なサーバーも多数見つかる

#### GitHub MCP Registry

[GitHub MCP Registry](https://github.com/mcp) は、GitHub公式が運営しているレジストリサービスです。

- GitHub、Microsoft、Googleなど大手企業が提供する公式MCPサーバーが多い
- セキュリティ面で信頼性が高い
- VS Codeから直接インストール可能な「Install in VS Code」ボタンを備えている
- 本ハンズオンで紹介したPlaywright MCPサーバーもこちらで公開されている

### MCPサーバーを探す際の注意点

世の中には多数のMCPサーバーが公開されていますが、セキュリティ的に問題のあるMCPサーバーも存在します。

- **公式レジストリを優先**: 上記のレジストリサービスで公開されているMCPサーバーは比較的安全
- **提供元の確認**: 企業の公式サーバーや、信頼できる開発者のサーバーを選ぶ
- **セキュリティリスクの理解**: MCPサーバーの利用にはリスクが伴うことを理解する

安全にMCPサーバーを利用するための詳細については、[付録：MCPサーバーのセキュリティガイド](appendix/mcp_security.md)をご覧ください。

---

## まとめ

- stdio方式とStreamable HTTP方式の違いを理解し、それぞれの特徴を体験した
- Playwright MCPサーバーでブラウザ操作を自動化し、スクリーンショット取得やフォーム入力を体験できる
- 「駅すぱあと API MCPサーバー」で経路検索や駅情報取得を自然言語で実行できる
- Slack、MarkItDown、Atlassianなど、実務で活用できる便利なMCPサーバーが多数公開されている
- MCP Registryサービス（Official MCP Registry、GitHub MCP Registry）を活用することで、目的に応じたMCPサーバーを見つけられる
- MCPサーバーを選ぶ際は、セキュリティ面にも注意を払うことが重要

---

[← 前へ：MCPサーバー利用準備](03_mcp_vscode_setup.md) | [目次](../README.md)