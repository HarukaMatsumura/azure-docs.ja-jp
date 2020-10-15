---
author: tfitzmac
ms.service: azure-resource-manager
ms.topic: include
ms.date: 01/30/2019
ms.author: tomfitz
ms.openlocfilehash: aac2f3ea2b52ac0319f96279deed13c1145749bd
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "74451571"
---
## <a name="deploy-template-from-cloud-shell"></a>Cloud Shell からのテンプレートのデプロイ

テンプレートは、[Cloud Shell](../articles/cloud-shell/overview.md) を使ってデプロイすることができます。 外部テンプレートをデプロイするには、外部デプロイの場合とまったく同じように、テンプレートの URI を指定します。 ローカル テンプレートをデプロイするには、最初に Cloud Shell のストレージ アカウントにテンプレートを読み込む必要があります。 このセクションでは、Cloud Shell アカウントにテンプレートを読み込み、ローカル ファイルとしてデプロイする方法について説明します。 Cloud Shell の使用経験がない場合は、その設定について、「[Azure Cloud Shell の概要](../articles/cloud-shell/overview.md)」を参照してください。

1. [Azure portal](https://portal.azure.com) にサインインする

1. Cloud Shell リソース グループを選択します。 名前のパターンは `cloud-shell-storage-<region>` です。

   ![リソース グループの選択](./media/resource-manager-cloud-shell-deploy/select-cloud-shell-resource-group.png)

1. Cloud Shell のストレージ アカウントを選択します。

   ![ストレージ アカウントを選択する](./media/resource-manager-cloud-shell-deploy/select-storage.png)

1. **[BLOB]** を選択します。

   ![BLOB の選択](./media/resource-manager-cloud-shell-deploy/select-blobs.png)

1. **[+ コンテナー]** を選択します。

   ![コンテナーの追加](./media/resource-manager-cloud-shell-deploy/add-container.png)

1. コンテナーに名前とアクセス レベルを付与します。 この記事のサンプル テンプレートには機密性の高い情報は含まれていないため、匿名の読み取りアクセスを許可します。 **[OK]** を選択します。

   ![コンテナーの値の指定](./media/resource-manager-cloud-shell-deploy/provide-container-values.png)

1. 作成したコンテナーを選択します。

   ![新しいコンテナーの選択](./media/resource-manager-cloud-shell-deploy/select-container.png)

1. **[アップロード]** を選択します。

   ![BLOB のアップロード](./media/resource-manager-cloud-shell-deploy/upload-blob.png)

1. テンプレートを見つけてアップロードします。

   ![ファイルをアップロードする](./media/resource-manager-cloud-shell-deploy/find-and-upload-template.png)

1. アップロードが完了したら、テンプレートを選択します。

   ![新しいテンプレートの選択](./media/resource-manager-cloud-shell-deploy/select-new-template.png)

1. URL をコピーします。

   ![URL のコピー](./media/resource-manager-cloud-shell-deploy/copy-url.png)

1. プロンプトを開きます。

   ![Cloud Shell を開く](./media/resource-manager-cloud-shell-deploy/start-cloud-shell.png)
