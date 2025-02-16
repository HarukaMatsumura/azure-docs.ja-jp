---
title: チュートリアル:Azure Active Directory シングル サインオン (SSO) と Spotinst の統合 | Microsoft Docs
description: Azure Active Directory と Spotinst の間でシングル サインオンを構成する方法について説明します。
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 06/10/2021
ms.author: jeedes
ms.openlocfilehash: b463cbcdef8d255599cea743dccf1237b42477e2
ms.sourcegitcommit: 677e8acc9a2e8b842e4aef4472599f9264e989e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2021
ms.locfileid: "132333297"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-spotinst"></a>チュートリアル:Azure Active Directory シングル サインオン (SSO) と Spotinst の統合

このチュートリアルでは、Spotinst と Azure Active Directory (Azure AD) を統合する方法について説明します。 Spotinst を Azure AD と統合すると、次のことができます。

* Spotinst にアクセスできるユーザーを Azure AD で制御できます。
* ユーザーが自分の Azure AD アカウントを使用して Spotinst に自動的にサインインできるように設定できます。
* 1 つの中央サイト (Azure Portal) で自分のアカウントを管理します。

## <a name="prerequisites"></a>前提条件

開始するには、次が必要です。

* Azure AD サブスクリプション。 サブスクリプションがない場合は、[無料アカウント](https://azure.microsoft.com/free/)を取得できます。
* Spotinst のシングル サインオン (SSO) が有効なサブスクリプション。

## <a name="scenario-description"></a>シナリオの説明

このチュートリアルでは、テスト環境で Azure AD の SSO を構成してテストします。

* Spotinst では、**SP Initiated SSO と IDP Initiated SSO** がサポートされます。

> [!NOTE]
> このアプリケーションの識別子は固定文字列値であるため、1 つのテナントで構成できるインスタンスは 1 つだけです。

## <a name="add-spotinst-from-the-gallery"></a>ギャラリーからの Spotinst の追加

Azure AD への Spotinst の統合を構成するには、ギャラリーからマネージド SaaS アプリの一覧に Spotinst を追加する必要があります。

1. 職場または学校アカウントか、個人の Microsoft アカウントを使用して、Azure portal にサインインします。
1. 左のナビゲーション ウィンドウで **[Azure Active Directory]** サービスを選択します。
1. **[エンタープライズ アプリケーション]** に移動し、 **[すべてのアプリケーション]** を選択します。
1. 新しいアプリケーションを追加するには、 **[新しいアプリケーション]** を選択します。
1. **[ギャラリーから追加する]** セクションで、検索ボックスに「**Spotinst**」と入力します。
1. [結果] パネルから **[Spotinst]** を選択し、アプリを追加します。 お使いのテナントにアプリが追加されるのを数秒待機します。

## <a name="configure-and-test-azure-ad-sso-for-spotinst"></a>Spotinst の Azure AD SSO の構成とテスト

**B.Simon** というテスト ユーザーを使用して、Spotinst に対する Azure AD SSO を構成してテストします。 SSO を機能させるためには、Azure AD ユーザーと Spotinst の関連ユーザーとの間にリンク関係を確立する必要があります。

Spotinst に対して Azure AD SSO を構成してテストするには、次の手順を行います。

1. **[Azure AD SSO の構成](#configure-azure-ad-sso)** - ユーザーがこの機能を使用できるようにします。
    1. **[Azure AD のテスト ユーザーの作成](#create-an-azure-ad-test-user)** - B.Simon で Azure AD のシングル サインオンをテストします。
    1. **[Azure AD テスト ユーザーの割り当て](#assign-the-azure-ad-test-user)** - B.Simon が Azure AD シングル サインオンを使用できるようにします。
1. **[Spotinst の SSO の構成](#configure-spotinst-sso)** - アプリケーション側でシングル サインオン設定を構成します。
    1. **[Spotinst のテスト ユーザーの作成](#create-spotinst-test-user)** - Spotinst で B.Simon に対応するユーザーを作成し、Azure AD のこのユーザーにリンクさせます。
1. **[SSO のテスト](#test-sso)** - 構成が機能するかどうかを確認します。

## <a name="configure-azure-ad-sso"></a>Azure AD SSO の構成

これらの手順に従って、Azure portal で Azure AD SSO を有効にします。

1. Azure portal の **Spotinst** アプリケーション統合ページで、 **[管理]** セクションを見つけて、 **[シングル サインオン]** を選択します。
1. **[シングル サインオン方式の選択]** ページで、 **[SAML]** を選択します。
1. **[SAML によるシングル サインオンのセットアップ]** ページで、 **[基本的な SAML 構成]** の鉛筆アイコンをクリックして設定を編集します。

   ![基本的な SAML 構成を編集する](common/edit-urls.png)

1. **[基本的な SAML 構成]** セクションで、アプリケーションを IDP Initiated モードで構成する場合は、次の手順を行います。

   1. **[返信 URL]** が https://console.spotinst.com/auth/saml に設定されていることを確認します。
   1. **[リレー状態]** で、Spotinst 組織 ID を入力します。これは、 **[SSO]** タブでも確認できます。
   1. **[サインオン URL]** は空である必要があります。

1. **[保存]** をクリックします。

1. Spotinst アプリケーションは、特定の形式の SAML アサーションを使用するため、カスタム属性のマッピングを SAML トークンの属性の構成に追加する必要があります。 次のスクリーンショットには、既定の属性一覧が示されています。

    ![image](common/default-attributes.png)

1. その他に、Spotinst アプリケーションでは、いくつかの属性が SAML 応答で返されることが想定されています。それらの属性を次に示します。 これらの属性も値が事前に設定されますが、要件に従ってそれらの値を確認することができます。

    | 名前 | ソース属性|
    | -----| --------------- |
    | Email | User.mail |
    | FirstName | User.givenname |
    | LastName | User.surname |

1. **[SAML でシングル サインオンをセットアップします]** ページの **[SAML 署名証明書]** セクションで、 **[フェデレーション メタデータ XML]** を探して **[ダウンロード]** を選択し、証明書をダウンロードして、お使いのコンピューターに保存します。

    ![証明書のダウンロードのリンク](common/metadataxml.png)

1. **[Spotinst のセットアップ]** セクションで、要件に基づいて適切な URL をコピーします。

    ![構成 URL のコピー](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD のテスト ユーザーの作成

このセクションでは、Azure portal 内で B.Simon というテスト ユーザーを作成します。

1. Azure portal の左側のウィンドウから、 **[Azure Active Directory]** 、 **[ユーザー]** 、 **[すべてのユーザー]** の順に選択します。
1. 画面の上部にある **[新しいユーザー]** を選択します。
1. **[ユーザー]** プロパティで、以下の手順を実行します。
   1. **[名前]** フィールドに「`B.Simon`」と入力します。  
   1. **[ユーザー名]** フィールドに「username@companydomain.extension」と入力します。 たとえば、「 `B.Simon@contoso.com` 」のように入力します。
   1. **[パスワードを表示]** チェック ボックスをオンにし、 **[パスワード]** ボックスに表示された値を書き留めます。
   1. **Create** をクリックしてください。

### <a name="assign-the-azure-ad-test-user"></a>Azure AD テスト ユーザーの割り当て

このセクションでは、B.Simon に Spotinst へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

1. Azure portal で **[エンタープライズ アプリケーション]** を選択し、 **[すべてのアプリケーション]** を選択します。
1. アプリケーションの一覧で **[Spotinst]** を選択します。
1. アプリの概要ページで、 **[管理]** セクションを見つけて、 **[ユーザーとグループ]** を選択します。
1. **[ユーザーの追加]** を選択し、 **[割り当ての追加]** ダイアログで **[ユーザーとグループ]** を選択します。
1. **[ユーザーとグループ]** ダイアログの [ユーザー] の一覧から **[B.Simon]** を選択し、画面の下部にある **[選択]** ボタンをクリックします。
1. ユーザーにロールが割り当てられることが想定される場合は、 **[ロールの選択]** ドロップダウンからそれを選択できます。 このアプリに対してロールが設定されていない場合は、[既定のアクセス] ロールが選択されていることを確認します。
1. **[割り当ての追加]** ダイアログで、 **[割り当て]** をクリックします。

## <a name="configure-spotinst-sso"></a>Spotinst の SSO の構成

1. 別の Web ブラウザー ウィンドウで、セキュリティ管理者として Spotinst にサインインします。

2. 画面の右上にある **ユーザー アイコン** をクリックして、**[設定]** をクリックします。

    ![ユーザー アイコンから [設定] が選択された画面のスクリーンショット。](./media/spotinst-tutorial/settings.png)

3. 上部の **[SECURITY]\(セキュリティ\)** タブをクリックし、**[Identity Providers]\(ID プロバイダー\)** を選択して、以下の手順を実行します。

    ![Spotinst のセキュリティ](./media/spotinst-tutorial/security.png)

    a. インスタンスの **[Relay State]\(リレー状態\)** の値をコピーして、Azure portal の **[基本的な SAML 構成]** セクションの **[リレー状態]** テキスト ボックスに貼り付けます。

    b. **[BROWSE]\(参照\)** をクリックし、Azure portal からダウンロードしたメタデータ xml ファイルをアップロードします。

    c. **[保存]** をクリックします。

### <a name="create-spotinst-test-user"></a>Spotinst のテスト ユーザーの作成

このセクションの目的は、Spotinst で Britta Simon というユーザーを作成することです。

1. **SP** 開始モードでアプリケーションを構成してある場合は、次の手順を実行します。

   a. 別の Web ブラウザー ウィンドウで、セキュリティ管理者として Spotinst にサインインします。

   b. 画面の右上にある **ユーザー アイコン** をクリックして、**[設定]** をクリックします。

    ![ユーザー アイコンから [設定] が選択された画面のスクリーンショット。](./media/spotinst-tutorial/settings.png)

    c. **[Users]\(ユーザー\)** をクリックして、**[ADD USER]\(ユーザーの追加\)** を選択します。

    ![[Users]\(ユーザー\) から [ADD USER]\(ユーザーの追加\) が選択された画面のスクリーンショット。](./media/spotinst-tutorial/add-user.png)

    d. ユーザーの追加セクションで、次の手順を実行します。

    ![[Add user]\(ユーザーの追加\) セクションを示すスクリーンショット。ここで、説明されている値を入力できます。](./media/spotinst-tutorial/new-user.png)

    1. **[Full Name]\(フルネーム\)** ボックスに、ユーザーの氏名 (`BrittaSimon` など) を入力します。

    1. **[Email]\(電子メール\)** テキスト ボックスに、ユーザーのメール アドレスを入力します (`brittasimon@contoso.com` など)。

    1. **[Organization Role, Account Role, and Accounts]\(組織ロール、アカウント ロール、アカウント\)** で組織に固有の詳細を選択します。

2. **IDP** 開始モードでアプリケーションを構成してある場合は、このセクションにアクション項目はありません。 Spotinst では、Just-In-Time プロビジョニングがサポートされています。この設定は、既定で有効になっています。 存在しない Spotinst ユーザーにアクセスしようとすると、新しいユーザーが自動的に作成されます。

## <a name="test-sso"></a>SSO のテスト 

このセクションでは、次のオプションを使用して Azure AD のシングル サインオン構成をテストします。 

#### <a name="sp-initiated"></a>SP Initiated:

* Azure portal で **[このアプリケーションをテストします]** をクリックします。 これにより、Spotinst のサインオン URL にリダイレクトされ、そこでログイン フローを開始できます。  

* Spotinst のサインオン URL に直接移動し、そこからログイン フローを開始します。

#### <a name="idp-initiated"></a>IDP Initiated:

* Azure portal で **[このアプリケーションをテストします]** をクリックすると、SSO を設定した Spotinst に自動的にサインインされます。 

また、Microsoft マイ アプリを使用して、任意のモードでアプリケーションをテストすることもできます。 マイ アプリで [Spotinst] タイルをクリックすると、SP モードで構成されている場合は、ログイン フローを開始するためのアプリケーション サインオン ページにリダイレクトされます。IDP モードで構成されている場合は、SSO を設定した Spotinst に自動的にサインインされます。 マイ アプリの詳細については、[マイ アプリの概要](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

Spotinst を構成したら、組織の機密データを流出と侵入からリアルタイムで保護するセッション制御を適用できます。 セッション制御は、条件付きアクセスを拡張したものです。 [Microsoft Defender for Cloud Apps でセッション制御を強制する方法](/cloud-app-security/proxy-deployment-aad)をご覧ください。
