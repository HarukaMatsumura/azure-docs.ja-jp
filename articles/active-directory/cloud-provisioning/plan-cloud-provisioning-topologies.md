---
title: Azure AD Connect クラウド プロビジョニングがサポートされているトポロジとシナリオ
description: Azure AD Connect クラウド プロビジョニングを使用する、さまざまなオンプレミス トポロジおよび Azure Active Directory (Azure AD) トポロジについて説明します。
services: active-directory
author: billmath
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 02/26/2020
ms.subservice: hybrid
ms.author: billmath
ms.collection: M365-identity-device-management
ms.openlocfilehash: d442c980ad5bbe3b56eae127b6e9eaeddf380a4e
ms.sourcegitcommit: 03662d76a816e98cfc85462cbe9705f6890ed638
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2020
ms.locfileid: "90526852"
---
# <a name="azure-ad-connect-cloud-provisioning-supported-topologies-and-scenarios"></a>Azure AD Connect クラウド プロビジョニングがサポートされているトポロジとシナリオ
この記事では、Azure AD Connect クラウド プロビジョニングを使用する、さまざまなオンプレミス トポロジおよび Azure Active Directory (Azure AD) トポロジについて説明します。 この記事には、サポートされている構成とシナリオのみが含まれています。

> [!IMPORTANT]
> 公式に文書化されている構成やアクションを除き、Microsoft は Azure AD Connect クラウド プロビジョニングの変更や操作をサポートしません。 このような構成やアクションを行うと、Azure AD Connect クラウド プロビジョニングが不整合な状態になったり、サポートされていない状態になったりする可能性があります。 結果的に、Microsoft ではこのようなデプロイについてテクニカル サポートを提供できなくなります。

## <a name="things-to-remember-about-all-scenarios-and-topologies"></a>すべてのシナリオとトポロジに関する注意事項
ソリューションを選択するときに注意すべき情報の一覧を次に示します。

- ユーザーとグループは、すべてのフォレストで一意に識別される必要がある
- クラウド プロビジョニングでは、フォレスト間の照合が行われない
- ユーザーまたはグループは、すべてのフォレストで 1 回だけ表示可能
- オブジェクトのソース アンカーは自動的に選択されます。  ms-DS-ConsistencyGuid を使用します (存在する場合)。それ以外の場合は、ObjectGUID が使用されます。
- ソース アンカーに使用される属性を変更することはできません。

## <a name="single-forest-single-azure-ad-tenant"></a>単一のフォレスト、単一の Azure AD テナント
![単一のフォレストと単一のテナントのトポロジ](media/plan-cloud-provisioning-topologies/single-forest.png)

最も単純なトポロジは、1 つのオンプレミス フォレスト (1 つまたは複数のドメイン) と、1 つの Azure AD テナントです。  このシナリオの例については、[チュートリアル:単一のフォレストと単一の Azure AD テナント](tutorial-single-forest.md)に関する記事を参照してください


## <a name="multi-forest-single-azure-ad-tenant"></a>複数のフォレスト、単一の Azure AD テナント
![複数のフォレストと単一のテナントのトポロジ](media/plan-cloud-provisioning-topologies/multi-forest.png)

一般的なトポロジは、複数の AD フォレスト (1 つまたは複数のドメイン) と、1 つの Azure AD テナントです。  

## <a name="existing-forest-with-azure-ad-connect-new-forest-with-cloud-provisioning"></a>既存のフォレストを使用した Azure AD Connect、クラウド プロビジョニングを使用した新しいフォレスト
![単一のフォレストと単一のテナントのトポロジ](media/plan-cloud-provisioning-topologies/existing-forest-new-forest.png)

このシナリオは複数フォレストのシナリオに似ていますが、これには既存の Azure AD Connect 環境が関係し、Azure AD Connect クラウド プロビジョニングを使用して新しいフォレストに導入されます。  このシナリオの例については、[チュートリアル:1 つの Azure AD テナントを持つ既存のフォレスト](tutorial-existing-forest.md)を参照してください。

## <a name="piloting-azure-ad-connect-cloud-provisioning-in-an-existing-hybrid-ad-forest"></a>既存のハイブリッド AD フォレストで Azure AD Connect クラウド プロビジョニングをパイロットする
![単一のフォレストと単一のテナントのトポロジ](media/plan-cloud-provisioning-topologies/migrate.png) パイロット シナリオでは、両方の Azure AD Connect と Azure AD Connect クラウド プロビジョニングの両方が同じフォレストに存在し、それに応じてユーザーとグループのスコープを設定します。 注:オブジェクトは、いずれかのツールでのみスコープ内にある必要があります。 

このシナリオの例については、[チュートリアル:既存の同期済み AD フォレストで Azure AD Connect クラウド プロビジョニングのパイロットを実施する](tutorial-pilot-aadc-aadccp.md)に関する記事を参照してください。



## <a name="next-steps"></a>次のステップ 

- [プロビジョニングとは](what-is-provisioning.md)
- [Azure AD Connect クラウド プロビジョニングとは](what-is-cloud-provisioning.md)

