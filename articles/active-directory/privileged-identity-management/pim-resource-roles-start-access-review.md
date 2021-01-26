---
title: PIM で Azure リソース ロールのアクセス レビューを作成する - Azure AD | Microsoft Docs
description: Azure AD Privileged Identity Management (PIM) で Azure リソース ロールに対するアクセス レビューを作成する方法を説明します。
services: active-directory
documentationcenter: ''
author: curtand
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
ms.subservice: pim
ms.date: 12/08/2020
ms.author: curtand
ms.custom: pim
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a618da7c9a66b8f687c1b75914530080ed56bea
ms.sourcegitcommit: 80c1056113a9d65b6db69c06ca79fa531b9e3a00
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96905827"
---
# <a name="create-an-access-review-of-azure-resource-roles-in-privileged-identity-management"></a>Privileged Identity Management で Azure リソース ロールのアクセス レビューを作成する

従業員の特権 Azure リソース ロールへのアクセスは、時間の経過に伴って変化します。 古くなったロールの割り当てに関連するリスクを軽減するために、アクセスを定期的に確認する必要があります。 Azure Active Directory (Azure AD) Privileged Identity Management (PIM) を使用して、特権 Azure リソース ロールのアクセス レビューを作成できます。 自動的に実行される定期的なアクセス レビューを構成することもできます。

この記事では、特権 Azure リソース ロールに対して 1 つ以上のアクセス レビューを作成する方法について説明します。

## <a name="prerequisites"></a>前提条件

[特権ロール管理者](../roles/permissions-reference.md#privileged-role-administrator)

## <a name="open-access-reviews"></a>アクセス レビューを開く

1. 特権ロール管理者ロールのメンバー ユーザーで [Azure portal](https://portal.azure.com/) にサインインします。

1. **[Azure AD Privileged Identity Management]** を開きます。

1. 左側のメニューで、 **[Azure リソース]** を選択します。

1. サブスクリプションなど、管理するリソースを選択します。

1. [管理] の下の **[アクセス レビュー]** を選択します。

    ![すべてのレビューの状態を示す [Azure リソース] - [アクセス レビュー] 一覧](./media/pim-resource-roles-start-access-review/access-reviews.png)

[!INCLUDE [Privileged Identity Management access reviews](../../../includes/active-directory-privileged-identity-management-access-reviews.md)]

## <a name="start-the-access-review"></a>アクセス レビューを開始する

アクセス レビューの設定を指定したら、 **[開始]** をクリックします。 アクセス レビューはステータスと共にリストに表示されます。

![開始されたレビューの状態を示す [アクセス レビュー] 一覧](./media/pim-resource-roles-start-access-review/access-reviews-list.png)

既定では、レビューの開始直後に Azure AD からレビュー担当者宛てにメールが送信されます。 Azure AD からメールを送信することを選択しなかった場合は、アクセス レビューが実行待ちになっていることを必ずレビュー担当者に伝えてください。 レビュー担当者には、[Azure リソース ロールのアクセス レビューを実行する](pim-resource-roles-perform-access-review.md)手順を案内することができます。

## <a name="manage-the-access-review"></a>アクセスレビューを管理する

アクセス レビューの **[概要]** ページでは、レビュー担当者が完了したレビューの進捗状況を追跡できます。 ディレクトリのアクセス権は、[レビューが完了する](pim-resource-roles-complete-access-review.md)まで変更されません。

![レビューの詳細を示す [アクセス レビューの概要] ページ](./media/pim-resource-roles-start-access-review/access-review-overview.png)

これが 1 回限りのレビューである場合は、アクセス レビュー期間が終了するか、管理者がアクセス レビューを停止した後に、[Azure リソース ロールのアクセス レビューを完了する](pim-resource-roles-complete-access-review.md)手順に従って結果を確認および適用します。  

アクセス レビューの系列を管理するには、アクセス レビューに移動し、[Scheduled]\(スケジュール済み\) レビューで今後予定されている実行を見つけ、それに応じて終了日を編集したり、レビュー担当者を追加/削除したりします。

**[Upon completion]\(完了時\)** 設定での選択に基づいて、レビューの終了日の後、またはレビューを手動で停止したときに自動適用が実行されます。 レビューの状態は、 **[完了]** から **[適用中]** などの中間状態を経由して、最後に状態 **[適用済み]** まで変化します。 拒否されたユーザーが存在する場合は、それらのユーザーが数分以内にロールから削除されることを確認できます。

## <a name="next-steps"></a>次のステップ

- [Azure リソース ロールのアクセス レビューを実行する](pim-resource-roles-perform-access-review.md)
- [Azure リソース ロールのアクセス レビューを完了する](pim-resource-roles-complete-access-review.md)
- [Azure AD ロールのアクセス レビューを作成する](pim-how-to-start-security-review.md)
