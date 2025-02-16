---
title: 'Train Model (モデルのトレーニング): コンポーネント リファレンス'
titleSuffix: Azure Machine Learning
description: Azure Machine Learning で **モデルのトレーニング** コンポーネントを使用して、分類または回帰モデルをトレーニングする方法について説明します。
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: likebupt
ms.author: keli19
ms.date: 05/10/2021
ms.openlocfilehash: a0954bc577e7712b12885ddb354ee48c925f5599
ms.sourcegitcommit: e41827d894a4aa12cbff62c51393dfc236297e10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2021
ms.locfileid: "131565738"
---
# <a name="train-model-component"></a>モデルのトレーニング コンポーネント

この記事では Azure Machine Learning デザイナーのコンポーネントについて説明します。

分類または回帰モデルをトレーニングするには、このコンポーネントを使用します。 トレーニングは、モデルを定義してそのパラメーターを設定した後に行います。トレーニングには、タグ付けされたデータが必要です。 **モデルのトレーニング** を使用して、既存のモデルを新しいデータで再トレーニングすることもできます。 

## <a name="how-the-training-process-works"></a>トレーニング プロセスのしくみ

通常、Azure Machine Learning における機械学習モデルの作成と使用は、3 つのステップから成るプロセスです。 

1. 特定の種類のアルゴリズムを選択し、そのパラメーターまたはハイパーパラメーターを定義してモデルを構成します。 次のいずれかの種類のモデルを選択します。 

    + **分類** モデル: ニューラル ネットワーク、デシジョン ツリー、デシジョン フォレストなどのアルゴリズムに基づくモデルです。
    + **回帰** モデル: 標準線形回帰のほか、ニューラル ネットワークやベイジアン回帰といったアルゴリズムを使用できます。  

2. ラベル付けされていて、かつアルゴリズムに適合したデータを含んだデータセットを指定します。 データとモデルの両方を **モデルのトレーニング** に接続してください。

    トレーニングからは、データから学習した統計的パターンをカプセル化した特定のバイナリ形式 (iLearner) が生成されます。 この形式を直接変更したり読み取ったりすることはできません。ただし、このトレーニング済みのモデルは、他のコンポーネントから使用することができます。 
    
    モデルのプロパティを確認することもできます。 詳細については、「結果」セクションを参照してください。

3. トレーニングが完了したら、いずれかの[スコアリング コンポーネント](./score-model.md)でトレーニング済みのモデルを使用し、新しいデータの予測を行います。

## <a name="how-to-use-train-model"></a>[モデルのトレーニング] の使用方法 
    
1. **モデルのトレーニング** コンポーネントをパイプラインに追加します。  **[Machine Learning]** カテゴリの下でこのコンポーネントを見つけることができます。 **[トレーニング]** を展開し、**モデルのトレーニング** コンポーネントをパイプラインにドラッグします。
  
1.  左側の入力に、トレーニングされていないモードをアタッチします。 **モデルのトレーニング** の右側の入力にトレーニング データセットをアタッチします。

    トレーニング データセットには、ラベル列が含まれている必要があります。 ラベルのない行は無視されます。
  
1.  **[ラベル列]** について、コンポーネントの右パネルの **[列の編集]** をクリックし、モデルがトレーニングに使用できる結果を含む 1 つの列を選択します。
  
    - 分類問題の場合、ラベル列には **カテゴリ** 値または **離散** 値が含まれている必要があります。 たとえば、Yes/No 評価や疾患分類コード (または名前)、所得層が該当します。  非カテゴリ列を選んだ場合、トレーニング中にコンポーネントからエラーが返されます。
  
    -   回帰問題の場合、ラベル列には、応答変数を表す **数値** データが含まれている必要があります。 連続スケールを表す数値データが理想です。 
    
    たとえば、信用リスク スコアや、ハード ドライブの推定故障時間、特定の日時におけるコール センターの推定着信数が該当します。  数値列を選択しなかった場合、エラーが返されます。
  
    -   使用するラベル列を指定しなかった場合、Azure Machine Learning は、データセットのメタデータを使用して適切なラベル列の推測を試みます。 間違った列が選択された場合は、列セレクターを使用して修正してください。
  
    > [!TIP] 
    > 列セレクターの使い方のヒントについては、「[Select Columns in Dataset (データセットの列を選択する)](./select-columns-in-dataset.md)」の記事を参照してください。 **[WITH RULES]\(規則を使用\)** オプションと **[名前別]** オプションの使い方についてのヒントといくつかの一般的なシナリオが取り上げられています。
  
1.  パイプラインを送信します。 データの量が多いと、しばらく時間がかかる場合があります。

    > [!IMPORTANT] 
    > 各行の ID となる ID 列がある場合、あるいは、テキスト列に含まれる一意の値が多すぎる場合、**モデルのトレーニング** が原因で、"列: "{column_name}" 内の一意の値の数が許可されている数を超えています" などのエラーが発生することがあります。
    >
    > これは、列が一意の値のしきい値に達し、メモリが不足する場合があるためです。 [メタデータの編集](edit-metadata.md)を使用してその列を **[Clear feature]\(特徴のクリア\)** としてマークできます。テキスト列を事前処理する目的でトレーニングや[テキストからの N-gram 特徴抽出コンポーネント](extract-n-gram-features-from-text.md)で使用されることがありません。 エラーの詳細については、[デザイナーのエラー コード](././designer-error-codes.md)に関する記事を参照してください。

## <a name="model-interpretability"></a>モデルの解釈可能性

モデルの解釈可能性により、ML モデルを理解し、人間が理解できる方法で意思決定の基礎を提示する可能性が提供されます。

現在、**モデルのトレーニング** コンポーネントでは、[ML モデルを説明するための解釈可能性パッケージの使用がサポートされています](../how-to-machine-learning-interpretability-aml.md#generate-feature-importance-values-via-remote-runs)。 次の組み込みアルゴリズムがサポートされています。

- 線形回帰
- ニューラル ネットワーク回帰
- 増幅デシジョン ツリーの回帰
- デシジョン フォレスト回帰
- ポワソン回帰
- 2 クラスのロジスティック回帰
- 2 クラス サポート ベクター マシン
- 2 クラスの増幅デシジョン ツリー
- 2 クラス デシジョン フォレスト
- 多クラス デシジョン フォレスト
- 多クラス ロジスティック回帰
- 多クラス ニューラル ネットワーク

モデルの説明を生成するには、モデルのトレーニング コンポーネントでモデルの **[モデルの説明]** のドロップダウン リストから **[True]** を選択します。 **モデルのトレーニング** コンポーネントでは、これは既定で False に設定されています。 説明を生成するには、追加のコンピューティング コストが必要であることにご注意ください。

![モデルの説明チェックボックスを示すスクリーンショット](./media/module/train-model-explanation-checkbox.png)

パイプラインの実行が完了したら、**モデルのトレーニング** コンポーネントの右側のウィンドウにある **[説明]** タブにアクセスし、モデルのパフォーマンス、データセット、および特徴量の重要度を調べることができます。

![モデルの説明グラフを示すスクリーンショット](./media/module/train-model-explanations-tab.gif)

Azure Machine Learning におけるモデルの説明を使用する方法の詳細については、[ML モデルの解釈](../how-to-machine-learning-interpretability-aml.md#generate-feature-importance-values-via-remote-runs)に関するハウツー記事を参照してください。

## <a name="results"></a>結果

モデルのトレーニング後、次の作業を行います。


+ 他のパイプラインでモデルを使用するには、コンポーネントを選択し、右側のパネルの **[出力]** タブの下にある **[データセットの登録]** アイコンをクリックします。 保存したモデルは、コンポーネント パレットの **[データセット]** からアクセスできます。

+ 新しい値の予測にモデルを使用するには、それを新しい入力データと共に[モデルのスコア付け](./score-model.md)コンポーネントに接続します。


## <a name="next-steps"></a>次の手順

Azure Machine Learning で[使える一連のコンポーネント](component-reference.md)を参照してください。