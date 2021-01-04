---
title: 'クイックスタート: Java Web アプリに "Microsoft でサインイン" を追加する | Azure'
titleSuffix: Microsoft identity platform
description: このクイックスタートでは、OpenID Connect を使用して、Java Web アプリケーションに Microsoft サインインを実装する方法について説明します。
services: active-directory
author: sangonzal
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 10/09/2019
ms.author: sagonzal
ms.custom: aaddev, scenarios:getting-started, languages:Java, devx-track-java
ms.openlocfilehash: e188c00840a4d043e94f94f9db565e2d4e06aaba
ms.sourcegitcommit: 3ea45bbda81be0a869274353e7f6a99e4b83afe2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "97031064"
---
# <a name="quickstart-add-sign-in-with-microsoft-to-a-java-web-app"></a>クイック スタート:Java Web アプリに "Microsoft でサインイン" を追加する

このクイックスタートでは、Java Web アプリケーションでユーザーをサインインし、Microsoft Graph API を呼び出す方法を示すコード サンプルをダウンロードして実行します。 Azure Active Directory (Azure AD) 組織のユーザーはアプリケーションにサインインできます。

 図については、「[このサンプルのしくみ](#how-the-sample-works)」を参照してください。

## <a name="prerequisites"></a>前提条件

このサンプルを実行するには、次のものが必要になります。

- [Java Development Kit (JDK)](https://openjdk.java.net/) 8 以降および [Maven](https://maven.apache.org/)。

> [!div renderon="docs"]
> ## <a name="register-and-download-your-quickstart-app"></a>クイック スタート アプリを登録してダウンロードする
> クイックスタート アプリケーションを開始する方法としては、[簡易] (オプション 1) と [手動] (オプション 2) の 2 つの選択肢があります。
>
> ### <a name="option-1-register-and-auto-configure-your-app-and-then-download-your-code-sample"></a>オプション 1: アプリを登録して自動構成を行った後、コード サンプルをダウンロードする
>
> 1. [Azure portal のアプリの登録](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/applicationsListBlade/quickStartType/JavaQuickstartPage/sourceType/docs)クイックスタート エクスペリエンスに移動します。
> 1. アプリケーションの名前を入力し、 **[登録]** を選択します。
> 1. ポータルのクイックスタート エクスペリエンスの案内に従って、自動的に構成されたアプリケーション コードをダウンロードします。
>
> ### <a name="option-2-register-and-manually-configure-your-application-and-code-sample"></a>オプション 2:アプリケーションを登録し、アプリケーションとコード サンプルを手動で構成する
>
> #### <a name="step-1-register-your-application"></a>手順 1:アプリケーションの登録
>
> アプリケーションを登録し、そのアプリの登録情報をアプリケーションに手動で追加するには、次の手順を実行します。
>
> 1. [Azure portal](https://portal.azure.com) にサインインします。
> 1. 複数のテナントにアクセスできる場合は、トップ メニューの **[ディレクトリとサブスクリプション]** フィルター:::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false":::を使用して、アプリケーションを登録するテナントを選択します。
> 1. **Azure Active Directory** を検索して選択します。
> 1. **[管理]** で **[アプリの登録]**  >  **[新規登録]** の順に選択します。
> 1. アプリケーションの **名前** を入力します (例: `java-webapp`)。 この名前は、アプリのユーザーに表示される場合があります。また、後で変更することができます。
> 1. **[登録]** を選択します。
> 1. 後で使用するために、 **[概要]** ページの **アプリケーション (クライアント) ID** と **ディレクトリ (テナント) ID** を書き留めておきます。
> 1. **[管理]** で、 **[認証]** を選択します。
> 1. **[プラットフォームの追加]**  >  **[Web]** の順に選択します。
> 1. **[リダイレクト URI]** セクションで、`https://localhost:8443/msal4jsample/secure/aad` を追加します。
> 1. **[構成]** をクリックします。
> 1. **[Web]** セクションで、2 つ目の **リダイレクト URI** として `https://localhost:8443/msal4jsample/graph/me` を追加します。
> 1. **[管理]** で、 **[証明書とシークレット]** を選択します。 **[クライアント シークレット]** セクションで、 **[新しいクライアント シークレット]** を選択します。
> 1. キーの説明 (アプリのシークレットなど) を入力し、既定の有効期限のままにして、 **[追加]** を選択します。
> 1. 後で使用するために、 **[クライアント シークレット]** の **値** を書き留めます。

> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-1-configure-your-application-in-the-azure-portal"></a>手順 1:Azure portal でのアプリケーションの構成
>
> このクイックスタートのコード サンプルを動作させるには、以下の操作が必要です。
>
> 1. 応答 URL として `https://localhost:8443/msal4jsample/secure/aad` および `https://localhost:8443/msal4jsample/graph/me` を追加します
> 1. クライアント シークレットを作成します。
> > [!div renderon="portal" id="makechanges" class="nextstepaction"]
> > [これらの変更を行います]()
>
> > [!div id="appconfigured" class="alert alert-info"]
> > ![構成済み](media/quickstart-v2-aspnet-webapp/green-check.png) アプリケーションはこれらの属性で構成されています。

#### <a name="step-2-download-the-code-sample"></a>手順 2:コード サンプルのダウンロード
> [!div renderon="docs"]
> [コード サンプルのダウンロード](https://github.com/Azure-Samples/ms-identity-java-webapp/archive/master.zip)

> [!div class="sxs-lookup" renderon="portal"]
> プロジェクトをダウンロードし、ルート フォルダーに近いローカル フォルダー (例: **C:\Azure-Samples**) に ZIP ファイルを展開します。
>
> localhost で https を使用するには、server.ssl.key プロパティを入力します。 自己署名証明書を生成するには、keytool ユーティリティ (JRE に含まれています) を使用します。
>
>  ```
>   Example:
>   keytool -genkeypair -alias testCert -keyalg RSA -storetype PKCS12 -keystore keystore.p12 -storepass password
>
>   server.ssl.key-store-type=PKCS12
>   server.ssl.key-store=classpath:keystore.p12
>   server.ssl.key-store-password=password
>   server.ssl.key-alias=testCert
>   ```
>   生成されたキーストア ファイルを "resources" フォルダーに配置します。

> [!div renderon="portal" id="autoupdate" class="sxs-lookup nextstepaction"]
> [コード サンプルをダウンロードします](https://github.com/Azure-Samples/ms-identity-java-webapp/archive/master.zip)

> [!div class="sxs-lookup" renderon="portal"]
> > [!NOTE]
> > `Enter_the_Supported_Account_Info_Here`

> [!div renderon="docs"]
> #### <a name="step-3-configure-the-code-sample"></a>手順 3:コード サンプルの構成
> 1. ZIP ファイルをローカル フォルダーに展開します。
> 1. 統合開発環境を使用する場合は、その IDE でサンプルを開きます (オプション)。
> 1. application.properties ファイルを開きます。これは、src/main/resources/ フォルダーにあり、フィールド *aad. clientId*、*aad. authority*、および *aad.secretKey* の値を **アプリケーション ID**、**テナント ID**、および **クライアント シークレット** のそれぞれの値で置き換えます。
>
>    ```file
>    aad.clientId=Enter_the_Application_Id_here
>    aad.authority=https://login.microsoftonline.com/Enter_the_Tenant_Info_Here/
>    aad.secretKey=Enter_the_Client_Secret_Here
>    aad.redirectUriSignin=https://localhost:8443/msal4jsample/secure/aad
>    aad.redirectUriGraph=https://localhost:8443/msal4jsample/graph/me
>    aad.msGraphEndpointHost="https://graph.microsoft.com/"
>    ```
> 各値の説明:
>
> - `Enter_the_Application_Id_here` - 登録したアプリケーションのアプリケーション ID。
> - `Enter_the_Client_Secret_Here` - 登録済みアプリケーション用に **[証明書とシークレット]** で作成した **[クライアント シークレット]** です。
> - `Enter_the_Tenant_Info_Here` - 登録したアプリケーションの **ディレクトリ (テナント) ID** 値です。
> 1. localhost で https を使用するには、server.ssl.key プロパティを入力します。 自己署名証明書を生成するには、keytool ユーティリティ (JRE に含まれています) を使用します。
>
>  ```
>   Example:
>   keytool -genkeypair -alias testCert -keyalg RSA -storetype PKCS12 -keystore keystore.p12 -storepass password
>
>   server.ssl.key-store-type=PKCS12
>   server.ssl.key-store=classpath:keystore.p12
>   server.ssl.key-store-password=password
>   server.ssl.key-alias=testCert
>   ```
>   生成されたキーストア ファイルを "resources" フォルダーに配置します。


> [!div class="sxs-lookup" renderon="portal"]
> #### <a name="step-3-run-the-code-sample"></a>手順 3:コード サンプルの実行
> [!div renderon="docs"]
> #### <a name="step-4-run-the-code-sample"></a>手順 4:コード サンプルの実行

プロジェクトを実行するには、次のいずれかを行うことができます。

埋め込みの Spring Boot サーバーを使用して IDE から直接実行するか、または [maven](https://maven.apache.org/plugins/maven-war-plugin/usage.html) を使用して WAR ファイルにパッケージ化し、[Apache Tomcat](http://tomcat.apache.org/) などの J2EE コンテナー ソリューションにデプロイします。

##### <a name="running-from-ide"></a>IDE からの実行

IDE から Web アプリケーションを実行している場合は、[実行] を選択し、プロジェクトのホーム ページに移動します。 このサンプルでは、標準のホームページ URL は https://localhost:8443 です。

1. 前面のページで、 **[ログイン]** ボタンを選択して Azure Active Directory にリダイレクトし、ユーザーに資格情報の入力を求めます。

1. ユーザーは認証されると、 *https://localhost:8443/msal4jsample/secure/aad* にリダイレクトされます。 ユーザーがサインインしたので、ページにサインインしたアカウントに関する情報が表示されます。 サンプル UI には、次のボタンがあります。
    - "*サインアウト*": 現在のユーザーをアプリケーションからサインアウトし、ホーム ページにリダイレクトします。
    - *Show User Info (ユーザー情報の表示)* :Microsoft Graph のトークンを取得し、そのトークンを含む要求で Microsoft Graph を呼び出します。これにより、サインインしたユーザーに関する基本情報が返されます。

##### <a name="running-from-tomcat"></a>Tomcat からの実行

Web サンプルを Tomcat にデプロイする場合は、ソース コードにいくつかの変更を加える必要があります。

1. ms-identity-java-webapp/pom.xml を開きます
    - `<name>msal-web-sample</name>` の下に `<packaging>war</packaging>` を追加します

2. ms-identity-java-webapp/src/main/java/com.microsoft.azure.msalwebsample/MsalWebSampleApplication を開きます

    - すべてのソース コードを削除し、次のコードに置き換えます。

   ```Java
    package com.microsoft.azure.msalwebsample;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.boot.builder.SpringApplicationBuilder;
    import org.springframework.boot.web.servlet.support.SpringBootServletInitializer;

    @SpringBootApplication
    public class MsalWebSampleApplication extends SpringBootServletInitializer {

     public static void main(String[] args) {
      SpringApplication.run(MsalWebSampleApplication.class, args);
     }

     @Override
     protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
      return builder.sources(MsalWebSampleApplication.class);
     }
    }
   ```

3.   Tomcat の既定の HTTP ポートは 8080 ですが、ポート 8443 経由の HTTPS 接続が必要です。 これを構成するには、次のようにします。
        - tomcat/conf/system.xml にアクセスします
        - `<connector>` タグを検索し、既存のコネクタを次のように置き換えます。

        ```xml
        <Connector
                   protocol="org.apache.coyote.http11.Http11NioProtocol"
                   port="8443" maxThreads="200"
                   scheme="https" secure="true" SSLEnabled="true"
                   keystoreFile="C:/Path/To/Keystore/File/keystore.p12" keystorePass="KeystorePassword"
                   clientAuth="false" sslProtocol="TLS"/>
        ```

4. コマンド プロンプトを開き、このサンプルのルート フォルダー (pom ファイルが配置されている場所) に移動して、`mvn package` を実行してプロジェクトをビルドします。
    - これにより、/targets ディレクトリに `msal-web-sample-0.1.0.war` ファイルが生成されます。
    - このファイルの名前を `msal4jsample.war` に変更します
    - Tomcat またはその他の J2EE コンテナー ソリューションを使用して、この war ファイルをデプロイします。
        - デプロイするには、msal4jsample.war ファイルを Tomcat インストールの下にある `/webapps/` ディレクトリにコピーしてから、Tomcat サーバーを起動します。

5. デプロイされたら、ブラウザーで https://localhost:8443/msal4jsample にアクセスします。


> [!IMPORTANT]
> このクイック スタート アプリケーションは、クライアント シークレットを使用して、それ自体を機密クライアントとして識別します。 クライアント シークレットはプロジェクト ファイルにプレーン テキストとして追加されるため、セキュリティ上の理由から、アプリケーションを運用アプリケーションと見なす前に、クライアント シークレットの代わりに証明書を使用することをお勧めします。 証明書の使用方法の詳細については、「[アプリケーションを認証するための証明書資格情報](./active-directory-certificate-credentials.md)」を参照してください。

## <a name="more-information"></a>詳細情報

### <a name="how-the-sample-works"></a>このサンプルのしくみ
![このクイック スタートで生成されたサンプル アプリの動作の紹介](media/quickstart-v2-java-webapp/java-quickstart.svg)

### <a name="getting-msal"></a>MSAL の取得

MSAL for Java (MSAL4J) は、ユーザーをサインインさせるために使用されたり、Microsoft ID プラットフォームによって保護されている API にアクセスするためのトークンを要求するために使用されたりする Java ライブラリです。

Maven または Gradle を使用して、アプリケーションに MSAL4J を追加し、アプリケーションの pom.xml (Maven) または build.gradle (Gradle) ファイルに対して以下の変更を行うことで、依存関係を管理します。

pom.xml 内:

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>msal4j</artifactId>
    <version>1.0.0</version>
</dependency>
```

build.gradle 内:

```$xslt
compile group: 'com.microsoft.azure', name: 'msal4j', version: '1.0.0'
```

### <a name="msal-initialization"></a>MSAL の初期化

MSAL for Java を使用するファイルの先頭に次のコードを追加して、MSAL4J への参照を追加します。

```Java
import com.microsoft.aad.msal4j.*;
```

[!INCLUDE [Help and support](../../../includes/active-directory-develop-help-support-include.md)]

## <a name="next-steps"></a>次のステップ

Microsoft ID プラットフォームでユーザーをサインインさせる Web アプリの構築に関する詳しい解説が必要であれば、複数のパートから構成されるシナリオ シリーズにお進みください。

> [!div class="nextstepaction"]
> [シナリオ: ユーザーをサインインさせる Web アプリ](scenario-web-app-sign-user-overview.md?tabs=java)
