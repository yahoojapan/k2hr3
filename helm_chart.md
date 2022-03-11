---
layout: contents
language: en-us
title: Helm Chart
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: helm_chartja.html
lang_opp_word: To Japanese
prev_url: cli.html
prev_string: Command Line Interface
top_url: usage.html
top_string: Usage
next_url: rancher_helm_chart.html
next_string: RANCHER Helm Chart
---

# Helm Chart
[K2HR3 Helm Chart](https://k2hr3.antpick.ax/helm_chart.html) is a **Helm Chart** for building a K2HR3 system using [Helm(The package manager for Kubernetes)](https://helm.sh/) in a [kubernetes](https://kubernetes.io/) environment.  

## Overview
You can easily install a K2HR3 system in a kubernetes environment by using **K2HR3 Helm Chart**.  

**K2HR3 Helm Chart** is one of **Helm Chart** used by [Helm (The package manager for Kubernetes)](https://helm.sh/).  
**K2HR3 Helm Chart** is published as a Chart repository at [K2HR3 Helm Chart repository](https://helm.k2hr3.antpick.ax/) and [Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3).  

You can install a K2HR3 system easily, by using the `Helm command` and loading the **K2HR3 Helm Chart** published in [Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) as a repository.  

The source code of K2HR3 Helm Chart is published in [k2hr3_helm_chart -Github](https://github.com/yahoojapan/k2hr3_helm_chart).　　

### RANCHER
The [K2HR3 Helm Chart](rancher_helm_chart.html) is used as **RANCHER Helm Chart**.  
You can easily build up a K2HR3 system by registering it in the [RANCHER](https://rancher.com/) repository.  
Please refer to [K2HR3 Helm Chart with RANCHER](rancher_helm_chart.html) for how to use from [RANCHER](https://rancher.com/).  

## About Helm
The K2HR3 Helm Chart is one of **Helm Chart** used by [Helm (The package manager for Kubernetes)](https://helm.sh/).  

The K2HR3 Helm Chart is published at [Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) and can be used from anywhere.  

See "[Helm docuuments](https://helm.sh/)" for how to use Helm.  

See [Setup by Helm](setup_helm_chartja.html) for information on how to install a K2HR3 system by using `Helm command` with **K2HR3 Helm Chart**.  

## Options for K2HR3 Helm Chart
You can specify options when installing(`helm install`) the K2HR3 Helm Chart using [Helm (The package manager for Kubernetes)](https://helm.sh/).  

Below is a list of the options offered by the **K2HR3 Helm Chart**.  

| Options                      | Required     | Default value                                          |
|------------------------------|--------------|--------------------------------------------------------|
| `nameOverride`               |              | `k2hr3`                                                |
| `fullnameOverride`           |              | n/a                                                    |
| `serviceAccount.create`      |              | true                                                   |
| `serviceAccount.annotations` |              | {}                                                     |
| `serviceAccount.name`        |              | ""                                                     |
| `antpickax.configDir`        |              | "/etc/antpickax"                                       |
| `antpickax.certPeriodYear`   |              | 5                                                      |
| `minikube`                   |              | false                                                  |
| `k2hr3.clusterName`          |              | ""                                                     |
| `k2hr3.startManual`          |              | false                                                  |
| `k2hr3.baseDomain`           |              | ""                                                     |
| `k2hr3.dkc.baseName`         |              | ""                                                     |
| `k2hr3.dkc.count`            |              | 2                                                      |
| `k2hr3.api.baseName`         |              | ""                                                     |
| `k2hr3.api.count`            |              | 2                                                      |
| `k2hr3.api.extHostname`      |              | ""                                                     |
| `k2hr3.api.extPort`          |              | 0                                                      |
| `k2hr3.app.baseName`         |              | ""                                                     |
| `k2hr3.app.count`            |              | 2                                                      |
| `k2hr3.app.extHostname`      |              | ""                                                     |
| `k2hr3.app.extPort`          |              | 0                                                      |
| `mountPoint.configMap`       |              | "/configmap"                                           |
| `mountPoint.ca`              |              | "/secret-ca"                                           |
| `k8s.namespace`              |              | ""                                                     |
| `k8s.domain`                 |              | "svc.cluster.local"                                    |
| `k8s.caCert`                 |              | "/var/run/secrets/kubernetes.io/serviceaccount/ca.crt" |
| `k8s.saToken`                |              | "/var/run/secrets/kubernetes.io/serviceaccount/token"  |
| `k8s.apiUrl`                 |              | "https://kubernetes.default.svc"                       |
| `oidc.clientId`              | **required** | n/a                                                    |
| `oidc.clientSecret`          | **required** | n/a                                                    |
| `oidc.cookieExpire`          | **required** | n/a                                                    |
| `oidc.cookieName`            | **required** | n/a                                                    |
| `oidc.issuerUrl`             | **required** | n/a                                                    |
| `oidc.usernameKey`           |              | ""                                                     |
| `unconvertedFiles.k2hr3`     |              | files/*.sh                                             |
| `convertedFiles.k2hr3`       |              | files/*.sh                                             |

Below is a description of each option.  

### nameOverride
If the `fullnameOverride` option is not specified, it overrides the release part of the full name.  
If this option is omitted, `k2hr3` will be used as the default value.  

### fullnameOverride
Specify(overwrite) the release name of the Chart.  
If this option is omitted, it will be used empty string.  

### serviceAccount.create
Specifies whether to create a kubernetes service account.  
If this option is omitted, `true` is used as the default value.  

### serviceAccount.annotations
When you create a kubernetes service account, specify the `annotations` to set for that service account in the object.  
If this option is omitted, `{}`(empty object) will be used as the default value.  

### serviceAccount.name
When you create a kubernetes service account, specify the service account name.  
If this value is not specified, no service account will be created.  
If this option is omitted, it will be used empty string.  

### antpickax.configDir
Specifies the directory path where the configuration files used by the K2HR3 system are located.  
If this option is omitted, `/etc/antpickax` will be used as the default value.  

### antpickax.certPeriodYear
Specify the validity period(year) of the TLS self-signed certificate (including CA certificate) created and used inside the K2HR3 system.  
If this option is omitted, `5(year)` is used as the default value.  

### minikube
Specify `true` for this option when installing in a `minikube` environment.  
If this option is omitted, `false` will be used as the default value and it means the installation will be executed on not a `minikube` environment.  

### k2hr3.clusterName
Specifies the cluster name for the K2HR3 system.  
If this option is omitted, it will be used empty string and the cluster name will be set release name(`.Release.Name`) of Helm Chart.  

### k2hr3.startManual
Specifies whether to manually launch each K2HR3 system component(K2HR3 Web Appilcation / K2HR3 REST API) when building the K2HR3 system.  
If this option is omitted, it will be `false` and will be installed automatically.  
This option is for developers.  

### k2hr3.baseDomain
Specifies the base domain name of the K2HR3 system within the kubernetes cluster.  
If this option is omitted, it will be used empty string and the value of `k8s.domain` will be used.  

### k2hr3.dkc.baseName
Specifies the base name of the K2HDKC cluster that will be built as the backend for the K2HR3 system.  
If this option is omitted, it will be used empty string and `r3dkc` will be used.  

### k2hr3.dkc.count
Specifies the number of servers in the K2HDKC cluster that will be built as the backend for the K2HR3 system.  
If this option is omitted, the number of servers will be `2`.  

### k2hr3.api.baseName
Specifies the base name of the REST API server for the K2HR3 system.  
If this option is omitted, it will be used empty string and `r3api` will be used.  

### k2hr3.api.count
Specifies the number of REST API servers in the K2HR3 system.  
If this option is omitted, the number of servers will be `2`.  

### k2hr3.api.extHostname
Specifies the host name(FQDN) for access from outside the kubernetes cluster to the REST API server on the K2HR3 system.  
If this option is omitted, it will be used empty string and the host name(FQDN) used `inside kubernetes cluster` will be used.  
For this option, specify a host name(mainly the Node host name) that can access `NodePort` of kubernetes cluster.  
If you are using `minikube`, be sure to specify the host name that run `minikube`.  

### k2hr3.api.extPort
Specifies the port number for access from outside the kubernetes cluster to the REST API server on the K2HR3 system.  
If this option is omitted, it will be used `0` and the `31443` port will be used.  

### k2hr3.app.baseName
Specifies the base name of the Web Application server for the K2HR3 system.  
If this option is omitted, it will be used empty string and `r3app` will be used.  

### k2hr3.app.count
Specifies the number of Web Application servers in the K2HR3 system.  
If this option is omitted, the number of servers will be `2`.  

### k2hr3.app.extHostname
Specifies the host name(FQDN) for access from outside the kubernetes cluster to the Web Application server on the K2HR3 system.  
If this option is omitted, it will be used empty string and the host name(FQDN) used `inside kubernetes cluster` will be used.  
For this option, specify a host name(mainly the Node host name) that can access `NodePort` of kubernetes cluster.  
If you are using `minikube`, be sure to specify the host name that run `minikube`.  

### k2hr3.app.extPort
Specifies the port number for access from outside the kubernetes cluster to the Web Application server on the K2HR3 system.  
If this option is omitted, it will be used `0` and the `32443` port will be used.  

### mountPoint.configMap
Specifies the directory path to mount the `configMap` used by each container on the K2HR3 system you are installing.  
If this option is omitted, `/configmap` will be used.  

### mountPoint.ca
Specifies the directory path to store the self-signed CA certificate and private key used by the K2HR3 system to be installed.  
If this option is omitted, `/secret-ca` will be used.  

### k8s.namespace
Specifies the `namespace` of the kubernetes cluster for installing the K2HR3 system.  
If this option is omitted, it will be used empty string and `.Release.Namespace` will be used.  

### k8s.domain
Specifies the domain name of the kubernetes cluster that installs the K2HR3 system.  
If this option is omitted, `svc.cluster.local` will be used.  

### k8s.caCert
Specifies the file path of the CA certificate for the kubernetes cluster that installs the K2HR3 system.  
If this option is omitted, `/var/run/secrets/kubernetes.io/serviceaccount/ca.crt` will be used.  

### k8s.saToken
Specifies the token file path for the service account of the kubernetes cluster that installs the K2HR3 system.  
If this option is omitted, `/var/run/secrets/kubernetes.io/serviceaccount/token` will be used.  

### k8s.apiUrl
Specifies the API endpoint for the kubernetes cluster that installs the K2HR3 system.  
If this option is omitted, `https://kubernetes.default.svc` will be used.  

### oidc.clientId `(Required)`
Specifies the `client ID` of `OpenID Connect`(OIDC) used to authenticate the K2HR3 system to be installed.  
This option is mandatory and cannot be omitted.  
The K2HR3 system installed by this Helm Chart expects to authenticate with `OpenID Connect`(OIDC), so this option must be specified.  

### oidc.clientSecret `(Required)`
Specifies the `Secret` of `OpenID Connect`(OIDC) used to authenticate the K2HR3 system to be installed.  
This option is mandatory and cannot be omitted.  
The K2HR3 system installed by this Helm Chart expects to authenticate with `OpenID Connect`(OIDC), so this option must be specified.  

### oidc.cookieExpire `(Required)`
Specifies the `Cookie expiration` of `OpenID Connect`(OIDC) used to authenticate the K2HR3 system to be installed.  
This option is mandatory and cannot be omitted.  
The K2HR3 system installed by this Helm Chart expects to authenticate with `OpenID Connect`(OIDC), so this option must be specified.  

### oidc.cookieName `(Required)`
Specifies the `Cookie name` of `OpenID Connect`(OIDC) used to authenticate the K2HR3 system to be installed.  
This option is mandatory and cannot be omitted.  
The K2HR3 system installed by this Helm Chart expects to authenticate with `OpenID Connect`(OIDC), so this option must be specified.  

### oidc.issuerUrl `(Required)`
Specifies the `Issure URL` of `OpenID Connect`(OIDC) used to authenticate the K2HR3 system to be installed.  
This option is mandatory and cannot be omitted.  
The K2HR3 system installed by this Helm Chart expects to authenticate with `OpenID Connect`(OIDC), so this option must be specified.  

### oidc.usernameKey
Specifies the `User name key` of `OpenID Connect`(OIDC) used to authenticate the K2HR3 system to be installed, if the OIDC has a key name that indicates the username.  
This option can be omitted, and if omitted the K2HR3 system behaves as if there is no user name key.  

### unconvertedFiles.k2hr3
Specify the file(without transformations) to be registered in the `configMap` used by the K2HR3 system to be built.  
Normally, you do not need to change this value and can omit it.  
If omitted, the files under the `files` directory of this Helm Chart will be placed as `configMap`.  

### convertedFiles.k2hr3
Specify the file(with transformations) to be registered in the `configMap` used by the K2HR3 system to be built.  
Normally, you do not need to change this value and can omit it.  
If omitted, the files under the `files` directory of this Helm Chart will be placed as `configMap`.  
