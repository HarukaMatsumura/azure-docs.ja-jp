---
title: Azure AD Connect クラウド プロビジョニングとは | Microsoft Docs
description: Azure AD Connect クラウド プロビジョニングについて説明します。
services: active-directory
author: billmath
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.topic: overview
ms.date: 12/11/2020
ms.subservice: hybrid
ms.author: billmath
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0acef468aa53e456cd6fb416fe45558aee064699
ms.sourcegitcommit: dfc4e6b57b2cb87dbcce5562945678e76d3ac7b6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97355819"
---
# <a name="what-is-azure-ad-connect-cloud-provisioning"></a>Azure AD Connect クラウド プロビジョニングとは
Azure AD Connect クラウド プロビジョニングは、ユーザー、グループ、および連絡先を Azure AD に同期するためのハイブリッド ID の 目標を満たすために設計された新しい Microsoft エージェントです。  これは Azure AD Connect sync と共に使用することができ、次のような利点があります。
    
- 複数のフォレストに接続されていない Active Directory フォレスト環境からの Azure AD テナントへの同期のサポート:一般的なシナリオには、合併と買収があります。買収した企業の AD フォレストが親企業の AD フォレストから分離されていて、以前は複数の AD フォレストがあった企業の AD フォレストがある場合などがあります。
- 軽量プロビジョニングエージェントを使用したい簡易インストール：エージェントは AD から Azure AD へのブリッジとして機能し、すべての同期構成がクラウドで管理されます。 
- 複数のプロビジョニングエージェントを使用して高可用性の展開を簡素化することができます。特に、AD から Azure AD へのパスワードハッシュ同期に依存している組織にとって重要です。


![What is Azure AD Connect](media/what-is-cloud-provisioning/architecture.png)

## <a name="how-is-azure-ad-connect-cloud-provisioning-different-from-azure-ad-connect-sync"></a>Azure AD Connect クラウドプロビジョニングは、Azure AD Connect同期とどのように違いますか。
Azure AD Connect クラウドプロビジョニングでは、Microsoft Online Services で AD から Azure AD へのプロビジョニングが調整されます。 組織は、オンプレミスと IaaS ホスト環境で、Azure AD と AD の間のブリッジとして機能する軽量のエージェントをデプロイするだけです。 プロビジョニングの構成は Azure AD に格納され、サービスの一部として管理されます。

## <a name="azure-ad-connect-cloud-provisioning-video"></a>Azure AD Connect クラウド プロビジョニングのビデオ
次の短いビデオでは、Azure AD Connect クラウド プロビジョニングの概要をわかりやすく説明しています。

> [!VIDEO https://youtube.com/embed/mOT3ID02_YQ]


## <a name="comparison-between-azure-ad-connect-and-cloud-provisioning"></a>Azure AD Connect とクラウド プロビジョニングの比較

次の表は、Azure AD Connect と Azure AD Connect のクラウドプロビジョニングの比較を示しています。

| 機能 | Azure Active Directory Connect 同期| Azure Active Directory Connect クラウド プロビジョニング |
|:--- |:---:|:---:|
|単一のオンプレミス AD フォレストへの接続|● |● |
| 複数のオンプレミス AD フォレストへの接続 |● |● |
| 切断された複数のオンプレミスADフォレストに接続する | |● |
| ライトウェイト エージェント インストール モデル | |● |
| 高可用性のための複数のアクティブなエージェント | |● |
| LDAP ディレクトリへの接続|●| | 
| ユーザーオブジェクトのサポート |● |● |
| グループオブジェクトのサポート |● |● |
| Contact オブジェクトのサポート |● |● |
| デバイスオブジェクトのサポート |● | |
| 属性フローの基本的なカスタマイズを許可する |● |● |
| Exchange Online 属性の同期 |● |● |
| 拡張属性 1 から 15 の同期 |● |● |
| ユーザー定義 AD 属性の同期 (ディレクトリ拡張機能) |● | |
| パスワード ハッシュ同期のサポート |●|●|
| パススルー認証のサポート |●||
| フェデレーションのサポート |●|●|
| シームレス シングル サインオン|● |●|
| ドメイン コントローラーへのインストールのサポート |● |● |
| Windows Server 2012 および Windows Server 2012 R2 のサポート |● |● |
| ドメイン/OU/グループのフィルター処理 |● |● |
| オブジェクトの属性値でのフィルター処理 |● | |
| 最小の属性セットの同期 (MinSync) の許可 |● |● |
| AD から Azure AD に流れる属性の削除の許可 |● |● |
| 属性フローの高度なカスタマイズの許可 |● | |
| 書き戻しのサポート (パスワード、デバイス、グループ) |● | |
| Azure AD Domain Services のサポート|● | |
| [Exchange ハイブリッドの書き戻し](../hybrid/reference-connect-sync-attributes-synchronized.md#exchange-hybrid-writeback) |● | |
| AD ドメインあたり 5 万を超えるオブジェクトのサポート |● | |
| クロス ドメイン参照|● | |

## <a name="next-steps"></a>次のステップ 

- [プロビジョニングとは](what-is-provisioning.md)
- [クラウド プロビジョニングのインストール](how-to-install.md)
