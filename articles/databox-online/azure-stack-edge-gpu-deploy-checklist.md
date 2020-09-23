---
title: Azure Stack Edge Pro GPU デバイスを配置するための配置前チェックリスト | Microsoft Docs
description: この記事では、Azure Stack Edge Pro GPU デバイスを配置する前に収集できる情報について説明します。
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: article
ms.date: 08/31/2020
ms.author: alkohli
ms.openlocfilehash: 82751ea821bb1edfea5dfb353cbb3cdc51fe59d3
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90903004"
---
# <a name="deployment-checklist-for-your-azure-stack-edge-pro-gpu-device"></a>Azure Stack Edge Pro GPU デバイスのデプロイ チェックリスト  

この記事では、Azure Stack Edge Pro デバイスを実際にデプロイする前に収集できる情報について説明します。 

次のチェックリストを使用して、Azure Stack Edge Pro デバイスを注文した後、デバイスを受け取る前にこの情報を確実に入手してください。 

## <a name="deployment-checklist"></a>展開のチェックリスト 

| 段階                             | パラメーター                                                                                                                                                                                                                           | 詳細                                                                                                           |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| デバイスの管理               | <li>Microsoft Azure のサブスクリプション</li><li>Azure Active Directory Graph API</li><li>Microsoft Azure Storage アカウント</li>|<li>Azure Stack Edge Pro および Data Box Gateway について共同作成者アクセス許可が有効であること</li><li>管理者またはユーザーのアクセス権を確保します</li><li>アクセスの資格情報が必要</li> |
| デバイスのインストール               | パッケージ内の電源ケーブル。 <br>米国の場合、定格 125 V、15 アンペアの SVE 18/3 ケーブルと NEMA 5-15P to C13 (入力から出力) コネクタが付属しています。                                                                                                                                                                                                          | デバイスに付属しています。<br>詳細については、[国別のサポートされている電源コード](azure-stack-edge-technical-specifications-power-cords-regional.md)の一覧を参照してください。                                                                                        |
|                                   | <li>ポート 1 用の少なくとも 1 本の 1 GbE RJ-45 ネットワーク ケーブル  </li><li> ポート 3、ポート 4、ポート 5、またはポート 6 用の少なくとも 1 本の 25 GbE SFP+ 銅線ケーブル</li>| これらのケーブルはお客様が調達する必要があります。<br>デバイス ネットワーク カードでサポートされているネットワーク ケーブル、スイッチ、トランシーバーの詳細な一覧については、[Cavium FastlinQ 41000 シリーズの相互運用性マトリックス](https://www.marvell.com/documents/xalflardzafh32cfvi0z/)および [Mellanox デュアル ポート 25G ConnectX-4 チャネル ネットワーク アダプター互換製品](https://docs.mellanox.com/display/ConnectX4LxFirmwarev14271016/Firmware+Compatible+Products)に関するドキュメントを参照してください。| 
| 初回のデバイス接続      | ポート 1 には、初回接続用の固定 IP (192.168.100.10/24) があります。 <li>ポート 1 に直接接続するには、192.168.100.0/24 ネットワークの IP アドレスを使用するラップトップが必要です。</li><li> 詳細な構成を行うには、デバイスのローカル UI (`https://192.168.100.10`) を使用します。</li><li> 初期設定が完了したら、デバイスに 1 GbE 以上のスイッチを使用する必要があります。 接続されたスイッチが 1 GbE 以上でない場合、ローカル Web UI にアクセスできません。</li>|                                                                                                                   |
| デバイスのログオン                      | デバイスの管理者パスワードの長さは、8 から 16 文字です。 <br>さらに、大文字、小文字、数字、および特殊文字のうちの 3 種類の文字を含める必要があります。                                            | 既定のパスワードは *Password1* であり、最初のサインイン時に有効期限が切れます。                                                     |
| ネットワークの設定                  | デバイスには、2 x 1 GbE、4 x 25 GbE ネットワーク ポートが付属しています。 <li>ポート 1 は、管理設定の構成にのみ使用されます。 1 つ以上のデータ ポートを接続して構成できます。 </li><li> 少なくとも 1 つのデータ ネットワーク インターフェイス (ポート 2 からポート 6) がインターネットに接続されている必要があります (Azure への接続が可能なもの)。</li><li> IP 設定によって、DHCP または静的 IPv4 構成がサポートされます。 | 静的 IPv4 構成には、IP、DNS サーバーと既定のゲートウェイが必要です。                                                                                                                  |
| ネットワーク設定を計算する     | <li>コンピューティング モジュールにアクセスするには、Kubernetes ノード用に 2 つの静的パブリック IP、Azure Stack Edge Pro Hub サービス用に少なくとも 1 つの静的 IP が必要です。</li><li>Kubernetes クラスターの外部から外部にアクセスする必要がある追加のサービスまたはコンテナーごとに 1 つの IP が必要です。</li>                                                                                                                       | 静的 IPv4 構成のみがサポートされています。                                                                      |
| (省略可能) Web プロキシ設定     | <li>Web プロキシ サーバーの IP または FQDN、ポート </li><li>Web プロキシのユーザー名、パスワード</li>                                                                                                                                                                                                    | 現在、コンピューティング設定ではサポートされていません。                                                                     |
| ファイアウォールとポートの設定        | デバイスの IP で許可されるように、[一覧にある URL パターンとポート](azure-stack-edge-system-requirements.md#networking-port-requirements)を使用します。                                                                                                                                                  |                                                                                                                   |
| (省略可能) MAC アドレス            | MAC アドレスをホワイトリストに登録する必要がある場合は、デバイスのローカル UI から接続されたポートのアドレスを取得します。 |                                                                                                                   |
| (省略可能) ネットワーク スイッチ ポート    | デバイスでは、コンピューティングのために Hyper-V VM をホストしています。 一部のネットワーク スイッチ ポート構成は、既定ではこのような設定に対応していません。                                                                                                        |                                                                                                                   |
| (推奨) 時間設定       | タイム ゾーン、プライマリ NTP サーバー、セカンダリ NTP サーバーを構成します。                                                                                                                                                                    | ローカル ネットワークでプライマリおよびセカンダリ NTP サーバーを構成します。<br>ローカル サーバーを使用できない場合は、パブリック NTP サーバーを構成できます。                                                    |
| (省略可能) サーバー設定を更新する | <li>ローカル ネットワーク上の更新サーバーの IP アドレス、WSUS サーバーへのパスが必要です。 </li> | 既定では、パブリック Windows 更新サーバーが使用されます。|
| デバイスの設定                   | <li>DNS 組織内に登録されているデバイス名 </li><li>DNS ドメイン</li> |                                                                                                                   |
| (省略可能) 証明書                      | デバイスによって生成された証明書を使用する <br><br> 独自の証明書を持ち込む場合は、以下が必要です。 <li>*.cer* の拡張子が付いた DER 形式の信頼されたルート署名証明書 </li><li>*pfx* 形式のエンドポイント証明書</li>|エンドポイント証明書には、Azure Resource Manager、BLOB ストレージ、ローカル Web UI が含まれます。                                                                                                                   |
| アクティベーション                        | Azure Stack Edge Pro および Data Box Gateway リソースのアクティブ化キーが必要です。                                                                                                                                                       | 生成されたキーは 3 日後に有効期限が切れます。                                                                        |


## <a name="next-steps"></a>次のステップ

[Azure Stack Edge Pro デバイス](azure-stack-edge-gpu-deploy-prep.md)のデプロイを準備します。



