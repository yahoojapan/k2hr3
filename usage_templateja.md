---
layout: contents
language: ja
title: Template Engine
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_template.html
lang_opp_word: To English
prev_url: 
prev_string: 
top_url: usage_baseja.html
top_string: Basic Usage
next_url: 
next_string: 
---

# K2HR3 テンプレートエンジン

K2HR3システムは、動的なリソース（RESOURCE）を定義するときに利用できる **テンプレート（TEMPLATE）** 記法を提供します。  
このテンプレート（TEMPLATE）で記述された内容は、**K2HR3テンプレートエンジン** により展開されます。  
K2HR3テンプレートエンジンとテンプレート（TEMPLATE）について、以下に説明します。

# 適用
K2HR3システムでは、リソース（RESOURCE）データとして文字列を設定することができます。  
設定されている文字列は、ユーザ（USER）、ロール（ROLE）から読み出しができます。  
リソース（RESOURCE）に設定された文字列の読み出しにおいて、本仕様を満たしたテンプレートとして文字列を展開することができます。  

# 概要
K2HR3テンプレートエンジンの基本的な記述方法、仕様について説明します。

## テンプレート解析範囲
テンプレートとして読み込む文字列の中に、以下のキーワードで区切られた範囲（以下ステートメント）の文字列をK2HR3テンプレートエンジンが解析、展開します。
{% raw %}```
{{ .... }}
```{% endraw %}

## テンプレートエンジン指定
_この機能は現在プレースホルダとして予約されており、固定値（K2HR3テンプレートエンジン）のみサポートしています。_

テンプレートエンジンの指定を可能とするステートメントです。  
文字列の先頭から開始されている必要があります。  
K2HR3テンプレートエンジンを使用する場合には、省略してください。（もしくは例のように記述してください。）
- k2hr3テンプレートエンジン以外を指定する場合  
{% raw %}```
{{#!xxxxxxxxxxxxxx }}
```{% endraw %}
- k2hr3テンプレートエンジンを指定する場合  
{% raw %}```
{{#!k2hr3template }}
```{% endraw %}

## コメント指定
以下の記述のようにしたステートメントは、テンプレートエンジンにより展開された場合、出力（表示）されません。  
一般的なコメントとして利用するためのステートメントです。
{% raw %}```
{{# This is comment strings.... }}
```{% endraw %}

## 変数表示
以下のように記述することで、テンプレート内で利用している変数（後述）などの値を表示することができます。  
表示する変数は、定数を指定することもできます。
{% raw %}```
{{= 'print static string' }}
{{= true }}
{{= 1000 }}
{{= %variable% }}
```{% endraw %}

## エスケープ
テンプレートの解析範囲を指定するために利用されているキーワードをテンプレートとして認識したくない場合があります。  
また、文字列（後述）を指定するために利用されているキーワードをテンプレートとして認識したくない場合もあります。  
これらのエスケープする方法を以下に示します。
- {% raw %}{{{、}}}{% endraw %}  
{% raw %}{{ および }} のエスケープには、それぞれ {{{ と }}} と記述することで、 {{ もしくは }} に変換できますので、このエスケープを利用してください。{% endraw %}  
{% raw %}```
{{{ This is not statement }}}
```{% endraw %}
- シンクルクォート、ダブルクォート
ステートメント範囲の中で、文字列の指定をするためには、'...'もしくは、"..."と記述します。  
各々の範囲内で、それぞれのキーワードをエスケープするには、\ 記号を前置してください。  
```
"The \"test\" is in escaped quote."
```

## 定数
K2HR3テンプレートエンジンのサポートする定数を以下に示します。
- null
- true
- false

## 数値
K2HR3テンプレートエンジンのサポートする数値の表現には以下のような方法があります。
- 10進数  
0～9までの数字を任意数列挙してください。（例： 123456789）
- 16進数  
プレフィックスとして、0xもしくは x を指定して16進数を列挙してください。（例： 0xff）
- 8進数  
プレフィックスとして、0o を指定して0～7の数を列挙してください。（例： 0o1234）
- 2進数  
プレフィックスとして、0b を指定して0～1の数を列挙してください。（例： 0b1010）

## 文字列
ステートメント内に文字列を記述するには、シングルクォートもしくは、ダブルクォートで範囲を指定します。
```
'This is string in single quote'
"This is string in double quote"
```

## 変数
K2HR3テンプレートエンジンはテンプレートを展開するときに、展開する単位で変数を永続的に利用できます。  
変数とは、以下に示すいずれかの形式を持っています。
```
%variable%
%var_array%[0] もしくは %var_array%['0']
%var_object%{'key'} もしくは %var_object%['key']
```
変数は、テンプレートの中で自由に定義できます。  
または、K2HR3システムに登録されている**リソース（RESOURCE）、ロール（ROLE）の[YRN](detail_variousja.html)パスを指定でき、これらのリソース（RESOURCE）、ロール（ROLE）のデータを展開できます**。
```
%yrn:yahoo:yjcore:::resource:k2hr3api_res%
```

### 配列とオブジェクトの要素
配列とオブジェクトの要素へのアクセスは、'[...]'もしくは'{...}'を指定します。  
配列の場合には、'[...]'に数値もしくは文字列として位置番号が指定できます。  
```
%var_array%[0]
%var_array%['0']
```
オブジェクトの場合は、'{...}'もしくは'[...]'にキー名を文字列で指定してアクセスできます。
```
%var_object%{'key'}
%var_object%['key']
```

### 配列とオブジェクトの要素数
配列とオブジェクトの要素数は、'.length'もしくは'.size'、'.count'を使うことで取得できます。  
以下の例では、%var_array%配列変数の要素数を表示します。  
{% raw %}```
{{= %var_array%.length }}
```{% endraw %}

### 制限
複数段の配列、オブジェクトはサポートしていません。  
複数談の配列、オブジェクトにアクセスする場合は、以下のようにテンポラリー変数を準備してアクセスすることで実現できます。  
{% raw %}```
{{ %tmparray% = %multiarray%[2] }}
{{= %tmparray%[0] }}
```{% endraw %}

## 構文
K2HR3テンプレートエンジンで利用できる制御構文を以下に示します。
- if文  
if、elif、else、endifで構成される制御構文です。  
{% raw %}```
{{ if 0 == %variable% }}
    %variable%が0のときに出力されます。
{{ elif 1 == %variable% }}
    %variable%が1のときに出力されます。
{{ else }}
    %variable%が0、1以外のときに出力されます。
{{ endif }}
```{% endraw %}
- while文  
while、doneで構成される制御構文です。  
{% raw %}```
{{ while 0 < %variable% }}
    %variable%が1以上のときに出力されます。
    {{ --%variable% }}
{{ done }}
```{% endraw %}
- do while文  
do、whileで構成される制御構文です。  
{% raw %}```
{{ do }}
    %variable%が1以上のときまで出力されます。
    {{ --%variable% }}
{{ while 0 < %variable% }}
```{% endraw %}
- for文  
for、doneで構成される制御構文です。  
{% raw %}```
{{ for %variable% = 0 ; %variable% < 2 ; ++%variable% }}
    %variable%が0、1のときまで出力されます。
{{ done }}
```{% endraw %}
変数が配列（オブジェクト）の場合、'.length'を使ってループの上限数を定義することができます。  
{% raw %}```
{{ for %variable% = 0 ; %variable% < %var_array%.length ; ++%variable% }}
    %variable%.lengthにより配列の要素をすべて出力します。
    {{= %var_array%[%variable%] }}
{{ done }}
```{% endraw %}
- foreach文  
foreach、doneで構成される制御構文です。  
変数に配列を指定した場合には、配列の要素を直接取得できます。  
{% raw %}```
{{ foreach %subvar% in %variable% }}
    %variable%が配列の場合、配列の要素が出力されます。
    {{= %subvar% }}
{{ done }}
```{% endraw %}
オブジェクトを指定した場合には、要素のキー名を取得することができます。  
{% raw %}```
{{ foreach %subvar% in %variable% }}
    %variable%がオブジェクトの場合、オブジェクトのキー名が取得できます。
    {{= %subvar% }}
    {{= %variable%{%subvar%} }}
{{ done }}
```{% endraw %}
- break  
制御構文のループをブレークさせる命令であり、どこにでも記述できます。  
{% raw %}```
{{ break }}
```{% endraw %}
- continue  
制御構文のループをこの文が記述された以降を実行せずに、ループ条件に戻ります。  
{% raw %}```
{{ continue }}
```{% endraw %}

## 演算子
利用できる演算子を列挙します。条件演算子は主に制御構文の条件文として利用されます。
- 代入(=)  
{% raw %}```
{{ %variable_00% = %variable_01% }}
```{% endraw %}
- 加算(+)  
{% raw %}```
{{ %variable_00% + %variable_01% }}
```{% endraw %}
- 減算(-)  
{% raw %}```
{{ %variable_00% - %variable_01% }}
```{% endraw %}
- 除算(/)  
{% raw %}```
{{ %variable_00% / %variable_01% }}
```{% endraw %}
- 積算(*)  
{% raw %}```
{{ %variable_00% * %variable_01% }}
```{% endraw %}
- 余算(%)  
{% raw %}```
{{ %variable_00% % %variable_01% }}
```{% endraw %}
- ビットAND(&)  
{% raw %}```
{{ %variable_00% & %variable_01% }}
```{% endraw %}
- ビットOR(|)  
{% raw %}```
{{ %variable_00% | %variable_01% }}
```{% endraw %}
- 左ビットシフト(<<)  
{% raw %}```
{{ %variable_00%<<4 }}
```{% endraw %}
- 右ビットシフト(>>)  
{% raw %}```
{{ %variable_00%>>4 }}
```{% endraw %}
- 否定(!)  
{% raw %}```
{{ !%variable_00% }}
```{% endraw %}
- インクリメント(++)  
{% raw %}```
{{ %variable_00%++ }}
{{ ++%variable_00% }}
```{% endraw %}
- デクリメント(--)  
{% raw %}```
{{ %variable_00%-- }}
{{ --%variable_00% }}
```{% endraw %}
- AND(&&)  
{% raw %}```
{{ %variable_00% && %variable_01% }}
```{% endraw %}
- OR(||)  
{% raw %}```
{{ %variable_00% || %variable_01% }}
```{% endraw %}
- 等号・不等号(==、!=、<、>、<=、>=)  
{% raw %}```
{{ %variable_00% == %variable_01% }}
{{ %variable_00% != %variable_01% }}
{{ %variable_00% < %variable_01% }}
{{ %variable_00% > %variable_01% }}
{{ %variable_00% <= %variable_01% }}
{{ %variable_00% >= %variable_01% }}
```{% endraw %}

### 注意１
変数、定数は基本的に型（数値、文字列、論理値）を持っています。  
2項演算子にて、型の異なる変数、定数を指定した場合には、可能な限り左辺の型に揃えられます。

### 注意２
演算子の優先順位は、一般的な優先順位に従います。以下のテンプレートを展開した結果は、"20"となります。
{% raw %}```
{{ %tmp_priority_data00% = 1 + 3 * 2 * 3 + 1 }}
{{= %tmp_priority_data00% }}
```{% endraw %}

# サンプル
## サンプル（基本）
以下にサンプルのテンプレート文字列（複数行）を示します。
{% raw %}```
{{#!k2hr3template }}
{{# 上記の行は省略が可能です。}}
テンプレート展開例

1) 変数を使ったループ例
  {{ for %val% = 0 ; %val% < 2 ; ++%val% }}
    - ループ内の展開：現在の変数%val%の値は、{{= %val% }}です。
  {{ done }}

3) 計算
  {{ %val% = 10 + 10 * 9 / 3 }}
  %val% は、40となっているはずです。
　計算結果 = {{= %val% }}

以上、ここまで。
```{% endraw %}

上記のテンプレート文字列をK2HR3テンプレートエンジンにより展開した結果を以下に示します。（改行は見やすく調整してます。）
{% raw %}```
テンプレート展開例

1) 変数を使ったループ例
    - ループ内の展開：現在の変数%val%の値は、0です。
    - ループ内の展開：現在の変数%val%の値は、1です。

3) 計算
  %val% は、40となっているはずです。
　計算結果 = 40

以上、ここまで。
```{% endraw %}

## サンプル（ロール（ROLE）展開）
ロール（ROLE）は、ホスト（HOST）をデータとして保持しています。  
このホスト（HOST）の情報を、変数としてテンプレート（TEMPLATE）で利用することができます。  
以下にロール（ROLE）に含まれるホスト（HOST）の情報を展開するテンプレート（TEMPLATE）の例を示します。  
{% raw %}```
{{#!k2hr3template }}
{{ foreach %host_key% in %yrn:yahoo:::mytenant:role:myrole/hosts/ip% }}
    {{ %one_host% = %yrn:yahoo:::mytenant:role:myrole/hosts/ip%{%host_key%} }}
    {{= %one_host%{'host'} }}
    {{= %one_host%{'port'} }}
{{ done }}
```{% endraw %}
上記の例では、K2HR3アプリケーションなどからIPアドレスをロール（ROLE）に登録したホスト（HOST）の情報を表示できます。  
ホスト（HOST）の情報には、必ず**host**と**port**（任意の場合は**0**）が存在します。  
Openstackやkubernetesからロール（ROLE）にVirtualMachineやPod（Container）を自動登録した場合、いくつかのキーが存在します。  
以下のサンプルで、ロール（ROLE）が持つ個々のホスト（HOST）情報をJSON形式で示します。
{% raw %}```
'yrn:yahoo:::mytenant:role:myrole/hosts/ip': {
    '127.0.0.1,0,': {                                  <--- case of normal registration
        'host':   '127.0.0.1'
        'port':   0,
        'extra':  null,
        'cuk':    null
    },
    '127.0.0.2,0,': {                                  <--- case of automatically from openstack
        'host':   '127.0.0.2'
        'port':   0,
        'extra':  'openstack-auto-v1',
        'cuk':    null
    },
    '127.0.0.3,0,cuk-xxxxxxxxxxxxxxx': {               <--- case of automatically from kubernetes
        'host':                '127.0.0.3'
        'port':                0,
        'extra':               'k8s-auto-v1',
        'cuk':                 'cuk-xxxxxxxxxxxxxxx',
        'k8s_namespace':       'namespace'
        'k8s_service_account': 'sa'
        'k8s_node_name':       'nodename'
        'k8s_node_ip':         '127.0.0.3'
        'k8s_pod_name':        'podname'
        'k8s_pod_id':          'pod-id-yyyyyyyyyyyy'
        'k8s_pod_ip':          '192.0.0.3'
        'k8s_container_id':    'container-id-zzzzzz'
    },
    ...
}
```{% endraw %}
上記のサンプルのように、ホスト（HOST）の情報の要素から通常登録、Openstackによる登録、kubernetesによる登録を区別することができます。  
ロール（ROLE）のホスト（HOST）情報を示す変数名は以下のいずれかを使うことができます。  
{% raw %}```
1) Only IP address
   %yrn:<provider(domain)>:<service>:<region>:<tenant>:role:<role name>/hosts/ip%

2) Only hostname(FQDN)
   %yrn:<provider(domain)>:<service>:<region>:<tenant>:role:<role name>/hosts/name%

3) IP address and hostname(FQDN)
   %yrn:<provider(domain)>:<service>:<region>:<tenant>:role:<role name>/hosts/all%
```{% endraw %}
これらの変数は、ロール（ROLE）毎に定義されます。  
よって、テンプレート（TEMPLATE）から必要な時にアクセスして、その情報を展開することができます。

### ホスト（HOST）情報の展開について
例えば、特定のロール（ROLE）に登録されたホスト（HOST）のリストを取得し、アプリケーションで利用することを想定します。  
つまり、このアプリケーションはロール（ROLE）に登録されたIPアドレスにアクセスする必要があり、そのIPアドレスのリストをK2HR3を通して動的に生成することを考えています。  
これを実現するには、以下のように行います。  
- リソース（RESOURCE）にテンプレート（TEMPLATE）を登録します。
- ロール（ROLE）とポリシー（POLICIES）を作成し、そのリソース（RESOURCE）にアクセスできるように設定します。
- ロール（ROLE）にホスト（HOST）を登録します。
- リソース（RESOURCE）を取得することで、テンプレート（TEMPLATE）が展開され、ロール（ROLE）のホスト（HOST）のリストを取得することができます。

これを行うサンプルのテンプレート（TEMPLATE）を以下に示します。
{% raw %}```
{{ %host_no% = 0 }}
{{ foreach %host_key% in %yrn:yahoo:::mytenant:role:myrole/hosts/all% }}
    {{ %one_host% = %yrn:yahoo:::mytenant:role:myrole/hosts/all%{%host_key%} }}
    Host[{{= %host_no% }}] = {{= %one_host%{'host'} }}:{{= %one_host%{'port'} }}
    {{ ++%host_no% }}
{{ done }}
```{% endraw %}
上記のテンプレート（TEMPLATE）が展開されたサンプルです。
{% raw %}```
    Host[0] = abc.example.com:0
    Host[1] = 127.0.0.1:0
```{% endraw %}

以上のようにロール（ROLE）の動的なホスト（HOST）情報をテンプレート（TEMPLATE）を使い、リソース（RESOURCE）の一部として展開することができます。
