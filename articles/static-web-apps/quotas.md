---
title: Azure Static Web Apps のプレビューのクォータ
description: Azure Static Web Apps のプレビューに関連付けられているクォータについて説明します
services: static-web-apps
author: craigshoemaker
ms.service: static-web-apps
ms.topic: overview
ms.date: 05/08/2020
ms.author: cshoe
ms.openlocfilehash: 915f8675ffda0d70347905d11c7d93975b9d4526
ms.sourcegitcommit: 33368ca1684106cb0e215e3280b828b54f7e73e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92132739"
---
# <a name="quotas-in-azure-static-web-apps-preview"></a>Azure Static Web Apps のプレビューのクォータ

Azure Static Web Apps のプレビューには、次のクォータがあります。

> [!IMPORTANT]
> Azure Static Web Apps はパブリック プレビュー段階であり、運用環境での使用は想定されていません。

| 機能                     | Free プラン        |
|-----------------------------|------------------|
| 含まれる帯域幅          | 100 GB/月 |
| 超過帯域幅           | 使用不可      |
| Azure サブスクリプションあたりのアプリ数 | 10               |
| アプリのサイズ                    | 250 MB           |
| 実稼働前の環境数 | 1                |
| カスタム ドメイン              | 1                |
| 承認<br><br>カスタム ロールとルーティング規則を使用 | 招待されてロールを割り当てられるエンドユーザーの最大数は 25 人 |
| Azure Functions             | 利用可能        |
| SLA                         | なし             |

## <a name="github-storage"></a>GitHub ストレージ

GitHub Actions とパッケージでは、独自のクォータ セットを持つ GitHub ストレージが使用されます。 Azure Static Web Apps サイトを作成すると、デプロイ後でも GitHub によってサイトのアーティファクトが格納されます。

詳細については、次のリソースを参照してください。

- [Actions ストレージ領域の管理](https://github.community/t5/GitHub-Actions/Managing-Actions-storage-space/td-p/38944)
- [GitHub Actions の課金について](https://help.github.com/github/setting-up-and-managing-billing-and-payments-on-github/about-billing-for-github-actions#about-billing-for-github-actions)
- [GitHub Actions の使用制限の管理](https://help.github.com/github/setting-up-and-managing-billing-and-payments-on-github/managing-your-spending-limit-for-github-actions)

## <a name="next-steps"></a>次のステップ

- [概要](overview.md)
