---
title: Azure Table Storage の概要
description: Table Storage を使用すると、Web アプリケーションのユーザー データ、アドレス帳、デバイス情報、その他の種類のメタデータなど、柔軟なデータセットを格納できます。
ms.service: cosmos-db
ms.subservice: cosmosdb-table
ms.devlang: dotnet
ms.topic: overview
ms.date: 05/20/2019
author: sakash279
ms.author: akshanka
ms.reviewer: sngun
ms.openlocfilehash: abd88c3cdb54747c21ad8772860a3ed6929dbd15
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91318723"
---
# <a name="azure-table-storage-overview"></a>Azure Table Storage の概要

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Azure Table Storage は、NoSQL の構造化データをクラウド内に格納するサービスです。スキーマレスのデザインでキー/属性ストアを実現します。 Table Storage はスキーマがないため、アプリケーションの進化のニーズに合わせてデータを容易に修正できます。 Table Storage のデータ アクセスは、多くの種類のアプリケーションにとって高速でコスト効率に優れ、また一般に、従来の SQL と比較して、同様の容量のデータを低コストで保存することができます。

Table Storage を使用すると、Web アプリケーションのユーザー データ、アドレス帳、デバイス情報、サービスに必要なその他の種類のメタデータなど、柔軟なデータセットを格納できます。 ストレージ アカウントの容量の上限を超えない限り、テーブルには任意の数のエンティティを保存でき、ストレージ アカウントには任意の数のテーブルを含めることができます。

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

## <a name="next-steps"></a>次のステップ

* [Microsoft Azure ストレージ エクスプローラー](../vs-azure-tools-storage-manage-with-storage-explorer.md)は、Windows、macOS、Linux で Azure Storage のデータを視覚的に操作できる Microsoft 製の無料のスタンドアロン アプリです。

* [.NET SDK を使用した Azure Cosmos DB Table API と Azure Table Storage の概要](table-storage-how-to-use-dotnet.md)

* 利用可能な API の詳細については、Table service のリファレンス ドキュメントを参照してください。

    * [.NET 用ストレージ クライアント ライブラリ リファレンス](https://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

    * [REST API リファレンス](https://msdn.microsoft.com/library/azure/dd179355)
