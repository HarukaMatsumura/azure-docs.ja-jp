---
title: Azure セキュリティ コントロール - データの復旧
description: Azure セキュリティ コントロール データの復旧
author: msmbaldwin
ms.service: security
ms.topic: conceptual
ms.date: 04/14/2020
ms.author: mbaldwin
ms.custom: security-benchmark
ms.openlocfilehash: 4f3e8540902809f951a441aa2fe8d00026c44d82
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "81408590"
---
# <a name="security-control-data-recovery"></a>セキュリティ コントロールデータの復旧

定期的にすべてのシステム データ、構成、およびシークレットが自動的にバックアップされていることを確認します。

## <a name="91-ensure-regular-automated-back-ups"></a>9.1:定期的に自動バックアップを行う

| Azure ID | CIS IDs | 担当 |
|--|--|--|
| 9.1 | 10.1 | Customer |

Azure Backup を有効にし、バックアップ ソース (Azure VM、SQL Server、またはファイル共有)、および必要な頻度と保持期間を構成します。

- [Azure Backup を有効にする方法](https://docs.microsoft.com/azure/backup/)

## <a name="92-perform-complete-system-backups-and-backup-any-customer-managed-keys"></a>9.2: システムの完全バックアップを実行し、カスタマー マネージド キーをバックアップする

| Azure ID | CIS IDs | 担当 |
|--|--|--|
| 9.2 | 10.2 | Customer |

Azure Backup を有効にし、ターゲット VM および必要な頻度と保持期間を設定します。 Azure Key Vault 内のカスタマー マネージド キーをバックアップします。

- [Azure Backup を有効にする方法](https://docs.microsoft.com/azure/backup/)

- [Azure 上でキー コンテナーのキーをバックアップする方法](https://docs.microsoft.com/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-6.13.0)

## <a name="93-validate-all-backups-including-customer-managed-keys"></a>9.3:カスタマー マネージド キーを含むすべてのバックアップを検証する

| Azure ID | CIS IDs | 担当 |
|--|--|--|
| 9.3 | 10.3 | Customer |

Azure Backup 内でコンテンツのデータ復元を定期的に実行できるようにします。 バックアップされたカスタマー マネージド キーの復元をテストします。

- [Azure 仮想マシンのバックアップからファイルを復旧する方法](https://docs.microsoft.com/azure/backup/backup-azure-restore-files-from-vm)

- [Azure でキー コンテナーのキーを復元する方法](https://docs.microsoft.com/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-6.13.0)

## <a name="94-ensure-protection-of-backups-and-customer-managed-keys"></a>9.4: バックアップとカスタマー マネージド キーの保護を確保する

| Azure ID | CIS IDs | 担当 |
|--|--|--|
| 9.4 | 10.4 | Customer |

オンプレミスのバックアップでは、Azure にバックアップする際に指定するパスフレーズを使用して保存時の暗号化が行われます。 Azure VM の場合、データは Storage Service Encryption (SSE) を使用して暗号化された上で保存されます。 ロールベースのアクセス制御を使用して、バックアップとカスタマー マネージド キーを保護します。  

Key Vault で論理的な削除と消去保護を有効にして、偶発的または悪意のある削除からキーを保護します。  Azure Storage を使用してバックアップを格納した場合、BLOB または BLOB のスナップショットが削除されたときに、論理的な削除機能でデータを保存および復旧することができます。 

- [Azure RBAC について](https://docs.microsoft.com/azure/role-based-access-control/overview)

- [Key Vault で論理的な削除と消去保護を有効にする方法](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal)

- [Azure Storage Blob の論理的な削除](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal)


## <a name="next-steps"></a>次のステップ

- 次のセキュリティ コントロールを参照してください。[インシデント対応](security-control-incident-response.md)