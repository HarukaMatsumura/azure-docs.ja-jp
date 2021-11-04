---
title: 一般的に使用される Azure Sentinel ブック | Microsoft Docs
description: 追加設定なしで利用できる、人気の Azure Sentinel リソースを使用できるように、最も一般的に使用されるブックについて説明します。
services: sentinel
cloud: na
documentationcenter: na
author: batamig
manager: rkarlin
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 03/07/2021
ms.author: bagol
ms.custom: ignite-fall-2021
ms.openlocfilehash: a8e96969dc4edd5a79e1ca85ac32529c10b8a343
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131019554"
---
# <a name="commonly-used-azure-sentinel-workbooks"></a>一般的に使用される Azure Sentinel ブック

[!INCLUDE [Banner for top of topics](./includes/banner.md)]

次の表は、最も一般的に使用される組み込みの Azure Sentinel ブックを示しています。

左側の **[脅威管理]**  >  **[ブック]** で Azure Sentinel のブックにアクセスし、使用するブックを検索します。 詳細については、「[データの視覚化と監視](monitor-your-data.md)」を参照してください。

> [!TIP]
> 取り込みしているデータに関連しているブックをデプロイすることをお勧めします。 ブックによって、収集したデータに基づいたより広範な監視と調査が可能になります。
>
> 詳細については、「[データ ソースの接続](connect-data-sources.md)」と「[Azure Sentinel のすぐに使えるコンテンツとソリューションを一元的に検出してデプロイする](sentinel-solutions-deploy.md)」を参照してください。
>

|ブック名  |説明  |
|---------|---------|
|**分析の効率**     |  SOC のパフォーマンスを向上させることができる、ご使用の分析ルールの有効性に関する分析情報が提供されます。 <br><br>詳細については、[データドリブン SOC のためのツールキット](https://techcommunity.microsoft.com/t5/azure-sentinel/the-toolkit-for-data-driven-socs/ba-p/2143152)に関するページをご覧ください。|
|**Azure アクティビティ**     |     すべてのユーザー操作とイベントを分析して関連付け、組織の Azure アクティビティに対する広範な分析情報が提供されます。 <br><br>詳細については、[Azure のアクティビティログを使用した監査](audit-sentinel-data.md#auditing-with-azure-activity-logs)に関するページをご覧ください。    |
|**Azure AD 監査ログ**     |  Azure Active Directory 監査ログを使用して、Azure AD シナリオに関する分析情報を得ます。 <br><br>詳細については、「[クイック スタート: Azure Sentinel の概要](get-visibility.md)」をご覧ください。     |
|**Azure AD 監査、アクティビティ、サインイン ログ**     |   1 つのブックで Azure Active Directory 監査、アクティビティ、サインイン データに関する分析情報が提供されます。 サインインなどのアクティビティを場所別、デバイス別、エラー理由別、ユーザー操作別に示します。 <br><br> このブックは、セキュリティ管理者と Azure 管理者の両者が使用できます。   |
|**Azure AD サインイン ログ**     | Azure AD サインイン ログを使用して、Azure AD シナリオに関する分析情報を得ます。        |
|**Cybersecurity Maturity Model Certification (CMMC)**     |   Microsoft のセキュリティ製品、Office 365、Teams、Intune、Windows Virtual Desktop など、Microsoft ポートフォリオ全体にわたり、CMMC コントロールに合わせてログ クエリを表示するためのメカニズムが用意されています。 <br><br>詳細については、[パブリック プレビュー段階にある Cybersecurity Maturity Model Certification (CMMC) ブック](https://techcommunity.microsoft.com/t5/azure-sentinel/what-s-new-cybersecurity-maturity-model-certification-cmmc/ba-p/2111184)に関するページをご覧ください。|
|**データ収集の正常性を監視** / **利用状況の監視**     |  ワークスペースのデータ インジェストの状態 (取り込みサイズ、待ち時間、ソースあたりのログ数など) に関する分析情報が提供されます。 モニターを表示し、異常を検出して、ワークスペースのデータ収集の正常性を判断します。 <br><br>詳細については、「[この Azure Sentinel ブックを使用してデータ コネクタの正常性を監視する](monitor-data-connector-health.md)」をご覧ください。    |
|**イベント アナライザー**     |  セキュリティ、アプリケーション、システム、セットアップ、ディレクトリ サービス、DNS などのすべてのイベントの詳細と属性を含む、Windows イベント ログの分析を調査および監査したり高速化したりできます。       |
|**Exchange Online**     |すべての Exchange 操作とユーザー アクティビティをトレースおよび分析することで、Microsoft Exchange Online に関する分析情報が提供されます。         |
|**ID およびアクセス**     |   監査およびサインイン ログを含むセキュリティログを使用して、Microsoft 製品の使用における ID およびアクセス操作に関する分析情報が提供されます。     |
|**インシデントの概要**     |   一般情報、エンティティ データ、トリアージ時間、軽減時間、コメントなど、インシデントに関する詳細情報を提供することによって、トリアージと調査を支援するように設計されています。 <br><br>詳細については、[データドリブン SOC のためのツールキット](https://techcommunity.microsoft.com/t5/azure-sentinel/the-toolkit-for-data-driven-socs/ba-p/2143152)に関するページをご覧ください。      |
|<a name="investigation-insights"></a>**調査の分析情報**     | インシデント、ブックマーク、エンティティ データに関する分析情報がアナリストに提供されます。 一般的なクエリと詳細な視覚化は、アナリストが疑わしいアクティビティを調査するのに役立ちます。     |
|**Microsoft Cloud App Security - 検出ログ**     |   組織で使用されているクラウド アプリの詳細と、特定のユーザーおよびアプリケーションの使用傾向やドリルダウン データから得られる分析情報が提供されます。  <br><br>詳細については、「[Microsoft Cloud App Security からデータを接続する](./data-connectors-reference.md#microsoft-cloud-app-security-mcas)」をご覧ください。|
|**MITRE ATT&CK ブック**     |   Azure Sentinel の MITRE ATT&CK カバレッジについて詳細が提供されます。      |
|**Office 365**     | すべての操作とアクティビティをトレースおよび分析することで、Office 365 に関する分析情報が提供されます。 SharePoint、OneDrive、Teams、および Exchange のデータがドリルダウンされます。       |
|**セキュリティのアラート**     |  Azure Sentinel 環境でのアラートのセキュリティ アラート ダッシュボードが提供されます。 <br><br>詳細については、「[Microsoft セキュリティ アラートからインシデントを自動的に作成する](create-incidents-from-alerts.md)」を参照してください。      |
|**セキュリティ操作の効率性**     |  セキュリティ オペレーション センター (SOC) マネージャーが、チームのパフォーマンスに関する全体的な効率のメトリックとメジャーを表示するためのものです。 <br><br>詳細については、「[インシデント メトリックを使用して SOC をより適切に管理する](manage-soc-with-incident-metrics.md)」をご覧ください。  |
|**脅威インテリジェンス**     | 脅威の種類と重要度、時間の経過に伴う脅威アクティビティ、Office 365 やファイアウォールなどの他のデータソースとの相関関係など、脅威インジケーターに関する分析情報が提供されます。  <br><br>詳細については、「[Azure Sentinel の脅威インテリジェンスについて](understand-threat-intelligence.md)」を参照してください。      |
|**ゼロ トラスト (TIC 3.0)**     |  [トラステッド インターネット接続フレームワーク](https://www.cisa.gov/trusted-internet-connections)を横断的に説明したゼロ トラストの原則を自動的に視覚化できます。   <br><br>詳細については、[ゼロ トラスト (TIC 3.0) ブックのお知らせブログ](https://techcommunity.microsoft.com/t5/public-sector-blog/announcing-the-azure-sentinel-zero-trust-tic3-0-workbook/ba-p/2313761)を参照してください。  |
