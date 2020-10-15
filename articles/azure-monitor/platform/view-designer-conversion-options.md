---
title: Azure Monitor ビュー デザイナーからブックへの変換オプション
description: ''
author: austonli
ms.author: aul
ms.subservice: ''
ms.topic: conceptual
ms.date: 02/07/2020
ms.openlocfilehash: 7bfa831332451718c0c9c05023b90104d2b8b02b
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "77658712"
---
# <a name="azure-monitor-view-designer-to-workbooks-conversion-options"></a>Azure Monitor ビュー デザイナーからブックへの変換オプション
[ビュー デザイナー](view-designer.md)は Azure Monitor の機能で、Log Analytics ワークスペース内のデータを、グラフ、リスト、タイムラインを使用して視覚化するのに役立つカスタム ビューを作成できます。 これらは段階的に廃止され、追加機能を提供するブックに置き換えられています。 この記事では、この 2 つの基本概念を比較し、ビューをブックに変換するためのオプションについて説明します。

## <a name="basic-workbook-designs"></a>ブックの基本的なデザイン

ビュー デザイナーの表現スタイルは静的で固定されたものですが、ブックではデータの表示方法を自由に選択したり、変更したりすることができます。 次の 2 つの図は、ビューを変換した後のブックの配置方法の例を示しています。

[縦置きのブック](view-designer-conversion-examples.md#vertical)
![縦](media/view-designer-conversion-options/view-designer-vertical.png)

[タブ付きのブック](view-designer-conversion-examples.md#tabbed)
![データ型の分布タブ](media/view-designer-conversion-options/distribution-tab.png)
![経時的データ型タブ](media/view-designer-conversion-options/over-time-tab.png)

## <a name="tile-conversion"></a>タイルの変換
ビュー デザイナーでは、全体的な状態をまとめて表現するために、概要タイル機能を使用しています。 これは、数値やグラフなど、7 つのタイルで表されます。 ブックでは、ユーザーが同様の視覚化を作成してピン留めし、元の概要タイルのスタイルに似たものにすることができます。 

![[ギャラリー]](media/view-designer-conversion-options/overview.png)


## <a name="view-dashboard-conversion"></a>ダッシュボードの変換を表示する
ビュー デザイナーのタイルは、通常、2 つのセクションで構成されます。1 つは視覚化で、もう 1 つは視覚化のデータと一致するリストです (例: **ドーナツとリスト** タイル)。

![ドーナツ](media/view-designer-conversion-options/donut-example.png)

ブックを使用すると、ユーザーはビューの 1 つまたは両方のセクションに対してクエリを実行することができます。 ブックでのクエリ構成は、簡単な 2 段階のプロセスです。 まず、クエリからデータが生成され、次にデータが視覚化としてレンダリングされます。  このビューは次のようにブックで再作成されます。

![Convert](media/view-designer-conversion-options/convert-donut.png)


## <a name="next-steps"></a>次のステップ
- [ブックへのアクセスとアクセス許可](view-designer-conversion-access.md)