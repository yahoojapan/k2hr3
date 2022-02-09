---
layout: contents
language: ja
title: Setup
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: setup.html
lang_opp_word: To English
prev_url: usageja.html
prev_string: Usage
top_url: indexja.html
top_string: TOP
next_url: developerja.html
next_string: Developer
---

# セットアップ

このページでは、K2HR3 システムのセットアップ方法を説明します。  

## K2HR3 システムの構成

以下の構成例は、[OpenStack](https://www.openstack.org/)と連携するK2HR3システムです。  
最小構成の試用環境や、[kubernetes](https://kubernetes.io/ja/)環境への構築もほぼ同じ構成となります。  

![K2HR3 Setup overview](images/setup_overview.png)

## セットアップ手順

K2HR3 システムは、IaaS環境（ベアメタル、[OpenStack](https://www.openstack.org/)、[kubernetes](https://kubernetes.io/ja/)）に応じて構築することができます。
試用環境、およびIaaS環境に応じたセットアップの手順を以下に示します。

- [試用環境の構築](setup_trialja.html) （OpenStack対応）  
[OpenStack](https://www.openstack.org/)（[devpack](https://github.com/yahoojapan/k2hr3_utils/tree/master/devpack)で構築したOpenStackを含む）に 最小限のK2HR3システムを簡単に構築し、試すことができます。  
- K2HR3 サブシステムを[手動セットアップ](setup_manualja.html)  
K2HR3 システムは、いくつかのサブシステムにより構成されています。  
各サブシステムを構築する手順を説明します。  
- K2HR3 システムを[統合セットアップ](setup_integrateja.html)  
K2HR3 システムは、いくつかのサブシステムにより構成されています。  
これらのサブシステムを一括で設定し、K2HR3システムを構築します。
- K2HR3 システムを[Helmを使ってセットアップ](setup_helm_chartja.html)
K2HR3 システムを [Helm](https://helm.sh/ja/)（Kubernetes用パッケージマネージャー） を使って構築します。  
K2HR3 システムを kubernetes環境に簡単にセットアップできます。
