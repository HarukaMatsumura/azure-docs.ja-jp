---
title: Apache Spark からの InvalidClassException エラー - Azure HDInsight
description: Azure HDInsight で、Apache Spark ジョブが InvalidClassException で失敗し、クラスバージョンが一致しない
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 07/29/2019
ms.openlocfilehash: 070dd50f76f5c7ae2289b93b7c2a9b069fb0b0a2
ms.sourcegitcommit: d767156543e16e816fc8a0c3777f033d649ffd3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2020
ms.locfileid: "92539073"
---
# <a name="apache-spark-job-fails-with-invalidclassexception-class-version-mismatch-in-azure-hdinsight"></a>Azure HDInsight で、Apache Spark ジョブが InvalidClassException で失敗し、クラスバージョンが一致しない

この記事では、Azure HDInsight クラスターで Apache Spark コンポーネントを使用するときのトラブルシューティングの手順と考えられる解決策について説明します。

## <a name="issue"></a>問題

Spark 2.x クラスターに Apache Spark ジョブを作成しようとします。 次のようなエラーで失敗します。

```
18/09/18 09:32:26 WARN TaskSetManager: Lost task 0.0 in stage 1.0 (TID 1, wn7-dev-co.2zyfbddadfih0xdq0cdja4g.ax.internal.cloudapp.net, executor 4): java.io.InvalidClassException:
org.apache.commons.lang3.time.FastDateFormat; local class incompatible: stream classdesc serialVersionUID = 2, local class serialVersionUID = 1
        at java.io.ObjectStreamClass.initNonProxy(ObjectStreamClass.java:699)
        at java.io.ObjectInputStream.readNonProxyDesc(ObjectInputStream.java:1885)
        at java.io.ObjectInputStream.readClassDesc(ObjectInputStream.java:1751)
        at java.io.ObjectInputStream.readOrdinaryObject(ObjectInputStream.java:2042)
        at java.io.ObjectInputStream.readObject0(ObjectInputStream.java:1573)
```

## <a name="cause"></a>原因

このエラーは、`spark.yarn.jars` 構成にさらに jar (具体的には、別のバージョンの `commons-lang3` パッケージを含み、クラスの不一致を招くシェーディングされた jar) を追加することにより発生することがあります。 既定では、Spark 2.1/2/3 はバージョン 3.5 の `commons-lang3` を使用します。

> [!TIP]
> ライブラリのシェーディングとは、その内容を独自の jar に配置し、パッケージを変更することです。 これは、ライブラリのパッケージ化とは異なり、再パッケージせずに独自の jar にライブラリを配置します。

## <a name="resolution"></a>解決策

jar を削除するか、カスタマイズした jar (AzureLogAppender) を再コンパイルし、[maven-shade-plugin](https://maven.apache.org/plugins/maven-shade-plugin/examples/class-relocation.html) を使用してクラスを再配置します。

## <a name="next-steps"></a>次のステップ

問題がわからなかった場合、または問題を解決できない場合は、次のいずれかのチャネルでサポートを受けてください。

* [Azure コミュニティのサポート](https://azure.microsoft.com/support/community/)を通じて Azure エキスパートから回答を得る。

* [@AzureSupport](https://twitter.com/azuresupport) (Azure コミュニティを適切なリソース (回答、サポート、専門家) につなぐことで、カスタマー エクスペリエンスを向上させる Microsoft Azure の公式アカウント) に問い合わせる。

* さらにヘルプが必要な場合は、[Azure portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/) からサポート リクエストを送信できます。 メニュー バーから **[サポート]** を選択するか、 **[ヘルプとサポート]** ハブを開いてください。 詳細については、「[Azure サポート要求を作成する方法](../../azure-portal/supportability/how-to-create-azure-support-request.md)」をご覧ください。 サブスクリプション管理と課金サポートへのアクセスは、Microsoft Azure サブスクリプションに含まれていますが、テクニカル サポートはいずれかの [Azure のサポート プラン](https://azure.microsoft.com/support/plans/)を通して提供されます。