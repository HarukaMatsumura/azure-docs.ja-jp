---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 05/27/2019
ms.author: glenga
ms.openlocfilehash: d697334fe56fb9133a06cee79067c60bc3a37281
ms.sourcegitcommit: eb6bef1274b9e6390c7a77ff69bf6a3b94e827fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "68639154"
---
バインド拡張機能をインストールする最も簡単な方法は、[拡張機能のバンドル](../articles/azure-functions/functions-bindings-register.md#extension-bundles)を有効にすることです。 バンドルを有効にすると、事前定義された一連の拡張機能パッケージが自動的にインストールされます。

拡張機能のバンドルを有効にするには、host.json ファイルを開き、その内容を次のコードに合わせて更新します。

```json
{
    "version": "2.0",
    "extensionBundle": {
        "id": "Microsoft.Azure.Functions.ExtensionBundle",
        "version": "[1.*, 2.0.0)"
    }
}
```