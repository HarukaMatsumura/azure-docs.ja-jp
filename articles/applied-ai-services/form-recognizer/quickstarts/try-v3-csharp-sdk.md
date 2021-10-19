---
title: 'クイック スタート: Form Recognizer C# SDK v3.0 | プレビュー'
titleSuffix: Azure Applied AI Services
description: Form Recognizer C# クライアント ライブラリ SDK v3.0 を使用したフォームとドキュメントの処理、データ抽出、分析 (プレビュー)
author: laujan
manager: nitinme
ms.service: applied-ai-services
ms.subservice: forms-recognizer
ms.topic: quickstart
ms.date: 10/07/2021
ms.author: lajanuar
recommendations: false
ms.openlocfilehash: f0ed9d9b7574f6d8d1856c263b22dfa66e1207ca
ms.sourcegitcommit: 54e7b2e036f4732276adcace73e6261b02f96343
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2021
ms.locfileid: "129809829"
---
# <a name="quickstart-form-recognizer-c-client-library-sdks-v30--preview"></a>クイック スタート: Form Recognizer C# クライアント ライブラリ SDK v3.0 | プレビュー

C# プログラミング言語を使用して、Azure Form Recognizer の使用を開始します。 Azure Form Recognizer は、機械学習テクノロジを利用して自動データ処理ソフトウェアを構築することができる [Azure Applied AI Services](../../../applied-ai-services/index.yml) クラウド サービスです。 Form Recognizer は、REST API または SDK を介して使用できます。 テクノロジを学習している場合は、無料のサービスを使用することをお勧めします。 無料のページは 1 か月あたり 500 ページに制限されていることに注意してください。

>[!NOTE]
> Form Recognizer v3.0 は現在、パブリック プレビューの段階です。 一部の機能がサポートされなかったり、機能が制限されたりすることがあります。 

[リファレンスのドキュメント](/dotnet/api/overview/azure/ai.formrecognizer-readme?view=azure-dotnet&preserve-view=true ) | [ライブラリのソース コード](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/formrecognizer/Azure.AI.FormRecognizer/src) | [パッケージ (NuGet)](https://www.nuget.org/packages/Azure.AI.FormRecognizer) | [サンプル](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/formrecognizer/Azure.AI.FormRecognizer/samples/README.md)

Azure Cognitive Services Form Recognizer は、機械学習を使用してドキュメントからフォーム フィールド、テキスト、テーブルを抽出して分析するクラウド サービスです。 お使いのワークフローとアプリケーションに Microsoft のクライアント ライブラリ SDK を統合することで、Form Recognizer モデルを簡単に呼び出すことができます。

### <a name="form-recognizer-models"></a>Form Recognizer モデル

C# SDK では、次のモデルと機能がサポートされています。

* 🆕一般的なドキュメント — テキスト、テーブル、構造体、キーと値のペア、名前付きエンティティを分析および抽出します。
* レイアウト - モデルをトレーニングすることなく、フォーム ドキュメント内のテーブル、行、単語、およびラジオ ボタンやチェック ボックスなどの選択マークを分析および抽出します。
* カスタム - 独自のフォームの種類でトレーニングしたモデルを使用して、カスタム フォームからフォーム フィールドや他のコンテンツを分析および抽出します。
* 請求書 - 事前トレーニング済みの請求書モデルを使用して、請求書から共通フィールドを分析および抽出します。
* 領収書 - 事前トレーニング済みの領収書モデルを使用して、領収書の共通フィールドを分析および抽出します。
* 身分証明書 - 事前トレーニング済みの身分証明書モデルを使用して、パスポートや運転免許証などの身分証明書から共通フィールドを分析および抽出します。
* 名刺 - 事前トレーニング済みの名刺モデルを使用して、名刺から共通フィールドを分析および抽出します。

このクイックスタートでは、次の機能を使用して、フォームとドキュメントからデータと値を分析および抽出します。

* [**一般的なドキュメント**](#try-it-general-document-model)

* [**Layout**](#try-it-layout-model)

* [**事前構築済みの請求書**](#try-it-prebuilt-invoice-model)

## <a name="prerequisites"></a>前提条件

* Azure サブスクリプション - [無料アカウントを作成します](https://azure.microsoft.com/free/cognitive-services/)

* [Visual Studio IDE](https://visualstudio.microsoft.com/vs/) または [.NET Core](https://dotnet.microsoft.com/download) の現在のバージョン。

* Cognitive Services または Form Recognizer リソース。 Azure サブスクリプションを用意できたら、Azure portal で[単一サービス](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesFormRecognizer)または[マルチサービス](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesAllInOne)の Form Recognizer リソースを作成し、キーとエンドポイントを取得します。 Free 価格レベル (<ph id="ph1">`F0`</ph>) を使用してサービスを試用し、後から運用環境用の有料レベルにアップグレードすることができます。

> [!TIP] 
> 1 つのエンドポイントまたはキーで複数のコグニティブ サービスにアクセスすることを予定している場合は、新しい Cognitive Services リソースを作成します。 Form Recognizer アクセスのみの場合は、Form Recognizer リソースを作成します。 [Azure Active Directory 認証](/azure/active-directory/authentication/overview-authentication)を使用する場合は、単一サービス リソースが必要になることに注意してください。

* リソースがデプロイされたら、 **[リソースに移動]** をクリックします。 自分のアプリケーションを Form Recognizer API に接続するには、作成したリソースのキーとエンドポイントが必要になります。 このクイックスタートで後に示すコードに、自分のキーとエンドポイントを貼り付けます。

  :::image type="content" source="../media/containers/keys-and-endpoint.png" alt-text="スクリーンショット: Azure portal のキーとエンドポイントの場所。":::

## <a name="set-up"></a>設定

### <a name="option-1-net-command-line-interface-cli"></a>[オプション 1: .NET コマンド ライン インターフェイス (CLI)](#tab/cli)

コンソール ウィンドウ (cmd、PowerShell、Bash など) で、`dotnet new` コマンドを使用し、`formrecognizer-quickstart` という名前で新しいコンソール アプリを作成します。 このコマンドにより、1 つのソース ファイルを使用する単純な "Hello World" C# プロジェクトが作成されます。*Program.cs*。

```console
dotnet new console -n formrecognizer-quickstart
```

コマンド ラインを開き、プロジェクト ファイルが含まれるディレクトリに切り替えます。 次を使用してアプリケーションをビルドします。

```console
dotnet build
```

ビルドの出力に警告やエラーが含まれないようにする必要があります。

```console
...
Build succeeded.
 0 Warning(s)
 0 Error(s)
...
```

### <a name="install-the-client-library-with-nuget"></a>NuGet を使用してクライアント ライブラリをインストールする

次のコマンドを使用して、ご自分のプロジェクトが含まれているディレクトリ内に .NET 用 Form Recognizer クライアント ライブラリをインストールします。

```console
dotnet add package Azure.AI.FormRecognizer
```

このバージョンのクライアント ライブラリは、既定で 2021-09-30-preview バージョンのサービスになります。

### <a name="option-2-visual-studio"></a>[方法 2: Visual Studio](#tab/vs)

1. Visual Studio 2019 を起動します。

1. スタート ページで、 [新しいプロジェクトの作成] を選択します。

    :::image type="content" source="../media/quickstarts/start-window.png" alt-text="スクリーンショット: Visual Studio のスタート ウィンドウ。":::

1. **[新しいプロジェクトの作成]** ページで、検索ボックスに「**コンソール**」と入力します。 **[コンソール アプリケーション]** テンプレートを選択し、 **[次へ]** を選択します。

    :::image type="content" source="../media/quickstarts/create-new-project.png" alt-text="スクリーンショット: Visual Studio の [新しいプロジェクトの作成] ページ。":::

1. **[新しいプロジェクトの構成]** ダイアログ ウィンドウの [プロジェクト名] ボックスに「`formRecognizer_quickstart`」と入力します。 その後、[次へ] を選択します。

    :::image type="content" source="../media/quickstarts/configure-new-project.png" alt-text="スクリーンショット: Visual Studio の [新しいプロジェクトの構成] ダイアログ ウィンドウ。":::

1. **[追加情報]** ダイアログ ウィンドウで、 **[.NET 5.0 (最新)]** を選択し、 **[作成]** を選択します。

    :::image type="content" source="../media/quickstarts/additional-information.png" alt-text="スクリーンショット: Visual Studio の [追加情報] ダイアログ ウィンドウ。":::

### <a name="install-the-client-library-with-nuget"></a>NuGet を使用してクライアント ライブラリをインストールする

 1. **formRecognizer_quickstart** プロジェクトを右クリックし、 **[NuGet パッケージの管理...]** を選択します。

    :::image type="content" source="../media/quickstarts/select-nuget-package.png" alt-text="スクリーンショット: select-nuget-package.png":::

 1. [参照] タブを選択し、「Azure.AI.FormRecognizer」と入力します。

     :::image type="content" source="../media/quickstarts/azure-nuget-package.png" alt-text="スクリーンショット: select-form-recognizer-package.png":::

 1. ドロップダウン メニューから目的のバージョンを選び、 **[インストール]** を選択します。

     このバージョンのクライアント ライブラリは、既定で 2021-09-30-preview バージョンのサービスになります。

---

## <a name="build-your-application"></a>アプリケーションをビルドする

Form Recognizer サービスと対話するには、`DocumentAnalysisClient` クラスのインスタンスを作成する必要があります。 これを行うには、ご自分の apiKey を使用して `AzureKeyCredential` を作成し、`AzureKeyCredential` とお使いの Form Recognizer `endpoint` を使用して `DocumentAnalysisClient` インスタンスを作成します。

1. **Program.cs** ファイルを開きます。

1. 次の using ディレクティブを含めます。

    ```csharp
    using System;
    using System.Threading.Tasks;
    using Azure.AI.FormRecognizer.DocumentAnalysis;
    ```

1. `endpoint` と `apiKey` の環境変数を設定し、`AzureKeyCredential` と `DocumentAnalysisClient` のインスタンスを作成します。

    ```csharp
    string endpoint = "<your-endpoint>";
    string apiKey = "<your-apiKey>";
    var credential = new AzureKeyCredential(apiKey);
    var client = new DocumentAnalysisClient(new Uri(endpoint), credential);
    ```

1. 行 `Console.Writeline("Hello World!");` を削除し、**Program.cs** ファイルの **Main** メソッドに **Try It** コードを追加します。

    :::image type="content" source="../media/quickstarts/add-code-here.png" alt-text="スクリーンショット: サンプル コードを Main メソッドに追加する。":::

## <a name="try-it-general-document-model"></a>**試してみる**: 一般的なドキュメント モデル

> [!div class="checklist"]
>
> * この例では、**URI にフォーム ドキュメント ファイル** が必要になります。 このクイックスタートでは、Microsoft の[サンプル フォーム ドキュメント](https://raw.githubusercontent.com/Azure-Samples/cognitive-services-REST-api-samples/master/curl/form-recognizer/sample-layout.pdf)を使用できます。
> * Main メソッドの上部にある `string fileUri` 変数にファイル URI 値を追加します。
> * URI で指定されたファイルの内容を分析するには、`StartAnalyzeDocumentFromUri` メソッドを使用します。 戻り値は、送信されたドキュメントに関するデータを含む `AnalyzeResult` オブジェクトです。

### <a name="add-the-following-code-to-your-general-document-application-main-method"></a>一般的なドキュメント アプリケーションの **Main** メソッドに次のコードを追加します

```csharp
// sample form document
string fileUri = "https://raw.githubusercontent.com/Azure-Samples/cognitive-services-REST-api-samples/master/curl/form-recognizer/sample-layout.pdf";

AnalyzeDocumentOperation operation = await client.StartAnalyzeDocumentFromUriAsync("prebuilt-document", fileUri);

await operation.WaitForCompletionAsync();

AnalyzeResult result = operation.Value;

Console.WriteLine("Detected entities:");

foreach (DocumentEntity entity in result.Entities)
{
    if (entity.SubCategory == null)
    {
        Console.WriteLine($"  Found entity '{entity.Content}' with category '{entity.Category}'.");
    }
    else
    {
        Console.WriteLine($"  Found entity '{entity.Content}' with category '{entity.Category}' and sub-category '{entity.SubCategory}'.");
    }
}

Console.WriteLine("Detected key-value pairs:");

foreach (DocumentKeyValuePair kvp in result.KeyValuePairs)
{
    if (kvp.Value.Content == null)
    {
        Console.WriteLine($"  Found key with no value: '{kvp.Key.Content}'");
    }
    else
    {
        Console.WriteLine($"  Found key-value pair: '{kvp.Key.Content}' and '{kvp.Value.Content}'");
    }
}

foreach (DocumentPage page in result.Pages)
{
    Console.WriteLine($"Document Page {page.PageNumber} has {page.Lines.Count} line(s), {page.Words.Count} word(s),");
    Console.WriteLine($"and {page.SelectionMarks.Count} selection mark(s).");

    for (int i = 0; i < page.Lines.Count; i++)
    {
        DocumentLine line = page.Lines[i];
        Console.WriteLine($"  Line {i} has content: '{line.Content}'.");

        Console.WriteLine($"    Its bounding box is:");
        Console.WriteLine($"      Upper left => X: {line.BoundingBox[0].X}, Y= {line.BoundingBox[0].Y}");
        Console.WriteLine($"      Upper right => X: {line.BoundingBox[1].X}, Y= {line.BoundingBox[1].Y}");
        Console.WriteLine($"      Lower right => X: {line.BoundingBox[2].X}, Y= {line.BoundingBox[2].Y}");
        Console.WriteLine($"      Lower left => X: {line.BoundingBox[3].X}, Y= {line.BoundingBox[3].Y}");
    }

    for (int i = 0; i < page.SelectionMarks.Count; i++)
    {
        DocumentSelectionMark selectionMark = page.SelectionMarks[i];

        Console.WriteLine($"  Selection Mark {i} is {selectionMark.State}.");
        Console.WriteLine($"    Its bounding box is:");
        Console.WriteLine($"      Upper left => X: {selectionMark.BoundingBox[0].X}, Y= {selectionMark.BoundingBox[0].Y}");
        Console.WriteLine($"      Upper right => X: {selectionMark.BoundingBox[1].X}, Y= {selectionMark.BoundingBox[1].Y}");
        Console.WriteLine($"      Lower right => X: {selectionMark.BoundingBox[2].X}, Y= {selectionMark.BoundingBox[2].Y}");
        Console.WriteLine($"      Lower left => X: {selectionMark.BoundingBox[3].X}, Y= {selectionMark.BoundingBox[3].Y}");
    }
}

foreach (DocumentStyle style in result.Styles)
{
    // Check the style and style confidence to see if text is handwritten.
    // Note that value '0.8' is used as an example.

    bool isHandwritten = style.IsHandwritten.HasValue && style.IsHandwritten == true;

    if (isHandwritten && style.Confidence > 0.8)
    {
        Console.WriteLine($"Handwritten content found:");

        foreach (DocumentSpan span in style.Spans)
        {
            Console.WriteLine($"  Content: {result.Content.Substring(span.Offset, span.Length)}");
        }
    }
}

Console.WriteLine("The following tables were extracted:");

for (int i = 0; i < result.Tables.Count; i++)
{
    DocumentTable table = result.Tables[i];
    Console.WriteLine($"  Table {i} has {table.RowCount} rows and {table.ColumnCount} columns.");

    foreach (DocumentTableCell cell in table.Cells)
    {
        Console.WriteLine($"    Cell ({cell.RowIndex}, {cell.ColumnIndex}) has kind '{cell.Kind}' and content: '{cell.Content}'.");
    }
}

```

## <a name="try-it-layout-model"></a>**試してみる**: レイアウト モデル

テキスト、選択マーク、テキスト スタイル、およびテーブルの構造を、対応する境界領域の座標と共にドキュメントから抽出します。

> [!div class="checklist"]
>
> * この例では、**URI にフォーム ドキュメント ファイル** が必要になります。 このクイックスタートでは、Microsoft の[サンプル フォーム ドキュメント](https://raw.githubusercontent.com/Azure-Samples/cognitive-services-REST-api-samples/master/curl/form-recognizer/sample-layout.pdf)を使用できます。
> * Main メソッドの上部にある `string fileUri` 変数にファイル URI 値を追加します。
> * URI で指定されたファイルからレイアウトを抽出するには、`StartAnalyzeDocumentFromUri` メソッドを使用して `prebuilt-layout` をモデル ID として渡します。 戻り値は、送信されたドキュメントからのデータを含む `AnalyzeResult` オブジェクトです。

### <a name="add-the-following-code-to-your-layout-application-main-method"></a>レイアウト アプリケーションの **Main** メソッドに次のコードを追加します

```csharp
// sample form document
string fileUri = "https://raw.githubusercontent.com/Azure-Samples/cognitive-services-REST-api-samples/master/curl/form-recognizer/sample-layout.pdf";

AnalyzeDocumentOperation operation = await client.StartAnalyzeDocumentFromUriAsync("prebuilt-layout", fileUri);

await operation.WaitForCompletionAsync();

AnalyzeResult result = operation.Value;

foreach (DocumentPage page in result.Pages)
{
    Console.WriteLine($"Document Page {page.PageNumber} has {page.Lines.Count} line(s), {page.Words.Count} word(s),");
    Console.WriteLine($"and {page.SelectionMarks.Count} selection mark(s).");

    for (int i = 0; i < page.Lines.Count; i++)
    {
        DocumentLine line = page.Lines[i];
        Console.WriteLine($"  Line {i} has content: '{line.Content}'.");

        Console.WriteLine($"    Its bounding box is:");
        Console.WriteLine($"      Upper left => X: {line.BoundingBox[0].X}, Y= {line.BoundingBox[0].Y}");
        Console.WriteLine($"      Upper right => X: {line.BoundingBox[1].X}, Y= {line.BoundingBox[1].Y}");
        Console.WriteLine($"      Lower right => X: {line.BoundingBox[2].X}, Y= {line.BoundingBox[2].Y}");
        Console.WriteLine($"      Lower left => X: {line.BoundingBox[3].X}, Y= {line.BoundingBox[3].Y}");
    }

    for (int i = 0; i < page.SelectionMarks.Count; i++)
    {
        DocumentSelectionMark selectionMark = page.SelectionMarks[i];

        Console.WriteLine($"  Selection Mark {i} is {selectionMark.State}.");
        Console.WriteLine($"    Its bounding box is:");
        Console.WriteLine($"      Upper left => X: {selectionMark.BoundingBox[0].X}, Y= {selectionMark.BoundingBox[0].Y}");
        Console.WriteLine($"      Upper right => X: {selectionMark.BoundingBox[1].X}, Y= {selectionMark.BoundingBox[1].Y}");
        Console.WriteLine($"      Lower right => X: {selectionMark.BoundingBox[2].X}, Y= {selectionMark.BoundingBox[2].Y}");
        Console.WriteLine($"      Lower left => X: {selectionMark.BoundingBox[3].X}, Y= {selectionMark.BoundingBox[3].Y}");
    }
}

foreach (DocumentStyle style in result.Styles)
{
    // Check the style and style confidence to see if text is handwritten.
    // Note that value '0.8' is used as an example.

    bool isHandwritten = style.IsHandwritten.HasValue && style.IsHandwritten == true;

    if (isHandwritten && style.Confidence > 0.8)
    {
        Console.WriteLine($"Handwritten content found:");

        foreach (DocumentSpan span in style.Spans)
        {
            Console.WriteLine($"  Content: {result.Content.Substring(span.Offset, span.Length)}");
        }
    }
}

Console.WriteLine("The following tables were extracted:");

for (int i = 0; i < result.Tables.Count; i++)
{
    DocumentTable table = result.Tables[i];
    Console.WriteLine($"  Table {i} has {table.RowCount} rows and {table.ColumnCount} columns.");

    foreach (DocumentTableCell cell in table.Cells)
    {
        Console.WriteLine($"    Cell ({cell.RowIndex}, {cell.ColumnIndex}) has kind '{cell.Kind}' and content: '{cell.Content}'.");
    }
}

```

## <a name="try-it-prebuilt-invoice-model"></a>**試してみる**: 事前構築済みの請求書モデル

このサンプルでは、請求書を例として使用して、事前トレーニング済みのモデルを使用して、特定の種類の一般的なドキュメントのデータを分析する方法を示します。

> [!div class="checklist"]
>
> * この例では、**URI に請求書ドキュメント ファイル** が必要になります。 このクイックスタートでは、Microsoft の[サンプル請求書ドキュメント](https://raw.githubusercontent.com/Azure-Samples/cognitive-services-REST-api-samples/master/curl/form-recognizer/sample-invoice.pdf)を使用できます。
> * Main メソッドの上部にある `string fileUri` 変数にファイル URI 値を追加します。
> * URI で指定されたファイルを分析するには、`StartAnalyzeDocumentFromUri` メソッドを使用して `prebuilt-invoice` をモデル ID として渡します。 戻り値は、送信されたドキュメントからのデータを含む `AnalyzeResult` オブジェクトです。

### <a name="choose-the-invoice-prebuilt-model-id"></a>請求書の事前構築済みモデル ID を選択する

請求書に限定されません。いくつかの事前構築済みモデルから選択できます。各モデルには、サポートされているフィールドの独自のセットがあります。 分析操作に使用するモデルは、分析するドキュメントの種類によって異なります。 Form Recognizer サービスで現在サポートされている事前構築済みモデルのモデルの ID を次に示します。

* **prebuilt-invoice**: 請求書からテキスト、選択マーク、テーブル、キーと値のペア、およびキー情報を抽出します。
* **prebuilt-businessCard**: 名刺からテキストとキー情報を抽出します。
* **prebuilt-idDocument**: 運転免許証と国際パスポートからテキストとキー情報を抽出します。
* **prebuilt-receipt**: レシートからテキストとキー情報を抽出します。

### <a name="add-the-following-code-to-your-prebuilt-invoice-application-main-method"></a>事前構築済みの請求書アプリケーションの **Main** メソッドに次のコードを追加します

```csharp
// sample invoice document
string filePath = "(https://raw.githubusercontent.com/Azure-Samples/cognitive-services-REST-api-samples/master/curl/form-recognizer/sample-invoice.pdf";

using var stream = new FileStream(filePath, FileMode.Open);

AnalyzeDocumentOperation operation = await client.StartAnalyzeDocumentAsync("prebuilt-invoice", stream);

await operation.WaitForCompletionAsync();

AnalyzeResult result = operation.Value;

for (int i = 0; i < result.Documents.Count; i++)
{
    Console.WriteLine($"Document {i}:");

    AnalyzedDocument document = result.Documents[i];

    if (document.Fields.TryGetValue("VendorName", out DocumentField vendorNameField))
    {
        if (vendorNameField.ValueType == DocumentFieldType.String)
        {
            string vendorName = vendorNameField.AsString();
            Console.WriteLine($"Vendor Name: '{vendorName}', with confidence {vendorNameField.Confidence}");
        }
    }

    if (document.Fields.TryGetValue("CustomerName", out DocumentField customerNameField))
    {
        if (customerNameField.ValueType == DocumentFieldType.String)
        {
            string customerName = customerNameField.AsString();
            Console.WriteLine($"Customer Name: '{customerName}', with confidence {customerNameField.Confidence}");
        }
    }

    if (document.Fields.TryGetValue("Items", out DocumentField itemsField))
    {
        if (itemsField.ValueType == DocumentFieldType.List)
        {
            foreach (DocumentField itemField in itemsField.AsList())
            {
                Console.WriteLine("Item:");

                if (itemField.ValueType == DocumentFieldType.Dictionary)
                {
                    IReadOnlyDictionary<string, DocumentField> itemFields = itemField.AsDictionary();

                    if (itemFields.TryGetValue("Description", out DocumentField itemDescriptionField))
                    {
                        if (itemDescriptionField.ValueType == DocumentFieldType.String)
                        {
                            string itemDescription = itemDescriptionField.AsString();

                            Console.WriteLine($"  Description: '{itemDescription}', with confidence {itemDescriptionField.Confidence}");
                        }
                    }

                    if (itemFields.TryGetValue("Amount", out DocumentField itemAmountField))
                    {
                        if (itemAmountField.ValueType == DocumentFieldType.Double)
                        {
                            double itemAmount = itemAmountField.AsDouble();

                            Console.WriteLine($"  Amount: '{itemAmount}', with confidence {itemAmountField.Confidence}");
                        }
                    }
                }
            }
        }
    }

    if (document.Fields.TryGetValue("SubTotal", out DocumentField subTotalField))
    {
        if (subTotalField.ValueType == DocumentFieldType.Double)
        {
            double subTotal = subTotalField.AsDouble();
            Console.WriteLine($"Sub Total: '{subTotal}', with confidence {subTotalField.Confidence}");
        }
    }

    if (document.Fields.TryGetValue("TotalTax", out DocumentField totalTaxField))
    {
        if (totalTaxField.ValueType == DocumentFieldType.Double)
        {
            double totalTax = totalTaxField.AsDouble();
            Console.WriteLine($"Total Tax: '{totalTax}', with confidence {totalTaxField.Confidence}");
        }
    }

    if (document.Fields.TryGetValue("InvoiceTotal", out DocumentField invoiceTotalField))
    {
        if (invoiceTotalField.ValueType == DocumentFieldType.Double)
        {
            double invoiceTotal = invoiceTotalField.AsDouble();
            Console.WriteLine($"Invoice Total: '{invoiceTotal}', with confidence {invoiceTotalField.Confidence}");
        }
    }
}

```

## <a name="run-your-application"></a>アプリケーションを実行する

### <a name="net-command-line-interface-cli"></a>[.NET コマンド ライン インターフェイス (CLI)](#tab/cli)

コマンド プロンプトを開き、目的のプロジェクトが含まれているディレクトリに移動し、次を入力します。

```console
dotnet run formrecognizer-quickstart.dll
```

### <a name="visual-studio"></a>[Visual Studio](#tab/vs)

プログラムをビルドして実行するには、formRecognizer_quickstart の横にある緑色の **[スタート]** ボタンを選択するか、**F5** キーを押します。

  :::image type="content" source="../media/quickstarts/run-visual-studio.png" alt-text="スクリーンショット: Visual Studioプログラムの実行。":::

---

おめでとうございます。 このクイックスタートでは、Form Recognizer C# SDK を使用して、さまざまな方法でフォームとドキュメントを分析しました。 次に、Form Recognizer API の詳細を把握するためにリファレンス ドキュメントを探索します。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [REST API v3.0 リファレンス ドキュメント](https://westus.dev.cognitive.microsoft.com/docs/services/form-recognizer-api-v3-0-preview-1/operations/AnalyzeDocument)