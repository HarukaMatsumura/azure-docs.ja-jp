---
title: Kubernetes と Helm と共に Computer Vision コンテナーを使用する
titleSuffix: Azure Cognitive Services
description: Kubernetes と Helm を使用して、Computer Vision コンテナーをデプロイする方法について説明します。
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: conceptual
ms.date: 04/01/2020
ms.author: aahi
ms.openlocfilehash: 9a8e0dde8b24c39180a584c26af725ab82ea0176
ms.sourcegitcommit: 829d951d5c90442a38012daaf77e86046018e5b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "90907103"
---
# <a name="use-computer-vision-container-with-kubernetes-and-helm"></a>Kubernetes と Helm と共に Computer Vision コンテナーを使用する

オンプレミスの Computer Vision コンテナーを管理するための 1 つの方法は、Kubernetes と Helm を使用することです。 Kubernetes と Helm を使用して Computer Vision コンテナー イメージを定義し、Kubernetes パッケージを作成します。 このパッケージは、オンプレミスの Kubernetes クラスターに展開されます。 最後に、デプロイされたサービスをテストする方法を検討します。 Kubernetes オーケストレーションを使用せずに Docker コンテナーを実行する方法の詳細については、「[Computer Vision コンテナーをインストールして実行する](computer-vision-how-to-install-containers.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

オンプレミスの Computer Vision コンテナーを使用する前の前提条件は次のとおりです。

| 必須 | 目的 |
|----------|---------|
| Azure アカウント | Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント][free-azure-account] を作成してください。 |
| Kubernetes CLI | コンテナー レジストリからの共有資格情報を管理するには、[Kubernetes CLI][kubernetes-cli] が必要です。 また、Kubernetes は、Kubernetes のパッケージ マネージャーである Helm の前に必要です。 |
| Helm CLI | Helm Chart (コンテナー パッケージ定義) のインストールに使用される [Helm CLI][helm-install] をインストールします。 |
| Computer Vision リソース |コンテナーを使用するためには、以下が必要です。<br><br>Azure **Computer Vision** リソースとその関連する API キーおよびエンドポイント URI。 どちらの値も、対象リソースの概要ページとキー ページで使用でき、コンテナーを開始するために必要です。<br><br>**{API_KEY}** : **[キー]** ページにある 2 つの利用可能なリソース キーのどちらか<br><br>**{ENDPOINT_URI}** : **[概要]** ページに提示されているエンドポイント|

[!INCLUDE [Gathering required parameters](../containers/includes/container-gathering-required-parameters.md)]

### <a name="the-host-computer"></a>ホスト コンピューター

[!INCLUDE [Host Computer requirements](../../../includes/cognitive-services-containers-host-computer.md)]

### <a name="container-requirements-and-recommendations"></a>コンテナーの要件と推奨事項

[!INCLUDE [Container requirements and recommendations](includes/container-requirements-and-recommendations.md)]

## <a name="connect-to-the-kubernetes-cluster"></a>Kubernetes クラスターに接続する

ホスト コンピューターには使用可能な Kubernetes クラスターがあることが想定されます。 ホスト コンピューターへの Kubernetes クラスターの展開方法の概念を理解するには、[Kubernetes クラスターの展開](../../aks/tutorial-kubernetes-deploy-cluster.md)に関するこのチュートリアルをご覧ください。 デプロイの詳細については、[Kubernetes のドキュメント](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)をご覧ください。

### <a name="sharing-docker-credentials-with-the-kubernetes-cluster"></a>Kubernetes クラスターと Docker の資格情報を共有する

Kubernetes クラスターで `containerpreview.azurecr.io` コンテナー レジストリの構成済みイメージに対して `docker pull` を実行できるようにするには、Docker の資格情報をクラスターに転送する必要があります。 下の [`kubectl create`][kubectl-create] コマンドを実行し、コンテナー レジストリのアクセスの前提条件から提供された資格情報に基づいて、"*docker-registry シークレット*" を作成します。

適切なコマンド ライン インターフェイスから、次のコマンドを実行します。 `<username>`、`<password>`、`<email-address>` は、コンテナー レジストリの資格情報に置き換えてください。

```console
kubectl create secret docker-registry containerpreview \
    --docker-server=containerpreview.azurecr.io \
    --docker-username=<username> \
    --docker-password=<password> \
    --docker-email=<email-address>
```

> [!NOTE]
> `containerpreview.azurecr.io` コンテナー レジストリへのアクセス権が既にある場合は、代わりに汎用フラグを使って Kubernetes シークレットを作成できます。 Docker 構成 JSON に対して実行する次のコマンドを検討してください。
> ```console
>  kubectl create secret generic containerpreview \
>      --from-file=.dockerconfigjson=~/.docker/config.json \
>      --type=kubernetes.io/dockerconfigjson
> ```

シークレットが正常に作成されると、次の出力がコンソールに表示されます。

```console
secret "containerpreview" created
```

シークレットが作成されたことを確認するには、`secrets` フラグを指定して [`kubectl get`][kubectl-get] を実行します。

```console
kubectl get secrets
```

`kubectl get secrets` を実行すると、構成されているすべてのシークレットが表示されます。

```console
NAME                  TYPE                                  DATA      AGE
containerpreview      kubernetes.io/dockerconfigjson        1         30s
```

## <a name="configure-helm-chart-values-for-deployment"></a>展開に対する Helm チャートの値を構成する

まず、*read* という名前のフォルダを作成します。 次に、次の YAML コンテンツを `chart.yaml` という名前の新しいファイルに貼り付けます。

```yaml
apiVersion: v2
name: read
version: 1.0.0
description: A Helm chart to deploy the microsoft/cognitive-services-read to a Kubernetes cluster
dependencies:
- name: rabbitmq
  condition: read.image.args.rabbitmq.enabled
  version: ^6.12.0
  repository: https://kubernetes-charts.storage.googleapis.com/
- name: redis
  condition: read.image.args.redis.enabled
  version: ^6.0.0
  repository: https://kubernetes-charts.storage.googleapis.com/
```

Helm チャートの既定値を構成するために、次の YAML をコピーし、`values.yaml` という名前のファイルに貼り付けます。 `# {ENDPOINT_URI}` と `# {API_KEY}` のコメントを独自の値に置き換えます。 必要に応じて、resultExpirationPeriod、Redis、RabbitMQ を構成します。

```yaml
# These settings are deployment specific and users can provide customizations

read:
  enabled: true
  image:
    name: cognitive-services-read
    registry:  containerpreview.azurecr.io/
    repository: microsoft/cognitive-services-read
    tag: latest
    pullSecret: containerpreview # Or an existing secret
    args:
      eula: accept
      billing: # {ENDPOINT_URI}
      apikey: # {API_KEY}
      
      # Result expiration period setting. Specify when the system should clean up recognition results.
      # For example, resultExpirationPeriod=1, the system will clear the recognition result 1hr after the process.
      # resultExpirationPeriod=0, the system will clear the recognition result after result retrieval.
      resultExpirationPeriod: 1
      
      # Redis storage, if configured, will be used by read container to store result records.
      # A cache is required if multiple read containers are placed behind load balancer.
      redis:
        enabled: false # {true/false}
        password: password

      # RabbitMQ is used for dispatching tasks. This can be useful when multiple read containers are
      # placed behind load balancer.
      rabbitmq:
        enabled: false # {true/false}
        rabbitmq:
          username: user
          password: password
```

> [!IMPORTANT]
> - `billing` 値と `apikey` 値が指定されていない場合、サービスは 15 分後に期限切れになります。 さらに、サービスが利用できないため、検証は失敗します。
> 
> - Docker Compose または Kubernetes の下など、ロード バランサーの背後に複数の読み取りコンテナーをデプロイする場合は、外部キャッシュが必要です。 処理コンテナーと GET 要求コンテナーは同じではない可能性があるため、外部キャッシュに結果が保存され、コンテナー間で共有されます。 キャッシュ設定の詳細については、「[Computer Vision Docker コンテナーを構成する](https://docs.microsoft.com/azure/cognitive-services/computer-vision/computer-vision-resource-container-config)」をご覧ください。
>

*read* ディレクトリの下に *templates* フォルダーを作成します。 次の YAML をコピーし、`deployment.yaml` という名前のファイルに貼り付けます。 `deployment.yaml` ファイルは Helm テンプレートとして機能します。

> テンプレートによってマニフェスト ファイルが生成されます。マニフェスト ファイルは、Kubernetes が理解できる YAML 形式のリソース記述です。 [- Helm チャート テンプレート ガイド][chart-template-guide]

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: read
  labels:
    app: read-deployment
spec:
  selector:
    matchLabels:
      app: read-app
  template:
    metadata:
      labels:
        app: read-app       
    spec:
      containers:
      - name: {{.Values.read.image.name}}
        image: {{.Values.read.image.registry}}{{.Values.read.image.repository}}
        ports:
        - containerPort: 5000
        env:
        - name: EULA
          value: {{.Values.read.image.args.eula}}
        - name: billing
          value: {{.Values.read.image.args.billing}}
        - name: apikey
          value: {{.Values.read.image.args.apikey}}
        args:        
        - ReadEngineConfig:ResultExpirationPeriod={{ .Values.read.image.args.resultExpirationPeriod }}
        {{- if .Values.read.image.args.rabbitmq.enabled }}
        - Queue:RabbitMQ:HostName={{ include "rabbitmq.hostname" . }}
        - Queue:RabbitMQ:Username={{ .Values.read.image.args.rabbitmq.rabbitmq.username }}
        - Queue:RabbitMQ:Password={{ .Values.read.image.args.rabbitmq.rabbitmq.password }}
        {{- end }}      
        {{- if .Values.read.image.args.redis.enabled }}
        - Cache:Redis:Configuration={{ include "redis.connStr" . }}
        {{- end }}
      imagePullSecrets:
      - name: {{.Values.read.image.pullSecret}}      
--- 
apiVersion: v1
kind: Service
metadata:
  name: read-service
spec:
  type: LoadBalancer
  ports:
  - port: 5000
  selector:
    app: read-app
```

同じ *templates* フォルダーで、次のヘルパー関数をコピーして `helpers.tpl` に貼り付けます。 `helpers.tpl` には、Helm テンプレートの生成に役立つ便利な関数が定義されています。

```yaml
{{- define "rabbitmq.hostname" -}}
{{- printf "%s-rabbitmq" .Release.Name -}}
{{- end -}}

{{- define "redis.connStr" -}}
{{- $hostMaster := printf "%s-redis-master:6379" .Release.Name }}
{{- $hostSlave := printf "%s-redis-slave:6379" .Release.Name -}}
{{- $passWord := printf "password=%s" .Values.read.image.args.redis.password -}}
{{- $connTail := "ssl=False,abortConnect=False" -}}
{{- printf "%s,%s,%s,%s" $hostMaster $hostSlave $passWord $connTail -}}
{{- end -}}
```
テンプレートでは、ロード バランサー サービスと、読み取り用のコンテナー/イメージのデプロイが指定されています。

### <a name="the-kubernetes-package-helm-chart"></a>Kubernetes パッケージ (Helm チャート)

"*Helm チャート*" には、`containerpreview.azurecr.io` コンテナー レジストリからプルする Docker イメージの構成が含まれます。

> [Helm チャート][helm-charts] は、関連する Kubernetes リソースのセットが記述されているファイルのコレクションです。 1 つのチャートを使って、memcached ポッドのような単純なものや、HTTP サーバー、データベース、キャッシュなどを含む完全な Web アプリ スタックのような複雑なものを、展開できます。

提供されている "*Helm チャート*" では、Computer Vision サービスと対応するサービスの Docker イメージが、`containerpreview.azurecr.io` コンテナー レジストリからプルされます。

## <a name="install-the-helm-chart-on-the-kubernetes-cluster"></a>Kubernetes クラスターに Helm チャートをインストールする

"*Helm チャート*" をインストールするには、[`helm install`][helm-install-cmd] コマンドを実行する必要があります。 必ず `read` フォルダーの上のディレクトリから install コマンドを実行します。

```console
helm install read ./read
```

インストールが正常に実行されると表示される出力の例を次に示します。

```console
NAME: read
LAST DEPLOYED: Thu Sep 04 13:24:06 2019
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Pod(related)
NAME                    READY  STATUS             RESTARTS  AGE
read-57cb76bcf7-45sdh   0/1    ContainerCreating  0         0s

==> v1/Service
NAME     TYPE          CLUSTER-IP    EXTERNAL-IP  PORT(S)         AGE
read     LoadBalancer  10.110.44.86  localhost    5000:31301/TCP  0s

==> v1beta1/Deployment
NAME    READY  UP-TO-DATE  AVAILABLE  AGE
read    0/1    1           0          0s
```

Kubernetes の展開が完了するには数分かかります。 ポッドとサービスの両方が適切に展開されて使用可能なことを確認するには、次のコマンドを実行します。

```console
kubectl get all
```

次のような出力結果が表示されます。

```console
kubectl get all
NAME                        READY   STATUS    RESTARTS   AGE
pod/read-57cb76bcf7-45sdh   1/1     Running   0          17s

NAME                   TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
service/kubernetes     ClusterIP      10.96.0.1      <none>        443/TCP          45h
service/read           LoadBalancer   10.110.44.86   localhost     5000:31301/TCP   17s

NAME                   READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/read   1/1     1            1           17s

NAME                              DESIRED   CURRENT   READY   AGE
replicaset.apps/read-57cb76bcf7   1         1         1       17s
```
<!--  ## Validate container is running -->

[!INCLUDE [Container's API documentation](../../../includes/cognitive-services-containers-api-documentation.md)]

## <a name="next-steps"></a>次のステップ

Azure Kubernetes Service (AKS) での Helm を使用したアプリケーションのインストールについて詳しくは、[こちらをご覧ください][installing-helm-apps-in-aks]。

> [!div class="nextstepaction"]
> [Cognitive Services コンテナー][cog-svcs-containers]

<!-- LINKS - external -->
[free-azure-account]: https://azure.microsoft.com/free
[git-download]: https://git-scm.com/downloads
[azure-cli]: https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest
[docker-engine]: https://www.docker.com/products/docker-engine
[kubernetes-cli]: https://kubernetes.io/docs/tasks/tools/install-kubectl
[helm-install]: https://helm.sh/docs/using_helm/#installing-helm
[helm-install-cmd]: https://helm.sh/docs/intro/using_helm/#helm-install-installing-a-package
[helm-charts]: https://helm.sh/docs/topics/charts/
[kubectl-create]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[helm-test]: https://helm.sh/docs/helm/#helm-test
[chart-template-guide]: https://helm.sh/docs/chart_template_guide

<!-- LINKS - internal -->
[vision-container-host-computer]: computer-vision-how-to-install-containers.md#the-host-computer
[installing-helm-apps-in-aks]: ../../aks/kubernetes-helm.md
[cog-svcs-containers]: ../cognitive-services-container-support.md
