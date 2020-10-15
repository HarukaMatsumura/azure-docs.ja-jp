---
title: NSG で RDP ポートが有効になっていないため、Azure VM に接続できない | Microsoft Docs
description: Azure portal での NSG の構成のために RDP が失敗する問題をトラブルシューティングする方法について説明します | Microsoft Docs
services: virtual-machines-windows
documentationCenter: ''
author: genlin
manager: dcscontentpm
editor: v-jesits
ms.service: virtual-machines-windows
ms.topic: troubleshooting
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 11/20/2018
ms.author: genli
ms.openlocfilehash: 878e2c233f2171c3c9a6fbd2a8d629d3f3987c3a
ms.sourcegitcommit: d103a93e7ef2dde1298f04e307920378a87e982a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91976727"
---
#  <a name="cannot-connect-remotely-to-a-vm-because-rdp-port-is-not-enabled-in-nsg"></a>NSG で RDP ポートが有効ではないために VM にリモート接続できない

この記事では、リモート デスクトップ プロトコル (RDP) のポートがネットワーク セキュリティ グループ (NSG) で有効になっていないために、Azure Windows 仮想マシン (VM) に接続できない問題を解決する方法について説明します。


## <a name="symptom"></a>症状

RDP ポートがネットワーク セキュリティ グループで開かれていないために、Azure 内の VM に RDP 接続できません。

## <a name="solution"></a>解決策 

新しい VM を作成すると、インターネットからのすべてのトラフィックが既定でブロックされます。 

NSG で RDP ポートを有効にするには、次の手順のようにします。
1. [Azure ポータル](https://portal.azure.com)にサインインします。
2. **[仮想マシン]** で、問題のある VM を選択します。 
3. **[設定]** の **[ネットワーク]** を選択します。 
4. **[受信ポートの規則]** で、RDP のポートが正しく設定されていることを確認します。 構成の例を次に示します。 

    **[優先度]** :該当なし </br>
    **Name**:Port_3389 </br>
    **ポート (宛先)** :3389 </br>
    **プロトコル**:TCP </br>
    **ソース**:Any </br>
    **宛先**:Any </br>
    **アクション**:Allow </br>

ソース IP アドレスを指定した場合、この設定では、特定の IP アドレスまたは IP アドレス範囲からのトラフィックのみが VM への接続を許可されます。 RDP セッションを開始するために使用しているコンピューターが範囲内にあることを確認します。

NSG の詳細については、[ネットワーク セキュリティ グループ](../../virtual-network/network-security-groups-overview.md)に関するページを参照してください。

> [!NOTE]
> RDP ポート 3389 がインターネットに公開されます。 そのため、このポートはテストのみに使用することをお勧めします。 運用環境では、VPN またはプライベート接続を使用することをお勧めします。

## <a name="next-steps"></a>次のステップ

RDP ポートが NSG で既に有効になっている場合は、「[Azure VM での RDP 一般エラーのトラブルシューティング](./troubleshoot-rdp-general-error.md)」をご覧ください。