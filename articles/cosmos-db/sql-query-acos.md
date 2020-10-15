---
title: Azure Cosmos DB クエリ言語の ACOS
description: Azure Cosmos DB の ACOS（arccosice）SQL システム関数が、コサインが指定された数値式である角度をラジアンで返す方法について学習する
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 03/03/2020
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: 733d6b009f03d61c37170cc506a3b2ec842d7c47
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "78300963"
---
# <a name="acos-azure-cosmos-db"></a>ACOS (Azure Cosmos DB)
 コサインが指定された数値式となる角度をラジアン単位で返します。アークコサインとも呼ばれます。  
  
## <a name="syntax"></a>構文
  
```sql
ACOS(<numeric_expr>)  
```  
  
## <a name="arguments"></a>引数
  
*numeric_expr*  
   数値式です。  
  
## <a name="return-types"></a>戻り値の型
  
  数値式を返します。  
  
## <a name="examples"></a>例
  
  次の例では、-1 の `ACOS` を返します。  
  
```sql
SELECT ACOS(-1) AS acos 
```  
  
 結果セットは次のようになります。  
  
```json
[{"acos": 3.1415926535897931}]  
```  

## <a name="remarks"></a>解説

このシステム関数では、インデックスは使用されません。

## <a name="next-steps"></a>次のステップ

- [Azure Cosmos DB の数学関数](sql-query-mathematical-functions.md)
- [Azure Cosmos DB のシステム関数](sql-query-system-functions.md)
- [Azure Cosmos DB の概要](introduction.md)
