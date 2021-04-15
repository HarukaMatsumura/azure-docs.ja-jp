---
title: インクルード ファイル
description: インクルード ファイル
services: virtual-machines
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 01/28/2020
ms.author: cynthn
ms.custom: include file
ms.openlocfilehash: 1c06f5ab8995e7285365fa2d0ee77c327be2b1bd
ms.sourcegitcommit: 2654d8d7490720a05e5304bc9a7c2b41eb4ae007
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2021
ms.locfileid: "107386581"
---
## <a name="list-information"></a>リストの情報

[az sig list](/cli/azure/sig#az-sig-list) を使用して、利用可能なイメージ ギャラリーに関する場所、ステータス、およびその他の情報を取得します。

```azurecli-interactive 
az sig list -o table
```

[az sig image-definition list](/cli/azure/sig/image-definition#az-sig-image-definition-list) を使用して、OS の種類とステータスに関する情報を含め、ギャラリーにあるイメージ定義を一覧表示します。

```azurecli-interactive 
az sig image-definition list --resource-group myGalleryRG --gallery-name myGallery -o table
```

[az sig image-version list](/cli/azure/sig/image-version#az-sig-image-version-list) を使用して、ギャラリーにある共有イメージ バージョンを一覧表示します。

```azurecli-interactive
az sig image-version list --resource-group myGalleryRG --gallery-name myGallery --gallery-image-definition myImageDefinition -o table
```

[az sig image-version show](/cli/azure/sig/image-version#az-sig-image-version-show) を使用して、イメージ バージョンの ID を取得します。

```azurecli-interactive
az sig image-version show \
   --resource-group myGalleryRG \
   --gallery-name myGallery \
   --gallery-image-definition myImageDefinition \
   --gallery-image-version 1.0.0 \
   --query "id"
```
