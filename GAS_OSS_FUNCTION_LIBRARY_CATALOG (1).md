# GAS OSS 機能ライブラリ・実装サンプル一覧

> 🍪🛒🎩 共同開発用メモ  
> Google Apps Script / Google Workspace の業務改善で再利用できる、**機能系のOSSライブラリ・フレームワーク・実装サンプル**を用途別に整理した一覧です。

## この一覧の範囲

- `clasp`、VS Code、Git、スターターテンプレート、ローカルテスト環境などの**開発環境系**は含めていません。
- Cloud Run、Python、pandas はGASライブラリではないため、本一覧の対象外です。
- URLは載せず、GitHubでそのまま検索できるように**リポジトリ名・ライブラリ名を正確に記載**しています。
- `Library` はGASのライブラリ追加またはソース取り込みで使うもの、`Sample` は必要部分をコピー・改造するもの、`Framework` は複数機能を組み立てる基盤、`Application` は完成形に近い参考実装です。

---

## 🍮 サイドバー構想との対応早見表

| 🍮で作りたい機能 | 主に参考にするOSS |
|---|---|
| Driveから複数のSpreadsheetを選ぶ | `Google Picker sample` |
| サイドバー内でDriveのフォルダやファイルを選ぶ | `File_Picker_using_Google_Apps_Script_and_Javascript_without_3rd_party` |
| PCからExcel・CSV・画像を複数アップロードする | `AsynchronousResumableUploadForGoogleDrive` |
| 入力フォームや画像を受け取り、Spreadsheetへ記入する | `HtmlFormApp`、`ImgApp`、`GeminiWithFiles` |
| 現在のSpreadsheetを整える | `TableApp`、`RangeListApp`、`RichTextAssistant` |
| 指定フォルダ内のファイルを列挙する | `FilesApp` |
| Docs・Slides・PDFを自動生成する | `TemplateApp`、`PDFApp` |
| 外部API・Webhookへ画像やファイルを送る | `FetchApp`、`apps-script-oauth2`、`GoogleApiApp` |
| 長い処理を分割・再開・定期実行する | `LongRun`、`TriggerApp`、`RunAll` |
| Gmailの添付やメッセージを自動処理する | `Gmail Processor`、`GmailToList` |
| Geminiで画像・PDFを読み、構造化して記入する | `GeminiWithFiles`、`GenAIApp` |
| GASをMCPやAIエージェントの入口にする | `MCPApp`、`ToolsForMCPServer`、`GASADK`、`A2AApp` |

---

# 1. サイドバー・ボタン・ファイル選択・アップロード

## `Google Picker sample`

**種別:** Google公式 `Sample`

Google Driveのファイル選択画面を、GASのダイアログやサイドバーから開くための公式サンプルです。複数選択を有効にできるため、複数のSpreadsheetを選んで統合処理へ渡す「🍮まとめて整える」ボタンの土台になります。

## `File_Picker_using_Google_Apps_Script_and_Javascript_without_3rd_party`

**種別:** `Sample` / Tanaike

GASと素のJavaScriptだけで、SpreadsheetのサイドバーにDriveファイル選択UIを作るサンプルです。フォルダをたどる処理やMIMEタイプによる絞り込みが含まれ、🍮サイドバーへ独自デザインのファイル選択欄を組み込む時の参考になります。

## `AsynchronousResumableUploadForGoogleDrive`

**種別:** `Sample` / Tanaike

Spreadsheetのサイドバー、ダイアログ、Web Appから、PC上の複数ファイルをGoogle Driveへ非同期アップロードするサンプルです。大きなファイルの分割アップロードと進捗表示があり、Excel・CSV・画像を複数選んで🍮へ渡す画面に使えます。

## `HtmlFormApp`

**種別:** `Library` / Tanaike

HTMLフォームの入力値や添付ファイルを解析し、指定したSpreadsheetへ行として記録するライブラリです。列名の対応付け、保存先フォルダ、複数回答、複数ファイルなどを扱えるため、「画像アップロードと記入」や社内入力フォームの基礎部品になります。

## `Google Workspace Add-ons Samples` (`add-ons-samples`)

**種別:** Google公式 `Sample Collection`

Gmail、Calendar、Drive、Docs、Sheetsなどへ共通サイドバーやカードUIを表示するWorkspace Add-onの公式実装集です。ボタン、入力欄、通知、画面更新など、全社員へ共通の🍮メニューを配る時のUIパターンを確認できます。

---

# 2. Spreadsheet・表データ操作

## `TableApp`

**種別:** `Library` / Tanaike

Google Sheetsの「テーブル」をGASから扱いやすくするラッパーです。生のSheets API用JSONを毎回組み立てずに、テーブルの作成・取得・管理を行えるため、構造化された業務表を作る時に使えます。

## `RangeListApp`

**種別:** `Library` / Tanaike

離れた複数セルや複数シートの範囲をまとめて取得・更新・置換するライブラリです。各セルへ異なる値を入れる、正規表現で置換する、チェックボックスを設定するなど、点在したセルを一括処理する時に向いています。

## `RichTextAssistant`

**種別:** `Library` / Tanaike

Spreadsheetのセル内リッチテキストを、既存の装飾を保ったまま編集するためのライブラリです。文字の追加・削除・挿入、部分的なスタイル変更、RichTextとJSONの相互変換を行えます。

## `RichTextApp`

**種別:** `Library` / Tanaike

Google DocsとSpreadsheetの間で、文字装飾を保ちながらテキストを移動するライブラリです。セル内リッチテキストのHTML化や、Spreadsheet範囲のHTMLテーブル化にも使えるため、書式付きメールや資料生成へつなげられます。

## `DocsServiceApp`

**種別:** `Library` / Tanaike

Document、Spreadsheet、Slidesの標準サービスや各APIだけでは届きにくい操作を補う横断ライブラリです。Spreadsheet内の画像・コメント取得や、文書・表・スライドに関する特殊処理をまとめて扱う補助層として使えます。

---

# 3. Docs・Slides・PDF・画像

## `TemplateApp`

**種別:** `Library` / Tanaike

Spreadsheetの各行をデータベースとして使い、Google DocsやGoogle Slidesのテンプレートから文書を量産するライブラリです。文字の置換に加えて、セルの書式や画像も反映できるため、見積書、証明書、顧客資料、定型報告書の生成に使えます。

## `PDFApp`

**種別:** `Library` / Tanaike

GAS上でPDFの結合、ページ抽出、並べ替え、PNG変換、メタデータ操作、PDFフォームの読み書きなどを行うライブラリです。SpreadsheetやDocsから出力したPDFへページ番号・ヘッダー・画像・文字を追加する処理にも使えます。

## `ImgApp`

**種別:** `Library` / Tanaike

画像のサイズ・DPI取得、リサイズ、形式変換、切り抜き、結合、Driveサムネイル更新を行う画像処理ライブラリです。Drive APIを使ったOCR機能もあり、🍮の画像アップロードから文字起こし・セル記入へつなぐ部品になります。

---

# 4. Google Drive・ファイル管理

## `FilesApp`

**種別:** `Library` / Tanaike

指定したGoogle Driveフォルダ以下のファイルとサブフォルダを再帰的に取得し、一覧またはツリーとして返すライブラリです。共有ドライブにも対応しており、「指定フォルダに入れた複数ファイルをまとめて処理する」入口に使えます。

## `CopyFolder`

**種別:** `Library` / Tanaike

Google Driveのフォルダ構造を保ったまま、配下のファイルとサブフォルダを別の場所へコピーするライブラリです。バックアップ、案件テンプレートの複製、更新されたファイルだけを反映する同期処理などに使えます。

## `OwnershipTransfer`

**種別:** `Library` / Tanaike

指定フォルダ配下のファイル・サブフォルダを含め、所有権移転をまとめて処理するライブラリです。所有権変更後は元の所有者が管理できなくなる場合があるため、組織ルールとテスト用データを前提に扱う機能です。

---

# 5. Gmail・メール処理

## `GmailToList`

**種別:** `Library` / Tanaike

Gmail内のメッセージを一覧データとして書き出すライブラリです。メール監査用の台帳作成、過去メールの棚卸し、送受信履歴をSpreadsheetへ集約する処理の土台になります。

## `Gmail Processor`

**種別:** `Application / Library`

JSON設定に基づいてGmailのスレッド、メッセージ、添付ファイルを判定し、Drive保存やSpreadsheetへの記録を自動実行するOSSです。添付PDFや画像のOCR、メールやスレッドのPDF保存なども含み、設定駆動型の業務自動化を読む完成例になります。

---

# 6. 外部API・Google API・Webhook・認証

## `apps-script-oauth2`

**種別:** Google Workspace公式 `Library`

GASから外部サービスへOAuth 2.0接続する時に、認可画面、アクセストークン、更新トークン、期限切れ後の再取得を管理するライブラリです。Workspace標準サービスに含まれないSaaSや独自APIと連携する時に使います。

## `FetchApp`

**種別:** `Library` / Tanaike

`UrlFetchApp`を拡張し、`multipart/form-data`形式のHTTPリクエストを作りやすくするライブラリです。画像・PDF・ExcelなどのBlobを外部APIやWebhookへ送る処理、複数リクエストの送信に使えます。

## `GoogleApiApp`

**種別:** `Library` / Tanaike

API名、バージョン、メソッド、パラメータからGoogle APIへのRESTリクエストを組み立てる共通ラッパーです。自動ページング、キャッシュ、ログを備え、Advanced Google ServicesにないAPIや多数のGoogle APIを統一した書き方で扱えます。

## `BatchRequest`

**種別:** `Library` / Tanaike

複数のGoogle APIリクエストをbatch requestへまとめ、結果を一括で受け取るライブラリです。Drive、Gmail、Calendarなどの大量API操作を減らす時に使えますが、batch対応状況や上限はAPIごとに確認して使います。

---

# 7. 長時間処理・並列処理・スケジュール

## `LongRun`

**種別:** `Class / Source Library`

GASの実行時間を超える処理を途中で止め、時間主導トリガーから続きの位置を再開するためのクラスです。大量行を少しずつ処理する、進捗を保存する、完了時にトリガーを片付ける構成の参考になります。

## `RunAll`

**種別:** `Library` / Tanaike

`UrlFetchApp.fetchAll()`とApps Script Execution APIまたはWeb Appを組み合わせ、複数のGAS関数を並行実行するライブラリです。6分制限の中で独立処理を分散させる設計に使えますが、現在のAPI仕様・同時実行上限・クォータを小さく検証してから採用します。

## `TriggerApp`

**種別:** `Library / MCP Server` / Tanaike

複雑な時間主導トリガーを一つの設定データから生成・確認・シミュレーションするライブラリです。曜日、時間帯、間隔などを組み合わせた定期実行を管理でき、必要に応じてMCP経由でトリガー操作を公開する構成も持っています。

---

# 8. Gemini・生成AI・MCP・A2A

## `GeminiWithFiles`

**種別:** `Library` / Tanaike

GASからGemini APIへ画像、PDF、Docs、Sheets、Slidesなどを渡し、内容を解析・生成するためのライブラリです。JSON Schemaによる構造化出力、複数ファイル処理、会話履歴、Google Search Grounding、Code Executionなどがあり、「画像を読み取って所定列へ記入する」処理に使えます。

## `GenAIApp`

**種別:** `Library`

Gemini APIとOpenAI APIをGASから共通の操作感で扱うための生成AIライブラリです。テキスト会話、画像・文書分析、Function Calling、Web検索、Vector Store、MCP Connectorなどを一つの枠組みにまとめています。

## `GASADK` (`adk-gas`)

**種別:** `Framework` / Tanaike

GASの6分制限と同期通信を前提に、LLMエージェント、ツール実行、状態保持、ルーティング、HITL停止・再開を組むためのAgent Development Kitです。MCP、A2A、Agent Skills、sub-agentを含むため、Workspace上で複数段階のAI処理を組む時の基盤になります。

## `MCPApp`

**種別:** `Library / Framework` / Tanaike

GAS Web AppをMCP ServerまたはMCP Clientとして動かし、AIクライアントからWorkspace機能をツールとして呼べるようにするライブラリです。既存GAS関数をMCP toolへ変換し、Sheets、Drive、Gmailなどの操作入口を共通化する時に使えます。

## `ToolsForMCPServer`

**種別:** `Library / Tool Collection` / Tanaike

`MCPApp`と組み合わせて使う、Google Workspace向けのMCPツール集です。Gmail、Drive、Calendar、Sheets、Docs、Slidesなどの操作が多数用意されており、自作ツールの粒度やschemaを考えるための標本箱としても使えます。

## `A2AApp`

**種別:** `Library / Framework` / Tanaike

GAS Web AppをAgent2Agentのサーバーまたはクライアントとして動かし、複数のAIエージェントを接続するライブラリです。WorkspaceのSheets、Drive、Calendarなどを担当するエージェントを分け、相互に依頼・応答させる構成に使えます。

## `Autonomous Google API Agent`

**種別:** `Application / Reference Implementation` / Tanaike

`GASADK`と`GoogleApiApp`を組み合わせ、自然言語からGoogle API操作を計画・実行する参考実装です。API schemaの確認、RBAC、メソッド単位の制御、監査をLLMの前後に置く構造を読むための実装例になります。

---

# 9. 公式サンプル・探索用カタログ

## `Google Apps Script Samples` (`apps-script-samples`)

**種別:** Google公式 `Sample Collection`

Sheets、Drive、Gmail、Docs、Slides、Calendar、Forms、Triggers、Web Apps、Google Chat Appsなどの公式サンプル集です。新しい機能を作る時に、認証・イベント・サービス呼び出しの基本形を確認する基準棚として使えます。

## `Google Apps Script Library Database`

**種別:** `Catalog` / Tanaike

世界中のGoogle Apps Scriptライブラリを検索するためのデータベースと検索アプリです。必要な機能がこの一覧にない時、新しいOSS候補を探す入口として使えます。

## `taking-advantage-of-google-apps-script`

**種別:** `Index / Knowledge Base` / Tanaike

Tanaike氏が公開しているGASライブラリ、Web App、Add-on、サンプル、ベンチマーク、技術調査をまとめた巨大インデックスです。ライブラリ名だけでは使い方が見えない時に、関連する検証記事やサンプル実装をたどる索引になります。

---

# 導入時の共通メモ

1. **Library追加型か、ソース取り込み型かを確認する。** 会社の保守方針に合わせ、外部Library参照、社内fork、必要部分のソース取り込みを選ぶ。
2. **Advanced Google ServicesとOAuth Scopeを確認する。** Drive API、Sheets API、Docs APIなどの有効化が必要なライブラリがある。
3. **本番では検証済みバージョンを固定する。** 最新版へ自動追従させず、テスト用Spreadsheetで挙動を確認してから更新する。
4. **Sampleは完成品として扱わず、業務要件へ合わせて組み込む。** 特にサイドバー、アップロード、MCP、A2Aは認証・権限・ログの構成を利用環境に合わせる。
5. **GASだけで重くなる処理は処理境界を分ける。** UI、権限、通知はGASに置き、数万行の整形やExcel処理はCloud Run + Pythonなどへ渡す構成と組み合わせられる。

---

## 🍮 この一覧から作りやすい共通メニュー

```text
🍮 Workspaceお手伝い
├─ 📎 Driveからファイルを選ぶ
├─ ⬆️ PCからExcel・CSV・画像をアップロード
├─ 📷 画像を読み取って記入
├─ 🧹 このSpreadsheetを整える
├─ 🗂️ 複数ファイルを一枚にまとめる
├─ 📄 Docs・PDFを作る
├─ ✉️ Gmail添付を保存・記録
├─ 🔗 Webhook・外部APIへ送る
└─ ⏰ 長い処理を予約・再開する
```

このメニューの表側はGASのサイドバーまたはWorkspace Add-onで共通化し、裏側の処理ごとに本一覧のライブラリを差し込んでいく想定です。
