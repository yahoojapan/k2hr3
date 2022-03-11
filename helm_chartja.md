---
layout: contents
language: ja
title: Helm Chart
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: helm_chart.html
lang_opp_word: To English
prev_url: clija.html
prev_string: Command Line Interface
top_url: usageja.html
top_string: Usage
next_url: rancher_helm_chartja.html
next_string: RANCHER Helm Chart
---

# Helm Chart
K2HR3 Helm Chartは、[kubernetes](https://kubernetes.io/ja/)環境に [Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー） を使って **K2HR3システム** を構築するための **Helm Chart** です。  

## 概要
**K2HR3 Helm Chart** を使うことで、簡単にkubernetes環境へK2HR3システムの構築ができます。  

**K2HR3 Helm Chart** は、[Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー）に対応した **Helm Chart**です。  
**K2HR3 Helm Chart** は、Chartリポジトリを [K2HR3 Helm Chart repository](https://helm.k2hr3.antpick.ax/) で公開し、[Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) に登録しています。  

`Helmコマンド` を使って、[Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) で公開されている **K2HR3 Helm Chart**をリポジトリとしてロードし、簡単にK2HR3システムの構築ができます。  

K2HR3 Helm Chartのソースコードは、[k2hr3_helm_chart - Github](https://github.com/yahoojapan/k2hr3_helm_chart)で公開されています。

### RANCHER対応
**K2HR3 Helm Chart**は、**RANCHER Helm Chart** として利用できます。  
[RANCHER](https://www.rancher.co.jp/)のリポジトリに登録し、K2HR3システムを簡単に構築できます。  
[RANCHER](https://www.rancher.co.jp/)からの利用方法は、[こちら](rancher_helm_chartja.html)を参照してください。  

## Helmについて
K2HR3 Helm Chartは、[Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー）が利用する **Helm Chart** です。  

K2HR3 Helm Chartは、[Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) で公開されており、どこからでも利用できます。  

Helmの使い方については、[こちら](https://helm.sh/ja/)を参照してください。

`Helmコマンド`を使い、**K2HR3 Helm Chart**からK2HR3システムを構築する方法は、[こちら](setup_helm_chartja.html)を参照してください。  

## K2HR3 Helm Chart オプション
K2HR3 Helm Chart を [Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー）を使い、インストール（`helm install`）するときに、オプションを指定できます。

以下に、**K2HR3 Helm Chart** が提供するオプションの一覧を以下に示します。  


| オプション名                 | 必須     | 初期値                                                 |
|------------------------------|----------|--------------------------------------------------------|
| `nameOverride`               |          | `k2hr3`                                                |
| `fullnameOverride`           |          | n/a                                                    |
| `serviceAccount.create`      |          | true                                                   |
| `serviceAccount.annotations` |          | {}                                                     |
| `serviceAccount.name`        |          | ""                                                     |
| `antpickax.configDir`        |          | "/etc/antpickax"                                       |
| `antpickax.certPeriodYear`   |          | 5                                                      |
| `minikube`                   |          | false                                                  |
| `k2hr3.clusterName`          |          | ""                                                     |
| `k2hr3.startManual`          |          | false                                                  |
| `k2hr3.baseDomain`           |          | ""                                                     |
| `k2hr3.dkc.baseName`         |          | ""                                                     |
| `k2hr3.dkc.count`            |          | 2                                                      |
| `k2hr3.api.baseName`         |          | ""                                                     |
| `k2hr3.api.count`            |          | 2                                                      |
| `k2hr3.api.extHostname`      |          | ""                                                     |
| `k2hr3.api.extPort`          |          | 0                                                      |
| `k2hr3.app.baseName`         |          | ""                                                     |
| `k2hr3.app.count`            |          | 2                                                      |
| `k2hr3.app.extHostname`      |          | ""                                                     |
| `k2hr3.app.extPort`          |          | 0                                                      |
| `mountPoint.configMap`       |          | "/configmap"                                           |
| `mountPoint.ca`              |          | "/secret-ca"                                           |
| `k8s.namespace`              |          | ""                                                     |
| `k8s.domain`                 |          | "svc.cluster.local"                                    |
| `k8s.caCert`                 |          | "/var/run/secrets/kubernetes.io/serviceaccount/ca.crt" |
| `k8s.saToken`                |          | "/var/run/secrets/kubernetes.io/serviceaccount/token"  |
| `k8s.apiUrl`                 |          | "https://kubernetes.default.svc"                       |
| `oidc.clientId`              | **必須** | n/a                                                    |
| `oidc.clientSecret`          | **必須** | n/a                                                    |
| `oidc.cookieExpire`          | **必須** | n/a                                                    |
| `oidc.cookieName`            | **必須** | n/a                                                    |
| `oidc.issuerUrl`             | **必須** | n/a                                                    |
| `oidc.usernameKey`           |          | ""                                                     |
| `unconvertedFiles.k2hr3`     |          | files/*.sh                                             |
| `convertedFiles.k2hr3`       |          | files/*.sh                                             |

各々のオプションの説明をします。

### nameOverride
`fullnameOverride`オプションが指定されていない場合、完全な名前のリリース部分をオーバーライドします。  
本オプションを省略した場合、`k2hr3`をデフォルト値として使います。  

### fullnameOverride
Chartのリリース名を（上書き）指定します。  
本オプションを省略した場合、未指定（空文字列）となります。  

### serviceAccount.create
kubernetesのサービスアカウントを作成するかどうかを指定します。  
本オプションを省略した場合、`true`をデフォルト値として使います。  

### serviceAccount.annotations
kubernetesサービスアカウントを作成する場合、そのサービスアカウントに設定する`annotations`をオブジェクトで指定します。  
本オプションを省略した場合、`{}`（空オブジェクト）をデフォルト値として使います。  

### serviceAccount.name
kubernetesサービスアカウントを作成する場合、そのサービスアカウント名を指定します。この値が空の場合、サービスアカウントは作成されません。  
本オプションを省略した場合、未指定（空文字列）となります。  

### antpickax.configDir
K2HR3システムで使用するコンフィグレーションファイルのあるディレクトリパスを指定します。  
本オプションを省略した場合、`/etc/antpickax` をデフォルト値として使います。  

### antpickax.certPeriodYear
K2HR3システム内部で作成し、利用するTLS自己署名証明書（CA証明書含む）の有効期間（年）を指定します。  
本オプションを省略した場合、`5（年）` をデフォルト値として使います。  

### minikube
`minikube`環境に構築する場合には、このオプションに`true`を指定します。  
本オプションを省略した場合、`false` をデフォルト値として使い、`minikube`環境では**ない**ものとしてインストールが実行されます。  

### k2hr3.clusterName
K2HR3システムのクラスター名を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、クラスター名は Helm Chartの リリース名（`.Release.Name`）が使われます。  

### k2hr3.startManual
K2HR3システムを構築するときに、各K2HR3システムコンポーネント（K2HR3 Web Appilcation / K2HR3 REST API）を手動で起動するか否かを指定します。  
本オプションを省略した場合、`false`となり、自動で構築されます。  
このオプションは、開発者向けのオプションです。  

### k2hr3.baseDomain
K2HR3システムのkubernetesクラスター内でのベースドメイン名を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、 `k8s.domain` の値が使用されます。  

### k2hr3.dkc.baseName
K2HR3システムのバックエンドとして構築されるK2HDKCクラスターのベース名を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、 `r3dkc` が使用されます。  

### k2hr3.dkc.count
K2HR3システムのバックエンドとして構築されるK2HDKCクラスターのサーバ数を指定します。  
本オプションを省略した場合、サーバー数は`2`となります。

### k2hr3.api.baseName
K2HR3システムのREST APIサーバーのベース名を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、 `r3api` が使用されます。  

### k2hr3.api.count
K2HR3システムのREST APIのサーバ数を指定します。  
本オプションを省略した場合、サーバー数は`2`となります。

### k2hr3.api.extHostname
K2HR3システムのREST APIサーバーのkubernetesクラスター外部からのアクセスするためのホスト名（FQDN）を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、 kubernetes内部で使用されるホスト名（FQDN）が使用されます。  
本オプションには、K2HR3システムがkubernetesクラスター内に構築された場合の `NodePort`へアクセスできるホスト名（主にNodeホスト名）を指定してください。  
`minikube`を利用している場合、`minikube`を起動したホスト名を指定するようにしてください。  

### k2hr3.api.extPort
K2HR3システムのREST APIサーバーのkubernetesクラスター外部からのアクセスするためのポート番号を指定します。  
本オプションを省略した場合、未指定（`0`）となり、`31443` ポートが使用されます。  

### k2hr3.app.baseName
K2HR3システムのWeb Applicationサーバーのベース名を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、 `r3app` が使用されます。  

### k2hr3.app.count
K2HR3システムのWeb Applicationのサーバ数を指定します。  
本オプションを省略した場合、サーバー数は`2`となります。

### k2hr3.app.extHostname
K2HR3システムのWeb Applicationサーバーのkubernetesクラスター外部からのアクセスするためのホスト名（FQDN）を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、 kubernetes内部で使用されるホスト名（FQDN）が使用されます。  
本オプションには、K2HR3システムがkubernetesクラスター内に構築された場合の `NodePort`へアクセスできるホスト名（主にNodeホスト名）を指定してください。  
`minikube`を利用している場合、`minikube`を起動したホスト名を指定するようにしてください。  

### k2hr3.app.extPort
K2HR3システムのWeb Applicationサーバーのkubernetesクラスター外部からのアクセスするためのポート番号を指定します。  
本オプションを省略した場合、未指定（`0`）となり、`32443` ポートが使用されます。  

### mountPoint.configMap
構築するK2HR3システムの各コンテナーが利用する `configMap`をマウントするディレクトリパスを指定します。  
本オプションを省略した場合、`/configmap` が使用されます。  

### mountPoint.ca
構築するK2HR3システムで使用する自己署名CA証明書とその秘密鍵を保管するディレクトリパスを指定します。  
本オプションを省略した場合、`/secret-ca` が使用されます。  

### k8s.namespace
K2HR3システムを構築するkubernetesクラスターで使用する `namespace`（名前空間） を指定します。  
本オプションを省略した場合、未指定（空文字列）となり、`.Release.Namespace` が使われます。  

### k8s.domain
K2HR3システムを構築するkubernetesクラスターのドメイン名を指定します。  
本オプションを省略した場合、`svc.cluster.local` が使用されます。  

### k8s.caCert
K2HR3システムを構築するkubernetesクラスターのCA証明書のファイルパスを指定します。  
本オプションを省略した場合、`/var/run/secrets/kubernetes.io/serviceaccount/ca.crt` が使用されます。  

### k8s.saToken
K2HR3システムを構築するkubernetesクラスターのサービスアカウントのトークンファイルパスを指定します。  
本オプションを省略した場合、`/var/run/secrets/kubernetes.io/serviceaccount/token` が使用されます。  

### k8s.apiUrl
K2HR3システムを構築するkubernetesクラスターのAPIエンドポイントを指定します。  
本オプションを省略した場合、`https://kubernetes.default.svc` が使用されます。  

### oidc.clientId [必須]
構築するK2HR3システムの認証で使う `OpenID Connect`（OIDC）のクライアントID（`Client ID`）を指定します。  
このオプションは必須であり、省略はできません。  
このHelm Chartで構築されるK2HR3システムは、`OpenID Connect`（OIDC）による認証を行うことを前提としていますので、このオプションは必ず指定しなくてはなりません。  

### oidc.clientSecret [必須]
構築するK2HR3システムの認証で使う `OpenID Connect`（OIDC）の `Secret` を指定します。  
このオプションは必須であり、省略はできません。  
このHelm Chartで構築されるK2HR3システムは、`OpenID Connect`（OIDC）による認証を行うことを前提としていますので、このオプションは必ず指定しなくてはなりません。  

### oidc.cookieExpire [必須]
構築するK2HR3システムの認証で使う `OpenID Connect`（OIDC）の `Cookie有効期限` を指定します。  
このオプションは必須であり、省略はできません。  
このHelm Chartで構築されるK2HR3システムは、`OpenID Connect`（OIDC）による認証を行うことを前提としていますので、このオプションは必ず指定しなくてはなりません。  

### oidc.cookieName [必須]
構築するK2HR3システムの認証で使う `OpenID Connect`（OIDC）の `Cookie名`を指定します。  
このオプションは必須であり、省略はできません。  
このHelm Chartで構築されるK2HR3システムは、`OpenID Connect`（OIDC）による認証を行うことを前提としていますので、このオプションは必ず指定しなくてはなりません。  

### oidc.issuerUrl [必須]
構築するK2HR3システムの認証で使う `OpenID Connect`（OIDC）の発行者URL（`Issure URL`）を指定します。  
このオプションは必須であり、省略はできません。  
このHelm Chartで構築されるK2HR3システムは、`OpenID Connect`（OIDC）による認証を行うことを前提としていますので、このオプションは必ず指定しなくてはなりません。  

### oidc.usernameKey
構築するK2HR3システムの認証で使う `OpenID Connect`（OIDC）にユーザ名が実装されている場合、そのユーザ名を示すキー名を指定します。  
このオプションは省略でき、省略された場合、ユーザ名を示すキーは存在しないものとしてK2HR3システムは動作します。  

### unconvertedFiles.k2hr3
構築するK2HR3システムが使う `configMap`に登録するファイル（加工なし）を指定します。  
通常、この値を変更する必要はなく、省略することができます。  
省略した場合には、このHelm Chartの持つ `files` ディレクトリ以下のファイルが `configMap` として配置されます。  

### convertedFiles.k2hr3
構築するK2HR3システムが使う `configMap`に登録するファイル（加工あり）を指定します。  
通常、この値を変更する必要はなく、省略することができます。  
省略した場合には、このHelm Chartの持つ `files` ディレクトリ以下のファイルが `configMap` として配置されます。  
