---
title: Azure portal を使用して、ユーザー割り当てマネージド ID を管理する - Azure AD
description: ユーザー割り当てマネージド ID を作成、一覧表示、削除したり、それにロールを割り当てたりする方法に関する詳細な手順。
services: active-directory
documentationcenter: ''
author: barclayn
manager: daveba
editor: ''
ms.custom: subject-rbac-steps
ms.service: active-directory
ms.subservice: msi
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/20/2021
ms.author: barclayn
ms.collection: M365-identity-device-management
ROBOTS: NOINDEX
ms.openlocfilehash: 72a9cfe6142b4c82cd122068e096776c19c4e392
ms.sourcegitcommit: 3bb9f8cee51e3b9c711679b460ab7b7363a62e6b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/14/2021
ms.locfileid: "112080905"
---
# <a name="create-list-delete-or-assign-a-role-to-a-user-assigned-managed-identity-using-the-azure-portal"></a>Azure portal を使用してユーザー割り当てマネージド ID を作成、一覧表示、削除したり、それにロールを割り当てたりする

Azure リソースのマネージド ID は、Azure Active Directory のマネージド ID を Azure サービスに提供します。 この ID を使用すると、コード内に資格情報を埋め込む必要なく、Azure AD の認証をサポートするサービスに認証することができます。 

この記事では、Azure portal を使用してユーザー割り当てマネージド ID を作成、一覧表示、削除したり、それにロールを割り当てたりする方法について説明します。

## <a name="prerequisites"></a>前提条件

- Azure リソースのマネージド ID の基本点な事柄については、[概要](overview.md)に関するセクションを参照してください。 **[システム割り当てマネージド ID とユーザー割り当てマネージド ID の違い](overview.md#managed-identity-types)を必ず確認してください**。
- まだ Azure アカウントを持っていない場合は、[無料のアカウントにサインアップ](https://azure.microsoft.com/free/)してから先に進んでください。

## <a name="create-a-user-assigned-managed-identity"></a>ユーザー割り当てマネージド ID を作成する

ユーザー割り当てマネージド ID を作成するには、お使いのアカウントに[マネージド ID 共同作成者](../../role-based-access-control/built-in-roles.md#managed-identity-contributor)ロールの割り当てが必要です。

1. Azure サブスクリプションに関連付けられているアカウントを使用して、[Azure portal](https://portal.azure.com) にサインインして、ユーザー割り当てマネージド ID を作成します。
2. 検索ボックスに "*マネージド ID*" と入力して、 **[サービス]** の下で **[マネージド ID]** をクリックします。
3. **[追加]** をクリックして、 **[ユーザー割り当てマネージド ID の作成]** ウィンドウの次のフィールドに値を入力します。
    - **サブスクリプション**:ユーザー割り当てマネージド ID を作成するサブスクリプションを選択します。
    - **[リソース グループ]** :ユーザー割り当てマネージド ID を作成するリソースグループを選択するか、 **[新規作成]** をクリックして新しいリソースグループを作成します。
    - **[リージョン]** :ユーザー割り当てマネージド ID をデプロイするリージョンを選択します。たとえば、 **[米国西部]** などです。
    - **Name**:これは、ユーザー割り当てマネージド ID の名前です。たとえば、UAI1 とします。
    ![ユーザー割り当てマネージド ID を作成する](./media/how-to-manage-ua-identity-portal/create-user-assigned-managed-identity-portal.png)
4. **[確認と作成]** をクリックして変更を確認します。
5. **Create** をクリックしてください。

## <a name="list-user-assigned-managed-identities"></a>ユーザー割り当てマネージド ID を一覧表示する

ユーザー割り当てマネージド ID の一覧表示/読み取りには、お使いのアカウントに[マネージド ID オペレーター](../../role-based-access-control/built-in-roles.md#managed-identity-operator)ロールまたは[マネージド ID 共同作成者](../../role-based-access-control/built-in-roles.md#managed-identity-contributor)ロールの割り当てが必要です。

1. Azure サブスクリプションに関連付けられているアカウントを使用して、[Azure portal](https://portal.azure.com) にサインインして、ユーザー割り当てマネージド ID を一覧表示します。
2. 検索ボックスに "*マネージド ID*" と入力して、[サービス] の下で **[マネージド ID]** をクリックします。
3. ご使用のサブスクリプションのユーザー割り当てマネージド ID の一覧が表示されます。  ユーザー割り当てマネージド ID の詳細を確認するには、名前をクリックします。

![ユーザー割り当てマネージド ID を一覧表示する](./media/how-to-manage-ua-identity-portal/list-user-assigned-managed-identity-portal.png)

## <a name="delete-a-user-assigned-managed-identity"></a>ユーザー割り当てマネージド ID を削除する

ユーザー割り当てマネージド ID を削除するには、お使いのアカウントに[マネージド ID 共同作成者](../../role-based-access-control/built-in-roles.md#managed-identity-contributor)ロールの割り当てが必要です。

ユーザー割り当て ID を削除しても、それが割り当てられていた VM やリソースから削除されることはありません。  VM からユーザー割り当てマネージド ID を削除する場合は、「[VM からユーザー割り当て ID を削除する](./qs-configure-portal-windows-vm.md#remove-a-user-assigned-managed-identity-from-a-vm)」を参照してください。

1. Azure サブスクリプションに関連付けられているアカウントを使用して、[Azure portal](https://portal.azure.com) にサインインして、ユーザー割り当てマネージド ID を削除します。
2. ユーザー割り当てマネージド ID を選択して、 **[削除]** をクリックします。
3. 確認ボックスで、 **[はい]** を選択します。

![ユーザー割り当てマネージド ID を削除する](./media/how-to-manage-ua-identity-portal/delete-user-assigned-managed-identity-portal.png)

## <a name="assign-a-role-to-a-user-assigned-managed-identity"></a>ユーザー割り当てマネージド ID にロールを割り当てる 

ユーザー割り当てマネージド ID にロールを割り当てるには、お使いのアカウントに[ユーザー アクセス管理者](../../role-based-access-control/built-in-roles.md#user-access-administrator)ロールの割り当てが必要です。

詳細な手順については、「[Azure portal を使用して Azure ロールを割り当てる](../../role-based-access-control/role-assignments-portal.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

- [Azure CLI を使用して、リソースにマネージド ID アクセスを割り当てる](howto-assign-access-cli.md)
- [PowerShell を使用して、リソースにマネージド ID アクセスを割り当てる](howto-assign-access-powershell.md)