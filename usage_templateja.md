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
%var_array%[0]
%var_object%{'key'}
```
_複数段の配列、オブジェクトはサポートしていません。_  

変数は、テンプレートの中で自由に定義できます。  
または、K2HR3システムに登録されている**リソース（RESOURCE）、ロール（ROLE）の[YRN](detail_variousja.html)パスを指定でき、これらのリソース（RESOURCE）、ロール（ROLE）のデータを展開できます**。
```
%yrn:yahoo:yjcore:::resource:k2hr3api_res%
```

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
- foreach文  
foreach、doneで構成される制御構文です  。
{% raw %}```
{{ foreach %subvar% in %variable% }}
    %variable%が配列であることが前提で、配列の要素分出力されます。
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
