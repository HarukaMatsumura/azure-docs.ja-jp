---
title: Azure Cosmos DB クエリ言語の REPLACE
description: Azure Cosmos DB の SQL システム関数 REPLACE について説明します。
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 09/13/2019
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: 758ac13530752df481d27e7e253f025f5c8d6430
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "78302204"
---
# <a name="replace-azure-cosmos-db"></a>REPLACE (Azure Cosmos DB)
 指定した文字列値をすべて別の文字列値に置き換えます。  
  
## <a name="syntax"></a>構文
  
```sql
REPLACE(<str_expr1>, <str_expr2>, <str_expr3>)  
```  
  
## <a name="arguments"></a>引数
  
*str_expr1*  
   検索対象となる文字列式です。  
  
*str_expr2*  
   検出する文字列式です。  
  
*str_expr3*  
   *str_expr1*内で見つかった *str_expr2* を置きかえる文字列式です。  
  
## <a name="return-types"></a>戻り値の型
  
  文字列式を返します。  
  
## <a name="examples"></a>例
  
  次の例は、クエリ内での `REPLACE` の使用方法を示しています。  
  
```sql
SELECT REPLACE("This is a Test", "Test", "desk") AS replace
```  
  
 結果セットは次のようになります。  
  
```json
[{"replace": "This is a desk"}]  
```  

## <a name="remarks"></a>解説

このシステム関数では、インデックスは使用されません。

## <a name="next-steps"></a>次のステップ

- [Azure Cosmos DB の文字列関数](sql-query-string-functions.md)
- [Azure Cosmos DB のシステム関数](sql-query-system-functions.md)
- [Azure Cosmos DB の概要](introduction.md)
