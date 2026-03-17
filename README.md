# Databricks
This is a note about what I learned.

## data engineer associate
https://www.databricks.com/learn/certification/data-engineer-associate

- target date: 2025/7/13
- note: <https://github.com/seiji1997/Databricks/tree/master/data_engineer_associate>

## data engineer professional
https://www.databricks.com/learn/certification/data-engineer-professional

- target date: 2025/7/20
- note: <https://github.com/seiji1997/Databricks/tree/master/data_engineer_professional>



### Snowflake と Databricks の AI 比較は、優劣ではなく適合性で見る
- Snowflake は自然言語BI・semantic views・managed な活用導線に強く、Databricks は Agent 開発・評価監視・作り込み自由度に強い。

本資料の目的は、Snowflake と Databricks の AI / LLM 関連機能について、どちらが一律に優れているかを決めることではない。見るべきなのは、どのユースケースに、どの条件下で、どちらがより自然にフィットするかである。Snowflake は Cortex Analyst、Cortex Search、Cortex Agents、semantic views、AI Observability を通じて、Snowflake 上の構造化・非構造化データを自然言語や AI で活用する導線を強く打ち出している。一方 Databricks は Genie spaces、Unity Catalog metric views、Mosaic AI Agent Framework、AI agent tools、MLflow Tracing / evaluation を通じて、GenAI アプリや AI agent を build・deploy・manage する基盤として整理している。

### 本比較の目的は、ユースケースごとに「どちらが自然か」を整理すること
- この比較は機能一覧の勝敗表ではなく、AI 活用の主戦場と導入条件の違いを整理するためのものである。

比較の前提は、Snowflake と Databricks が AI を置いている中心領域がやや異なる、という点にある。Snowflake は、構造化データへの自然言語アクセスや、意味定義されたデータ資産の活用を短い導線で実現する方向に強みがある。Databricks は、RAG や agent を構築し、その後に評価・監視・改善まで回していくライフサイクル全体を強く打ち出している。したがって本資料では、製品機能を横並びで比較するのではなく、自然言語BI、KPI 統一、Enterprise RAG、横断アシスタント、Agent 開発基盤、LLMOps といったユースケース単位で整理する。

### 比較は「使う」「作る」「育てる」の3層で整理するとわかりやすい
- 構造化データへの自然言語活用、RAG / Agent の構築、評価・監視を含む運用の3層に分けると、比較の粒度が揃う。

第1層は「使う」層であり、主に自然言語BI、Text-to-SQL、KPI 統一、セマンティック定義を扱う。ここでは Snowflake の Cortex Analyst と semantic views、Databricks の Genie spaces と Unity Catalog metric views の関係が中心になる。第2層は「作る」層であり、Enterprise RAG、構造化 + 非構造化をまたぐ社内アシスタント、tool calling agent の構築を扱う。ここでは Snowflake の Cortex Search / Cortex Agents と、Databricks の Mosaic AI Agent Framework / AI agent tools の比較が中心になる。第3層は「育てる」層であり、評価、監視、トレース、継続改善、品質管理を扱う。ここでは Snowflake の AI Observability / Cortex Agent evaluations と、Databricks の MLflow Tracing / evaluation / production monitoring が主な比較対象になる。

### 全体マトリックスでは、Snowflake は「短い導線」、Databricks は「広い自由度」が見える
- 構造化データ活用では Snowflake が見えやすく、Agent 基盤や LLMOps では Databricks が前に出やすい。一方で RAG やガバナンスは要件と既存基盤への寄り方で評価が分かれる。

自然言語BIと KPI 統一では、semantic views と Cortex Analyst の直結がある Snowflake の方が、業務定義を壊さずに自然言語分析を成立させる流れを描きやすい。Enterprise RAG では、Snowflake は Cortex Search により managed な検索導線を短く描きやすく、Databricks は AI agent tools を通じて retrieval をより柔軟に組み込みやすい。構造化 + 非構造化をまたぐ社内アシスタントでは両者とも対応可能だが、Snowflake は Snowflake 上の資産を中心に活用する構成に自然であり、Databricks は将来の外部接続や agent system 化まで伸ばしやすい。本格的な Agent 開発基盤と LLMOps では、Databricks が Agent Framework、AI agent tools、MLflow Tracing / evaluation / monitoring をより明示的にそろえており、比較上は前に出やすい。

### 自然言語BI と KPI 統一は、Snowflake の強みが最も出やすい領域
- semantic views と Cortex Analyst の直結により、業務定義を壊さずに自然言語分析を成立させやすい。

この領域で重要なのは、単に自然言語で質問できることではなく、業務用語を理解できるか、複数テーブルを正しく結合できるか、KPI の意味を壊さないかである。Snowflake の semantic views は、ビジネス概念、メトリクス、エンティティ間の関係性をデータベース内に保持でき、Cortex Analyst から自然言語クエリに利用できる。そのため、「governed な自然言語BIを短い導線で実現する」という観点では Snowflake の構成はかなり一直線である。Databricks も Genie spaces と Unity Catalog metric views により、自然言語分析体験と KPI の一貫定義を実現できるが、比較上は自然言語BIの主戦場として Snowflake の方が見えやすい。したがって、現場向けに自然言語BIを早く立ち上げたい場合や、KPI 定義を先に固めてその上に AI を載せたい場合は、Snowflake が自然な選択になりやすい。

### Enterprise RAG と横断アシスタントは、要件次第で評価が分かれる
- Snowflake は managed に速く立ち上げやすく、Databricks は retrieval や agent 接続を深く設計しやすい。差は「できる / できない」より「どこまで作り込むか」にある。

Enterprise RAG では、検索品質、更新反映、構築速度、将来の拡張性が主な評価ポイントになる。Snowflake の Cortex Search は、ハイブリッド検索を managed に提供し、embedding、インフラ保守、検索パラメータ調整、継続的なインデックス更新を大きく意識せずに立ち上げやすい。さらに Cortex Agents は structured / unstructured の両方をまたいでオーケストレーションでき、custom tools によって追加ロジックも組み込める。Databricks は AI agent tools を通じて、文書検索、データベース照会、REST API 呼び出し、custom code 実行を組み合わせやすく、managed MCP / external MCP / custom tools によって retrieval を agent の一部として柔軟に設計しやすい。そのため、Snowflake 上の資産で企業内検索や文書QAを素早く成立させたいなら Snowflake が自然であり、RAG を agent 基盤の一部として設計し、将来的な外部接続や継続改善まで見据えるなら Databricks が自然である。

### 本格的な Agent 開発と継続改善まで含めると、Databricks が優位に見えやすい
- Databricks は Mosaic AI Agent Framework、AI agent tools、MLflow Tracing / evaluation / monitoring により、build・deploy・monitor の流れを強く打ち出している。Snowflake も機能は揃うが、開発基盤としての見せ方は Databricks の方が強い。

本格的な agent 開発基盤では、tool 接続の自由度、authoring の柔軟性、外部 API 連携、デプロイ導線、将来の拡張性が重要になる。Databricks は、任意の authoring library で作成した agent を扱える構成を取り、AI agent tools で構造化データ、非構造化データ、REST API、custom logic を接続できる。さらに MLflow Tracing は inputs、outputs、intermediate steps、metadata を記録し、evaluation では開発時に使った scorers を本番監視にも持ち込みやすい。Snowflake も Cortex Agents、custom tools、AI Observability、Cortex Agent evaluations を持っており、agent の評価やトレースは可能である。ただし比較上は、PoC を越えて agent を継続的に設計・評価・改善していく「開発基盤」としての前面の出し方は Databricks の方が強く、本格的な Agent 開発や LLMOps を主戦場とする場合は Databricks が自然に見えやすい。

### 最終的な選択は、目指すゴールと既存基盤で決まる
- 構造化データを自然言語で早く価値化したいなら Snowflake、Agent や GenAI アプリを継続改善前提で育てたいなら Databricks が自然である。ガバナンスは優劣より、主要データ資産と定義・権限の重心がどこにあるかに依存する。

Snowflake を選びやすいのは、構造化データへの自然言語アクセスを早く立ち上げたい場合、KPI や業務定義をセマンティックに整えた上で AI を載せたい場合、Snowflake 上の資産をできるだけ短い導線で活用したい場合である。Databricks を選びやすいのは、RAG や agent を開発対象として深く作り込みたい場合、外部ツールや API を柔軟につなぎたい場合、Tracing・evaluation・monitoring を含む継続改善まで前提に置く場合である。一方で、ガバナンスやデータ統合の論点は、製品単体の優劣というより、自社の主要データ資産、メトリクス定義、権限制御をどちら側に寄せるかで重みが変わる。したがって最終判断は、製品機能の単純比較ではなく、「何を早く実現したいのか」「将来的にどこまで育てたいのか」「自社データはどこに重心があるのか」という3つの問いで行うべきである。
