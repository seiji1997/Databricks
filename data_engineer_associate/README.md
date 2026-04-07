## data engineer associate
https://www.databricks.com/learn/certification/data-engineer-associate

- target date: 2025/7/13

# Snowflake × Databricks

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

  
