---
title: Azure Container Instances を実行する - 音声サービス
titleSuffix: Azure Cognitive Services
description: 音声サービス コンテナーを Azure Container Instance にデプロイし、Web ブラウザーでテストします。
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 09/03/2020
ms.author: aahi
ms.openlocfilehash: 9b77474d63cb47b561f9913ff06be5718aba4152
ms.sourcegitcommit: 10d00006fec1f4b69289ce18fdd0452c3458eca5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "96009647"
---
# <a name="deploy-the-speech-service-container-to-azure-container-instances"></a>音声サービス コンテナーを Azure Container Instances にデプロイする

Cognitive Services の[音声サービス](speech-container-howto.md) コンテナーを Azure [Container Instances](../../container-instances/index.yml) にデプロイする方法について説明します。 この手順では、Azure 音声サービス リソースの作成方法を示します。 次に、関連するコンテナー イメージをプルする方法について説明します。 最後に、ブラウザーからこの 2 つのオーケストレーションを行う機能を取り上げます。 コンテナーを使用することで、開発者の関心をインフラストラクチャの管理から切り離し、アプリケーション開発に専念させることができます。

[!INCLUDE [Prerequisites](../containers/includes/container-preview-prerequisites.md)]

## <a name="request-access-to-the-container-registry"></a>コンテナー レジストリへのアクセスの要求

コンテナーへのアクセスを要求するには、最初に [Cognitive Services Speech コンテナー要求フォーム](https://aka.ms/csgate/)に記入して送信する必要があります。 

[!INCLUDE [Request access to the container registry](../../../includes/cognitive-services-containers-request-access-only.md)]

[!INCLUDE [Create a Cognitive Services Speech service resource](includes/create-speech-resource.md)]

[!INCLUDE [Create a Speech service container on Azure Container Instances](../containers/includes/create-container-instances-resource-from-azure-cli.md)]

[!INCLUDE [API documentation](../../../includes/cognitive-services-containers-api-documentation.md)]

[!INCLUDE [Containers Next Steps](../containers/includes/containers-next-steps.md)]