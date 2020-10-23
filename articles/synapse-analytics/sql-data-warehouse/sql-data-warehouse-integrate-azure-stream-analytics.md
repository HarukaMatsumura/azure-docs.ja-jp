---
title: Azure Stream Analytics の使用
description: リアルタイム ソリューション開発のための、Azure Synapse での Azure Stream Analytics のデータ ウェアハウスとの使用に関するヒント。
services: synapse-analytics
author: kevinvngo
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 9/25/2020
ms.author: kevin
ms.reviewer: igorstan
ms.custom: azure-synapse
ms.openlocfilehash: 60fb258fe2c6063b9b9a3ced0f4ba5f71ffd9d7c
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91449497"
---
# <a name="use-azure-stream-analytics-with-azure-synapse-analytics"></a>Azure Synapse Analytics での Azure Stream Analytics の使用

Azure Stream Analytics は、待機時間の短縮、高可用性、クラウド内のデータのストリーミング データに対する拡張性の高い複雑なイベント処理を実現する、フル マネージドのサービスです。 基本事項については、「 [Azure Stream Analytics の概要](../../stream-analytics/stream-analytics-introduction.md?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json)」をお読みください。 その後で、「 [Azure Stream Analytics の使用](../../stream-analytics/stream-analytics-real-time-fraud-detection.md?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json) 」チュートリアルに従って、Stream Analytics を使用してエンド ツー エンド ソリューションを作成する方法を知ることができます。

この記事では、データウェア ハウスを出力シンクとして使用して、Azure Stream Analytics ジョブを使用した高スループットのデータ インジェストを行う方法について説明します。

## <a name="prerequisites"></a>前提条件

* Azure Stream Analytics ジョブ - Azure Stream Analytics ジョブを作成するには、「 [Azure Stream Analytics の使用](../../stream-analytics/stream-analytics-real-time-fraud-detection.md?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json) 」チュートリアルの手順に従ってください。  

    1. Event Hub 入力の作成
    2. イベント ジェネレーター アプリケーションの構成と起動
    3. Stream Analytics のジョブの準備
    4. ジョブの入力とクエリの指定
* データ ウェアハウスの Azure Synapse SQL プール - 新しいデータ ウェアハウスを作成するには、「[新しいデータ ウェアハウス作成クイックスタート](create-data-warehouse-portal.md)」の手順に従ってください。

## <a name="specify-streaming-output-to-point-to-your-data-warehouse"></a>データ ウェアハウスを指すストリーミング出力の指定

### <a name="step-1"></a>手順 1

Azure portal から Stream Analytics ジョブにアクセスし、**ジョブ トポロジ** メニューの **出力** をクリックします。

### <a name="step-2"></a>手順 2.

**[追加]** ボタンをクリックし、ドロップ ダウンメニューから **[Azure Synapse Analytics]** を選択します。

![Azure Synapse Analytics を選択します](./media/sql-data-warehouse-integrate-azure-stream-analytics/sql-pool-azure-stream-analytics-output.png)

### <a name="step-3"></a>手順 3.

次の値を入力します。

* *[出力のエイリアス]* :このジョブの出力のフレンドリ名を入力します。
* *サブスクリプション*:
  * データ ウェアハウスが Stream Analytics ジョブと同じサブスクリプション内にある場合は、***[サブスクリプションから Azure Synapse Analytics を選択]*** をクリックします。
  * データ ウェアハウスが別のサブスクリプションにある場合は、[Azure Synapse Analytics 設定を手動で行う] をクリックします。
* *データベース*:次に、ドロップ ダウン リストから同期先にデータベースを選択します。
* *User Name*:データベースの書き込みアクセス許可を持つアカウントのユーザー名を指定します。
* *パスワード*:指定したユーザー アカウントのパスワードを入力します。
* *テーブル*:データベース内の対象テーブルの名前を指定します。
* **保存** ボタンをクリックします。

![すべて入力されている Azure Synapse Analytics フォーム](./media/sql-data-warehouse-integrate-azure-stream-analytics/sql-pool-azure-stream-analytics-output-db-settings.png)

### <a name="step-4"></a>手順 4.

テストを実行する前に、データ ウェアハウスに表を作成する必要があります。  SQL Server Management Studio (SSMS) または任意のクエリ ツールを使用して、次の表作成スクリプトを実行します。

```sql
CREATE TABLE SensorLog
(
    RecordType VARCHAR(2)
    , SystemIdentity VARCHAR(2)
    , FileNum INT
    , SwitchNum VARCHAR(50)
    , CallingNum VARCHAR(25)
    , CallingIMSI VARCHAR(25)
    , CalledNum VARCHAR(25)
    , CalledIMSI VARCHAR(25)
    , DateS VARCHAR(25)
    , TimeS VARCHAR(25)
    , TimeType INT
    , CallPeriod INT
    , CallingCellID VARCHAR(25)
    , CalledCellID VARCHAR(25)
    , ServiceType VARCHAR(25)
    , [Transfer] INT
    , IncomingTrunk VARCHAR(25)
    , OutgoingTrunk VARCHAR(25)
    , MSRN VARCHAR(25)
    , CalledNum2 VARCHAR(25)
    , FCIFlag VARCHAR(25)
    , callrecTime VARCHAR(50)
    , EventProcessedUtcTime VARCHAR(50)
    , PartitionId int
    , EventEnqueuedUtcTime VARCHAR(50)
    )
WITH (DISTRIBUTION = ROUND_ROBIN)
```

### <a name="step-5"></a>手順 5.

Azure Portal の Stream Analytics ジョブで、ジョブ名をクリックします。  ***出力の詳細*** ペインで ***テスト*** ボタンをクリックします。

![出力の詳細上の [テスト] ボタン](./media/sql-data-warehouse-integrate-azure-stream-analytics/sqlpool-asatest.png) データベースへの接続が成功すると、ポータルに通知が表示されます。

### <a name="step-6"></a>手順 6.

***ジョブ トポロジ*** の下にある ***クエリ*** メニューをクリックし、クエリを変更して、作成したストリーム出力にデータを挿入します。  クエリをテストするには ***選択したクエリのテスト*** をクリックします。  クエリ テストが成功した場合は ***クエリの保存*** ボタンをクリックします。

![クエリを保存する](./media/sql-data-warehouse-integrate-azure-stream-analytics/sqlpool-asaquery.png)

### <a name="step-7"></a>手順 7.

Azure Stream Analytics ジョブを開始します。  ***概要*** メニューの ***開始*** ボタンをクリックします。

![Stream Analytics ジョブを開始する](./media/sql-data-warehouse-integrate-azure-stream-analytics/sqlpool-asastart.png)

[ジョブの開始] ウィンドウの ***[開始]*** ボタンをクリックします。

![[開始] をクリックする](./media/sql-data-warehouse-integrate-azure-stream-analytics/sqlpool-asastartconfirm.png)

## <a name="next-steps"></a>次のステップ

統合の概要については、[その他のサービスの統合](sql-data-warehouse-overview-integrate.md)に関する記事を参照してください。
開発に関するその他のヒントについては、[データ ウェアハウスの設計上の決定とコーディング技法](sql-data-warehouse-overview-develop.md)に関する記事を参照してください。
