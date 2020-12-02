---
title: Azure Container インスタンスで LUIS コンテナーをデプロイする
titleSuffix: Azure Cognitive Services
description: LUIS コンテナーを Azure Container インスタンスにデプロイし、Web ブラウザーでテストします。
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 04/07/2020
ms.author: aahi
ms.openlocfilehash: edc2ad0f895b8a1bb6448ce1cdf79b1b2ce83951
ms.sourcegitcommit: 10d00006fec1f4b69289ce18fdd0452c3458eca5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "95997199"
---
# <a name="deploy-the-language-understanding-luis-container-to-azure-container-instances"></a>Language Understanding (LUIS) コンテナーを Azure Container インスタンスにデプロイする

Cognitive Services [LUIS](luis-container-howto.md) コンテナーを Azure [Container インスタンス](../../container-instances/index.yml)にデプロイする方法について説明します。 この手順では、Anomaly Detector リソースの作成方法を実演します。 次に、関連するコンテナー イメージをプルする方法について説明します。 最後に、ブラウザーからこの 2 つのオーケストレーションを行う機能を取り上げます。 コンテナーを使用することで、開発者の関心をインフラストラクチャの管理から切り離し、アプリケーション開発に専念させることができます。

[!INCLUDE [Prerequisites](../containers/includes/container-prerequisites.md)]

[!INCLUDE [Create LUIS resource](includes/create-luis-resource.md)]

[!INCLUDE [Gathering required parameters](../containers/includes/container-gathering-required-parameters.md)]

## <a name="create-an-azure-file-share"></a>Azure ファイル共有を作成する

LUIS コンテナーには、実行時にでプルされる `.gz` モデル ファイルが必要です。 コンテナーからは、コンテナー インスタンスからのボリューム マウントを介してこのモデル ファイルにアクセスできる必要があります。 Azure ファイル共有の作成については、[ファイル共有の作成](../../storage/files/storage-how-to-create-file-share.md)に関する記事を参照してください。 後で必要になるため、Azure ストレージ アカウント名、キー、およびファイル共有名をメモします。

### <a name="export-and-upload-packaged-luis-app"></a>パッケージ化された LUIS アプリのエクスポートとアップロード

LUIS モデル (パッケージ アプリ) を Azure ファイル共有にアップロードするには、<a href="luis-container-howto.md#export-packaged-app-from-luis" target="_blank" rel="noopener">まず LUIS ポータルからエクスポートします<span class="docon docon-navigate-external x-hidden-focus"></span></a>。 Azure portal から、ストレージ アカウント リソースの **[概要]** ページに移動し、 **[ファイル共有]** を選択します。 最近作成したファイル共有名を選択し、 **[アップロード]** ボタンを選択します。

> [!div class="mx-imgBorder"]
> ![ファイル共有にアップロードする](media/luis-how-to-deploy-to-aci/upload-file-share.png)

LUIS モデル ファイルをアップロードします。

[!INCLUDE [Create LUIS Container instance resource](../containers/includes/create-container-instances-resource-from-azure-cli.md)]

[!INCLUDE [API documentation](../../../includes/cognitive-services-containers-api-documentation.md)]

[!INCLUDE [Next steps](../containers/includes/containers-next-steps.md)]