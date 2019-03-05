---
layout: contents
language: ja
title: App Role
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_app_role.html
lang_opp_word: To English
prev_url: usage_app_policyja.html
prev_string: App Policy-Rule
top_url: usage_appja.html
top_string: Web Application
next_url: usage_app_serviceja.html
next_string: App Service
---

# ロール（ROLE）
K2HR3 Webアプリケーションでのロール（ROLE）操作の説明をします。

## ロール（ROLE）の表示
テナント（TENANT）にまだロール（ROLE）が登録されていない場合（初めてK2HR3システムを利用する場合など）、まずロール（ROLE）の登録が必要となります。  
すでにロール（ROLE）が存在する場合、左側ツリー表示の中の**ROLE**を選択することで、登録済みのロール（ROLE）を見ることができます。  

![K2HR3 Usage Application - Role Top](images/usage_app_role_top.png)

## ロール（ROLE）の登録
ロール（ROLE）を登録するには、左側ツリー中の**ROLE**を選択した後、上部の**[ROLE]**横の ![K2HR3 Add Button](images/button_add.png)  ボタンをクリックします。  
_階層化したロール（ROLE）を登録する場合には、左側ツリーから親とする既存ロール（ROLE）を選択後、ボタンをクリックしてください。_  
ロール（ROLE）登録用のダイアログが表示されます。  

![K2HR3 Usage Application - Role Create Dialog](images/usage_app_role_add.png)

表示されたダイアログにロール（ROLE）名を入力し、 ![K2HR3 OK Button](images/button_ok.png)  ボタンをクリックすれば、ロール（ROLE）が登録されます。  
ダイアログに表示される項目とその内容を以下に示します。  
- TENANT  
ロール（ROLE）を登録するテナント（TENANT）名が表示されます。
- TYPE  
ロール（ROLE）であることを示す**role**が表示されます。
- PARENT PATH  
登録するロール（ROLE）の親の**[YRN](detail_variousja.html)パス**が表示されます。  
階層化していないトップレベル（親を持たない）のロール（ROLE）の場合、**/**と表示されます。  
親ロール（ROLE）の下に登録する場合には、その親ロール（ROLE）の**[YRN](detail_variousja.html)パス**が表示されます。  
たとえば、ロール（ROLE）名 **toplevel** の下にロール（ROLE）を登録する場合、**/toplevel** と表示されます。
- CREATE PATH  
登録するロール（ROLE）名を入力します。

登録されたロール（ROLE）は、左側ツリーの**ROLE**を展開することで確認できます。  

## ロール（ROLE）の編集
登録されているロール（ROLE）の内容を編集するには、まず編集するロール（ROLE）を左側ツリーで選択します。  
選択後、メインの画面エリアにそのロール（ROLE）の情報が表示されます。  
この表示されている内容を編集、およびデータの追加をします。  
編集後は、 ![K2HR3 SAVE Button](images/button_save.png)  ボタンをクリックし、その内容を保存します。  
編集を破棄する場合は、 ![K2HR3 CANCEL Button](images/button_cancel.png)  ボタンをクリックしてください。  

![K2HR3 Usage Application - Role Page](images/usage_app_role_all.png)

ロール（ROLE）選択後のメインの画面エリアに表示される項目について説明します。
- HOST NAMES  
ロール（ROLE）のメンバーとして登録されているFQDNで表現されたホスト（HOST）が列挙されます。  
  - HOST NAME  
    FQDNが表示されます。
  - AUX  
    付属情報として設定されている情報が表示されます。  
    詳しくは[付属情報（AUX）](detail_variousja.html)を参照してください。
- IP ADDRESSES  
ロール（ROLE）のメンバーとして登録されているIPアドレス表現されたホスト（HOST）が列挙されます。  
  - IP ADDRESSE  
    IPアドレスが表示されます。
  - AUX  
    付属情報として設定されている情報が表示されます。  
    詳しくは[付属情報（AUX）](detail_variousja.html)を参照してください。
- POLICIES  
登録されているポリシー/ルール（POLICY）の**[YRN](detail_variousja.html)フルパス**が列挙されます。  
編集・追加する場合にも、**[YRN](detail_variousja.html)フルパス**で入力します。
- ALIAS  
登録されているエリアス（ALIAS）が表示されます。  
エリアス（ALIAS）は他ロール（ROLE）への**[YRN](detail_variousja.html)フルパス**で表示されます。  
編集・追加する場合にも、**[YRN](detail_variousja.html)フルパス**で入力します。

## ロール（ROLE）の属性情報
登録されているロール（ROLE）の属性情報を表示するには、まずロール（ROLE）を左側ツリーで選択します。  
選択後、上部の**[ROLE]**左横の ![K2HR3 Path Button](images/button_path.png)  をクリックし、ロール（ROLE）の属性情報（Selected Path Information）ダイアログを表示します。  
このダイアログに、ロール（ROLE）の属性情報が表示されます。  

![K2HR3 Usage Application - Role Information](images/usage_app_role_info.png)

ロール（ROLE）の属性情報について説明します。
- TENANT  
ロール（ROLE）が属しているテナント（TENANT）名を表示します。
- TYPE  
"role"と表示します。
- PATH  
このロール（ROLE）への**[YRN](detail_variousja.html)フルパス**を表示します。  
この**[YRN](detail_variousja.html)フルパス**は、ロール（ROLE）のエリアス（ALIAS）等の設定を行うときに使います。
- ROLE TOKEN  
ロール（ROLE）のトークン（ [TOKEN](apija.html) ）を表示します。  
[K2HR3 REST API](apija.html)を使うときにこのトークンを指定します。  
詳細は、[K2HR3 REST API](apija.html)を参照してください。
- USER DATA SCRIPT  
ロール（ROLE）のメンバーであるホスト（HOST）をIaaS（OpenStack）と連携し、自動で登録する際に使う**USER DATA SCRIPT**です。  
"USER DATA SCRIPT"横にある![K2HR3 Copy Button](images/button_copy.png)ボタンをクリックすることで、**USER DATA SCRIPT**をコピーすることができます。  
この**USER DATA SCRIPT**のデータをOpenStackで仮想コンピューティング（Virtual Machine）を起動するときに指定してください。  
指定することにより、仮想コンピューティング（Virtual Machine）が起動したら自動的にそのホスト（HOST）のIPアドレスが、このロール（ROLE）のメンバーとして登録されます。  
以下は、OpenStackの**USER DATA SCRIPT**を指定するダイアログです。（バージョンにより多少異なります）  

![K2HR3 Usage Application - OpenStack User Data Script](images/usage_app_role_osuds.png)

