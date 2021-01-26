---
title: Apache Spark からの InvalidClassException エラー - Azure HDInsight
description: Azure HDInsight で、Apache Spark ジョブが InvalidClassException で失敗し、クラスバージョンが一致しない
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 07/29/2019
ms.openlocfilehash: 6220c328d05e7cd68460b7bfd0708a9d393a290f
ms.sourcegitcommit: 7863fcea618b0342b7c91ae345aa099114205b03
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93287888"
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

[!INCLUDE [troubleshooting next steps](../../../includes/hdinsight-troubleshooting-next-steps.md)]