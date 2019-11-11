---
layout: contents
language: en-us
title: Template Engine
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_templateja.html
lang_opp_word: To Japanese
prev_url: 
prev_string: 
top_url: usage_base.html
top_string: Basic Usage
next_url: 
next_string: 
---

# K2HR3 Template Engine
**Dynamic RESOURCE** can be defined for **RESOURCE** of K2HR3 system.  
The K2HR3 system provides a **TEMPLATE notation** for defining **dynamic RESOURCE**.  
The contents described in this **TEMPLATE** pass through the **K2HR3 Template Engine** and are expanded as **RESOURCE** data.
The **K2HR3 Template Engine** and **TEMPLATE notation** are described below.

# Apply
In the K2HR3 system, USER can set a character string as **RESOURCE** data.  
For character strings set as **RESOURCE**, **USER** and **ROLE** member **HOST** can be read.  
The **K2HR3 Template Engine** can expand template strings that satisfy the **TEMPLATE notation**.  

# Overview
Explain the description method and specification of the basic **TEMPLATE** to be understood by the **K2HR3 Template Engine**.

## Analysis range of TEMPLATE
The **K2HR3 Template Engine** analyzes and expands the character string of the range(statement) separated by the following keywords in the character string read as a **TEMPLATE**.
{% raw %}```
{{ .... }}
```{% endraw %}

## Specifying the template engine
_This feature is reserved and currently only fixed value **"k2hr3template"**(for K2HR3 Template Engine) is supported._  

This is a statement specified by the template engine.  
It must start from the beginning of all **TEMPLATE** strings.  
You can omit it when using the **K2HR3 Template Engine**.  
- Specifying a template other than the **K2HR3 Template Engine**  
{% raw %}```
{{#!xxxxxxxxxxxxxx }}
```{% endraw %}
- Specifying the **K2HR3 Template Engine**  
{% raw %}```
{{#!k2hr3template }}
```{% endraw %}

## Comment
Statements as described below will not be output(displayed) when expanded by the template engine.  
It is a statement to use as a general comment.  
{% raw %}```
{{# This is comment strings.... }}
```{% endraw %}

## Display variables
By describing as follows, you can display values such as variables (described later) used in the template.  
You can also specify constants for variables to be displayed.  
{% raw %}```
{{= 'print static string' }}
{{= true }}
{{= 1000 }}
{{= %variable% }}
```{% endraw %}

## Escape keyword
You may not want to recognize the keywords used to specify the analysis range of the template as a template.  
Also, you may not want to recognize the keywords used to specify the character string (described later) as a template.  
These escaping methods are shown below.  
- {% raw %}{{{, }}}{% endraw %}  
{% raw %}To escape **"{{"** and **"}}"**, you can convert it to **"{{"** or **"}}"** by describing **"{{{"** or **"}}}"** respectively.{% endraw %}  
{% raw %}```
{{{ This is not statement }}}
```{% endraw %}
- Single quotes, double quotes  
To specify a character string in the statement range, write '...' or "...".  
To escape each keyword within each range, prefix the \ character.
```
"The \"test\" is in escaped quote."
```

## Constant
The constants supported by the **K2HR3 Template Engine** are shown below.
- null
- true
- false

## Number
There are the following methods for expressing numerical values supported by the **K2HR3 Template Engine**.
- Decimal number  
Please list any number from 0 to 9. (ex. 123456789)
- Hexadecimal  
Specify 0x or x as a prefix to enumerate hexadecimal numbers. (ex. 0xff)
- Octal number  
Please specify 0o as the prefix and enumerate the number of 0 - 7. (ex. 01234)
- Binary number  
Please specify 0b as the prefix and enumerate the number of 0 or 1. (ex. 0b1010)

## String
To describe a character string in a statement, specify the range with single quote or double quote.
```
'This is string in single quote'
"This is string in double quote"
```

## Variable
When analyzing the template, the **K2HR3 Template Engine** permanently uses the variables of each template to be expanded.  
A variable has one of the following forms.  
```
%variable%
%var_array%[0] or %var_array%['0'] 
%var_object%{'key'} or %var_object%['key']
```
You can freely define variables in templates.  
Alternatively, you can specify **the [YRN](detail_various.html) path of RESOURCE, ROLE registered in the K2HR3 system, and use the data set for these as variables**.  
```
%yrn:yahoo:yjcore:::resource:k2hr3api_res%
```

### Array and object elements
Specify '[...]' or '{...}' to access array and object elements.  
In the case of an array, the position number can be specified as a numerical value or character string in '[...]'.  
```
%var_array%[0]
%var_array%['0']
```
In the case of an object, you can access it by specifying the key name as a character string in '{...}' or '[...]'.  
```
%var_object%{'key'}
%var_object%['key']
```

### Number of array and object elements
The number of elements in arrays and objects can be obtained using '.length' or '.size', '.count'.  
The following example displays the number of elements in the %var_array% array variable.  
{% raw %}```
{{= %var_array%.length }}
```{% endraw %}

### Limit
Multi-level arrays and objects are not supported.  
But accessing multiple arrays and objects can be achieved by preparing and accessing temporary variables as shown below.  
{% raw %}```
{{ %tmparray% = %multiarray%[2] }}
{{= %tmparray%[0] }}
```{% endraw %}

## Syntax
The control syntax available for the **K2HR3 Template Engine** is shown below.  
- if  
It is a control syntax consisting of **if, elif, else, and endif**.  
{% raw %}```
{{ if 0 == %variable% }}
    display if %variable% is 0.
{{ elif 1 == %variable% }}
    display if %variable% is 1.
{{ else }}
    display if %variable% is not 0 nor 1.
{{ endif }}
```{% endraw %}
- while  
It is a control syntax consisting of **while, done**.  
{% raw %}```
{{ while 0 < %variable% }}
    display if %variable% is over 1.
    {{ --%variable% }}
{{ done }}
```{% endraw %}
- do while  
It is a control syntax consisting of **do, while**.  
{% raw %}```
{{ do }}
    display until %variable% is over 1.
    {{ --%variable% }}
{{ while 0 < %variable% }}
```{% endraw %}
- for  
It is a control syntax consisting of **for, done**.  
{% raw %}```
{{ for %variable% = 0 ; %variable% < 2 ; ++%variable% }}
    display if %variable% is 0 or 1.
{{ done }}
```{% endraw %}
If the variable is an array (object), you can use '.length' to define the maximum number of loops.  
{% raw %}```
{{ for %variable% = 0 ; %variable% < %var_array%.length ; ++%variable% }}
    Output all array elements by %variable% .length.
    {{= %var_array%[%variable%] }}
{{ done }}
```{% endraw %}
- foreach  
It is a control syntax consisting of **foreach, done**.  
If you specify an array for the variable, you can get the elements of the array directly.  
{% raw %}```
{{ foreach %subvar% in %variable% }}
    If %variable% is an array, the elements of the array are output.
    {{= %subvar% }}
{{ done }}
```{% endraw %}
If you specify an object, you can get the key name of the element.  
{% raw %}```
{{ foreach %subvar% in %variable% }}
    If %variable% is an object, you can get the key name of the object.
    {{= %subvar% }}
    {{= %variable%{%subvar%} }}
{{ done }}
```{% endraw %}
- break  
It is an instruction to break control loop of control syntax and can be described anywhere.  
{% raw %}```
{{ break }}
```{% endraw %}
- continue  
The loop of the control syntax returns to the loop condition without executing the statement after this statement is written.  
{% raw %}```
{{ continue }}
```{% endraw %}

## Operator
Enumerate available operators. Conditional operators are mainly used as conditional statements of control syntax.  
- Assignment(=)  
{% raw %}```
{{ %variable_00% = %variable_01% }}
```{% endraw %}
- Addition(+)  
{% raw %}```
{{ %variable_00% + %variable_01% }}
```{% endraw %}
- Subtraction(-)  
{% raw %}```
{{ %variable_00% - %variable_01% }}
```{% endraw %}
- Divide(/)  
{% raw %}```
{{ %variable_00% / %variable_01% }}
```{% endraw %}
- Integration(*)  
{% raw %}```
{{ %variable_00% * %variable_01% }}
```{% endraw %}
- Surplus(%)  
{% raw %}```
{{ %variable_00% % %variable_01% }}
```{% endraw %}
- Bit operation AND(&)  
{% raw %}```
{{ %variable_00% & %variable_01% }}
```{% endraw %}
- Bit operation OR(|)  
{% raw %}```
{{ %variable_00% | %variable_01% }}
```{% endraw %}
- Left bit shift(<<)  
{% raw %}```
{{ %variable_00%<<4 }}
```{% endraw %}
- right bit shift(>>)  
{% raw %}```
{{ %variable_00%>>4 }}
```{% endraw %}
- denial(!)  
{% raw %}```
{{ !%variable_00% }}
```{% endraw %}
- Increment(++)  
{% raw %}```
{{ %variable_00%++ }}
{{ ++%variable_00% }}
```{% endraw %}
- Decrement(--)  
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
- Equal/Inequality(==、!=、<、>、<=、>=)  
{% raw %}```
{{ %variable_00% == %variable_01% }}
{{ %variable_00% != %variable_01% }}
{{ %variable_00% < %variable_01% }}
{{ %variable_00% > %variable_01% }}
{{ %variable_00% <= %variable_01% }}
{{ %variable_00% >= %variable_01% }}
```{% endraw %}

### Attention 1
Variables and constants basically have types (numbers, strings, logical values).  
When binary operators specify variables and constants of different types, they are aligned to the type on the left side as much as possible.  

### Attention 2
Operator priorities follow general priorities.  
The result of expanding the following template is "20".  
{% raw %}```
{{ %tmp_priority_data00% = 1 + 3 * 2 * 3 + 1 }}
{{= %tmp_priority_data00% }}
```{% endraw %}

# Samples
## Samples(Basics)
The sample template character string (multiple lines) is shown below.  
{% raw %}```
{{#!k2hr3template }}
{{# COMMENT LINE : The above line can be omitted. }}
Example of template expansion.

1) Examples of loops using variables
  {{ for %val% = 0 ; %val% < 2 ; ++%val% }}
    - Expansion within a loop: The value of the current variable {{= %val% }}.
  {{ done }}

3) Calculation
  {{ %val% = 10 + 10 * 9 / 3 }}
  %val% should be 40.
　Calculation result = {{= %val% }}

That 's all.
```{% endraw %}

The following shows the result of expansion of the above template character string by the **K2HR3 Template Engine**.  
_Line feeds are adjusted_  
{% raw %}```
Example of template expansion.

1) Examples of loops using variables
    - Expansion within a loop: The value of the current variable 0.
    - Expansion within a loop: The value of the current variable 1.

3) Calculation
  %val% should be 40.
　Calculation result = 40

That 's all.
```{% endraw %}

## Samples(expanding **ROLE** member **HOST**)
**ROLE** has the **HOST** information as its member.  
The **HOST** information can be used as a variable in the template which is using **K2HR3 Template Engine**.  
The following is an example of a template that expands **HOST** information included in a **ROLE**.  
{% raw %}```
{{#!k2hr3template }}
{{ foreach %host_key% in %yrn:yahoo:::mytenant:role:myrole/hosts/ip% }}
    {{ %one_host% = %yrn:yahoo:::mytenant:role:myrole/hosts/ip%{%host_key%} }}
    {{= %one_host%{'host'} }}
    {{= %one_host%{'port'} }}
{{ done }}
```{% endraw %}
In the above example, the IP addresses in **ROLE** which are register by the K2HR3 application etc are displayed as the information of those **HOST**.  
The **HOST** information always includes **'host'** and **'port'**(**0** for any).  
If VirtualMachine and Pod(container) are automatically registered to **ROLE** from Openstack and kubernetes, there are some keys in addition to the above.  
The following sample shows the individual **HOST** information for **ROLE** in like a JSON format.  
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
Please refer to the sample above.  
That way, you can distinguish regular registration, Openstack registration, and kubernetes registration from the elements of the **HOST** information.  
Any of the following variable names can be used to indicate **HOST** information of **ROLE**.  
{% raw %}```
1) Only IP address
   %yrn:<provider(domain)>:<service>:<region>:<tenant>:role:<role name>/hosts/ip%

2) Only hostname(FQDN)
   %yrn:<provider(domain)>:<service>:<region>:<tenant>:role:<role name>/hosts/name%

3) IP address and hostname(FQDN)
   %yrn:<provider(domain)>:<service>:<region>:<tenant>:role:<role name>/hosts/all%
```{% endraw %}
These variables are defined every **ROLE**.  
So you can use them from the template when you need them to unpack that information.  

### About expansion of **HOST** information
Here, it is assumed that a list of **HOST** registered in a specific **ROLE** is obtained and used in your application.  
For example, the application needs to access an IP address registered in **ROLE** and expects to be able to dynamically generate a list of that IP address from the K2HR3 system.  
To achieve this, do the following:  
- Register the template in **RESOURCE**.
- Create **ROLE** and **POLICY-RULE** and set them to be accessible to **RESOURCE**.
- Register **HOST** in **ROLE**.
- By getting **RESOURCE**, the template is expanded and you can get the list of **HOST** of **ROLE**.

The sample template is shown below.
{% raw %}```
{{ %host_no% = 0 }}
{{ foreach %host_key% in %yrn:yahoo:::mytenant:role:myrole/hosts/all% }}
    {{ %one_host% = %yrn:yahoo:::mytenant:role:myrole/hosts/all%{%host_key%} }}
    Host[{{= %host_no% }}] = {{= %one_host%{'host'} }}:{{= %one_host%{'port'} }}
    {{ ++%host_no% }}
{{ done }}
```{% endraw %}
The following is a sample of the above template expanded.  
{% raw %}```
    Host[0] = abc.example.com:0
    Host[1] = 127.0.0.1:0
```{% endraw %}

As mentioned above, **ROLE** dynamic **HOST** information can be expanded as a part of **RESOURCE** using a template.
