---
layout: contents
language: ja
title: Setup by Helm
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_helm_chart.html
lang_opp_word: To English
prev_url: setup_integrateja.html
prev_string: Integrated installation
top_url: setupja.html
top_string: Setup
next_url: 
next_string: 
---

# Setup by Helm
**K2HR3 Helm Chart** を使うことで、簡単にkubernetes環境へK2HR3システムの構築ができます。  

K2HR3 Helm Chartは、[kubernetes](https://kubernetes.io/ja/)環境に [Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー） を使って **K2HR3システム** を構築するための **Helm Chart** です。  

**K2HR3 Helm Chart** は、[Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー）に対応した **Helm Chart**です。  
**K2HR3 Helm Chart** は、Chartリポジトリを [K2HR3 Helm Chart repository](https://helm.k2hr3.antpick.ax/) で公開し、[Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) に登録しています。  

[Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) で公開されている **K2HR3 Helm Chart**を使い、`Helmコマンド` を使って、簡単にK2HR3システムの構築ができます。  

K2HR3 Helm Chartのソースコードは、[k2hr3_helm_chart - Github](https://github.com/yahoojapan/k2hr3_helm_chart)で公開されています。

## 概要
このページでは、`Helmコマンド`を使い、**K2HR3 Helm Chart**からK2HR3システムを構築する方法を説明します。  

### kubernetes環境について
K2HR3システムを構築する環境として、kubernetes環境（クラスター）を準備、もしくはそれを使える必要があります。  
利用できるkubernetes環境をお持ちでない場合、[minikube](https://minikube.sigs.k8s.io/docs/)を使い、kubernetes環境を準備できます。  

## Helmコマンドの準備
**K2HR3 Helm Chart** を利用するには、[Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー）が必要となります。  

**K2HR3 Helm Chart** は、**Helm3**（バージョン3）に対応してます。（Helm2には対応していませんので、注意してください。）  

まず、[Helm](https://helm.sh/ja/) のインストールをしてください。  
正確なインストール方法は、[Helmのインストール](https://helm.sh/ja/docs/intro/install/)を参照するようにしてください。  

以下のようにして、HelmをHelmコマンドを実行するホストにインストールします。  
```
$ curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

インストール後、バージョンなどを実行し、そのインストールが正常に行われているか確認してください。  
```
$ helm version
  version.BuildInfo{Version:"v3.7.1", GitCommit:"1d11fcb5d3f3bf00dbe6fe31b8412839a96b3dc4", GitTreeState:"clean", GoVersion:"go1.16.9"}
```

## Helmリポジトリの登録
[Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) (Helm Hub)から、**K2HR3 Helm Chart**を見つけ、このChartをローカルの`repo`に登録します。  
```
$ helm search hub k2hr3
  URL                                               CHART VERSION  APP VERSION  DESCRIPTION
  https://artifacthub.io/packages/helm/k2hr3/k2hr3  1.0.0          1.0.0        K2HR3 Helm Chart - K2HR3(K2Hdkc based Resource ...
```

上記の結果から、[https://artifacthub.io/packages/helm/k2hr3/k2hr3](https://artifacthub.io/packages/helm/k2hr3/k2hr3) を確認します。  
このページの左側に **INSTALL**リンクがありますので、それをクリックしてコマンド例をコピーし、実行してください。
```
$ helm repo add k2hr3 https://helm.k2hr3.antpick.ax/
  "k2hr3" has been added to your repositories
```

以上で、リポジトリの登録が完了します。

## Helmインストール
登録した **K2HR3 Helm Chart** を使い、kubernetes環境に K2HR3システムをインストール（構築）します。  

```
$ helm install my-k2hr3 k2hr3/k2hr3 --version 1.0.0 \
    --set k2hr3.api.extHostname=< host fqdn (ex. myhost.antpick.ax) > \
    --set k2hr3.app.extHostname=< host fqdn (ex. myhost.antpick.ax) > \
    --set oidc.clientId=< OIDC Client ID >                            \
    --set oidc.clientSecret=< OIDC Client Secret >                    \
    --set oidc.cookieExpire=120                                       \
    --set oidc.cookieName=id_token                                    \
    --set oidc.issuerUrl=< OIDC Issuer URL >
```
K2HR3 Helm Chartをインストールするときに指定できる **オプション** については、[こちら](helm_chartja.html) を参照してください。  

上記で指定しているオプションは、構築時に必要となる必須オプションです。  

[minikube](https://minikube.sigs.k8s.io/docs/)環境を使っている場合には、上記のコマンドに以下のオプションを加えて実行してください。  
```
--set minikube=true
```

上記の`helm install`が正常に完了すると、以下の`NOTES`が表示されます。  
```
  NAME: my-k2hr3
  LAST DEPLOYED: Wed Feb  9 17:51:41 2022
  NAMESPACE: default
  STATUS: deployed
  REVISION: 1
  NOTES:
  -----------------------------------------------------------------
                       CONGRATULATIONS!
  
  The my-k2hr3 K2HR3 Cluster for K2HDKC DBaaS has been started.
  
  Follow the steps below to complete the K2HR3 Cluster setup.
  
  [1] Check my-k2hr3 K2HR3 Cluster
      At first, check if you have access to the K2HR3 Cluster.
      Please access the following URL after a while after starting.
  
      K2HR3 API:
        https://< host fqdn (ex. myhost.antpick.ax) >:31443/
  
      K2HR3 APP:
        https://< host fqdn (ex. myhost.antpick.ax) >:32443/
  
      [NOTE]
        Since a self-signed certificate is used, a certificate
        exception will occur, so please access accordingly.
  
  [2] Get K2HR3 Unscoped Token
      After completing the above checks, log in to your K2HR3 Cluster.
  
      After logging in, select the [Account] -> [About Account]
      menu to display the [Account Information] dialog.
      Make a copy of the [Unscoped Token] in this displayed dialog.
      Use this value when setting up K2HDKC DBaaS.
  
  Next, use Helm to launch K2HDKC DBaaS.
```

[minikube](https://minikube.sigs.k8s.io/docs/)環境を使っている場合には、上記の`NOTES`に、以下に示す **[0] You are using minikube** が表示されます。  
```
  [0] You are using minikube
      You need to use a browser to access the K2HR3 Cluster running
      inside minikube.
      Therefore, enable socat to forward HTTPS requests as shown
      below.(You can also use something other than socat.)
  
      socat TCP-LISTEN:32443,fork TCP:$(minikube ip):32443
      socat TCP-LISTEN:31443,fork TCP:$(minikube ip):31443
```

[minikube](https://minikube.sigs.k8s.io/docs/)環境を使っている場合には、この例のように、外部からHelmコマンドを実行したホスト（minikubeを実行しているホスト）を通してminikube内のリソースにアクセスできるようにしてください。  
```
$ socat TCP-LISTEN:32443,fork TCP:$(minikube ip):32443 &
$ socat TCP-LISTEN:31443,fork TCP:$(minikube ip):31443 &
```

上記の例では、`socat`を使っていますが、他のproxyができるツールを使うこともできます。  

## 確認（helm test）
Helmインストール後に、K2HR3システムが起動するまで少し待ってください。（数分）  
その後、インストールが正常に完了したかどうかは、以下のコマンドで確認できます。  
```
$ helm test my-k2hr3
  NAME: my-k2hr3
  LAST DEPLOYED: Wed Feb  9 17:51:41 2022
  NAMESPACE: default
  STATUS: deployed
  REVISION: 1
  TEST SUITE:     pod-r3-check-my-k2hr3
  Last Started:   Wed Feb  9 18:10:42 2022
  Last Completed: Wed Feb  9 18:10:45 2022
  Phase:          Succeeded
  NOTES:
  -----------------------------------------------------------------
  ...
  ...
```

正常にK2HR3システムが起動している場合には、以下のようにPodの起動を確認できます。
```
$ kubectl get pods
  NAME                                  READY   STATUS    RESTARTS   AGE
  pod-r3api-my-k2hr3-0                  2/2     Running   0          20m
  pod-r3api-my-k2hr3-1                  2/2     Running   0          19m
  pod-r3app-my-k2hr3-5cc8cbf6ff-nqwbw   1/1     Running   0          20m
  pod-r3app-my-k2hr3-5cc8cbf6ff-pgq44   1/1     Running   0          20m
  pod-r3dkc-my-k2hr3-0                  2/2     Running   0          20m
  pod-r3dkc-my-k2hr3-1                  2/2     Running   0          19m
```

## 確認
構築したK2HR3システムにブラウザなどからアクセスし、その動作を確認してください。

構築後に表示される `NOTES` には、K2HR3 Web Application および K2HR3 REST API へのURLが表示されます。  
```
  K2HR3 API:
    https://< host fqdn (ex. myhost.antpick.ax) >:31443/
  K2HR3 APP:
    https://< host fqdn (ex. myhost.antpick.ax) >:32443/
```

ブラウザなどから、これらのURLに直接アクセスして動作を確認することができます。

### 注意
構築されるK2HR3システムは、自己署名証明書を使っています。  
ブラウザなどでアクセスする場合、`安全ではないアクセス` などの表示がされます。  
お使いのブラウザの使い方を確認し、適宜アクセスするようにしてください。  

## 完了
以上の手順で、**K2HR3 Helm Chart**により、K2HR3システムの構築ができます。  

構築したK2HR3システムの使い方については、[K2HR3 Web Application の使い方](https://k2hr3.antpick.ax/usage_appja.html) や [K2HR3 REST API の使い方](https://k2hr3.antpick.ax/apija.html) を参照してください。  
