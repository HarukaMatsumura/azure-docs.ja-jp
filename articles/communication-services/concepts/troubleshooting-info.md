---
title: Azure Communication Services でのトラブルシューティング
description: Communication Services ソリューションのトラブルシューティングに必要な情報を収集する方法について説明します。
author: manoskow
manager: jken
services: azure-communication-services
ms.author: manoskow
ms.date: 10/23/2020
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: 4921078e9e7b5d9de06fbbc9a97dc4a964569e04
ms.sourcegitcommit: 8c7f47cc301ca07e7901d95b5fb81f08e6577550
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92754665"
---
# <a name="troubleshooting-in-azure-communication-services"></a>Azure Communication Services でのトラブルシューティング

このドキュメントは、Communication Services ソリューションのトラブルシューティングに必要な情報の収集に役立ちます。

## <a name="getting-help"></a>ヘルプの表示

開発者の皆さんは、ご質問の送信、機能のご提案、および Communication Services [GitHub リポジトリ](https://github.com/Azure/communication)の問題のレポートに関してぜひご協力ください。 他に次のフォーラムもあります。

* [Microsoft Q&A](https://docs.microsoft.com/answers/questions/topics/single/101418.html)
* [StackOverflow](https://stackoverflow.com/questions/tagged/azure+communication)

Azure サブスクリプションの[サポート プラン](https://azure.microsoft.com/support/plans/)によっては、[Azure portal](https://azure.microsoft.com/support/create-ticket/) を通じてサポート チケットを直接送信することもできます。

特定の種類の問題のトラブルシューティングを支援するために、次の情報をおたずねする場合があります。

* **MS-CV ID** : この ID は、通話とメッセージのトラブルシューティングに使用されます。 
* **通話 ID** : この ID は、Communication Services の通話を識別するために使用されます。
* **SMS メッセージ ID** : この ID は、SMS メッセージを識別するために使用されます。

## <a name="access-your-ms-cv-id"></a>MS-CV ID にアクセスする

MS-CV ID にアクセスするには、クライアント ライブラリを初期化する際に、`clientOptions` オブジェクト インスタンスで診断を構成します。 診断は、チャット、管理、VoIP 通話など、任意の Azure クライアント ライブラリに対して構成できます。

### <a name="client-options-example"></a>クライアント オプションの例

次のコード スニペットは、診断の構成を示しています。 診断を有効にした状態でクライアント ライブラリを使用すると、構成済みのイベント リスナーに診断の詳細が出力されます。

# <a name="c"></a>[C#](#tab/csharp)
``` 
// 1. Import Azure.Core.Diagnostics
using Azure.Core.Diagnostics;

// 2. Initialize an event source listener instance
using var listener = AzureEventSourceListener.CreateConsoleLogger();
Uri endpoint = new Uri("https://<RESOURCE-NAME>.communication.azure.net");
var (token, communicationUser) = await GetCommunicationUserAndToken();
CommunicationUserCredential communicationUserCredential = new CommunicationUserCredential(token);

// 3. Setup diagnostic settings
var clientOptions = new ChatClientOptions()
{
    Diagnostics =
    {
        LoggedHeaderNames = { "*" },
        LoggedQueryParameters = { "*" },
        IsLoggingContentEnabled = true,
    }
};

// 4. Initialize the ChatClient instance with the clientOptions 
ChatClient chatClient = new ChatClient(endpoint, communicationUserCredential, clientOptions);
ChatThreadClient chatThreadClient = await chatClient.CreateChatThreadAsync("Thread Topic", new[] { new ChatThreadMember(communicationUser) });
```

# <a name="python"></a>[Python](#tab/python)
``` 
from azure.communication.chat import ChatClient, CommunicationUserCredential
endpoint = "https://communication-services-sdk-live-tests-for-python.communication.azure.com"
chat_client = ChatClient(
    endpoint,
    CommunicationUserCredential(token),
    http_logging_policy=your_logging_policy)
```
---

## <a name="access-your-call-id"></a>通話 ID にアクセスする

Azure portal を通じて通話の問題に関連したサポート リクエストを提出する場合は、参照している通話の ID を提供するよう求められることがあります。 これには、通話クライアント ライブラリを介してアクセスできます。

# <a name="javascript"></a>[JavaScript](#tab/javascript)
```javascript
// `call` is an instance of a call created by `callAgent.call` or `callAgent.join` methods 
console.log(call.id)
```

# <a name="ios"></a>[iOS](#tab/ios)
```objc
// The `call id` property can be retrieved by calling the `call.getCallId()` method on a call object after a call ends 
// todo: the code snippet suggests it's a property while the comment suggests it's a method call
print(call.callId) 
```

# <a name="android"></a>[Android](#tab/android)
```java
// The `call id` property can be retrieved by calling the `call.getCallId()` method on a call object after a call ends
// `call` is an instance of a call created by `callAgent.call(…)` or `callAgent.join(…)` methods 
Log.d(call.getCallId()) 
```
---


## <a name="access-your-sms-message-id"></a>SMS メッセージ ID にアクセスする

SMS の問題については、応答オブジェクトからメッセージ ID を収集できます。

# <a name="net"></a>[.NET](#tab/dotnet)
```
// Instantiate the SMS client
const smsClient = new SmsClient(connectionString);
async function main() {
  const result = await smsClient.send({
    from: "+18445792722",
    to: ["+1972xxxxxxx"],
    message: "Hello World 👋🏻 via Sms"
  }, {
    enableDeliveryReport: true // Optional parameter
  });
console.log(result); // your message ID will be in the result
}
```
---

## <a name="related-information"></a>関連情報
- [ログと診断](logging-and-diagnostics.md)
- [メトリック](metrics.md)
