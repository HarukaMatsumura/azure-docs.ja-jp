---
title: Logic Apps との統合
titleSuffix: Azure Digital Twins
description: カスタム コネクタを使用して Logic Apps を Azure Digital Twins に接続する方法について説明します
author: baanders
ms.author: baanders
ms.date: 9/11/2020
ms.topic: how-to
ms.service: digital-twins
ms.reviewer: baanders
ms.openlocfilehash: 54a96d1f3227cd4a66e344b63b2ecb337df31aba
ms.sourcegitcommit: 9b8425300745ffe8d9b7fbe3c04199550d30e003
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2020
ms.locfileid: "92461075"
---
# <a name="integrate-with-logic-apps-using-a-custom-connector"></a>カスタム コネクタを使用して Logic Apps と統合する

[Azure Logic Apps](../logic-apps/logic-apps-overview.md) は、アプリとサービス全体のワークフローを自動化するのに役立つクラウド サービスです。 Logic Apps を Azure Digital Twins API に接続すると、Azure Digital Twins とそのデータに関するそのような自動化されたフローを作成できます。

現在、Azure Digital Twins に、Logic Apps 用の認定された (構築済みの) コネクタはありません。 代わりに、Azure Digital Twins で Logic Apps を使用するための現在のプロセスでは、Logic Apps で動作するように変更された [カスタム Azure Digital Twins Swagger](/samples/azure-samples/digital-twins-custom-swaggers/azure-digital-twins-custom-swaggers/) を使用して、[**カスタム Logic Apps コネクタ**](../logic-apps/custom-connector-overview.md)を作成します。

> [!NOTE]
> 上記のリンクされたカスタム Swagger サンプルには、複数のバージョンの Swagger が含まれています。 最新バージョンは、最新の日付のサブフォルダーにありますが、サンプルに含まれていた以前のバージョンも引き続きサポートされます。

この記事では、[Azure portal](https://portal.azure.com) を使用して、Azure Digital Twins インスタンスに Logic Apps を接続するために使用できる **カスタム コネクタを作成** します。 その後、シナリオの例にこの接続を使用する **ロジック アプリを作成** します。ここでは、タイマーによってトリガーされるイベントにより、Azure Digital Twins インスタンスのツインが自動的に更新されます。 

## <a name="prerequisites"></a>前提条件

Azure サブスクリプションをお持ちでない場合は、開始する前に **[無料のアカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)を作成** してください。
このアカウントを使用して、[Azure portal](https://portal.azure.com) にサインインします。 

事前に必要な設定の一部として、さらに次の項目を完了する必要があります。 この手順については、残りのセクションで順を追って説明します。
- Azure Digital Twins インスタンスを設定する
- アプリの登録のクライアント シークレットを取得する
- デジタル ツインを追加する

### <a name="set-up-azure-digital-twins-instance"></a>Azure Digital Twins インスタンスを設定する

この記事で Azure Digital Twins インスタンスを Logic Apps に接続するには、**Azure Digital Twins インスタンス** を先に設定しておく必要があります。 

まず、**Azure Digital Twins インスタンスを設定** し、その操作を可能にするために必要な認証を設定します。 このためには、[*操作方法の手順に従うため、インスタンスと認証を設定する方法*](how-to-set-up-instance-portal.md)に関するページを参照してください。 推奨されるエクスペリエンスに応じて、[Azure portal](how-to-set-up-instance-portal.md)、[CLI](how-to-set-up-instance-cli.md)、または [ Cloud Shell の自動デプロイ スクリプト サンプル](how-to-set-up-instance-scripted.md)用のセットアップに関する記事が用意されています。 すべてのバージョンの説明には、各手順が正しく完了し、新しいインスタンスを使用する準備ができていることを確認する手順も含まれています。
* Azure Digital Twins インスタンスの設定後、インスタンスの "**_ホスト名_**" ([Azure portal で確認してください](how-to-set-up-instance-portal.md#verify-success-and-collect-important-values)) が必要になります。

コネクタを認証するには、**アプリの登録** も設定する必要があります。 [*アプリの登録の作成方法*](how-to-create-app-registration.md)に関するページでの指示に従って設定します。 
* アプリの登録が完了したら、登録の "**_アプリケーション (クライアント) ID_**" および "**_ディレクトリ (テナント) ID_**" ([Azure portal で確認してください](how-to-create-app-registration.md#collect-client-id-and-tenant-id)) が必要になります。

### <a name="get-app-registration-client-secret"></a>アプリの登録のクライアント シークレットを取得する

Azure AD アプリの登録に対する "**_クライアント シークレット_**" も作成する必要があります。 これを行うには、Azure portal の [[アプリの登録]](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) ページに移動します (このリンクを使用しても、ポータルの検索バーで検索してもかまいません)。 その詳細を開くには、前のセクションで作成した登録を一覧から選択します。 

登録のメニューから *[証明書とシークレット]* を選択して、 *[+ 新しいクライアント シークレット]* を選択します。

:::image type="content" source="media/how-to-integrate-logic-apps/client-secret.png" alt-text="Azure AD アプリの登録のポータル表示。リソース メニューの [証明書とシークレット] とページの [新しいクライアント シークレット] が強調して示されている":::

[説明] と [有効期限] に適切な値を入力して、 *[追加]* クリックします。

:::image type="content" source="media/how-to-integrate-logic-apps/add-client-secret.png" alt-text="クライアント シークレットの追加":::

_[証明書とシークレット]_ ページで、 _[有効期限]_ および _[値]_ フィールドと共にクライアント シークレットが表示されていることを確認します。 後で使用するので _[値]_ を記録しておきます ([コピー] アイコンを使用してクリップボードにコピーすることもできます)

:::image type="content" source="media/how-to-integrate-logic-apps/client-secret-value.png" alt-text="クライアント シークレットの値のコピー":::

### <a name="add-a-digital-twin"></a>デジタル ツインを追加する

この記事では、Logic Apps を使用して、Azure Digital Twins インスタンス内のツインを更新します。 続行するには、インスタンスにツインを少なくとも 1 つ追加する必要があります。 

[DigitalTwins API](/rest/api/digital-twins/dataplane/twins)、[NET (C#) SDK](/dotnet/api/overview/azure/digitaltwins/client?view=azure-dotnet-preview&preserve-view=true)、または [Azure Digital Twins CLI](how-to-use-cli.md) を使用してツインを追加できます。 これらの方法を使用してツインを作成する方法の詳細な手順については、"[ *「デジタル ツインを管理する」方法*](how-to-manage-twin.md)を参照してください。

作成したインスタンス内のツインの "**_ツイン ID_**" が必要になります。

## <a name="create-custom-logic-apps-connector"></a>カスタム Logic Apps コネクタを作成する

このステップでは、Azure Digital Twins API 用の[カスタム Logic Apps コネクタ](../logic-apps/custom-connector-overview.md)を作成します。 これを行った後は、次のセクションでロジック アプリを作成するときに、Azure Digital Twins を接続できるようになります。

Azure portal の [[Logic Apps カスタム コネクタ]](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Web%2FcustomApis) ページに移動します (このリンクを使用しても、ポータルの検索バーで検索してもかまいません)。 *[+ 追加]* をクリックします。

:::image type="content" source="media/how-to-integrate-logic-apps/logic-apps-custom-connector.png" alt-text="Azure portal の [Logic Apps カスタム コネクタ] ページ。[追加] ボタンが強調して示されている":::

次の *[Logic Apps カスタム コネクタの作成]* ページで、お使いのサブスクリプション、リソース グループ、新しいコネクタの名前とデプロイの場所を選択します。 *[確認および作成]* をクリックします。 

:::image type="content" source="media/how-to-integrate-logic-apps/create-logic-apps-custom-connector.png" alt-text="Azure portal の [Logic Apps カスタム コネクタの作成] ページ。":::

これにより表示される *[確認および作成]* タブによって、下部にある *[作成]* をクリックしてリソースを作成できます。

:::image type="content" source="media/how-to-integrate-logic-apps/review-logic-apps-custom-connector.png" alt-text="Azure portal の [Logic Apps カスタム コネクタの確認] ページの [確認と作成] タブ。[作成] ボタンが強調して示されている":::

コネクタのデプロイ ページが表示されます。 デプロイが完了したら、 *[リソースに移動]* ボタンをクリックして、ポータルでコネクタの詳細を表示します。

### <a name="configure-connector-for-azure-digital-twins"></a>Azure Digital Twins 用にコネクタを構成する

次に、作成したコネクタを Azure Digital Twins に接続するように構成します。

まず、Logic Apps で動作するように変更されたカスタム Azure Digital Twins Swagger をダウンロードします。 *[ZIP のダウンロード]* ボタンを押し、[**このリンク**](/samples/azure-samples/digital-twins-custom-swaggers/azure-digital-twins-custom-swaggers/)から **Azure Digital Twins Custom Swaggers (Logic Apps コネクタ)** サンプルをダウンロードします。 ダウンロードした *Azure_Digital_Twins_custom_Swaggers__Logic_Apps_connector_.zip* フォルダーに移動し、解凍します。 

このチュートリアル用のカスタム Swagger は _**Azure_Digital_Twins_custom_Swaggers__Logic_Apps_connector_\LogicApps **_ フォルダー内に配置されます。このフォルダーには、*stable* と *preview* という名前のサブフォルダーが含まれています。どちらも、日付別に編成された異なるバージョンの Swagger を保持しています。最新の日付のフォルダーには、Swagger の最新のコピーが含まれます。どちらのバージョンを選択した場合でも、Swagger ファイルには _** digitaltwins.json**_ という名前が付けられています。

> [!NOTE]
> プレビュー機能を使用している場合を除き、一般的には、最新の "*安定した*" バージョンの Swagger を使用することをお勧めします。 ただし、以前のバージョンとプレビュー バージョンの Swagger も、引き続きサポートされます。 

次に、[Azure portal](https://portal.azure.com) のコネクタの [概要] ページに進み、 *[編集]* を押します。

:::image type="content" source="media/how-to-integrate-logic-apps/edit-connector.png" alt-text="前のステップで作成したコネクタの [概要] ページ。[編集] ボタンが強調して示されている":::

次の *[Logic Apps カスタム コネクタの編集]* ページで、次の情報を構成します。
* **カスタム コネクタ**
    - API エンドポイント: REST (既定値のまま)
    - インポート モード: OpenAPI ファイル (既定値のまま)
    - ファイル: これは、前にダウンロードしたカスタム Swagger ファイルです。 *[インポート]* を押し、お使いのマシン上でファイルを探して (*Azure_Digital_Twins_custom_Swaggers__Logic_Apps_connector_\LogicApps\...\digitaltwins.json*)、 *[開く]* を押します。
* **一般情報**
    - アイコン: 使用するアイコンをアップロードします
    - アイコンの背景色:'#xxxxxx' という形式で、色の 16 進コードを入力します。
    - 説明:任意の値を入力します。
    - スキーム: HTTPS (既定値のまま)
    - [Host]\(ホスト\):Azure Digital Twins インスタンスの "*ホスト名*"。
    - ベース URL: / (既定値のまま)

次に、ウィンドウの下部にある *[セキュリティ]* ボタンをクリックして、次の構成ステップに進みます。

:::image type="content" source="media/how-to-integrate-logic-apps/configure-next.png" alt-text="[Logic Apps カスタム コネクタの編集] ページの下部のスクリーンショット。セキュリティに進むためのボタンが強調して示されている":::

[セキュリティ] ステップで、 *[編集]* クリックして次の情報を構成します。
* **[認証の種類]** : OAuth 2.0
* **OAuth 2.0**:
    - ID プロバイダー: Azure Active Directory
    - クライアント ID: お使いの Azure AD アプリ登録の "*アプリケーション (クライアント) ID*"
    - クライアント シークレット:Azure AD アプリ登録の "[*前提条件*](#prerequisites)" で作成した "*クライアント シークレット*"
    - ログイン URL: https://login.windows.net (既定のまま)
    - テナント ID: Azure AD アプリ登録の "*ディレクトリ (テナント) ID*"
    - リソース URL: 0b07f429-9f4b-4714-9392-cc5e8e80c8b0
    - スコープ:Directory.AccessAsUser.All
    - リダイレクト URL: (現時点では既定のまま)

[リダイレクト URL] フィールドに *[カスタム コネクタを保存してリダイレクト URL を生成します]* と表示されていることにご注意ください。 ペインの上部にある *[コネクタの更新]* をクリックしてこれを行い、コネクタの設定を確認します。

:::image type="content" source="media/how-to-integrate-logic-apps/update-connector.png" alt-text="[Logic Apps カスタム コネクタの編集] ページの上部のスクリーンショット。[コネクタの更新] ボタンの周囲が強調して示されている":::

<!-- Success message? didn't see one -->

[リダイレクト URL] フィールドに戻り、生成された値をコピーします。 次の手順で使用します。

:::image type="content" source="media/how-to-integrate-logic-apps/copy-redirect-url.png" alt-text="[Logic Apps カスタム コネクタの編集] ページの [リダイレクト URL] フィールドの値が、&quot;https://logic-apis-westus2.consent.azure-apim.net/redirect&quot; になっている。値をコピーするボタンが強調して示されている。":::

コネクタを作成するために必要な情報は、これですべてです ([セキュリティ] に続けて [定義] ステップを行う必要はありません)。 *[Logic Apps カスタム コネクタの編集]* ペインを閉じてかまいません。

>[!NOTE]
>最初に *[編集]* をクリックしたコネクタの [概要] ページに戻ります。 *[編集]* を再びクリックすると、構成選択入力プロセス全体が再び始まるのでご注意ください。 前回の設定値は残っていないので、変更した値で更新した構成を保存したい場合は、既定値で上書きされないように、他の値もすべて再入力する必要があります。

### <a name="grant-connector-permissions-in-the-azure-ad-app"></a>Azure AD アプリでコネクタのアクセス許可を付与する

次に、最後のステップでコピーしたカスタム コネクタの "*リダイレクト URL*" の値を使用して、Azure AD アプリの登録でコネクタのアクセス許可を付与します。

Azure portal の [[アプリの登録]](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) ページに移動し、一覧から登録を選択します。 

登録のメニューの *[認証]* で、URI を追加します。

:::image type="content" source="media/how-to-integrate-logic-apps/add-uri.png" alt-text="Azure portal でのアプリ登録の認証ページ。メニューの [認証] と、そのページの [URI の追加] ボタンが強調して示されている。"::: 

カスタム コネクタの "*リダイレクト URL*" を新しいフィールドに入力し、 *[保存]* アイコンをクリックします。

:::image type="content" source="media/how-to-integrate-logic-apps/save-uri.png" alt-text="Azure portal でのアプリ登録の認証ページ。新しいリダイレクト URL と、そのページの [保存] ボタンが強調して示されている。":::

これで、Azure Digital Twins API にアクセスできるカスタム コネクタの設定が完了しました。 

## <a name="create-logic-app"></a>ロジック アプリを作成する

次に、新しいコネクタを使用して Azure Digital Twins の更新を自動化するロジック アプリを作成します。

[Azure portal](https://portal.azure.com) の検索バーで、「*Logic Apps*」を検索します。 それを選択すると、 *[Logic Apps]* ページが表示されます。 *[ロジック アプリの作成]* ボタンをクリックして新しいロジック アプリを作成します。

:::image type="content" source="media/how-to-integrate-logic-apps/create-logic-app.png" alt-text="Azure portal の [Logic Apps] ページ。[追加] ボタンをクリックする":::

続いて表示される *[Logic Apps]* ページで、サブスクリプションとリソース グループを入力します。 また、ロジック アプリの名前を選択し、デプロイの場所を選択します。

_[確認および作成]_ ボタンをクリックします。

これにより表示される *[確認と作成]* タブで、詳細を確認し、下部にある *[作成]* をクリックしてリソースを作成できます。

ロジック アプリのデプロイ ページが表示されます。 デプロイが完了したら、 *[リソースに移動]* ボタンをクリックして *[Logic Apps デザイナー]* に進み、そこでワークフローのロジックを入力します。

### <a name="design-workflow"></a>ワークフローを設計する

*[Logic Apps デザイナー]* で、 *[一般的なトリガーで開始する]* の _**[繰り返し]**_ を選択します。

:::image type="content" source="media/how-to-integrate-logic-apps/logic-apps-designer-recurrence.png" alt-text="Azure portal の [Logic Apps デザイナー] ページ。[繰り返し] 一般トリガーが強調して示されている":::

次の *[Logic Apps デザイナー]* ページで、 **[繰り返し]** 頻度を *[秒]* に変更して、イベントが 3 秒ごとにトリガーされるようにします。 これにより、後で非常に長い時間待つことなく、簡単に結果を確認できるようになります。

*[+ 新しいステップ]* をクリックします。

これにより、 *[アクションの選択]* ボックスが開きます。 *[カスタム]* タブに切り替えます。上部のボックスに、前に作成したカスタム コネクタが表示されます。

:::image type="content" source="media/how-to-integrate-logic-apps/custom-action.png" alt-text="Azure portal の Logic Apps デザイナーでのフローの作成。[アクションの選択] ボックスの [カスタム] タブが選択されている。前に作成したユーザーのカスタム コネクタがボックスに表示され、その周囲が強調して示されている。":::

それを選択して、そのコネクタに含まれる API の一覧を表示します。 検索バーを使用するか、一覧をスクロールして、**DigitalTwins_Add** を選択します。 (この記事ではこの API が使用されていますが、他の API を Logic Apps の接続用に選択してもかまいません)。

コネクタに接続するために、Azure の資格情報でサインインするように求められる場合があります。 *[要求されているアクセス許可]* ダイアログが表示される場合は、画面の指示に従ってアプリに同意して受け入れます。

新しい *DigitalTwinsAdd* ボックスのフィールドを次のように設定します。
* _id_:ロジック アプリで更新するインスタンス内のデジタル ツインの "*ツイン ID*" を入力します。
* _ツイン_:このフィールドには、選択した API 要求で必要な本文を入力します。 *DigitalTwinsUpdate* の場合、この本文は JSON Patch コードの形式です。 ツインを更新するための JSON Patch の構成の詳細については、「[デジタル ツインを更新する](how-to-manage-twin.md#update-a-digital-twin)」セクションを参照してください ("*方法: 「デジタル ツインを管理する」方法* を参照してください。
* _API バージョン_:最新の API バージョン。 現在、この値は *2020-10-31* です。

Logic Apps デザイナーで *[保存]* をクリックします。

同じウィンドウで、 _[+ 新しいステップ]_ を選択すると、他の操作を選択できます。

:::image type="content" source="media/how-to-integrate-logic-apps/save-logic-app.png" alt-text="ロジック アプリ コネクタで完成したアプリの表示。DigitalTwinsAdd ボックスに、JSON Patch 本文のサンプルなど、上で説明した値が入力されている。ウィンドウの [保存] ボタンが強調して示されている。":::

## <a name="query-twin-to-see-the-update"></a>ツインのクエリを実行して更新を確認する

ロジック アプリを作成したので、Logic Apps デザイナーで定義したツイン更新イベントが、3 秒ごとに繰り返し発生するようになります。 つまり、3 秒後には、ツインに対してクエリを実行し、新しくパッチが適用された値が反映されていることを確認できるはずです。

任意の方法 ([カスタム クライアント アプリ](tutorial-command-line-app.md)、[Azure Digital Twins Explorer サンプル アプリ](/samples/azure-samples/digital-twins-explorer/digital-twins-explorer/)、[SDK と API](how-to-use-apis-sdks.md)、[CLI](how-to-use-cli.md) など) を選択して、ツインのクエリを実行できます。 

Azure Digital Twins インスタンスのクエリの詳細については、[*ツイン グラフにクエリを実行する*](how-to-query-graph.md)方法に関する記事を参照してください。

## <a name="next-steps"></a>次のステップ

この記事では、指定したパッチを使用して、Azure Digital Twins インスタンス内のツインを定期的に更新するロジック アプリを作成しました。 カスタム コネクタで他の API を選択して、インスタンスに対するさまざまなアクションのロジック アプリを作成することができます。

使用可能な API 操作とその詳細については、"[*Azure Digital Twins の API および SDK を使用する方法*](how-to-use-apis-sdks.md)" に関するページで参照してください。