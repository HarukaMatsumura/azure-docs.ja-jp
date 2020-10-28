---
title: Apache Hive ログによってディスク領域がいっぱいになる - Azure HDInsight
description: Apache Hive ログによって Azure HDInsight のヘッド ノードのディスク領域がいっぱいになる。
ms.service: hdinsight
ms.topic: troubleshooting
author: nisgoel
ms.author: nisgoel
ms.reviewer: jasonh
ms.date: 10/05/2020
ms.openlocfilehash: a102c9f375b37579cf6f92b08d67f762d3dfd26a
ms.sourcegitcommit: 8d8deb9a406165de5050522681b782fb2917762d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92220892"
---
# <a name="scenario-apache-hive-logs-are-filling-up-the-disk-space-on-the-head-nodes-in-azure-hdinsight"></a>シナリオ:Apache Hive ログによって Azure HDInsight のヘッド ノードのディスク領域がいっぱいになる

この記事では、Azure HDInsight クラスターのヘッド ノードのディスク領域不足に関連する問題のトラブルシューティングの手順と可能な解決策について説明します。

## <a name="issue"></a>問題

Apache Hive/LLAP クラスターで、不要なログによってヘッド ノードのディスク領域全体が占有されている。 そのため、次の問題が発生する可能性がある。

1. ヘッド ノードに空き領域がないため、SSH アクセスが失敗する。
2. Ambari によって " *HTTP エラー:503 サービス利用不可* " が返される。
3. HiveServer2 Interactive が再起動に失敗する

この問題が発生すると、`ambari-agent` ログに次のように表示されます。
```
ambari_agent - Controller.py - [54697] - Controller - ERROR - Error:[Errno 28] No space left on device
```
```
ambari_agent - HostCheckReportFileHandler.py - [54697] - ambari_agent.HostCheckReportFileHandler - ERROR - Can't write host check file at /var/lib/ambari-agent/data/hostcheck.result
```

## <a name="cause"></a>原因

高度な hive-log4j 構成では、最後に変更された日付に基づき、30 日以上経過しているファイルに対して現在の既定の削除スケジュールが設定されます。

## <a name="resolution"></a>解像度

1. Ambari ポータルの Hive コンポーネントの概要に移動し、[`Configs`] タブをクリックします。

2. [Advanced]\(詳細\) 設定の `Advanced hive-log4j` セクションに移動します。

3. `appender.RFA.strategy.action.condition.age` パラメーターを任意の期間に設定します。 14 日間の例: `appender.RFA.strategy.action.condition.age = 14D`

4. 関連設定が表示されない場合、次の設定を追加してください。
    ```
    # automatically delete hive log
    appender.RFA.strategy.action.type = Delete
    appender.RFA.strategy.action.basePath = ${sys:hive.log.dir}
    appender.RFA.strategy.action.condition.type = IfLastModified
    appender.RFA.strategy.action.condition.age = 30D
    appender.RFA.strategy.action.PathConditions.type = IfFileName
    appender.RFA.strategy.action.PathConditions.regex = hive*.*log.*
    ```

5. 次に示すように、`hive.root.logger` を `INFO,RFA` に設定します。 既定の設定は DEBUG で、これによりログが非常に大きくなります。

    ```
    # Define some default values that can be overridden by system properties
    hive.log.threshold=ALL
    hive.root.logger=INFO,RFA
    hive.log.dir=${java.io.tmpdir}/${user.name}
    hive.log.file=hive.log
    ```

6. 構成を保存し、必要なコンポーネントを再起動します。

## <a name="next-steps"></a>次のステップ

問題がわからなかった場合、または問題を解決できない場合は、次のいずれかのチャネルでサポートを受けてください。

* [Azure コミュニティのサポート](https://azure.microsoft.com/support/community/)を通じて Azure エキスパートから回答を得る。

* [@AzureSupport](https://twitter.com/azuresupport) (Azure コミュニティを適切なリソース (回答、サポート、専門家) につなぐことで、カスタマー エクスペリエンスを向上させる Microsoft Azure の公式アカウント) に問い合わせる。

* さらにヘルプが必要な場合は、[Azure portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/) からサポート リクエストを送信できます。 メニュー バーから **[サポート]** を選択するか、 **[ヘルプとサポート]** ハブを開いてください。 詳細については、「[Azure サポート要求を作成する方法](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request)」をご覧ください。 サブスクリプション管理と課金サポートへのアクセスは、Microsoft Azure サブスクリプションに含まれていますが、テクニカル サポートはいずれかの [Azure のサポート プラン](https://azure.microsoft.com/support/plans/)を通して提供されます。
