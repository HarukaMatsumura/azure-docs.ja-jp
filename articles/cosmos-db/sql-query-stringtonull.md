---
title: Azure Cosmos DB クエリ言語の StringToNull
description: Azure Cosmos DB の SQL システム関数 StringToNull について説明します。
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 03/03/2020
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: 7e17547f88465103b61eabec04978ea806ffa2c9
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "78296441"
---
# <a name="stringtonull-azure-cosmos-db"></a>StringToNull (Azure Cosmos DB)
 null 値に変換された式を返します。 式を変換できない場合は、undefined を返します。  
  
## <a name="syntax"></a>構文
  
```sql
StringToNull(<str_expr>)  
```  
  
## <a name="arguments"></a>引数
  
*str_expr*  
   null 式として解析される文字列式です。
  
## <a name="return-types"></a>戻り値の型
  
  null 式または undefined を返します。  
  
## <a name="examples"></a>例
  
  次の例は、異なる型間で `StringToNull` がどのように動作するかを示します。 

有効な入力を使用した例を次に示します。

 空白は "null" の前後のみで使用できます。

```sql
SELECT 
    StringToNull("null") AS n1, 
    StringToNull("  null ") AS n2,
    IS_NULL(StringToNull("null   ")) AS n3
```  
  
 結果セットは次のようになります。  
  
```json
[{"n1": null, "n2": null, "n3": true}]
```  

無効な入力を使用した例を次に示します。

null 値では大文字と小文字が区別されるので、すべて小文字で記述する必要があります (つまり、"null")。

```sql
SELECT    
    StringToNull("NULL"),
    StringToNull("Null")
```  
  
 結果セットは次のようになります。  
  
```json
[{}]
```  

渡された式は null 式として解析されます。これらの入力は null 型として評価されないため、undefined が返されます。

```sql
SELECT    
    StringToNull("true"), 
    StringToNull(false), 
    StringToNull(undefined),
    StringToNull(NaN) 
```  
  
 結果セットは次のようになります。  
  
```json
[{}]
```  

## <a name="remarks"></a>解説

このシステム関数では、インデックスは使用されません。

## <a name="next-steps"></a>次のステップ

- [Azure Cosmos DB の文字列関数](sql-query-string-functions.md)
- [Azure Cosmos DB のシステム関数](sql-query-system-functions.md)
- [Azure Cosmos DB の概要](introduction.md)
