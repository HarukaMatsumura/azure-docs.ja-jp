---
title: Web API を呼び出す Web アプリを登録する - Microsoft ID プラットフォーム | Azure
description: Web API を呼び出す Web アプリを登録する方法を説明します
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 05/07/2019
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: f94a3da96243e30faa90277ce86efec037f54672
ms.sourcegitcommit: bf1340bb706cf31bb002128e272b8322f37d53dd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "89436470"
---
# <a name="a-web-app-that-calls-web-apis-app-registration"></a>Web API を呼び出す Web アプリ: アプリの登録

Web API を呼び出す Web アプリの登録は、ユーザーをサインインさせる Web アプリと同じです。 そのため、「[ユーザーをサインインさせる Web アプリ: アプリの登録](scenario-web-app-sign-user-app-registration.md)」の手順に従ってください。

ただし、Web アプリは Web API も呼び出すようになっているため、機密クライアント アプリケーションになります。 そのため、追加の登録が必要になります。 アプリでは、クライアントの資格情報 ("*シークレット*") を Microsoft ID プラットフォームと共有する必要があります。

[!INCLUDE [Registration of client secrets](../../../includes/active-directory-develop-scenarios-registration-client-secrets.md)]

## <a name="api-permissions"></a>API のアクセス許可

Web アプリは、サインインしたユーザーの代わりに API を呼び出します。 そのためには、"*委任されたアクセス許可*" を要求する必要があります。 詳細については、「[Web API にアクセスするためのアクセス許可を追加する](quickstart-configure-app-access-web-apis.md#add-permissions-to-access-your-web-api)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Web API を呼び出す Web アプリ: コード構成](scenario-web-app-call-api-app-configuration.md)
