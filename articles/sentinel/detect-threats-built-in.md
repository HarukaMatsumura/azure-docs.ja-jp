---
title: Microsoft Sentinel で組み込みの分析ルールを使用して脅威を検出する | Microsoft Docs
description: 組み込みのテンプレートに基づいて難しい設定なしで使用できる脅威検出ルールの使用方法について説明します。これを使用すると、何か疑わしいことが発生したときに通知が届きます。
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/09/2021
ms.author: yelevin
ms.custom: ignite-fall-2021
ms.openlocfilehash: 1c9f9fd17c40503e456bb76c19d413b7e4bd8468
ms.sourcegitcommit: 0415f4d064530e0d7799fe295f1d8dc003f17202
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2021
ms.locfileid: "132724351"
---
# <a name="detect-threats-out-of-the-box"></a>難しい設定なしで脅威を検出する

[!INCLUDE [Banner for top of topics](./includes/banner.md)]

Microsoft Sentinel に[データ ソースを接続](quickstart-onboard.md)した後、不審な事態が起きたときに通知を受けるようにしたいことがあります。 そのため Microsoft Sentinel には、脅威検出規則の作成に役立つ、すぐに使用できる組み込みのテンプレートが用意されています。

ルール テンプレートは、セキュリティ専門家とアナリストから構成される Microsoft のチームが既知の脅威、一般的な攻撃ベクトル、疑わしい行動のエスカレーション チェーンに基づいて設計したものです。 これらのテンプレートから作成される規則により、環境全体にわたって、疑わしい活動がないか自動的に検査されます。 テンプレートの多くは、ニーズに合わせて特定の活動を検索したり、除外したりするようにカスタマイズできます。 これらの規則で生成されるアラートによって、環境内で割り当てて調査することができるインシデントが作成されます。

この記事は、Microsoft Sentinel で脅威を検出する方法を理解するのに役立ちます。

> [!div class="checklist"]
> * 難しい設定の要らない脅威検出機能を使用する
> * 脅威への対応を自動化する

## <a name="view-built-in-detections"></a>組み込みの検出を表示する

Microsoft Sentinel のすべての分析ルールと検出を表示するには、 **[Analytics]**  >  **[ルール テンプレート]** に移動します。 このタブには、すべての Microsoft Sentinel 組み込み規則が含まれています。

:::image type="content" source="media/tutorial-detect-built-in/view-oob-detections.png" alt-text="Microsoft Sentinel の組み込みの検出機能を利用して脅威を検出する":::

組み込みの検出には以下のものがあります。

| 規則の種類 | [説明] |
| --------- | --------- |
| **Microsoft セキュリティ** | Microsoft セキュリティ テンプレートでは、他の Microsoft セキュリティ ソリューションで生成されたアラートから、リアルタイムで Microsoft Sentinel インシデントが自動的に作成されます。 同様のロジックで新しい規則を作成するためのテンプレートとして Microsoft セキュリティ規則を利用できます。 <br><br>セキュリティ規則の詳細については、「[Microsoft セキュリティ アラートからインシデントを自動的に作成する](create-incidents-from-alerts.md)」を参照してください。 |
| <a name="fusion"></a>**Fusion**<br>(プレビューの一部の検出) | Microsoft Sentinel は、拡張可能な機械学習アルゴリズムと共に Fusion 相関エンジンを使用して、複数の製品にわたる低再現性のアラートとイベントを、忠実度の高い、実行可能なインシデントに相関させて、高度なマルチステージ攻撃を検出します。 Fusion は既定で有効になっています。 ロジックは非表示であるため、カスタマイズすることはできません。このテンプレートを使用して作成できる規則は 1 つだけです。 <br><br>また、Fusion エンジンでは、[スケジュールが設定された分析ルール](#scheduled)によって生成されたアラートを他のシステムからのアラートと関連付け、結果として忠実度の高いインシデントを生成することもできます。 |
| **機械学習 (ML) による行動分析** | ML 行動分析テンプレートは Microsoft が特許を所有する機械学習アルゴリズムを基盤としており、しくみや実行タイミングなどの内部ロジックをユーザーが見ることはできません。 <br><br>ロジックは非表示であるため、カスタマイズすることはできません。この種類の各テンプレートを使用して作成できる規則は 1 つだけです。 |
| <a name="anomaly"></a>**異常**<br>(プレビュー) | 異常ルール テンプレートでは、SOC-ML (機械学習) を使用して、特定の種類の異常な行動を検出します。 各ルールには、分析される動作に適した固有のパラメーターとしきい値があります。 <br><br>これらのルールの構成は変更も微調整もできませんが、ルールを複製し、その複製を変更したり微調整したりできます。 このような場合は、複製を **フライティング** モードで実行し、元のルールを **運用** モードで同時に実行します。 その後、結果を比較して、微調整が期待どおりであれば、その複製を **運用** に切り替えます。 <br><br>詳細については、「[Microsoft Sentinel で SOC-ML 異常検知を使用して脅威を検出する](soc-ml-anomalies.md)」および「[Microsoft Sentinel で異常検出分析ルールを使用する](work-with-anomaly-rules.md)」をご覧ください。 |
| <a name="scheduled"></a>**スケジュール付き** | スケジュール付き分析ルールは、Microsoft のセキュリティ専門家が記述した組み込みのクエリに基づいています。 ユーザーはクエリ ロジックを閲覧し、変更できます。 スケジュール付き規則のテンプレートを使用してクエリ ロジックやスケジュール設定をカスタマイズし、新しい規則を作成できます。 <br><br>いくつかの新しいスケジュール設定された分析ルール テンプレートでは、Fusion エンジンによって、他のシステムからのアラートと関連付けられたアラートが生成されるため、忠実度の高いインシデントが生成することができます。 詳細については、[高度なマルチステージ攻撃の検出](configure-fusion-rules.md#configure-scheduled-analytics-rules-for-fusion-detections)に関する記事をご覧ください。<br><br>**ヒント**: ルールのスケジュール設定オプションには、ルールを有効にしたときに開始されるクロックを使用して、指定した分、時間、または日ごとに実行するようにルールを構成することが含まれます。 <br><br>新しいまたは編集された分析規則を有効にして、新しいインシデントのスタックが時間内に規則で確実に取得されるようにするには、次のことを考慮することをお勧めします。 たとえば、SOC アナリストが就業時間の開始時に同期して規則を実行してから、規則を有効にすることができます。|
| <a name="nrt"></a>**ほぼリアルタイム (NRT)**<br>(プレビュー) | NRT ルールは、1分ごとに実行するように設計された、限られたスケジュールされたルールのセットであり、可能な限り最新の情報を提供するために用意されています。 <br><br>ほとんどの場合、スケジュールされたルールと同様に機能し、いくつかの制限があります。 詳細については、「[Microsoft Sentinel の準リアルタイム (NRT) の分析ルールを使用して脅威をすばやく検出する](near-real-time-rules.md)」を参照してください。 |
| | |

> [!IMPORTANT]
> - 上記のルール テンプレートは現在 **プレビュー** 段階にあります。**Fusion** 検出テンプレートの一部としても同様です(「[Microsoft Sentinel の高度なマルチステージ攻撃の検出](fusion.md)」を参照してください。) ベータ版、プレビュー版、または一般提供としてまだリリースされていない Azure の機能に適用されるその他の法律条項については、「[Microsoft Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)」を参照してください。
>
> - **ML 行動分析** テンプレートに基づいてルールを作成して有効にすると、機械学習エンジンおよびモデルによる処理を目的として、必要に応じて、**ご利用の Microsoft Sentinel ワークスペースの外部で取り込まれたデータをコピーするためのアクセス許可を Microsoft に付与することになります**。
>

## <a name="use-built-in-analytics-rules"></a>組み込みの分析ルールを使用する

この手順では、組み込みの分析ルール テンプレートを使用する方法について説明します。

**組み込みの分析ルールを使用するには**:

1. [Microsoft Sentinel] > **[分析]**  >  **[ルール テンプレート]** ページで、テンプレート名を選択してから、詳細ウィンドウの **[ルールの作成]** ボタンを選択し、そのテンプレートに基づく新しいアクティブなルールを作成します。 

    各テンプレートには、必要なデータ ソースの一覧があります。 テンプレートを開くと、データ ソースの可用性が自動的にチェックされます。 可用性の問題がある場合は、 **[規則の作成]** ボタンが無効にされていたり、その影響に対する警告が表示されたりすることがあります。

    :::image type="content" source="media/tutorial-detect-built-in/use-built-in-template.png" alt-text="検出規則のプレビュー パネル":::

1. **[ルールの作成]** を選択すると、選択したテンプレートに基づいてルールの作成ウィザードが開かれます。 すべての詳細が自動的に入力されます。**スケジュール付き** テンプレートや **Microsoft セキュリティ** テンプレートを使用する場合は、特定のニーズに合わせてロジックやその他の規則の設定をカスタマイズできます。 この手順を繰り返して、組み込みテンプレートに基づく追加の規則を作成できます。 最後まで規則の作成ウィザードの手順に従うと、テンプレートに基づく規則の作成が完了します。 **[アクティブな規則]** タブに新しい規則が表示されます。

    ルールの作成ウィザードでルールをカスタマイズする方法の詳細については、「[脅威を検出するためにカスタム分析ルールを作成する](detect-threats-custom.md)」をご覧ください。

> [!TIP]
> - 環境の完全なセキュリティを確保するために、**接続されたデータ ソースに関連付けられているすべてのルールが有効になっている** ことを確認してください。 分析ルールを有効にする最も効率的な方法として、関連するルールがすべて一覧表示されているデータ コネクタ ページから直接有効にすることができます。 詳細については、「[データ ソースの接続](connect-data-sources.md)」を参照してください。
> 
> - ルールは **[API](/rest/api/securityinsights/)や [PowerShell](https://www.powershellgallery.com/packages/Az.SecurityInsights/0.1.0) 経由で Microsoft Sentinel にプッシュする** こともできますが、それを行うには追加の作業が必要です。 
> 
>     API または PowerShell を使用する場合は、ルールを有効にする前に、最初にルールを JSON にエクスポートする必要があります。 API または PowerShell は、Microsoft Sentinel の複数のインスタンスでルールを有効にし、各インスタンスの設定を同じにする場合に役立つことがあります。
> 
## <a name="export-rules-to-an-arm-template"></a>ルールを ARM テンプレートにエクスポートする

ルールをコードとして管理およびデプロイする場合は、簡単に [Azure Resource Manager (ARM) テンプレートにルールをエクスポート](import-export-analytics-rules.md)できます。 また、ユーザー インターフェイスでルールを表示および編集するために、テンプレート ファイルからルールをインポートすることもできます。

## <a name="next-steps"></a>次のステップ

- カスタム ルールを作成するには、既存のルールをテンプレートとして、または参照用に使用します。 既存のルールをベースラインとして使用すると、ほとんどのロジックを構築したあとで、必要な変更を加えることができます。 詳細については、「[脅威を検出するためにカスタム分析ルールを作成する](detect-threats-custom.md)」をご覧ください。

- 脅威への対応を自動化する方法については、[Microsoft Sentinel で脅威への自動対応を設定する](tutorial-respond-threats-playbook.md)方法に関するページを参照してください。
