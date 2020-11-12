---
title: .NET での BLOB ストレージの要求時にカスタマー指定のキーを指定する - Azure Storage
description: .NET を使用した BLOB ストレージの要求時に、カスタマー指定のキーを指定する方法について説明します。
services: storage
author: tamram
ms.service: storage
ms.topic: how-to
ms.date: 07/20/2020
ms.author: tamram
ms.reviewer: ozgun
ms.subservice: common
ms.custom: devx-track-csharp
ms.openlocfilehash: 50d592d0020ae1b5a704296ef68f5153f0207714
ms.sourcegitcommit: 0dcafc8436a0fe3ba12cb82384d6b69c9a6b9536
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94427577"
---
# <a name="specify-a-customer-provided-key-on-a-request-to-blob-storage-with-net"></a>.NET での BLOB ストレージの要求時にカスタマー指定のキーを指定する

Azure BLOB ストレージに対して要求を行うクライアントには、個々の要求に対して暗号化キーを指定するオプションがあります。 要求に暗号化キーを含めると、BLOB ストレージ操作の暗号化設定をきめ細かく制御できます。 カスタマー指定のキーは、Azure Key Vault または別のキー ストアに格納できます。

この記事では、.NET での BLOB ストレージの要求時にカスタマー指定のキーを指定する方法を示します。

[!INCLUDE [storage-install-packages-blob-and-identity-include](../../../includes/storage-install-packages-blob-and-identity-include.md)]

Azure Storage から Azure ID クライアント ライブラリを使用して認証する方法の詳細については、 [Azure Active Directory と Azure リソースのマネージ ID を使用した BLOB およびキューへのアクセスの認証](../common/storage-auth-aad-msi.md?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json#authenticate-with-the-azure-identity-library)に関するページの「 **Azure ID ライブラリを使用した認証** 」を参照してください。

## <a name="example-use-a-customer-provided-key-to-upload-a-blob"></a>例:カスタマー指定のキーを使用して BLOB をアップロードする

次の例では、カスタマー指定のキーを作成し、そのキーを使用して BLOB をアップロードします。 このコードは、1 つのブロックをアップロードしてから、ブロック一覧をコミットして Azure Storage に BLOB を書き込みます。

```csharp
async static Task UploadBlobWithClientKey(string accountName, string containerName,
    string blobName, Stream data, byte[] key)
{
    const string blobServiceEndpointSuffix = ".blob.core.windows.net";
    Uri accountUri = new Uri("https://" + accountName + blobServiceEndpointSuffix);

    // Specify the customer-provided key on the options for the client.
    BlobClientOptions options = new BlobClientOptions()
    {
        CustomerProvidedKey = new CustomerProvidedKey(key)
    };

    // Create a client object for the Blob service, including options.
    BlobServiceClient serviceClient = new BlobServiceClient(accountUri, 
        new DefaultAzureCredential(), options);

    // Create a client object for the container.
    // The container client retains the credential and client options.
    BlobContainerClient containerClient = serviceClient.GetBlobContainerClient(containerName);

    // Create a new block blob client object.
    // The blob client retains the credential and client options.
    BlobClient blobClient = containerClient.GetBlobClient(blobName);

    try
    {
        // Create the container if it does not exist.
        await containerClient.CreateIfNotExistsAsync();

        // Upload the data using the customer-provided key.
        await blobClient.UploadAsync(data);
    }
    catch (RequestFailedException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="next-steps"></a>次のステップ

- [BLOB ストレージに対する要求で暗号化キーを指定する](encryption-customer-provided-keys.md)
- [保存データに対する Azure Storage 暗号化](../common/storage-service-encryption.md)
