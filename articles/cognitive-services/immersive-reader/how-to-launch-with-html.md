---
title: イマーシブ リーダーを起動して HTML コンテンツを表示する
titleSuffix: Azure Cognitive Services
description: この記事では、イマーシブ リーダーを起動して HTML コンテンツを表示する方法について説明します。
author: metanMSFT
manager: guillasi
ms.service: cognitive-services
ms.subservice: immersive-reader
ms.topic: conceptual
ms.date: 01/14/2020
ms.author: metan
ms.custom: devx-track-js
ms.openlocfilehash: f7f55d1d349fc7d02c2ac53f7a50f9d649688cbd
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91326764"
---
# <a name="how-to-launch-the-immersive-reader-with-html-content"></a>イマーシブ リーダーを起動して HTML コンテンツを表示する方法

この記事では、イマーシブ リーダーを起動して HTML コンテンツを表示する方法について説明します。

## <a name="prepare-the-html-content"></a>HTML コンテンツを準備する

イマーシブ リーダーでレンダリングしたいコンテンツをコンテナー要素内に配置します。 コンテナー要素に一意の `id` があることを確認してください。 イマーシブ リーダーは、基本的な HTML 要素をサポートします。詳細については、[リファレンス](./reference.md#html-support)を参照してください。

```html
<div id='immersive-reader-content'>
    <b>Bold</b>
    <i>Italic</i>
    <u>Underline</u>
    <strike>Strikethrough</strike>
    <code>Code</code>
    <sup>Superscript</sup>
    <sub>Subscript</sub>
    <ul><li>Unordered lists</li></ul>
    <ol><li>Ordered lists</li></ol>
</div>
```

## <a name="get-the-html-content-in-javascript"></a>JavaScript で HTML コンテンツを取得する

JavaScript コードで HTML コンテンツを取得するには、コンテナー要素の `id` を使用します。

```javascript
const htmlContent = document.getElementById('immersive-reader-content').innerHTML;
```

## <a name="launch-the-immersive-reader-with-your-html-content"></a>イマーシブ リーダーを起動して HTML コンテンツを表示する

`ImmersiveReader.launchAsync` を呼び出すときに、チャンクの `mimeType` プロパティを `text/html` に設定すると、HTML のレンダリングが有効になります。

```javascript
const data = {
    chunks: [{
        content: htmlContent,
        mimeType: 'text/html'
    }]
};

ImmersiveReader.launchAsync(YOUR_TOKEN, YOUR_SUBDOMAIN, data, YOUR_OPTIONS);
```

## <a name="next-steps"></a>次のステップ

* [イマーシブ リーダー SDK リファレンス](./reference.md)を参照する