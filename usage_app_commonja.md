---
layout: contents
language: ja
title: App Common
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_app_common.html
lang_opp_word: To English
prev_url: 
prev_string: 
top_url: usage_appja.html
top_string: Web Application
next_url: usage_app_tenantja.html
next_string: App Tenant
---

# 共通
K2HR3 Webアプリケーションの共通操作の説明をします。

### アクセス方法
K2HR3 WebサーバーとしてセットアップしたURIにアクセスすることで、K2HR3 Webアプリケーションが表示されます。  
```
http(s)://<k2hr3 web server fqdn[:port]>/
```

## Webアプリケーション画面
K2HR3 Webアプリケーションにアクセスすると、以下の画面が表示されます。  

![K2HR3 Usage Application - Signout](images/usage_app_signout.png)

上記の画面は、ユーザ（USER）がまだログインしていない状態です。

## サインイン
K2HR3 Webアプリケーションにサインインするには、右上のログインボタン ![K2HR3 Signin Button](images/button_signin.png) をクリックします。  
メニューが表示されますので、**Sign in** を選択してください。  

K2HR3システムのユーザ認証が、クレデンシャルに設定されている場合は、以下に示すダイアログが表示されます。  
他のユーザ認証を使うように設定されている場合は、その設定に応じた動作をします。  

表示されるダイアログに、ユーザ名、パスフレーズを入力し、サインインしてください。  

![K2HR3 Usage Application - Signin](images/usage_app_signin.png)

### ユーザ（USER）について
K2HR3システムは、OpenStackもしくは他のユーザ認証システムと連携して動作できます。  
K2HR3のユーザ（USER）は、OpenStackのユーザ、もしくは他のユーザ認証システムのユーザを意味しています。  
サインインするには、K2HR3システムが連携しているOpenStackもしくは他のユーザ認証システムのユーザとパスフレーズを使ってください。

## ユーザアカウント情報
K2HR3 Webアプリケーションにサインインした後、ユーザアカウント情報を表示できます。  
以下のように、ユーザアカウント情報を表示できます。  

![K2HR3 Usage Application - User Account Information](images/usage_app_user_account.png)

このダイアログの中には、ユーザ名と、ユーザの`Unscoped Token`が表示されます。

## サインアウト
K2HR3 Webアプリケーションからサインアウトするには、右上の![K2HR3 Signin Button](images/button_signout.png)ボタンをクリックします。  
メニューが表示されますので、**Sign out**を選択してください。

