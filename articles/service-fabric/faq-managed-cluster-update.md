---
title: Service Fabric マネージド クラスターに関するよくある質問
description: Service Fabric マネージド クラスターについてよく寄せられる質問 (機能、ユース ケース、一般的なシナリオなど)。
ms.topic: troubleshooting
ms.author: micraft
author: craftyhouse
ms.date: 7/14/2021
ms.custom: references_regions
ms.openlocfilehash: c78d66aca4b27ee6a21a53738789569c405fdb1a
ms.sourcegitcommit: 192444210a0bd040008ef01babd140b23a95541b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2021
ms.locfileid: "114342533"
---
# <a name="service-fabric-managed-clusters-frequently-asked-questions"></a>Service Fabric マネージド クラスターに関してよく寄せられる質問

Service Fabric マネージド クラスターについてよく寄せられる質問 (FAQ) とその回答を示します。

## <a name="general"></a>全般

### <a name="what-are-service-fabric-managed-clusters"></a>Service Fabric マネージド クラスターとはどのようなものですか?

Service Fabric マネージド クラスターは、クラスターのデプロイと管理を容易にするために設計された Service Fabric クラスター リソース モデルの進化版です。 Service Fabric マネージド クラスターで使用されている Azure Resource Manager カプセル化モデルにより、ユーザーはクラスター リソースを 1 つ定義してデプロイするだけでよく、現在のように多数の独立したリソース (仮想マシン スケール セット、Load Balancer、IP など) をデプロイする必要はありません。

### <a name="what-regions-are-supported"></a>どのリージョンがサポートされていますか?

Service Fabric マネージド クラスターは、すべてのパブリック クラウド リージョンでサポートされています。

### <a name="can-i-do-an-in-place-migration-of-my-existing-service-fabric-cluster-to-a-managed-cluster-resource"></a>既存の Service Fabric クラスターをマネージド クラスター リソースにインプレース移行することはできますか?

いいえ。 新しい Service Fabric マネージド クラスター リソースの種類を使用するには、新しい Service Fabric クラスター リソースを作成する必要があります。

### <a name="is-there-an-additional-cost-for-service-fabric-managed-clusters"></a>Service Fabric マネージド クラスターを使用すると追加料金が発生しますか?

いいえ。 クラスターに必要な基礎となるコンピューティング、ストレージ、ネットワーク リソースのコスト以外に、Service Fabric マネージド クラスターに関連する追加コストは発生しません。

### <a name="is-there-a-new-sla-introduced-by-the-service-fabric-managed-cluster-resource"></a>Service Fabric マネージド クラスター リソースによって導入される新しい SLA はありますか?

SLA は、現在の Service Fabric リソース モデルから変更されません。

### <a name="what-is-the-difference-between-a-basic-and-standard-sku-cluster"></a>Basic SKU と Standard SKU のクラスターでは何が違いますか?

Basic SKU クラスターを使用すると、ほとんどの構成が Service Fabric リソース プロバイダーによって提供されます。 Basic SKU クラスターは、テスト環境および運用前環境での使用が意図されています。 Standard SKU クラスターを使用すると、ユーザーがニーズを満たすようにクラスターを構成できます。 詳細については、「[Service Fabric マネージド クラスターの SKU](./overview-managed-cluster.md#service-fabric-managed-cluster-skus)」を参照してください。

## <a name="cluster-deployment-and-management"></a>クラスターのデプロイと管理

### <a name="i-run-custom-script-extensions-on-my-virtual-machine-scale-set-can-i-continue-to-do-that-with-a-managed-service-fabric-resource"></a>仮想マシン スケール セットでカスタム スクリプト拡張機能を実行しています。Service Fabric のマネージド リソースでも引き続き使用できますか?

はい。マネージド クラスター ノードの種類で VM 拡張機能を指定できます。 詳細については、「[Service Fabric 管理対象クラスター ノード タイプに仮想マシン スケール セット拡張機能を追加する (プレビュー)](./how-to-managed-cluster-vmss-extension.md)」を参照してください。

### <a name="i-want-to-have-an-internal-only-load-balancer-is-that-possible"></a>内部専用のロード バランサーを使用することはできますか?

いいえ。 現在、内部専用のロード バランサーを使用することはできません。 ネットワーク セキュリティ グループ (NSG) の規則をロックダウンし、不要な受信および送信トラフィックをブロックすることをお勧めします。

### <a name="can-i-autoscale-my-cluster"></a>クラスターを自動スケーリングできますか?

自動スケーリングは現在サポートされていません。

### <a name="can-i-deploy-my-cluster-across-availability-zones"></a>可用性ゾーンをまたいでクラスターをデプロイできますか?

はい、複数の可用性ゾーンにまたがる Service Fabric マネージド クラスターは、可用性ゾーンがサポートされている Azure リージョンでサポートされます。 詳細については、[複数の可用性ゾーンにまたがる Service Fabric マネージド クラスター](./how-to-managed-cluster-availability-zones.md)に関する記事を参照してください。

### <a name="can-i-deploy-stateless-node-types-on-a-service-fabric-managed-cluster"></a>Service Fabric マネージド クラスターにステートレス ノード タイプをデプロイできますか? 

はい、Service Fabric マネージド クラスターでは、すべてのセカンダリ ノード タイプでステートレス ノード タイプがサポートされます。 詳細については、[Service Fabric マネージド クラスターのステートレス ノード タイプ](./how-to-managed-cluster-stateless-node-type.md)に関する記事を参照してください。

### <a name="can-i-select-between-automatic-and-manual-upgrades-for-my-cluster-runtime"></a>クラスター ランタイムで自動アップグレードと手動アップグレードのどちらかを選択できますか?

はい、自動と手動アップグレードのどちらかを選択できます。 詳細については、[クラスターのアップグレード](./how-to-managed-cluster-upgrades.md)に関する記事を参照してください。

## <a name="applications"></a>アプリケーション

### <a name="is-there-a-local-development-experience-for-service-fabric-managed-clusters"></a>Service Fabric マネージド クラスター用のローカル開発エクスペリエンスはありますか?

ローカル開発エクスペリエンスは、既存の Service Fabric クラスターから変更されていません。 ローカル開発エクスペリエンスの詳細については、[開発環境の設定](./service-fabric-get-started.md)に関する記事を参照してください。

### <a name="can-i-deploy-my-applications-as-an-azure-resource-manager-resource"></a>アプリケーションを Azure Resource Manager リソースとしてデプロイできますか?

はい。 PowerShell と CLI を使用したデプロイに加えて、アプリケーションを Azure Resource Manager リソースとしてデプロイするためのサポートが追加されました。 利用を開始するには、「[ARM テンプレートを使用して Service Fabric マネージド クラスター アプリケーションをデプロイする](./how-to-managed-cluster-app-deployment-template.md)」を参照してください。

### <a name="can-i-deploy-applications-with-managed-identities"></a>マネージド ID を使用してアプリケーションをデプロイできますか?

 はい。マネージド ID を使用するアプリケーションを Service Fabric マネージド クラスターにデプロイできます。 詳細については、[アプリケーションのマネージド ID](./concepts-managed-identity.md) に関する記事を参照してください。