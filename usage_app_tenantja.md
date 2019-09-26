---
layout: contents
language: ja
title: App Tenant
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_app_tenant.html
lang_opp_word: To English
prev_url: usage_app_commonja.html
prev_string: App Common
top_url: usage_appja.html
top_string: Web Application
next_url: usage_app_resourceja.html
next_string: App Resource
---

# テナント（TENANT）
K2HR3 Webアプリケーションで使用するテナント（TENANT）の操作の説明をします。

### テナント（TENANT）について
K2HR3システムは、OpenStackもしくは他のユーザ認証システムと連携して動作できます。  
OpenStackと連携している場合、K2HR3のテナント（TENANT）は、IaaS（OpenStack）にてユーザ（USER）が属しているテナント（もしくはプロジェクト）のことを指します。  
ユーザ認証システムと連携している場合は、その認証システムでユーザ（USER）が属している（スコープされた）グループを指します。

## テナント（TENANT）の選択
K2HR3 Webアプリケーションにアクセスし、サインインした直後、以下の画面が表示されます。  

![K2HR3 Usage Application - Select Tenant](images/usage_app_tenant_unselect.png)

リソース（RESOURCE）、ポリシー/ルール（POLICY）、ロール（ROLE）、サービス（SERVICE）の操作をするためには、まずこれらが属するテナント（TENANT）を選択する必要があります。  
以下の手順で、テナント（TENANT）を選択します。  
1. テナント（TENANT）を選択するには、**[TENANT] Unselected**と表示されている横のボタン ![K2HR3 Select Tenant Button](images/button_tenant_select.png) をクリックします。
1. サインインしているユーザ（USER）が属しているテナント（TENANT）の一覧が表示されます。
1. いずれかのテナント（TENANT）を選択します。

![K2HR3 Usage Application - Select Tenant](images/usage_app_tenant_select.png)

テナント（TENANT）が選択されると、そのテナント（TENANT）に登録されているリソース（RESOURCE）、ポリシー/ルール（POLICY）、ロール（ROLE）、サービス（SERVICE）の情報が表示され、利用できるようになります。

![K2HR3 Usage Application - Selected Tenant](images/usage_app_tenant_selected.png)

