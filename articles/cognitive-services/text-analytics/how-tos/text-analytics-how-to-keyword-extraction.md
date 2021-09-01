---
title: Text Analytics REST API を使用したキー フレーズ抽出
titleSuffix: Azure Cognitive Services
description: Azure Cognitive Services の Text Analytics REST API を使用してキー フレーズを抽出する方法。
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: article
ms.date: 08/04/2021
ms.author: aahi
ms.openlocfilehash: 6a7dca4fd7fe74515f7532b457ce9e1aaad65b57
ms.sourcegitcommit: 0046757af1da267fc2f0e88617c633524883795f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "121745522"
---
# <a name="example-how-to-extract-key-phrases-using-text-analytics"></a>例:Text Analytics を使用してキー フレーズを抽出する方法

[キー フレーズ抽出](https://westus2.dev.cognitive.microsoft.com/docs/services/TextAnalytics-v3-1/operations/KeyPhrases) API は、非構造化テキストを評価し、各 JSON ドキュメントに対してキー フレーズのリストを返します。

この機能は、ドキュメントのコレクション内の要点をすばやく特定する必要がある場合に便利です。 たとえば、「食べ物はおいしくて、すばらしいスタッフがいた」というテキストを入力すると、このサービスは話題の中心として "食べ物" と "すばらしいスタッフ" を返します。

詳細については、[サポートされている言語](../language-support.md)に関するページを参照してください。

> [!TIP]
> * Text Analytics にはキー フレーズ抽出用の Linux ベースの Docker コンテナー イメージも用意されているため、データの近くに [Text Analytics コンテナーをインストールして実行](text-analytics-how-to-install-containers.md)することができます。
> * また、`/analyze` エンドポイントを使用して、この機能を[非同期に](text-analytics-how-to-call-api.md)使用することもできます。

## <a name="preparation"></a>準備

キー フレーズ抽出は、扱うテキストの量が多いほど効果を発揮します。 感情分析では逆で、テキストの量が少ないほどパフォーマンスが向上します。 両方の操作から最善の結果を得るには、両方の操作に応じて入力を再構成することを検討してください。

JSON ドキュメントは、次の形式である必要があります: ID、テキスト、言語

ドキュメントのサイズは、ドキュメントあたり 5,120 文字以下である必要があり、コレクションあたり最大 10 の項目 (ID) を含めることができます。 コレクションは、要求の本文で送信されます。 次の例では、キー フレーズの抽出用に送信するコンテンツを示しています。 

要求と応答オブジェクトの詳細については、[Text Analytics API の呼び出し方法](text-analytics-how-to-call-api.md)に関するページを参照してください。  

### <a name="example-synchronous-request-object"></a>同期要求オブジェクトの例


```json
    {
        "documents": [
            {
                "language": "en",
                "id": "1",
                "text": "We love this trail and make the trip every year. The views are breathtaking and well worth the hike!"
            },
            {
                "language": "en",
                "id": "2",
                "text": "Poorly marked trails! I thought we were goners. Worst hike ever."
            },
            {
                "language": "en",
                "id": "3",
                "text": "Everyone in my family liked the trail but thought it was too challenging for the less athletic among us. Not necessarily recommended for small children."
            },
            {
                "language": "en",
                "id": "4",
                "text": "It was foggy so we missed the spectacular views, but the trail was ok. Worth checking out if you are in the area."
            },
            {
                "language": "en",
                "id": "5",
                "text": "This is my favorite trail. It has beautiful views and many places to stop and rest"
            }
        ]
    }
```

### <a name="example-asynchronous-request-object"></a>非同期要求オブジェクトの例

`v3.1` 以降、`/analyze` エンドポイントを使用して、NER 要求を非同期的に送信できます。


```json
{
    "displayName": "My Job",
    "analysisInput": {
        "documents": [
            {
                "id": "doc1",
                "text": "It's incredibly sunny outside! I'm so happy"
            },
            {
                "id": "doc2",
                "text": "Pike place market is my favorite Seattle attraction."
            }
        ]
    },
    "tasks": {
        "keyPhraseExtractionTasks": [{
            "parameters": {
                "model-version": "latest"
            }
        }],
    }
}
```

## <a name="step-1-structure-the-request"></a>手順 1:要求を構造化する

要求定義の詳細については、[Text Analytics API の呼び出し方法](text-analytics-how-to-call-api.md)に関するページを参照してください。 確認に便利なように、以下に再度、要点を示します。

+ **POST** 要求を作成します。 この要求については次の API ドキュメントを確認してください。[Key Phrases API](https://westus2.dev.cognitive.microsoft.com/docs/services/TextAnalytics-v3-1/operations/KeyPhrases)。

+ Azure 上の Text Analytics リソースまたはインスタンス化された [Text Analytics コンテナー](text-analytics-how-to-install-containers.md)を使用して、キー フレーズ抽出用の HTTP エンドポイントを設定します。 API を同期的に使用している場合は、URL に `/text/analytics/v3.1/keyPhrases` を含める必要があります。 (例: `https://<your-custom-subdomain>.api.cognitiveservices.azure.com/text/analytics/v3.1/keyPhrases`)。

+ Text Analytics 操作用の[アクセス キー](../../cognitive-services-apis-create-account.md#get-the-keys-for-your-resource)が含まれるように要求ヘッダーを設定します。

+ 要求本文で、この分析のために準備した JSON ドキュメントのコレクションを提供します。

> [!Tip]
> [Postman](text-analytics-how-to-call-api.md) を使用するか、[ドキュメント](https://westus2.dev.cognitive.microsoft.com/docs/services/TextAnalytics-v3-1/operations/KeyPhrases)に記載されている **API テスト コンソール** を開き、要求を構造化して POST でサービスに投稿します。

## <a name="step-2-post-the-request"></a>手順 2:要求を投稿する

要求が受信されると分析が実行されます。 分単位または秒単位で送信できる要求のサイズと数については、「[データ制限](../concepts/data-limits.md)」の記事を参照してください。

サービスはステートレスであることを思い出してください。 ユーザーのアカウントに保存されるデータはありません。 結果はすぐに、応答で返されます。

## <a name="step-3-view-results"></a>手順 3:結果の表示

すべての POST 要求で、ID と検出されたプロパティを含む JSON 形式の応答が返されます。 返されるキー フレーズの順序は、モデル別に内部的に決定されます。

出力はすぐに返されます。 結果は、JSON を受け付けるアプリケーションにストリームするか、ローカル システム上のファイルに出力を保存してから、そのファイルを、データの並べ替え、検索、および操作が可能なアプリケーションにインポートすることができます。

v3.1 エンドポイントからのキー フレーズ抽出の出力例を次に示します。

### <a name="synchronous-result"></a>同期の結果

```json
{
    "documents": [
        {
            "id": "1",
            "keyPhrases": [
                "trail",
                "trip",
                "views",
                "hike"
            ],
            "warnings": []
        },
        {
            "id": "2",
            "keyPhrases": [
                "Worst hike",
                "trails"
            ],
            "warnings": []
        },
        {
            "id": "3",
            "keyPhrases": [
                "less athletic",
                "small children",
                "Everyone",
                "family",
                "trail"
            ],
            "warnings": []
        },
        {
            "id": "4",
            "keyPhrases": [
                "spectacular views",
                "trail",
                "area"
            ],
            "warnings": []
        },
        {
            "id": "5",
            "keyPhrases": [
                "favorite trail",
                "beautiful views",
                "many places"
            ],
            "warnings": []
        }
    ],
    "errors": [],
    "modelVersion": "2021-06-01"
}
```
前述のように、アナライザーは重要ではない単語を検索して破棄し、文の主語または目的語と思われる 1 つの用語または語句を保持します。

### <a name="asynchronous-result"></a>非同期の結果

非同期操作に `/analyze` エンドポイントを使用すると、API に送信したタスクを含む応答が返されます。

```json
{
    "jobId": "fa813c9a-0d96-4a34-8e4f-a2a6824f9190",
    "lastUpdateDateTime": "2021-07-07T18:16:45Z",
    "createdDateTime": "2021-07-07T18:16:15Z",
    "expirationDateTime": "2021-07-08T18:16:15Z",
    "status": "succeeded",
    "errors": [],
    "displayName": "My Job",
    "tasks": {
        "completed": 1,
        "failed": 0,
        "inProgress": 0,
        "total": 1,
        "keyPhraseExtractionTasks": [
            {
                "lastUpdateDateTime": "2021-07-07T18:16:45.0623454Z",
                "taskName": "KeyPhraseExtraction_latest",
                "state": "succeeded",
                "results": {
                    "documents": [
                        {
                            "id": "doc1",
                            "keyPhrases": [],
                            "warnings": []
                        },
                        {
                            "id": "doc2",
                            "keyPhrases": [
                                "Pike place market",
                                "Seattle attraction",
                                "favorite"
                            ],
                            "warnings": []
                        }
                    ],
                    "errors": [],
                    "modelVersion": "2021-06-01"
                }
            }
        ]
    }
}
```


## <a name="summary"></a>まとめ

この記事では、Cognitive Services の Text Analytics を使用するキー フレーズ抽出の概念とワークフローについて説明しました。 要約すると:

+ 選択した言語に対して、[キー フレーズ抽出 API](https://westus2.dev.cognitive.microsoft.com/docs/services/TextAnalytics-v3-1/operations/KeyPhrases) を使用できます。
+ 要求本文内の JSON ドキュメントには、ID、テキスト、および言語のコードが含まれます。
+ POST 要求は、ユーザーのサブスクリプションで有効な、個人用に設定された[アクセス キーとエンドポイント](../../cognitive-services-apis-create-account.md#get-the-keys-for-your-resource)を使用して `/keyphrases` エンドポイントまたは `/analyze` エンドポイントに対して行われます。
+ ドキュメント ID ごとのキーワードやキーフレーズで構成される応答出力は、Microsoft Office Excel や Power BI を含む JSON を受け取るすべてのアプリにストリーミングすることができます。

## <a name="see-also"></a>関連項目

 [Text Analytics の概要](../overview.md) [よく寄せられる質問 (FAQ)](../text-analytics-resource-faq.yml)</br>
 [Text Analytics 製品ページ](//go.microsoft.com/fwlink/?LinkID=759712)

## <a name="next-steps"></a>次のステップ

* [Text Analytics の概要](../overview.md)
* [Text Analytics クライアント ライブラリの使用](../quickstarts/client-libraries-rest-api.md)
* [新機能](../whats-new.md)
* [モデルのバージョン](../concepts/model-versioning.md)
