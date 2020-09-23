---
title: Azure Active Directory B2C のサンプル コード | Microsoft Docs
description: Azure Active Directory B2C のモバイル、デスクトップ、Web、およびシングルページ アプリケーションのコード サンプル。
services: active-directory-b2c
author: msmimart
manager: celestedg
ms.author: mimart
ms.date: 01/29/2020
ms.custom: mvc
ms.topic: sample
ms.service: active-directory
ms.subservice: B2C
ms.openlocfilehash: da84fee4e974f02f29dc9006fe740c415632ae53
ms.sourcegitcommit: 3fc3457b5a6d5773323237f6a06ccfb6955bfb2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90029020"
---
# <a name="azure-active-directory-b2c-code-samples"></a>Azure Active Directory B2C のサンプル コード

次の表には、iOS、Android、.NET、Node.js などのアプリケーションのサンプルへのリンクがまとめてあります。

## <a name="mobile-and-desktop-apps"></a>モバイル アプリとデスクトップ アプリ

| サンプル | 説明 |
|--------| ----------- |
| [ios-swift-native-msal](https://github.com/Azure-Samples/active-directory-b2c-ios-swift-native-msal) | Azure AD B2C ユーザーを認証し、OAuth 2.0 を使用して API を呼び出す Swift の iOS サンプル |
| [android-native-msal](https://github.com/Azure-Samples/ms-identity-android-java#b2cmodefragment-class) | MSAL を使用して Azure Active Directory B2C 経由でユーザーを認証し、結果として得られたトークンで Web API にアクセスする方法を示す単純な Android アプリ。 |
| [ios-native-appauth](https://github.com/Azure-Samples/active-directory-b2c-ios-native-appauth) | サード パーティのライブラリを使用して、Objective-C で iOS アプリケーションをビルドする方法を示すサンプル。このアプリケーションは、Azure AD B2C ID サービスに対して Microsoft ID ユーザーを認証します。 |
| [android-native-appauth](https://github.com/Azure-Samples/active-directory-b2c-android-native-appauth) | サード パーティのライブラリを使用して、Android アプリケーションをビルドする方法を示すサンプル。このアプリケーションは、B2C ID サービスに対して Microsoft ID ユーザーを認証し、OAuth 2.0 アクセス トークンを使用して Web API を呼び出します。 |
| [dotnet-desktop](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop) | Windows Desktop .NET (WPF) アプリケーションが Azure AD B2C を使用してユーザーのサインインを処理し、MSAL.NET を使用してアクセス トークンを取得して API を呼び出す方法を示すサンプル。 |
| [xamarin-native](https://github.com/Azure-Samples/active-directory-b2c-xamarin-native) | MSAL を使用して Azure Active Directory B2C 経由でユーザーを認証し、結果として得られたトークンで Web API にアクセスする方法を示す単純な Xamarin Forms アプリ。 |

## <a name="web-apps-and-apis"></a>Web アプリと API

| サンプル | 説明 |
|--------| ----------- |
| [dotnet-webapp-and-webapi](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi) | Azure AD B2C を使用してセキュリティで保護された、.NET Web API を呼び出す .NET Web アプリケーション用の結合されたサンプル。 |
| [dotnetcore-webapp](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapp) | Azure AD B2C を使用してユーザーのサインインを処理し、MSAL.NET を使用してアクセス トークンを取得して API を呼び出す ASP.NET Core Web アプリケーション。 |
| [openidconnect-nodejs](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS) | OpenID Connect を使用して、Web アプリケーションを Express ですばやく簡単にセットアップできるようにする Node.js アプリ。 |
| [javascript-nodejs-webapi](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) | passport.js を使用して Web API を保護し、B2C アクセス トークンを受け入れる方法を示す、Azure AD B2C 用の小さな node.js Web API。 |
| [ms-identity-python-webapp](https://github.com/Azure-Samples/ms-identity-python-webapp/blob/master/README_B2C.md) | Microsoft ID プラットフォームの B2C を Python Web アプリケーションに統合する方法を説明します。  |

## <a name="single-page-apps"></a>シングル ページ アプリ

| サンプル | 説明 |
|--------| ----------- |
| [javascript-msal-singlepageapp](https://github.com/Azure-Samples/active-directory-b2c-javascript-msal-singlepageapp) | Web API を呼び出すシングルページ アプリケーション (SPA)。 認証は、MSAL.js を使用して、Azure AD B2C によって行われます。 |

## <a name="saml-test-application"></a>SAML テスト アプリケーション

| サンプル | 説明 |
|--------| ----------- |
| [saml-sp-tester](https://github.com/azure-ad-b2c/saml-sp-tester/tree/master/source-code) | SAML ID プロバイダーとして動作するように構成された Azure AD B2C をテストするための SAML テスト アプリケーション。 |
