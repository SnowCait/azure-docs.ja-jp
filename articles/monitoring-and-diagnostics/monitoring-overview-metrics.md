---
title: "Microsoft Azure のメトリックの概要 | Microsoft Docs"
description: "Microsoft Azure のメトリックとその使用方法の概要"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: johnkem
ms.openlocfilehash: eb519aab87c13e8836bf1d41992812762f0cd737
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure のメトリックの概要
この記事では、Microsoft Azure のメトリック概要、利点、および使用方法について説明します。  

## <a name="what-are-metrics"></a>メトリックとは
Azure Monitor では、テレメトリを使用して、Azure のワークロードのパフォーマンスと正常性を視覚的に確認できます。 Azure テレメトリ データの種類の中でも最も重要なのは、Azure リソースのほとんどから出力されるメトリックであり、これはパフォーマンス カウンターとも呼ばれます。 Azure Monitor では、このメトリックを複数の方法で構成して使用し、監視やトラブルシューティングを行うことができます。

## <a name="what-can-you-do-with-metrics"></a>メトリックで行えること
テレメトリの重要なソースであるメトリックを使用すると、次の作業を行うことができます。

* **パフォーマンスを追跡する**: VM、Web サイト、ロジック アプリなどのリソースのメトリックをポータルのグラフにプロットし、そのグラフをダッシュボードに固定することで、リソースのパフォーマンスを追跡できます。
* **問題の通知を受け取る**: メトリックが特定のしきい値を超えたときに、リソースのパフォーマンスに影響する場合はその旨が通知されます。
* **自動化されたアクションを構成する**: メトリックが特定のしきい値を超えたときに、リソースを自動スケールしたり、Runbook を起動したりします。
* **高度な分析を実行する**: リソースのパフォーマンスや使用傾向も報告することもできます。
* **アーカイブする**: **コンプライアンス/監査**の目的で、リソースのパフォーマンスや正常性の履歴をアーカイブします。

## <a name="what-are-the-characteristics-of-metrics"></a>メトリックの特性
メトリックの特性を次に示します。

* すべてのメトリックが **1 分間隔**です。 リソースから 1 分ごとにメトリック値が届くため、リソースの状態と正常性をほぼリアルタイムで把握できます。
* メトリックは**すぐに使用可能です**。 追加の診断を設定する必要もありません。
* 各メトリックの **30 日間の履歴** にアクセスできます。 リソースのパフォーマンスまたは正常性における最近の傾向や月単位の傾向をすばやく確認できます。
* 一部のメトリックは、**ディメンション**と呼ばれる名前と値のペアの属性を持つことがあります。 ディメンションを使うと、わかりやすい方法でメトリックをさらに分割および探索することができます。

さらに、以下を実行できます。

* 設定したしきい値をメトリックが超えたときに、そのメトリックに対して、**通知を送信するアラート ルール、または自動化されたアクションを実行するアラート ルール**を構成します。 自動スケールは自動化された特別なアクションで、リソースをスケールアウトして、Web サイトまたはコンピューティング リソースの受信要求や負荷に対応します。 しきい値を超えたメトリックに基づいてスケールインまたはスケールアウトするように、自動スケール設定のルールを構成できます。

* すべてのメトリックを Application Insights または Log Analytics (OMS) に**ルーティング**して、リソースのメトリック データでインスタント分析、検索、カスタム アラートを使用できるようにします。 メトリックをイベント ハブにストリーミングすることもできます。これにより、メトリックを Azure Stream Analytics またはカスタム アプリにルーティングし、ほぼリアルタイムで分析できます。 イベント ハブへのストリーミングは、診断設定を使用して設定します。

* メトリックは、長期間保持するために**ストレージにアーカイブ**できるほか、オフライン レポートに使用することもできます。 リソースの診断設定を構成するときに、メトリックを Azure Blob Storage にルーティングできます。

* リソースを選択して、メトリックをグラフ上にプロットするときに、Azure Portal で検出やアクセスを容易に行えるほか、**すべてのメトリックを表示**できます。

* 新しい Azure Monitor REST API でメトリックを**使用**します。

* PowerShell コマンドレットまたはクロスプラットフォーム REST API を使用して、メトリックに**クエリ**を実行します。

  ![Azure Monitor のメトリックのルーティング](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-the-portal"></a>ポータルを使用してメトリックにアクセスする
ここでは、Azure Portal を使用してメトリック グラフを作成する手順を簡単に説明します。

### <a name="to-view-metrics-after-creating-a-resource"></a>リソースの作成後にメトリックを表示するには
1. Azure Portal を開きます。
2. Azure App Service の Web サイトを作成します。
3. 作成した Web サイトの **[概要]** ブレードに移動します。
4. 新しいメトリックは、**[監視]** タイルとして表示されます。 このタイルを編集して、さらに多くのメトリックを選択できます。

   ![Azure Monitor のリソースのメトリック](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="to-access-all-metrics-in-a-single-place"></a>1 か所ですべてのメトリックにアクセスするには
1. Azure Portal を開きます。
2. 新しい **[Monitor]** タブに移動し、その下にある **[メトリック]** オプションを選択します。
3. ドロップダウン リストから、サブスクリプション、リソース グループ、およびリソースの名前を選択します。
4. 使用可能なメトリックの一覧を表示します。 次に、対象のメトリックを選択し、プロットします。
5. それをダッシュボードに固定するには、右上隅にあるピン アイコンをクリックします。

   ![Azure Monitor の 1 か所ですべてのメトリックにアクセス](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> ホスト レベルのメトリックには、VM (Azure Resource Manager ベース) および Virtual Machine Scale Sets からアクセスできます。その際、追加の診断設定は不要です。 この新しいホスト レベルのメトリックは、Windows と Linux のインスタンスで使用できます。 VM や Virtual Machine Scale Sets で Azure 診断をオンにしている場合にアクセスできる、ゲスト OS レベルのメトリックと混同しないでください。 Azure 診断の構成の詳細については、「[What is Microsoft Azure Diagnostics (Microsoft Azure 診断とは)](../azure-diagnostics.md)」を参照してください。
>
>

Azure Monitor には、プレビューで利用できる新しいメトリック グラフ化エクスペリエンスもあります。 このエクスペリエンスでは、複数のリソースのメトリックを 1 つのグラフに重ねて表示できます。 また、この新しいメトリック グラフ化エクスペリエンスを使うと、多次元メトリックのプロット、分割、フィルター処理を行うこともできます。 詳しくは、[こちらをクリック](https://aka.ms/azuremonitor/new-metrics-charts)してください。

## <a name="access-metrics-via-the-rest-api"></a>REST API を使用してメトリックにアクセスする
Azure メトリックには、Azure Monitor API を使用してアクセスできます。 メトリックの検出とアクセスに役立つ API は 2 つあります。

* [Azure Monitor メトリック定義 REST API](https://docs.microsoft.com/en-us/rest/api/monitor/metricdefinitions) を使うと、サービスに利用できるメトリックの一覧および任意のディメンションにアクセスできます。
* [Azure Monitor メトリック REST API](https://docs.microsoft.com/en-us/rest/api/monitor/metrics) を使うと、実際のメトリック データの分割、フィルター処理、アクセスを行うことができます。

> [!NOTE]
> この記事では、Azure リソースの [メトリックを対象とした新しい API](https://docs.microsoft.com/en-us/rest/api/monitor/) で使用するメトリックについて説明します。 新しいメトリック定義 API およびメトリック API のバージョンは、2017-05-01-preview です。 従来のメトリック定義とメトリックには、API バージョン 2014-04-01 でアクセスできます。
>
>

Azure Monitor REST API を使用した詳細なチュートリアルについては、「[Azure 監視 REST API のチュートリアル](monitoring-rest-api-walkthrough.md)」を参照してください。

## <a name="export-metrics"></a>メトリックのエクスポート
**[Monitor]** タブで **[診断設定]** ブレードに移動し、メトリックのエクスポート オプションを表示できます。 この記事で前述したユースケースでは、メトリック (および診断ログ) を選択して、Blob Storage、Azure Event Hubs、または OMS にルーティングできます。

 ![Azure Monitor のメトリックのエクスポート オプション](./media/monitoring-overview-metrics/MetricsOverview3.png)

これを構成するには、Resource Manager テンプレート、[PowerShell](insights-powershell-samples.md)、[Azure CLI](insights-cli-samples.md)、または [REST API](https://msdn.microsoft.com/library/dn931943.aspx) を使用します。

## <a name="take-action-on-metrics"></a>メトリックでの操作
メトリック データの通知を受け取ったり、自動化されたアクションを実行したりするには、アラート ルールまたは自動スケール設定を構成します。

### <a name="configure-alert-rules"></a>アラート ルールの作成
メトリックにアラート ルールを構成できます。 このアラート ルールは、メトリックが特定のしきい値を超えたかどうかを確認し、 Azure Monitor には、2 つのメトリック アラート機能があります。

メトリック アラート: メールでユーザーに通知するか、カスタム スクリプトの実行に使うことができる webhook を生成することができます。 webhook を使用して、サードパーティ製品の統合を構成することもできます。

 ![Azure Monitor のメトリックとアラート ルール](./media/monitoring-overview-metrics/MetricsOverview4.png)

ほぼリアルタイムのアラート (プレビュー): リソースの複数のメトリックおよびしきい値を監視し、[アクション グループ](/monitoring-action-groups.md)経由でユーザーに通知できます。 [ほぼリアルタイムのメトリック アラート](https://aka.ms/azuremonitor/near-real-time-alerts)について詳しくはこちらをご覧ください。


### <a name="autoscale-your-azure-resources"></a>Azure リソースの自動スケール
Azure リソースの中には、複数のインスタンスをスケールアウトまたはスケールインして、ワークロードを処理できるものがあります。 自動スケールは、App Services (Web Apps)、Virtual Machine Scale Sets、および従来の Azure Cloud Services に適用されます。  ワークロードに影響する特定のメトリックが、指定したしきい値を超えたときにスケールアウトまたはスケールインするように、自動スケール ルールを構成することができます。 詳細については、 [自動スケールの概要](monitoring-overview-autoscale.md)に関するページをご覧ください。

 ![Azure Monitor のメトリックと自動スケール](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>サポートされているサービスとメトリックについて
サポートされているサービスとそのメトリックの詳細な一覧については、[Azure Monitor のメトリック - リソースの種類ごとのサポートされているメトリック](monitoring-supported-metrics.md)に関するページをご覧ください。

## <a name="next-steps"></a>次のステップ
この記事のリンクを参照してください。 さらに、次の情報も確認します。  

* [自動スケールの一般的なメトリック](insights-autoscale-common-metrics.md)
* [アラート ルールの作成方法](insights-alerts-portal.md)
* [Log Analytics を使用した、Azure ストレージからのログの分析](../log-analytics/log-analytics-azure-storage.md)
