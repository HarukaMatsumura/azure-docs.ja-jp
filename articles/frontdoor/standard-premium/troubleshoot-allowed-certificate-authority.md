---
title: Azure Front Door Standard/Premium で許可されている証明機関 (プレビュー)
description: この記事では、独自の証明書を作成するときに許可されるすべての証明機関の一覧を示します。
services: frontdoor
author: duongau
ms.service: frontdoor
ms.topic: troubleshooting
ms.date: 02/18/2021
ms.author: qixwang
ms.openlocfilehash: e31ad0734630fbd0b4960c26f8d562cea66ae675
ms.sourcegitcommit: e39ad7e8db27c97c8fb0d6afa322d4d135fd2066
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2021
ms.locfileid: "112003637"
---
# <a name="allowed-certificate-authorities-for-azure-front-door-standardpremium-preview"></a>Azure Front Door Standard/Premium で許可されている証明機関 (プレビュー)

Azure Front Door Standard/Premium のカスタム ドメインに対して独自の証明書を使用して HTTPS 機能を有効にする場合。 TLS/SSL 証明書を作成するには、許可された証明機関 (CA) が必要です。 許可されていない CA や自己署名証明書を使用すると、要求が拒否されます。

[!INCLUDE [cdn-front-door-allowed-ca](../../../includes/cdn-front-door-allowed-ca.md)]
