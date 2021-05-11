---
title: Azure Cosmos DB クエリ言語の LOWER
description: 大文字のデータが小文字に変換された後の文字列式を返す Azure Cosmos DB のLOWER SQL システム関数について説明します
author: ginamr
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.topic: conceptual
ms.date: 04/07/2021
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: b97b2806ebcf6613e9dde2e4d9172ee63e8ae719
ms.sourcegitcommit: 62e800ec1306c45e2d8310c40da5873f7945c657
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "108164491"
---
# <a name="lower-azure-cosmos-db"></a>LOWER (Azure Cosmos DB)
[!INCLUDE[appliesto-sql-api](includes/appliesto-sql-api.md)]

 文字列式の大文字データを小文字に変換して返します。  

LOWER システム関数では、インデックスは使用されません。 大文字と小文字を区別しない比較を頻繁に行う場合、LOWER システム関数は、大量の RU を消費する可能性があります。 この場合は、LOWER システム関数を使用して比較のたびにデータを正規化するのではなく、挿入時に大文字と小文字を正規化することができます。 次に、SELECT * FROM c (LOWER (c. name) = ' bob ') などのクエリは、単に SELECT * FROM c WHERE c.name = ' bob ' になります。

## <a name="syntax"></a>構文
  
```sql
LOWER(<str_expr>)  
```  
  
## <a name="arguments"></a>引数
  
*str_expr*  
   文字列式です。  
  
## <a name="return-types"></a>戻り値の型
  
  文字列式を返します。  
  
## <a name="examples"></a>例
  
  次の例は、クエリ内での `LOWER` の使用方法を示しています。  
  
```sql
SELECT LOWER("Abc") AS lower
```  
  
 結果セットは次のようになります。  
  
```json
[{"lower": "abc"}]  
  
```  

## <a name="remarks"></a>解説

このシステム関数では、[インデックスは使用](index-overview.md#index-usage)されません。

## <a name="next-steps"></a>次のステップ

- [Azure Cosmos DB の文字列関数](sql-query-string-functions.md)
- [Azure Cosmos DB のシステム関数](sql-query-system-functions.md)
- [Azure Cosmos DB の概要](introduction.md)
