---
title: Azure Service Fabric Mesh 用に Visual Studio を最適化する
description: この記事では、Visual Studio のパフォーマンスを Service Fabric Mesh 用に最適化して、初回のデバッグ実行 (F5) を大幅に高速化する方法について説明します。
author: georgewallace
ms.author: gwallace
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: aa7a959128d3bcdfcce67d3abeac245975339a9f
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91840304"
---
# <a name="optimize-visual-studio-performance-for-service-fabric-mesh-projects"></a>Visual Studio のパフォーマンスを Service Fabric Mesh プロジェクト用に最適化する

この記事では、Visual Studio のパフォーマンスを Service Fabric Mesh 用に最適化して、初回のデバッグ実行 (F5) を大幅に高速化する方法について説明します。  

## <a name="change-visual-studio-settings"></a>Visual Studio の設定を変更する
 
Visual Studio では、 **[ツール]**  >  **[オプション]**   >  **[Service Fabric Mesh Tools]\(Service Fabric Mesh ツール\)**  >  **[全般]** から、次の設定を調整することができます。

- **[プロジェクトを開く際に必要な Docker イメージをプルします]** : プロジェクトの読み込み中にイメージのダウンロードを開始することで、初回のデバッグ実行 (F5) を高速化します。  
- **[Deploy application on project open]\(プロジェクトを開く際にアプリケーションをデプロイします\)** : プロジェクトを開いたときにデプロイ プロセスを開始することで、初回のデバッグ実行 (F5) を高速化します。  
- **[Remove application on project close]\(プロジェクトを閉じたときにアプリケーションを削除します\)** : プロジェクトを閉じたときに Mesh アプリを削除することで、アプリに割り当てられたリソース (CPU、RAM) を解放します。  

Service Fabric Tools の出力ウィンドウに、Visual Studio が "イメージをプルしている"、"ウォーム アップしている"、または "アプリケーションを削除している" というメッセージが表示される場合は、上記の設定が参照されています。 これらの設定は無効にすることもできます。

## <a name="next-steps"></a>次のステップ

[Mesh アプリのデバッグに関するチュートリアル](service-fabric-mesh-tutorial-debug-service-fabric-mesh-app.md)を読んでください