---
title: Azure Monitor の簡易ログ エクスペリエンス (プレビュー) | Microsoft Docs
description: 簡易ログ エクスペリエンスを使用すると、KQL を直接扱うことなく Azure Monitor で基本的なクエリを作成できます。
ms.subservice: logs
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 09/12/2019
ms.openlocfilehash: 4926e18aa6b00fe36608843ea5253903ace774e2
ms.sourcegitcommit: 07166a1ff8bd23f5e1c49d4fd12badbca5ebd19c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90089110"
---
# <a name="simple-logs-experience-in-azure-monitor-preview"></a>Azure Monitor の簡易ログ エクスペリエンス (プレビュー)
Azure Monitor には、KQL 言語を使用して[ログ クエリ](log-query-overview.md)を作成するための[充実したエクスペリエンス](get-started-portal.md)が備わっています。 ただし、基本的なクエリ要件には、KQL の機能が全部揃っている必要はなく、簡素化されたエクスペリエンスの方が好ましい場合もあります。 簡易ログ エクスペリエンスを使用すると、KQL を直接扱うことなく基本的なクエリを作成できます。 簡易ログは、必要なクエリが高度化していく中で、KQL の学習ツールとしても使用できます。

> [!NOTE]
> 現在、簡易ログは、Cosmos DB と Key Vault のみを対象に、テストとして導入されています。 お使いになった感想を [User Voice](https://feedback.azure.com/forums/913690-azure-monitor) を通じて Microsoft に共有してください。この機能を拡張してリリースするかどうかの判断に役立てさせていただきます。


## <a name="scope"></a>スコープ
簡易ログ エクスペリエンスは、選択されたリソースについてのデータを *AzureDiagnostics*、*AzureMetrics*、*AzureActivity* の各テーブルから取得します。 

## <a name="using-simple-logs"></a>簡易ログを使用する
[Log Analytics ワークスペースにログを収集するように診断設定が構成された](../platform/resource-logs.md#send-to-azure-storage) Azure サブスクリプションの Cosmos DB または Key Vault に移動します。 **[監視]** メニューの **[ログ]** をクリックすると、簡易ログ エクスペリエンスが表示されます。

![スクリーンショットには、[ログ] が選択された [監視] メニューが表示されている。](media/simple-logs/menu.png)

**[フィールド]** と **[演算子]** を選択し、比較する**値**を指定します。 **[+]** をクリックし、 **[And] または [Or]** を指定して条件を追加します。

![スクリーンショットには、[簡易ログ] が選択された [Search in the logs]\(ログで検索する\) ペインが表示されている。](media/simple-logs/criteria.png)

**[実行]** をクリックしてクエリの結果を確認します。

## <a name="view-and-edit-kql"></a>KQL を表示して編集する
**[クエリ エディター]** を選択すると、簡易ログ クエリによって生成された KQL が、フル機能の Log Analytics エクスペリエンスで表示されます。 

![クエリ エディター](media/simple-logs/query-editor.png)

Log Analytics で KQL を直接編集して他の機能 (フィルターで結果を絞り込むなど) を使用することができます。

![KQL を編集する](media/simple-logs/edit-kql.png)


## <a name="next-steps"></a>次のステップ

- [Azure portal 内での Log Analytics の使用](get-started-portal.md)に関するチュートリアルを進めます。
- [ログ クエリの作成](get-started-portal.md)に関するチュートリアルを進めます。
