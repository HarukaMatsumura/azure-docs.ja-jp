---
title: 'クイックスタート: Microsoft ID プラットフォーム アプリ アカウントの変更 | Azure'
description: このクイック スタートでは、Microsoft ID プラットフォームに登録されているアプリケーションの構成を通じて、アプリケーションにアクセスできるユーザー (アカウント) を変更できます。
services: active-directory
author: rwike77
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 05/08/2019
ms.author: ryanwi
ms.custom: aaddev
ms.reviewer: aragra, lenalepa, sureshja
ms.openlocfilehash: d143bde9c22bc726f00b5c209d1b7fbc131905b0
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "91258015"
---
# <a name="quickstart-modify-the-accounts-supported-by-an-application"></a>クイック スタート:アプリケーションによってサポートされるアカウントを変更する

Microsoft ID プラットフォームにアプリケーションを登録する際、自分が所属する組織のユーザーだけがそのアプリケーションにアクセスできるようにしたい場合があります。 反対に、外部組織のユーザーや、組織に所属していないユーザー (個人用アカウント) に、アプリケーションへのアクセスを許可したい場合もあるでしょう。

このクイック スタートでは、アプリケーションにアクセスできるユーザー (アカウント) を、その構成を通じて変更する方法について説明します。

## <a name="prerequisites"></a>前提条件

* 次の項目の完了: 「[クイックスタート: Microsoft ID プラットフォームにアプリケーションを登録する](quickstart-register-app.md)

## <a name="sign-in-to-the-azure-portal-and-select-the-app"></a>Azure portal にサインインしてアプリを選択する

アプリを構成する前に、次の手順を実行します。

1. 職場または学校アカウントか、個人の Microsoft アカウントを使用して、[Azure portal](https://portal.azure.com) にサインインします。
1. ご利用のアカウントで複数のテナントにアクセスできる場合は、右上隅でアカウントを選択し、ポータルのセッションを目的の Azure AD テナントに設定します。
1. 左側のナビゲーション ウィンドウで、 **[Azure Active Directory]** サービスを選択し、 **[アプリの登録]** を選択します。
1. 構成するアプリケーションを探して選択します。 アプリを選択すると、アプリケーションの **[概要]** またはメイン登録ページが表示されます。
1. [異なるアカウントをサポートするようにアプリケーションの登録を変更する](#change-the-application-registration-to-support-different-accounts)ための手順に従います。
1. シングルページ アプリケーションの場合は、[OAuth 2.0 の暗黙的な許可を有効](#enable-oauth-20-implicit-grant-for-single-page-applications)にします。

## <a name="change-the-application-registration-to-support-different-accounts"></a>異なるアカウントをサポートするようにアプリケーションの登録を変更する

組織の外部の顧客やパートナーが利用できるアプリケーションを作成する場合には、Azure Portal でアプリケーションの定義を更新する必要があります。

> [!IMPORTANT]
> Azure AD では、マルチテナント アプリケーションのアプリケーション ID URI がグローバルで一意になっている必要があります。 アプリ ID URI は、プロトコル メッセージでアプリケーションを識別する手段の 1 つです。 シングル テナント アプリケーションの場合、アプリ ID URI はそのテナント内で一意であれば十分です。 これに対してマルチテナント アプリケーションの場合、Azure AD が全テナントから該当するアプリケーションを特定できるように、アプリ ID URI がグローバルで一意になっている必要があります。 グローバルな一意性を確保するため、アプリ ID URI には Azure AD テナントの検証済みドメインと一致するホスト名が含まれていなければならないという条件が存在します。 たとえば、テナントの名前が contoso.onmicrosoft.com の場合、有効なアプリ ID URI は `https://contoso.onmicrosoft.com/myapp` のようになります。 また、テナントの検証済みドメインが contoso.com の場合、有効なアプリ ID URI は `https://contoso.com/myapp` のようになります。 アプリ ID URI がこのパターンに従っていないと、アプリケーションのマルチテナントとしての設定が失敗します。

### <a name="to-change-who-can-access-your-application"></a>アプリケーションにアクセスできるユーザーを変更する

1. アプリの **[概要]** ページから **[認証]** セクションを選択し、 **[サポートされているアカウントの種類]** に選択されている値を変更します。
    * 基幹業務 (LOB) アプリケーションを作成している場合は、 **[このディレクトリ内のアカウントのみ]** を選択します。 アプリケーションがディレクトリに登録されていない場合、このオプションは選択できません。
    * 企業および教育機関のすべてのユーザーを対象とする場合は、 **[任意の組織のディレクトリ内のアカウント]** を選択します。
    * 最も広範なユーザーを対象にしたければ、 **[任意の組織のディレクトリ内のアカウントと、個人用の Microsoft アカウント]** を選択します。
1. **[保存]** を選択します。

## <a name="enable-oauth-20-implicit-grant-for-single-page-applications"></a>シングル ページ アプリケーションで OAuth 2.0 の暗黙的な許可を有効にする

シングル ページ アプリケーション (SPA) は、ブラウザー上で実行される JavaScript ヘビーなフロント エンドを使用して通常構成されています。これがアプリケーションの Web API バックエンドを呼び出してビジネス ロジックを実行します。 Azure AD でホストされている SPA では、Azure AD によるユーザー認証と、アプリケーションの JavaScript クライアントによるバックエンド Web API の呼び出しを保護するためのトークンの取得に、OAuth 2.0 Implicit Grant を使用します。

この認証プロトコルはほかにも、ユーザーが同意した後、クライアントとアプリケーション用に構成されている他の Web API リソースとの間に発生する呼び出しを保護するトークンを取得するときにも利用できます。 暗黙的な認可付与の詳細と、それが自身のアプリケーションのシナリオに適しているかどうかの判断に役立つ情報は、Azure AD [v1.0](../azuread-dev/v1-oauth2-implicit-grant-flow.md) および [v2.0](v2-oauth2-implicit-grant-flow.md) における OAuth 2.0 の暗黙的な許可フローを参照してください。

既定では、アプリケーションに対して OAuth 2.0 の暗黙的な許可が無効になっています。 実際のアプリケーションで OAuth 2.0 の暗黙的な許可を有効にするには、以下の手順に従ってください。

### <a name="to-enable-oauth-20-implicit-grant"></a>OAuth 2.0 Implicit Grant を有効にするには

1. 左側のナビゲーション ウィンドウで、 **[Azure Active Directory]** サービスを選択し、 **[アプリの登録]** を選択します。
1. 構成するアプリケーションを探して選択します。 アプリを選択すると、アプリケーションの **[概要]** またはメイン登録ページが表示されます。
1. アプリの **[概要]** ページで、 **[認証]** セクションを選択します。
1. **[詳細設定]** の **[暗黙的な許可]** セクションを探します。
1. **[ID トークン]** と **[アクセス トークン]** の両方またはどちらか一方を選択します。
1. **[保存]** を選択します。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリケーションのブランド化ガイドライン](howto-add-branding-in-azure-ad-apps.md)
