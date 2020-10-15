---
title: Azure Cosmos DB クエリ言語の TAN
description: Azure Cosmos DB の SQL システム関数 TAN について説明します。
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 03/04/2020
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: 9d7187ba116067445e835769fc33aa70677ef80b
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "78301983"
---
# <a name="tan-azure-cosmos-db"></a>TAN (Azure Cosmos DB)
 式で指定されたラジアン単位の角度のタンジェントを返します。  
  
## <a name="syntax"></a>構文
  
```sql
TAN (<numeric_expr>)  
```  
  
## <a name="arguments"></a>引数
  
*numeric_expr*  
   数値式です。  
  
## <a name="return-types"></a>戻り値の型
  
  数値式を返します。  
  
## <a name="examples"></a>例
  
  次の例は、PI()/2 のタンジェントを計算します。  
  
```sql
SELECT TAN(PI()/2) AS tan 
```  
  
 結果セットは次のようになります。  
  
```json
[{"tan": 16331239353195370 }]  
```  

## <a name="remarks"></a>解説

このシステム関数では、インデックスは使用されません。

## <a name="next-steps"></a>次のステップ

- [Azure Cosmos DB の数学関数](sql-query-mathematical-functions.md)
- [Azure Cosmos DB のシステム関数](sql-query-system-functions.md)
- [Azure Cosmos DB の概要](introduction.md)
