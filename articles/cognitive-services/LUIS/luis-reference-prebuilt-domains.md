---
title: 事前構築済みのドメインのリファレンス - LUIS
titleSuffix: Azure Cognitive Services
description: 事前構築済みのドメインのリファレンスです。事前構築済みのドメインは、Language Understanding Intelligent Service (LUIS) の意図とエンティティの事前構築済みのコレクションです。
services: cognitive-services
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: reference
ms.date: 09/27/2019
ms.openlocfilehash: e93822f4a2992f619b598474082caa56562b6e36
ms.sourcegitcommit: f5580dd1d1799de15646e195f0120b9f9255617b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91538366"
---
# <a name="prebuilt-domain-reference-for-your-luis-app"></a>LUIS アプリの事前構築済みのドメインのリファレンス
このリファレンスは、[事前構築済みのドメイン](luis-how-to-use-prebuilt-domains.md)に関する情報を提供します。事前構築済みのドメインは、LUIS が提供している意図とエンティティの事前構築済みのコレクションです。

対照的に、[カスタム ドメイン](luis-how-to-start-new-app.md)は意図とモデルがない状態から始まります。 任意の事前構築済みのドメインの意図とエンティティをカスタム モデルに追加できます。

## <a name="prebuilt-domains-per-language"></a>言語ごとの事前構築済みドメイン

次の表は、現在サポートされているドメインをまとめたものです。 通常、他の言語より、英語のサポートが完成されています。

| エンティティの種類       | EN-US      | ZH-CN   | DE    | FR     | ES    | IT      | PT-BR |  JP  |      KO |        NL |    TR |
|:-----------------:|:-------:|:-------:|:-----:|:------:|:-----:|:-------:| :-------:| :-------:| :-------:| :-------:|  :-------:|
| Calendar  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
|Communication  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Email     | ✓    | ✓       | ✓   | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| HomeAutomation          | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| メモ     | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| 場所   | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| RestaurantReservation  | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| ToDo     | ✓    | ✓       | ✓    | ✓     | ✓     | ✓  | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Utilities      | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Weather        | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |
| Web    | ✓    | ✓        | ✓    | ✓      | ✓     | ✓       | ✓  | ✓      | ✓    | ✓    | ✓     | ✓  |

事前構築済みドメインは次の場所では**サポートされていません**。

* フランス語 (カナダ)
* ヒンディー語
* スペイン語 (メキシコ)

## <a name="next-steps"></a>次のステップ

[シンプル エンティティ](reference-entity-simple.md)について学びます。
