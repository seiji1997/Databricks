## data engineer associate
https://www.databricks.com/learn/certification/data-engineer-associate

- target date: 2025/7/13

## 本資料で比較している対象

本資料は、Snowflake と Databricks の製品全体を比較するものではなく、  
AI・BI・agent 活用に関わる主要機能と、その組み合わせ方を比較したものである。

比較にあたっては、「ほぼ1対1で対応づけられる機能」と「ユースケース単位で組み合わせる機能」を分けて整理し、  
何を早く実現したいか、どこまで作り込みたいか、という実務上の観点を含めて評価している。

なお、成熟度はベンダー単位ではなく、各行ごとに GA / Preview / Mixed を付与している。


## 主要用語の注釈（一言説明）

### Snowflake 側
- **Semantic Views**：業務指標や関係性を含めて定義する Snowflake の semantic object
- **Cortex Analyst**：自然言語から SQL を生成して分析する Snowflake の機能
- **Cortex Search**：RAG や検索型AIに使える Snowflake のベクトル検索 / retrieval 機能
- **Cortex Agents**：Snowflake 上の各種機能やツールを組み合わせて agent を構成する機能
- **Cortex AI Functions / AI SQL**：SQL や Python から LLM / AI 推論を呼び出す Snowflake の機能群
- **Document AI / AI_PARSE_DOCUMENT**：文書から情報抽出や構造化を行う Snowflake の機能
- **AI Observability**：AI / agent 実行の可視化・監視・評価を支援する Snowflake の機能
- **Snowflake-managed MCP server**：Snowflake 資産やツールを MCP 経由で公開する Snowflake の機能

### Databricks 側
- **Metric Views**：KPI や指標を一貫して定義・再利用する Databricks の governed metrics 機能
- **Genie**：自然言語でデータに質問し、分析結果を得る Databricks の AI / BI 機能
- **Genie knowledge store**：Genie の回答精度を改善するための知識・文脈管理機能
- **AI Functions / ai_query**：SQL から LLM / モデル / agent を呼び出せる Databricks の機能
- **Mosaic AI Vector Search**：RAG や検索型AI向けの Databricks のベクトル検索機能
- **MLflow Tracing**：LLM / agent の実行過程を追跡する Databricks / MLflow の tracing 機能
- **mlflow.genai.evaluate**：LLM / agent の出力を評価するための Databricks / MLflow の評価機能
- **Databricks Apps**：作成した AI / データアプリを配備・公開する Databricks のアプリ提供機能
- **AI Playground**：GUI ベースで AI / agent を試作・検証できる Databricks の環境
- **Managed MCP / External MCP / Custom MCP**：Databricks 上で MCP によりツールや外部接続を構成する仕組み
- **Agent Framework**：Databricks 上で agent を構成・接続・運用するための枠組み

# Snowflake × Databricks

# 比較カテゴリーの説明一覧

本比較表では、Snowflake と Databricks の機能を単純に製品名で並べるのではなく、
「何を実現するための機能か」という観点で比較カテゴリーを設定している。
以下は、それぞれの比較カテゴリーが何を意味するかを整理したもの。

| 比較カテゴリー | このカテゴリで見ていること | 主に確認したい論点 |
|---|---|---|
| KPI / metric semantic layer | KPI、指標、業務定義、メトリクスの定義をどこで・どう一元管理できるかを見るカテゴリ。単なるテーブル定義ではなく、「売上」「件数」「粗利率」のような業務指標を統一的に扱えるかを確認する。 | KPI定義を共通化できるか、業務部門とIT部門で同じ指標を参照できるか、semantic layer がどこまで広く持てるか |
| 自然言語BI / Text-to-SQL | ユーザーが自然言語で質問し、その内容に応じてSQL生成や分析結果取得ができるかを見るカテゴリ。自然言語からの分析・可視化の入口としての使いやすさを確認する。 | 自然言語で質問できるか、SQL生成の精度をどう担保するか、業務利用しやすい導線があるか |
| governed metrics + NLQ（代表パターン） | KPIや指標の定義と、自然言語問い合わせをどれだけ素直につなげられるかを見るカテゴリ。単体機能ではなく、「定義された業務指標を自然言語で使う」という代表的な構成パターンを比較する。 | semantic / metric 定義と NLQ がどの程度自然につながるか、業務部門向けの説明がしやすいか |
| SQL / データ処理に AI を埋め込む | SQLやデータ処理フローの中に、LLMやAI推論を直接組み込めるかを見るカテゴリ。分析や前処理の延長でAIを使えるかを確認する。 | SQLの中で推論を呼べるか、データ処理基盤の延長としてAIを組み込めるか、開発・運用しやすいか |
| 文書抽出 / パース | PDF、帳票、非構造化文書などから、必要な情報を抽出・分類・構造化できるかを見るカテゴリ。文書をデータとして扱う導線があるかを確認する。 | 文書処理をすぐ始められるか、抽出のためにどこまで追加設計が必要か、製品として整っているか |
| Vector search / retrieval foundation | ベクトル検索や類似検索を使って、RAGや検索型AIの基盤を作れるかを見るカテゴリ。検索インデックスの管理や同期、検索品質の運用まで含めて確認する。 | ベクトル検索基盤を作れるか、RAGを立ち上げやすいか、検索インデックスの運用がしやすいか |
| MCP ベースのツール接続 | MCP を使って、AIが各種ツールやデータ資産に接続できるかを見るカテゴリ。AIに「何を触らせられるか」「どこまで外とつなげられるか」を確認する。 | MCPで何を公開できるか、Snowflake / Databricks 内外の資産に接続しやすいか、標準的な接続方式を持てるか |
| トレース / 評価 / 監視 | AIやagentの実行内容を追跡し、評価し、監視できるかを見るカテゴリ。開発後の可視化・検証・品質担保のしやすさを確認する。 | 実行ログを追えるか、評価を回せるか、本番運用時の品質監視を継続できるか |
| 管理者向け監視 / 監査性 | 管理者視点で、利用状況、アクセス状況、ログ、フィードバックなどを把握し、統制・監査できるかを見るカテゴリ。 | 管理者が状況を確認しやすいか、監査ログや利用状況を追えるか、統制しやすいか |
| 作者 / 運用者向けの品質改善 | 利用ログやフィードバックをもとに、回答精度や使い勝手を継続的に改善できるかを見るカテゴリ。管理者監視とは別に、「育てる運用」がどれだけしやすいかを確認する。 | フィードバックを改善につなげやすいか、チューニング運用がしやすいか、品質改善の導線が明確か |
| API / アプリ提供 | 作った機能を API として外部から使えるか、またはアプリとして提供しやすいかを見るカテゴリ。試作だけで終わらず、利用可能な形で提供できるかを確認する。 | REST API 化しやすいか、アプリとして公開しやすいか、PoC から本番利用へつなげやすいか |
| governed NL BI | 業務定義された指標を使いながら、自然言語で分析できる構成を作れるかを見るユースケースカテゴリ。 | KPI定義とNLQを組み合わせて、業務部門向けBIを成立させやすいか |
| enterprise RAG を速く立ち上げる | 社内文書やデータを検索しながら回答するRAGを、どれだけ速く立ち上げられるかを見るユースケースカテゴリ。 | RAGの初速、検索基盤の準備しやすさ、PoCの立ち上げやすさ |
| 構造化 + 非構造化をまたぐ社内アシスタント | DBの構造化データと、文書・ナレッジなどの非構造化データを横断して回答する社内アシスタントを作れるかを見るカテゴリ。 | structured / unstructured をまたぐ自然な構成を取りやすいか |
| SaaS / 外部APIまでつなぐ agent | 社内データを見るだけでなく、外部SaaSやAPIまで呼び出して処理できる agent を作れるかを見るカテゴリ。 | 外部接続のしやすさ、API連携の柔軟性、agent の拡張性 |
| 継続改善ループを回す agent 運用 | agent を作って終わりではなく、実利用の中で観測・評価・改善を回し続けられるかを見るカテゴリ。 | 評価運用を継続しやすいか、改善サイクルを業務として回せるか |
| GUI / no-code 起点で試作し、本番化する | GUIやno-codeに近い操作から試作を始め、その後にコード化・API化・本番化へつなげられるかを見るカテゴリ。 | 最初に触りやすいか、PoCから本番へ移しやすいか、利用者層を広げやすいか |

**2026-03-18時点の公式ドキュメントを反映**

- 1対1比較
- 組み合わせ比較
- GA / Preview を明示

## 成熟度の凡例

| ラベル | 意味 |
|---|---|
| GA | 一般提供 |
| Preview | 公開はされているが、成熟度には留意が必要 |
| Mixed | 中核機能は GA だが、周辺に Preview が混在 |

## この deck での見方
1. まず、比較対象が同じ粒度かを確認する  
2. 次に、各行で本当に比べている「機能の本体」は何かを見る  
3. 最後に、実務上どちらが自然に説明しやすいかを短く整理する


# ① ほぼ1対1で並べる比較表（前半）

| 比較カテゴリ | Snowflake | Databricks | 成熟度（2026-03-18時点） | 実務上の見方 |
|---|---|---|---|---|
| KPI / metric semantic layer | **Semantic Views** により、logical tables、relationships、dimensions、metrics を定義可能。Snowsight wizard / AI-assisted generator あり。 | **Unity Catalog Metric Views** により、ガバナンスされた KPI 定義を UC object として集中管理可能。SQL / Catalog Explorer UI で作成可能。 | Snowflake: Mixed — 中核は GA、周辺に Preview あり。 Databricks: Preview — Metric Views は Public Preview。 | 完全に同格ではない。Snowflake は broader semantic model、Databricks は KPI 中心。ただし governed BI の比較軸としては十分成立する。 |
| 自然言語BI / Text-to-SQL | **Cortex Analyst** により、semantic views に強く結びついた managed text-to-SQL を提供。REST API で組み込み可能。 | **Genie spaces** により、Unity Catalog metadata + space-level knowledge store を用いた自然言語分析が可能。tables / views / materialized views / metric views を利用可能。 | Snowflake: GA 寄り。 Databricks: 本番利用前提の surface はあるが、精度は space curation に依存。 | “一直線に立ち上げる” なら Snowflake が説明しやすい。“運用で育てる” なら Databricks の語りがしやすい。 |
| governed metrics + NLQ（代表パターン） | **Semantic Views + Cortex Analyst** により、semantic 定義と NLQ が直結する。 | **Metric Views + Genie** が代表パターン。ただし Genie は Metric Views のみに依存するわけではない。 | Snowflake: GA / tighter native binding。 Databricks: Preview + broader implementation path。 | 経営層・業務部門向け比較として最もきれいな行。Databricks 側は「代表パターン」と注記しておくのが安全。 |
| SQL / データ処理に AI を埋め込む | **Cortex AI Functions / AI SQL** により、SQL を中心に AI 推論を組み込める。Python からも利用可能。機能単位で成熟度に差がある。 | **AI Functions / ai_query** により、SQL から serving endpoint や deployed agent を呼び出せる。 | Snowflake: Mixed — function 単位で差がある。 Databricks: Preview — AI Functions は Public Preview。 | 比較軸は「SQL ネイティブな推論実行」。AI 基盤全体の比較に広げすぎない方が整理しやすい。 |
| 文書抽出 / パース | **Document AI / Document Processing Playground / AI_PARSE_DOCUMENT** により、文書抽出の製品化された導線がある。 | **AI Functions + Model Serving / served or external models** により、抽出・分類を組み合わせて柔軟に構成する。 | Snowflake: GA 寄りで productized。 Databricks: composable pattern。 | “すぐ使える文書ワークフロー” は Snowflake、“モデル設計込みで柔軟に組む” は Databricks。完全な1対1ではないため、その前提で使う。 |


# ① ほぼ1対1で並べる比較表（後半）

| 比較カテゴリ | Snowflake | Databricks | 成熟度（2026-03-18時点） | 実務上の見方 |
|---|---|---|---|---|
| Vector search / retrieval foundation | **Cortex Search** により、Snowsight / SQL / API から managed retrieval を利用可能。multi-index / custom embeddings は一部 Preview 要素あり。 | **Mosaic AI Vector Search** により、continuous / triggered sync を含む運用が可能。UI / SDK / REST に対応。 | Snowflake: Mixed — コア retrieval は成熟、一部拡張は Preview。 Databricks: 運用面の成熟度が高い。 | “まず managed に速く始める” なら Snowflake。“index lifecycle や運用柔軟性まで見る” なら Databricks。 |
| MCP ベースのツール接続 | **Snowflake-managed MCP server** により、Analyst / Search / Agents / custom tools / SQL execution を公開可能。 | **Managed MCP / External MCP / Custom MCP** を提供。Custom MCP は Databricks Apps 上でホスト可能。 | Snowflake: GA。 Databricks: Preview mixed — managed / external MCP は Public Preview。 | Snowflake は Snowflake 資産の接続が分かりやすい。Databricks は接続面の広がりが魅力だが、成熟度はまだ揃っていない。 |
| トレース / 評価 / 監視 | **AI Observability + Agent request monitoring + Cortex Agent evaluations** により、trace / evaluation / benchmarking が揃う。 | **MLflow Tracing + mlflow.genai.evaluate + production monitoring** により、開発から本番まで一貫した改善ループを構成しやすい。 | Snowflake: GA core。 Databricks: lifecycle の一貫性が強い。 | “機能があるか” は両者 yes。改善ループの説明しやすさは Databricks の方が前面に出る。 |
| 管理者向け監視 / 監査性 | **Analyst monitoring tab、feedback API、SQL で取得可能なログ** により、管理者視点の監視・監査が可能。 | **AI / BI 管理画面、usage monitoring、audit 系機能** により、管理者視点の可視化が可能。 | Snowflake: GA / admin log が明確。 Databricks: 監視面はあるが、チューニング面とは分けて見るべき。 | この行は「監査・管理」に限定した方が安全。精度改善の運用は次行に分ける方が説明しやすい。 |
| 作者 / 運用者向けの品質改善 | **Analyst feedback、agent feedback、monitoring logs** を用いて改善可能。 | **Genie knowledge store、inspect mode、benchmarks、quality monitoring** により、改善導線がより明示的。 | Snowflake: 機能はある。 Databricks: tuning workflow がより前面に出る。 | BI / NLQ の継続改善運用は Databricks の方が語りやすい。元表の「管理 / 監査」とは分けて置いた方が正確。 |
| API / アプリ提供 | **Cortex Analyst REST API、Cortex Search service endpoint、managed services** を既存アプリに組み込みやすい。 | **AI Playground で no-code 試作 → code export → Model Serving / Databricks Apps**。Apps は GA。 | Snowflake: managed API path が強い。 Databricks: Apps は GA、AI Playground は no-code 試作の導線。 | API として埋め込むなら Snowflake、agent 付きアプリとして前面に出すなら Databricks が分かりやすい。 |


# ② 組み合わせで比較する表

| 実装したいもの | Snowflake の組み合わせ | Databricks の組み合わせ | 成熟度 / 注記 | 実務上の見方 |
|---|---|---|---|---|
| governed NL BI | **Semantic Views + Cortex Analyst** | **Metric Views + Genie + knowledge store** | Snowflake は tighter native path。Databricks は代表パターンとして成立するが、Metric Views は Preview。 | 業務定義込みの自然言語BIを最短で語るなら Snowflake。Databricks も curation 前提なら十分比較対象になる。 |
| enterprise RAG を速く立ち上げる | **Cortex Search** 単体、必要に応じて **Cortex Agents** を追加 | **Vector Search + managed retriever / MCP**。試作は AI Playground も活用しやすい。 | Snowflake は managed setup が短い。Databricks は retrieval ops の調整幅が大きい。 | “まず速く立ち上げる” は Snowflake。“検索基盤として育てる” は Databricks。 |
| 構造化 + 非構造化をまたぐ社内アシスタント | **Cortex Analyst + Cortex Search + Cortex Agents** | **Genie / UC data + Vector Search + Agent Framework / MCP tools** | どちらも成立する。Snowflake は native composition、Databricks は compound-system 的。 | Snowflake は “Snowflake 内の横断活用”、Databricks は “外も含めた社内アシスタント” として整理しやすい。 |
| SaaS / 外部APIまでつなぐ agent | **Cortex Agents + custom tools + managed MCP** | **Agent Framework + external service tools + external / custom MCP** | Databricks の external service tools と external MCP は Public Preview。 | 外部接続を強く見せるなら Databricks が自然。Snowflake も追随可能だが、主戦場の見せ方ではない。 |
| 継続改善ループを回す agent 運用 | **AI Observability + Agent monitoring + Agent evaluations** | **MLflow Tracing + Evaluation + Production Monitoring + human feedback** | Snowflake も必要機能は揃う。Databricks は開発と本番の改善ループがより見えやすい。 | 改善ループの説明力は Databricks が強い。ただし Snowflake を “不足” と表現する必要はない。 |
| GUI / no-code 起点で試作し、本番化する | **Snowsight wizard / AI Studio → REST / service integration** | **AI Playground no-code → code export → Model Serving / Apps** | Databricks Apps は GA。AI Playground は no-code 試作の導線として整理しやすい。 | GUI でまず触る体験は Databricks がかなり近づいている。一方で semantic / search の統制された設定は Snowflake が綺麗。 |

# 参考URL（公式ドキュメント）

## Snowflake
- Semantic Views overview  
  https://docs.snowflake.com/en/user-guide/views-semantic/overview

- Semantic Views UI  
  https://docs.snowflake.com/en/user-guide/views-semantic/ui

- Cortex Analyst  
  https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-analyst

- Cortex Search  
  https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-search/cortex-search-overview

- Cortex Agents  
  https://docs.snowflake.com/en/user-guide/snowflake-cortex/cortex-agents

- Cortex AI Functions / AI SQL  
  https://docs.snowflake.com/en/user-guide/snowflake-cortex/aisql

- AI Observability (GA)  
  https://docs.snowflake.com/en/release-notes/2025/other/2025-07-31-ai-observability-ga

- Managed MCP / Agent evaluations (GA)  
  https://docs.snowflake.com/en/release-notes/2025/other/2025-11-04-cortex-agents-mcp

## Databricks
- Metric Views  
  https://docs.databricks.com/aws/en/metric-views/

- Genie  
  https://docs.databricks.com/aws/en/genie/

- Genie knowledge store  
  https://docs.databricks.com/aws/en/genie/knowledge-store

- AI Functions / ai_query  
  https://docs.databricks.com/gcp/en/large-language-models/ai-functions

- Vector Search  
  https://docs.databricks.com/aws/en/vector-search/vector-search

- MLflow Tracing / Evaluation  
  https://docs.databricks.com/aws/en/mlflow3/genai/tracing/

- MCP overview  
  https://docs.databricks.com/aws/en/generative-ai/mcp/

- AI Playground / Apps  
  https://docs.databricks.com/aws/en/getting-started/gen-ai-llm-agent

  
