---
title: Form Recognizer サービスによる保存データの暗号化
titleSuffix: Azure Applied AI Services
description: Microsoft からは Microsoft が管理する暗号化キーが提供されます。また、カスタマー マネージド キー (CMK) と呼ばれている独自のキーで自分の Cognitive Services サブスクリプションを管理することをお客様に許可します。 この記事では、Form Recognizer の保存データの暗号化と、CMK を有効化および管理する方法について説明します。
author: erindormier
manager: venkyv
ms.service: applied-ai-services
ms.subservice: forms-recognizer
ms.topic: conceptual
ms.date: 08/28/2020
ms.author: egeaney
ms.openlocfilehash: 343376c21f3ac63fbe5059ba66df77195f717413
ms.sourcegitcommit: 34feb2a5bdba1351d9fc375c46e62aa40bbd5a1f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2021
ms.locfileid: "111891971"
---
# <a name="form-recognizer-encryption-of-data-at-rest"></a>Form Recognizer による保存データの暗号化

Azure Form Recognizer では、クラウドに永続化されるときにデータが自動的に暗号化されます。 Form Recognizer の暗号化によってデータは保護され、組織のセキュリティおよびコンプライアンス コミットメントを満たすのに役立ちます。

[!INCLUDE [cognitive-services-about-encryption](../includes/cognitive-services-about-encryption.md)]

> [!IMPORTANT]
> カスタマー マネージド キーは、2020年 5 月 11 日より後に作成されたリソースのみに使用できます。 Form Recognizer と共に CMK を使用するには、新しい Form Recognizer リソースを作成する必要があります。 リソースが作成されたら、Azure Key Vault を使用してマネージド ID を設定できます。

[!INCLUDE [cognitive-services-cmk](../includes/configure-customer-managed-keys.md)]

## <a name="next-steps"></a>次のステップ

* [Form Recognizer カスタマー マネージド キー要求フォーム](https://aka.ms/cogsvc-cmk)
* [Azure Key Vault の詳細を確認する](../../key-vault/general/overview.md)