## 0.0.351 - 2025-10-24

- パス検出ヒューリスティックを改善し、様々な煩わしい不要なパーミッション要求を回避しました：
	- 読み取り専用として知られている多くの標準bash/PowerShellコマンドを実行する (https://github.com/github/sweagentd/issues/7372 の一部を修正)
	- PowerShellの`npm test -- --something`のようなコマンド
	- `> some_file.txt`のようなシェルリダイレクション（既にライト権限を付与したパス内）、`> /dev/null`、および`2>&1` (https://github.com/github/copilot-cli/issues/211 を修正)
	- `gh api /repos/user/repo/ec`のような`gh api`への引数 (https://github.com/github/copilot-cli/issues/216 を修正)
- Sonnet 4.5のプロンプトを改善し、ワークスペースに残された中間マークダウンファイルの数を削減しました
- 👀 ...[GitHub Universe](https://githubuniverse.com/)でお会いしましょう！

## 0.0.350 - 2025-10-23

- コンテキストウィンドウのスペースを節約するため、デフォルトGitHub MCPサーバーで利用可能なツールのリストを制限しました。テストでは、モデルは不足しているMCPツールの代わりに（インストールされている場合）[GitHub CLI `gh`](https://github.com/cli/cli)を使用します。利用可能なすべてのツールをオンにしたい場合は、`--enable-all-github-mcp-tools`フラグを追加しました。
デフォルトで利用可能なツール：
	- コード＆リポジトリナビゲーション
		- get_file_contents
		- search_code
		- search_repositories
		- list_branches
		- list_commits
		- get_commit
	- イシュー管理
		- get_issue
		- list_issues
		- get_issue_comments
		- search_issues
	- プルリクエスト管理
		- pull_request_read
		- list_pull_requests
		- search_pull_requests
	- ワークフロー情報
		- list_workflows
		- list_workflow_runs
		- get_workflow_run
		- get_job_logs
		- get_workflow_run_logs
	- その他の検索
		- user_search
- `sharp`依存関係をCLIパッケージにバンドルしました -- https://github.com/github/copilot-cli/issues/16 の実装に一歩近づき、Windows上の起動ブロッカーを修正しました (https://github.com/github/copilot-cli/issues/309 と https://github.com/github/copilot-cli/issues/287 を修正)
- 入力トークンが適切に追跡されていないバグを修正しました (https://github.com/github/copilot-cli/issues/337 を修正)
- ストリーミングが有効な場合、引数を持つMCPツールが失敗するバグを修正しました
- https://github.com/github/copilot-cli/issues/346 の調査に役立つ追加デバッグログを追加しました

## 0.0.349 - 2025-10-22

- モデルは複数のツールを並列で呼び出すことができるようになりました。各ツールは事前に確認する必要があります。この動作は`--disable-parallel-tools-execution`フラグで無効化できます
- `/quit`を`/exit`のエイリアスとして追加しました (https://github.com/github/copilot-cli/issues/357 を修正)
- ストリーミングされたすべての出力チャンクが会話の一部としてモデルに送信されるバグを修正しました (https://github.com/github/copilot-cli/issues/379 を修正)
- パスパーミッションチェックを実行する前に環境変数が展開されることを確認しました
- Ctrl+Kが入力ボックスの視覚的な行の末尾ではなく論理行の末尾を削除していたバグを修正しました
- モデルがデフォルトでアクセスできるパスに一時ディレクトリを追加しました (https://github.com/github/copilot-cli/issues/306 を修正)

## 0.0.348 - 2025-10-21

- Copilotの出力がトークンバイトークンでストリーミングされるようになりました！これは`--stream off`で無効化できます
- Copilot CLIのメモリフットプリント、特に非常に大きな出力を生成するシェルコマンドを処理する場合を改善しました
- `/terminal-setup`を使用する場合、VSCode設定ファイル内のコメントが保持されることを確認しました (https://github.com/github/copilot-cli/issues/325 を修正)
- `node-pty`をCLIパッケージにバンドルしました -- https://github.com/github/copilot-cli/issues/16 の実装に一歩近づきました
- ローカルツール呼び出しがセッションを破損させるという問題を修正しました (https://github.com/github/copilot-cli/issues/365、https://github.com/github/copilot-cli/issues/364、https://github.com/github/copilot-cli/issues/366 を修正)
- LICENSE.mdをNodeパッケージに追加しました (https://github.com/github/copilot-cli/issues/371 を修正)
- 認証ステータスの変更にデバッグログを追加して、https://github.com/github/copilot-cli/issues/346 の原因を突き止めました

## 0.0.347 - 2025-10-20

- 不正なPRU消費統計がフロントエンドに表示されるバグをさらに修正しました
  詳細については、https://github.com/github/copilot-cli/issues/351#issuecomment-3423735333 を参照してください
- 貼り付けた入力コンテンツがバックスペースで削除された場合でも、モデルに送信されるバグを修正しました
- ファイルdiffを表示する場合の行の折り返しと配置を改善しました

## 0.0.346 - 2025-10-19

- 構成ファイルから取得されたモデルがプレミアムリクエスト使用量の推定に正しく計上されていないバグを修正しました
  詳細については、https://github.com/github/copilot-cli/issues/351#issuecomment-3419045411 を参照してください

## 0.0.345 - 2025-10-18

- プレミアムリクエストが一部のユーザーに対して過剰にカウントされていたバグを修正しました (https://github.com/github/copilot-cli/issues/351)。影響を受けた場合、過剰請求されたプレミアムリクエストの払い戻しに取り組んでいます！

## 0.0.344 - 2025-10-17

- プロンプトモードでGitHub MCPサーバーを有効化しました
- bashツールにデタッチされたプロセスを実行するサポートを追加しました
- `copilot help config`テキストのサポート済みモデルのリストを追加しました
- セッション中止処理を修正して、<kbd>Esc</kbd>を押すか強制終了する際に孤立したツール呼び出しを適切にクリーンアップします
- ノード版の最小要件を起動時に強制しました
- `/terminal-setup`のメッセージを簡潔にしました


## 0.0.343 - 2025-10-16

- ```
  新しいモデルを追加しました：
  スラッシュモデルを実行して装備
  Haiku 4.5。
  ```
- MCPサーバー構成を拡張して、セッションごとにサーバー構成を一時的に追加または上書きするフラグを追加しました：`--additional-mcp-config` (https://github.com/github/copilot-cli/issues/288 を修正)
	- MCPサーバー構成を2つの方法で渡すことができます：
		- インラインJSON：`copilot --additional-mcp-config '{"mcpServers": {"my-tool": {...}}}'`
		- ファイルから（プレフィックス@）：`copilot --additional-mcp-config @/path/to/config.json`
	- フラグを複数回渡すこともできます（後の値が前の値をオーバーライドします）：`copilot --additional-mcp-config @base.json --additional-mcp-config @overrides.json`
- エージェントがWindows上でWindowsスタイルのパスを使用することを確認するプロンプトを改善しました (https://github.com/github/copilot-cli/issues/261 を修正)
- 必要に応じてマルチラインの入力を有効にするために`/terminal-setup`を実行するようユーザーに促すプロンプトを追加しました
- 様々なビジュアル改善：
	- 「考え中...」インジケーターにシマーエフェクトを追加しました
	- ユーザーメッセージの周りのボックスを削除しました
	- diffの削除されたイントララインハイライトのコントラストを向上させました
	- スラッシュコマンドをサイクル表示できます（リストの下から上に戻る）
	- パーミッション/確認プロンプトを統一して、すべてが同じビジュアルスタイルを使用することを確認しました


## 0.0.342 - 2025-10-15

- セッションログ形式を完全に改良しました：
	- セッションを保存する方法をタイムラインに表示する方法から切り離した新しいセッションログ形式を導入しました。新しい形式はより清潔で、より簡潔で、スケーラブルで、今後新機能を実装しやすくなります。
	- 新しいセッションは`~/.copilot/session-state`に保存されます
	- レガシーセッションは`~/.copilot/history-session-state`に保存されます -- これらは`copilot --resume`から再開すると新しい形式と場所に移行されます
- Kittyプロトコルをデフォルトで有効化しました。マルチラインの入力は、KittyプロトコルをサポートするターミナルでShift+Ctrlを使用してサポートされるようになりました。マルチラインの入力は、`/terminal-setup`コマンドを実行することで、VSCodeおよびそのフォークでもサポートされます (https://github.com/github/copilot-cli/issues/14 を部分的に修正)
- `GH_HOST`環境変数をPATおよび`gh`認証モードに対して尊重して、非対話的なGHEログインを有効化しました (https://github.com/github/copilot-cli/issues/296 を修正)
- `~/.copilot/config`に永続的な`log_level`オプションを追加してデバッグログ収集の便利性を改善しました。可能な値：`["none", "error", "warning", "info", "debug", "all", "default"]`
- `/model`への呼び出しがCopilot APIエラーになった場合のデバッグログを追加しました。これは、https://github.com/github/copilot-cli/issues/268 と https://github.com/github/copilot-cli/issues/116 のようなポリシー/モデルアクセスのエッジケースを診断するのに役立ちます
- `gradlew`をサブコマンドをホワイトリストできるコマンドのリストに追加しました (https://github.com/github/copilot-cli/issues/217#issuecomment-3393844685 を修正)
- セッションが失敗したMCPツール呼び出し後にスタック状態に入る可能性があるバグを修正しました (https://github.com/github/copilot-cli/issues/312 を修正)
- `--help`テキストの出力をより簡潔にしました

## 0.0.341 - 2025-10-14

- `/terminal-setup`コマンドを追加して、kittyプロトコルを実装していないターミナルでマルチラインの入力を設定しました
- MCPツール呼び出しを拒否すると、すべての将来のツール呼び出しが拒否されるバグを修正しました (https://github.com/github/copilot-cli/issues/290 を修正)
- 引数を指定して`/model`を呼び出しても正しく機能しない回帰を修正しました
- 各モデルのプレミアムリクエスト乗数を`/model`リストに追加しました（現在、サポートされているすべてのモデルは1xです）

## 0.0.340 - 2025-10-13

- 「Windows サポートは実験的です」という警告を削除しました -- ここ2週間、Windows サポートの改善で大きな進歩を遂げました！問題/フィードバックの報告を続けてください
- モデル呼び出しエラーのCopilot APIリクエストIDとクライアントエラーのスタックトレースを含めて、デバッグを改善しました
- 連続した孤立したツール呼び出しが「各`tool_use`ブロックは次のメッセージに対応する`tool_result`ブロックを持つ必要があります」というメッセージを引き起こす問題を修正しました (https://github.com/github/copilot-cli/issues/102 を修正)
- `-p`モードで新しいパスを承認するプロンプトを追加しました。また、すべてのパスへのアクセスを承認する`--allow-all-paths`引数も追加しました
- MCPサーバー構成での環境変数の解析を変更して、`env`セクションの値をリテラル値として扱うようにしました (https://github.com/github/copilot-cli/issues/26 を修正)。
  CLIで使用するためにMCPサーバーを構成しているお客様は、`~/.copilot/mcp-config.json`に若干の変更を加える必要があります。`env`セクションを含めて追加したサーバーについては、env ブロック内の各エントリのキー値ペアの「値」ペアの開始位置に`$`を追加する必要があります。これにより、値が環境変数への参照として扱われます。

  例：前：
    ```json
    {
        "env": {
            "GITHUB_ACCESS_TOKEN": "GITHUB_TOKEN"
         }
    }
    ```

    この変更の前、CLIは環境からの`GITHUB_TOKEN`の値を読み込み、MCPプロセスの`GITHUB_ACCESS_TOKEN`という名前の環境変数をその値に設定していました。この変更により、`GITHUB_ACCESS_TOKEN`はリテラル値`GITHUB_TOKEN`に設定されるようになりました。古い動作を取得するには、これに変更してください：

    ```json
    {
        "env": {
            "GITHUB_ACCESS_TOKEN": "${GITHUB_TOKEN}"
         }
    }
    ```


## 0.0.339 - 2025-10-10

- `/mcp add`でのMCPサーバーへの引数入力を改善しました -- 以前、ユーザーはカンマ区切りの構文を使用して引数を指定する必要がありました。現在、「コマンド」フィールドでは、ユーザーは シェルで実行していた場合と同様に、サーバーを起動するための完全なコマンドを入力できます
- Kittyプロトコルを使用するときに、`u`を含むテキストが正しく貼り付けられないという原因のバグを修正しました。Kittyプロトコルサポートは引き続き`COPILOT_KITTY`環境変数の後ろにあります (https://github.com/github/copilot-cli/issues/259 を修正)
- Kittyプロトコルを使用するときに、Windows上のVSCodeターミナルでプロセスがハングするという原因のバグを修正しました。Kittyプロトコルサポートは引き続き`COPILOT_KITTY`環境変数の後ろにあります (https://github.com/github/copilot-cli/issues/257 を修正)
- モデルが利用できない場合の`/model`ピッカーのエラー処理を改善しました (https://github.com/github/copilot-cli/issues/229 を修正)

## 0.0.338 - 2025-10-09

- 観察された回帰により、Kittyプロトコルサポートを`COPILOT_KITTY`環境変数の後ろに移動しました (https://github.com/github/copilot-cli/issues/257、https://github.com/github/copilot-cli/issues/259)
- マルチラインプロンプトの空行での折り返しの問題を修正しました

## 0.0.337 - 2025-10-08

- MCPサーバー名の検証を追加しました (https://github.com/github/copilot-cli/issues/110 を修正)
- Ctrl+BおよびCtrl+Fのサポートを追加して、カーソルを後ろと前に移動します (https://github.com/github/copilot-cli/issues/214 を修正)
- [Kittyプロトコル](https://sw.kovidgoyal.net/kitty/keyboard-protocol/)をサポートするターミナルでのマルチライン入力のサポートを追加しました (https://github.com/github/copilot-cli/issues/14 を部分的に修正 -- より広いターミナルサポートが間もなく!)
- OAuthログインUIを更新して、デバイスコードが生成されるとすぐにポーリングを開始するようにしました (これはhttps://github.com/github/copilot-cli/issues/89 で説明されているSSH エッジケースをより堅牢に修正します)

## 0.0.336 - 2025-10-07

- Node.jsのバージョンに関係なく、HTTPS_PROXY/HTTP_PROXY環境変数経由でプロキシサポートを有効化しました (https://github.com/github/copilot-cli/issues/41 を修正)
- トークン消費、ラウンドトリップあたりの数、結果までの時間を大幅に削減しました。より具体的なデータは金曜日の週刊変更ログで共有します！
- シェルに依存して現在の作業ディレクトリを取得せず、ファイル書き込みパフォーマンスを改善しました（特にWindows上）
- `/clear`が文脈切り詰めトラッキング状態を適切にリセットしないバグを修正しました
- セッション再開と`/clear`時に「GitHub Copilot CLI へようこそ」というウェルカムメッセージを非表示にして、より清潔な外観にしました
- スクロールバーが存在する場合のテーブル配置を改善しました
- `--help`の出力をより簡潔にして改善しました
- `--screen-reader`で起動するユーザーにこの設定を永続的に保存するよう促すプロンプトを追加しました
- 場合によっては点滅が改善される可能性があります。まだ取り組んでいます！

## 0.0.335 - 2025-10-06

- ファイル編集の可視性を向上させ、Ctrl+Rを必要とせず、デフォルトでタイムラインにファイルdiffを表示させました
- スラッシュコマンド入力を改善し、入力ボックスに引数ヒントを表示するようにしました
- 80列未満のウィンドウでインターフェースを表示させました
- マークダウン表示の色の数を減らし、間隔を改善しました
- プロキシサポートを使用しようとしているが、それが機能しない環境（Node <24、必要な環境変数が設定されていない）でユーザーに警告を追加しました (https://github.com/github/copilot-cli/issues/41 に対するより永続的な修正は明日頃に来ています)
- 文脈切り詰めメッセージの色をエラーの色から警告の色に更新しました
- `copilot`ログがWindows上で適切に作成されないバグを修正しました
- カスタムプロファイルを持つPowershellユーザーがコマンド実行で問題が発生する可能性があるバグを修正しました (https://github.com/github/copilot-cli/issues/196 を修正)
- 貼り付けおよび他のエッジケース後にプロンプトが切り詰められるバグを修正しました (https://github.com/github/copilot-cli/issues/208、https://github.com/github/copilot-cli/issues/218 を修正)
- ログインしているにもかかわらず、ユーザーが起動時にログインプロンプトを表示されるバグを修正しました (https://github.com/github/copilot-cli/issues/202 を修正)
- 一部のSSHユーザーが特定の環境でOAuthログインリンクを取得できず、ブラウザを開こうとしてプロセスがハングするという問題を修正しました (https://github.com/github/copilot-cli/issues/89 を修正)

## 0.0.334 - 2025-10-03

- 大きなコンテンツを貼り付ける体験を改善しました：10行以上貼り付けると、ターミナルにあふれるのではなく、`[Paste #1 - 15 lines]`のようなコンパクトトークンとして表示されます
- 会話コンテキストがモデルの制限の≤20%に近づくと警告を追加します。この時点で、新しいセッションを開始することをお勧めします (https://github.com/github/copilot-cli/issues/29 を改善)
- 保存されたセッション履歴から終了時の使用統計を削除しました
- バグ報告を支援するために、スタートアップログに現在のバージョンを追加しました
- 引数が存在する場合、TABオートコンプリートアイテムのサイクリングを削除しました。これにより、`/cwd /path/to/whatever`を実行して`TAB`を押すと、`/clear`オートコンプリートが表示されることを防ぎます

## 0.0.333 - 2025-10-02

- 画像サポートを追加しました！`@`-ファイルをメンションしてモデルへの入力として追加します
- Node.JS v24+のユーザーのプロキシサポートを改善しました。詳細については、[このコメント](https://github.com/github/copilot-cli/issues/41#issuecomment-3362444262)を参照してください (https://github.com/github/copilot-cli/issues/41 を修正)
- シェルコマンドを直接実行し、入力を`!`で前に付けてモデルをバイパスするサポートを追加しました (https://github.com/github/copilot-cli/issues/186、https://github.com/github/copilot-cli/issues/12 を修正)
- `/usage`スラッシュコマンドを追加して、プレミアムリクエスト使用量、セッション時間、コード変更、およびモデルごとのトークン使用に関する統計を提供します。この情報はセッションの終了時にも出力されます (https://github.com/github/copilot-cli/issues/27、https://github.com/github/copilot-cli/issues/121 を修正)
- `--screen-reader`モードを改善し、タイムラインのアイコンを情報ラベルに置き換えました
- 最後に閉じたセッションを再開する`--continue`フラグを追加しました
- `/clear`コマンドを更新して、古いタイムラインエントリ/セッション情報を適切にクリアするようにしました (https://github.com/github/copilot-cli/issues/170 を修正)

## 0.0.332 - 2025-10-01

- [GitHubのドキュメント](https://docs.github.com/en/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-access/manage-network-access)に従って、サブスクリプション別のCopilot APIエンドポイントを使用するように切り替えました (https://github.com/github/copilot-cli/issues/76 を修正)
- `/user [list | show | swtich]`がすべての認証モードからサインインしたユーザーを含まないバグを修正しました (https://github.com/github/copilot-cli/issues/58 を修正)
- `/user switch`で別のユーザーに切り替えてもGitHub MCPサーバーで有効にならないバグを修正しました
- スクリーンリーダーの体験を改善しました。`@`ファイルピッカー、`--resume`セッションピッカー、`/`コマンドピッカーのスクロールバーを無効化しました
- スクロールバーコンテナのポリッシュを改善しました（幅を広げ、ガターの不透明度を下げた）
- 入力領域へのマイナーなビジュアル改善（現在のモデルインジケーターを右に移動してCWDと混雑を避け、ファイルピッカーの「インデックス中」インジケーターのポジショニングを改善、完成メニューのヒント形式を改善）
- マークダウンの可読性を改善し、見出しの`#`プレフィックスを除外しました
- シェルコマンドからパスを抽出する方法を改善しました。これにより、https://github.com/github/copilot-cli/issues/159、https://github.com/github/copilot-cli/issues/67 を修正する可能性があります

## 0.0.331 - 2025-10-01

- ファイル読み取り/編集タイムラインイベントの情報密度を改善しました
- `--banner`ヘルプテキストの不正確性を修正しました。以前は、スタートアップバナーを常に表示するように設定を永続的に変更することを暗示していました
- `/model`リストを改善して、ユーザーがアクセスして使用できるモデルのみを表示するようにしました -- 以前、ユーザーがアクセスできないモデルを使用しようとすると（Copilotプラン、地理的領域などが原因）、`model_not_supported`エラーが表示されていました。これはそのようなモデルをリストにも表示しないことでそれを防ぐはずです (https://github.com/github/copilot-cli/issues/112、https://github.com/github/copilot-cli/issues/85、https://github.com/github/copilot-cli/issues/40 を修正)
- マルチラインプロンプトで下矢印を押すと最初の行にラップアラウンドされるバグを修正しました (これはhttps://github.com/github/copilot-cli/issues/14 の実装に向けて進行中です)
- `@`ファイルメンション ピッカーにスクロールバーを追加し、アクティブなバッファのサイズを10アイテムに増加させました
- エージェントが実行中にプロンプトを書き込む体験を改善しました -- 上/下矢印は`@`と`/`メニューのオプション間を正しくナビゲートできるようになりました

## 0.0.330 - 2025-09-29

- Sonnet 4.5がすべてのユーザーにまだロールアウトされていないため、デフォルトモデルをSonnet 4に戻しました。Sonnet 4.5は`/model`スラッシュコマンドから利用可能です

## 0.0.329 - 2025-09-29

- [Claude Sonnet 4.5](https://github.blog/changelog/2025-09-29-anthropic-claude-sonnet-4-5-is-in-public-preview-for-github-copilot/)のサポートを追加し、デフォルトモデルにしました
- `/model`スラッシュコマンドを追加してモデルを簡単に変更できます (https://github.com/github/copilot-cli/issues/10 を修正)
    - `/model`はモデルを変更するためのピッカーを開きます
    - `/model <model>`はモデルを指定されたパラメーターに設定します
- 入力テキストボックスの上に現在選択されたモデルの表示を追加しました (https://github.com/github/copilot-cli/issues/120、https://github.com/github/copilot-cli/issues/108 のフィードバックを対処)
- ユーザーが不正なコマンドライン引数を提供した場合のエラーメッセージを改善しました。(https://github.com/github/copilot-cli/issues/96 からの非対話モードの検出可能性に関するフィードバックを対処)
- `Ctrl+r`の動作を変更して、最近のタイムラインアイテムのみを展開するようにしました。`Ctrl+r`を実行した後、`Ctrl+e`を使用してすべてを展開できます
- 単語モーションロジックを改善してシュープトレンドラインを検出します：単語モーションキーを使用すると、行の最初の単語に正しく移動できるようになりました
- 入力ボックスでのマルチラインの入力処理を改善しました：入力テキストボックスはスクロール可能で、10行に制限されています。長いプロンプトが画面全体を占めることはなくなります！ (これはhttps://github.com/github/copilot-cli/issues/14 の実装に向けて進行中です)
- 入力ボックスから左と右のボーダーを削除しました。これにより、テキストをコピーしやすくなります！
- シェル ルールにグロブ マッチングを追加しました。`--allow-tool`と`--deny-tool`を使用する場合、`shell(npm run test:*)`などと指定して、`npm run test`で始まるシェルコマンドに一致させることができます
- 相対時間表示、セッションメッセージ数などで`copilot --resume`インターフェースを改善しました (https://github.com/github/copilot-cli/issues/97 を修正)

## 0.0.328 - 2025-09-26

- 組織のポリシーによってCopilot CLIがブロックされた場合のエラーメッセージを改善しました (https://github.com/github/copilot-cli/issues/18 を修正)
- 「Copilot Requests」パーミッションを持たないPATを使用する場合のエラーメッセージを改善しました (https://github.com/github/copilot-cli/issues/46 を修正)
- `/user list`の出力を改善して、どれが現在のユーザーであるかを明確にしました
- PowerShellの`ForEach-Object`の解析とコマンド名式（例：`& $someCommand`）の検出を改善しました
