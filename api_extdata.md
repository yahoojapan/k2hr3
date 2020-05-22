---
layout: contents
language: en-us
title: EXTDATA API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_extdataja.html
lang_opp_word: To Japanese
prev_url: api_userdata.html
prev_string: USERDATA API
top_url: api.html
top_string: REST API
next_url: 
next_string: 
---

# USERDATA API
This page describes K2HR3 EXTRA DATA API.  

This API is an API that expands the template defined by the user and returns the expanded data.  
The user specifies the EXTDATA API endpoint information, template, etc. in the K2HR3 API configuration.  
You can define the YRN full path of Role, RoleToken, K2HR3 API server URI, etc. as variables in the template.  
The EXTDATA API endpoint is a URI that contains the `registerpath` value(the string returned from the RoleToken acquisition API of the ROLE API).  
Thus, you can get the data that dynamically expands the template according to the specified Role.  

The following is an example of K2HR3 API configuration.  
```
{
  ...
  ...

  'extdata': {
    'dummy': {                                                // Extra data API(key=suburi) for trove k2hdkc
      'baseuri':     'https://localhost',                     // URI
      'template':    'config/extdata-dummy.sh.templ',         // Template for Shell part
      'useragent':   'dummy-client'                           // Allowed user-agent(can be omitted: default is allowed all)
      'contenttype': 'text/x-shellscript; charset="us-ascii"' // Response Content-Type(can be omitted: default is 'text/plain')
   },
   ...
   ...
 },
 ...
 ...
}
```

This API can be used as a user-defined API of the USERDATA API.  

## GET（Extdata）
Acquires the user-defined template as data expanded according to Role.  
For example, you can define a shell script as a user-defined template.  
By defining variables such as RoleToken in this shell script template, it can be acquired as a dedicated script according to Role.  

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/extdata/_uripath_/_registerpath_

### Header(Request)
```
Content-Type: application/octet-stream
User-Agent: <Allowed User Agent>
Accept-Encoding: gzip
```
- Content-Type  
Should be 'application/octet-stream'. Can be empty.  
- User-Agent  
Required header.  
The value of this header must match the value set in the K2HR3 API configuration.  
However, if it is not specified in the K2HR3 API settings (configuration), any character string is allowed.  
- Accept-Encoding  
The 'gzip' can be specified. The API returns plain text data if no Accept-Encoding or the value without 'gzip' is specified.  

### URL Path
- uripath  
Specify the EXTDATA API name set in the K2HR3 API configuration.  
- registerpath  
Specify the string(registerpath value) returned from the RoleToken acquisition API of the ROLE API.  

### URL Arguments
Empty

### Response status
200、40x

### Response（Gzip/Text）
The response data can be gzipped or plain text. The format doesn't determine the content.

#### Success
The template expanded data will be returned. Note that the URL path must contain a valid K2HR3 ROLE information.

##### Example: template
```
#/bin/sh

ROLE_NAME={{= %K2HR3_ROLE_NAME% }}
ROLE_TOKEN={{= %K2HR3_ROLE_TOKEN% }}
K2HR3_API_HOST={{= %K2HR3_API_HOST_URI% }}
ERROR_MSG={{= %K2HR3_ERROR_MSG% }}

echo "ROLE_NAME:      ${ROLE_NAME}"
echo "ROLE_TOKEN:     ${ROLE_TOKEN}"
echo "K2HR3_API_HOST: ${K2HR3_API_HOST}"
echo "ERROR_MSG:      ${ERROR_MSG}"

exit 0
```

##### Example: response
```
ROLE_NAME=yrn:yahoo:::mytenant:role:myrole
ROLE_TOKEN=9b7754271286ee8dd68fc7996937f72d788b81b28c071333ded449b2d824636b
K2HR3_API_HOST=https://localhost:3000
ERROR_MSG=null

echo "ROLE_NAME:      ${ROLE_NAME}"
echo "ROLE_TOKEN:     ${ROLE_TOKEN}"
echo "K2HR3_API_HOST: ${K2HR3_API_HOST}"
echo "ERROR_MSG:      ${ERROR_MSG}"

exit 0
```

#### Error
Returns a 40x HTTP status code if a fatal error is detected.
```
{
    result:       <false>
    message:      <error message string>
}
```
