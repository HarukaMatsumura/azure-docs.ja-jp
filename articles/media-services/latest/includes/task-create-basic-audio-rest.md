---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 08/18/2020
ms.author: inhenkel
ms.custom: CLI
ms.openlocfilehash: eacdfe663ee3ec323d59daf160fe33af073bc1c5
ms.sourcegitcommit: 59f506857abb1ed3328fda34d37800b55159c91d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92525013"
---
<!--Create a basic audio transform REST-->

次の Azure REST コマンドによって、基本的なオーディオ資産が作成されます。 値 `subscriptionID`、`resourceGroup`、`amsAccountName` を、処理中の値に置き換えてください。 ここで `assetName` を設定して、資産に名前を付けます。

```
PUT https://management.azure.com/subscriptions/{{subscriptionId}}/resourceGroups/{{resourceGroup}}/providers/Microsoft.Media/mediaServices/{{accountName}}/transforms/{{transformName}}?api-version=2020-05-01
```

## <a name="body"></a>Body
```json
{
    "properties": {
        "description": "Transform for Audio Analyzer Basic Mode",
        "outputs": [
            {
                "onError": "StopProcessingJob",
                "relativePriority": "Normal",
                "preset": {
                    "@odata.type": "#Microsoft.Media.AudioAnalyzerPreset",
                    "audioLanguage": "en-US",
                    "mode": "Basic"
                }
            }
        ]
    }
}
```

## <a name="sample-response"></a>応答のサンプル
```json
{
    "name": "audioAnalyzerTransform",
    "id": "/subscriptions/35c2594a-xxxx-4fce-b59c-f6fb9513eeeb/resourceGroups/myresourcegroup/providers/Microsoft.Media/mediaservices/mymediaservicesaccount/transforms/audioAnalyzerTransform",
    "type": "Microsoft.Media/mediaservices/transforms",
    "properties": {
        "created": "2020-10-23T18:03:37.4793962Z",
        "description": "Transform for Audio Analyzer Basic Mode",
        "lastModified": "2020-10-23T18:03:37.4793962Z",
        "outputs": [
            {
                "onError": "StopProcessingJob",
                "relativePriority": "Normal",
                "preset": {
                    "@odata.type": "#Microsoft.Media.AudioAnalyzerPreset",
                    "audioLanguage": "en-US",
                    "mode": "Basic",
                    "experimentalOptions": {
                        "basicAudioEnabled": "true"
                    }
                }
            }
        ]
    }
}
```