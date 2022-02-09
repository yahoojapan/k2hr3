---
layout: contents
language: ja
title: Setup by Helm
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup_helm_chartja.html
lang_opp_word: To Japanese
prev_url: setup_integrate.html
prev_string: Integrated installation
top_url: setup.html
top_string: Setup
next_url: 
next_string: 
---

# Setup by Helm
You can easily install a K2HR3 system in a kubernetes environment by using **K2HR3 Helm Chart**.  

[K2HR3 Helm Chart](https://k2hr3.antpick.ax/helm_chart.html) is one of **Helm Chart** for installing a K2HR3 system using [Helm(The package manager for Kubernetes)](https://helm.sh/) in a [kubernetes](https://kubernetes.io/) environment.  

**K2HR3 Helm Chart** is one of **Helm Chart** used by [Helm (The package manager for Kubernetes)](https://helm.sh/).  
**K2HR3 Helm Chart** is published as a Chart repository at [K2HR3 Helm Chart repository](https://helm.k2hr3.antpick.ax/) and [Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3).  

You can install a K2HR3 system easily, by using the `Helm command` and loading the **K2HR3 Helm Chart** published in [Artifact Hub](https://artifacthub.io/packages/helm/k2hr3/k2hr3) as a repository.  

The source code of K2HR3 Helm Chart is published in [k2hr3_helm_chart -Github](https://github.com/yahoojapan/k2hr3_helm_chart).　　

## Overview
This page describes how to install a K2HR3 system from **K2HR3 Helm Chart** using the `Helm command`.  

### About kubernetes environment
At first, prepare or use the kubernetes cluster as the environment for installing the K2HR3 system.  
If you don't have a kubernetes cluster available, you can also use [minikube](https://minikube.sigs.k8s.io/docs/) to prepare your kubernetes environment.  

## Preparing the Helm
To use **K2HR3 Helm Chart**, you need [Helm (The package manager for Kubernetes)](https://helm.sh/).  

**K2HR3 Helm Chart** is compatible with **Helm3**(version 3), but Helm2 is **not supported**.  

First, install [Helm](https://helm.sh/).  
See [Helm Installation](https://helm.sh/docs/intro/install/) for the exact installation method.  

Install Helm on the host as follows:  
```
$ curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

After installation, try to run the version option etc. and check whichever the installation is succeed.  
```
$ helm version
  version.BuildInfo{Version:"v3.7.1", GitCommit:"1d11fcb5d3f3bf00dbe6fe31b8412839a96b3dc4", GitTreeState:"clean", GoVersion:"go1.16.9"}
```

## Repository registration
From [Artifact Hub(Helm Hub)](https://artifacthub.io/packages/helm/k2hr3/k2hr3), find **K2HR3 Helm Chart** and register that Chart repository as the `local repository`.  
```
$ helm search hub k2hr3
  URL                                               CHART VERSION  APP VERSION  DESCRIPTION
  https://artifacthub.io/packages/helm/k2hr3/k2hr3  1.0.0          1.0.0        K2HR3 Helm Chart - K2HR3(K2Hdkc based Resource ...
```

From the above results, check [https://artifacthub.io/packages/helm/k2hr3/k2hr3](https://artifacthub.io/packages/helm/k2hr3/k2hr3) page.  
There is a **INSTALL** link on the left side of this page, click on it to copy the example command and run it.  
```
$ helm repo add k2hr3 https://helm.k2hr3.antpick.ax/
  "k2hr3" has been added to your repositories
```

This completes the repository registration.  

## Install K2HR3 Helm Chart
Install(build) the K2HR3 system in the kubernetes environment using the registered **K2HR3 Helm Chart**.  
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
See [Usage - Helm Char](helm_chart.html) for the **options** that you can specify when installing the K2HR3 Helm Chart.  

The options specified in the above example are required at installation.  

If you are using the [minikube](https://minikube.sigs.k8s.io/docs/), add the following options to the above command and execute.  
```
--set minikube=true
```

If the above `helm install` completes successfully, you will see the following` NOTES`.  
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

If you are using the [minikube](https://minikube.sigs.k8s.io/docs/), the above `NOTES` will have **[0] You are using minikube** as shown below.  
```
  [0] You are using minikube
      You need to use a browser to access the K2HR3 Cluster running
      inside minikube.
      Therefore, enable socat to forward HTTPS requests as shown
      below.(You can also use something other than socat.)
  
      socat TCP-LISTEN:32443,fork TCP:$(minikube ip):32443
      socat TCP-LISTEN:31443,fork TCP:$(minikube ip):31443
```

If you are using the [minikube](https://minikube.sigs.k8s.io/docs/), set the proxy as shown in the following example.  
It is because the outside host(or browser) needs to access to the K2HR3 system inside `minikube`.  
```
$ socat TCP-LISTEN:32443,fork TCP:$(minikube ip):32443 &
$ socat TCP-LISTEN:31443,fork TCP:$(minikube ip):31443 &
```

The `socat` is used in the above example, but you can also use another proxy tools.  

## Test - helm test
After installing K2HR3 Helm Chart, please wait a moment for the K2HR3 system to boot (it maybe 1 or 2 minutes).  
After that, you can check whether the installation was completed normally with the following command.  
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

If the K2HR3 system has booted normally, you can use the `kubectl` command to verify that the pod has booted.  
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

## Try to Use
Access the installed K2HR3 system from a browser etc. and check its operation.  

The `NOTES` displayed after installing shows the URLs to the K2HR3 Web Application and the K2HR3 REST API.  
You can check the operation by directly accessing these URLs from a browser or the like.  
```
  K2HR3 API:
    https://< host fqdn (ex. myhost.antpick.ax) >:31443/
  K2HR3 APP:
    https://< host fqdn (ex. myhost.antpick.ax) >:32443/
```

### Attention
The K2HR3 system being installed uses a self-signed certificate.  
When accessing with a browser etc., a message such as `Insecure access` will be displayed.  
Please check how to use your browser and avoid it as appropriate.  

## End a chapter
With the above procedure, you can install a K2HR3 system using the **K2HR3 Helm Chart** easily.  

For how to use the built K2HR3 system, see [How to use K2HR3 Web Application](https://k2hr3.antpick.ax/usage_app.html) and [How to use K2HR3 REST API](https://k2hr3.antpick.ax/api.html).  
