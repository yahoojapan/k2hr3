---
layout: contents
language: en-us
title: USERDATA API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_userdataja.html
lang_opp_word: To Japanese
prev_url: api_acr.html
prev_string: ACR API
top_url: api.html
top_string: REST API
next_url: 
next_string: 
---

# USERDATA API
This page describes K2HR3 USER DATA API for OpenStack as IaaS.
The purpose of the USER DATA API is to provide USER DATA, which user defined data to customize a cloud instance, to [cloud-init](https://cloudinit.readthedocs.io/en/latest/) that initializes OpenStack instances.
[cloud-init](https://cloudinit.readthedocs.io/en/latest/) reads the user data defined by K2HR3 by calling this K2HR3 USER DATA API. The content contains two types of data, a config file for [cloud-init](https://cloudinit.readthedocs.io/en/latest/) and a shell script.
[cloud-init](https://cloudinit.readthedocs.io/en/latest/) runs the shell script to pass the instance meta data(primarily including the unique id and the IP address) by using K2HR3 ROLE API.
See the [Detail](detail.html) page for K2HR3's collaboration with OpenStack.

## GET（Userdata）
Provides a [User-Data Script](https://cloudinit.readthedocs.io/en/latest/topics/format.html#user-data-script), which will be acted upon by [cloud-init](https://cloudinit.readthedocs.io/en/latest/). A successful response also contains a [Cloud Config Data](https://cloudinit.readthedocs.io/en/latest/topics/format.html#cloud-config-data).

Here is an example usage by using [Include File](https://cloudinit.readthedocs.io/en/latest/topics/format.html#include-file) directive. [cloud-init](https://cloudinit.readthedocs.io/en/latest/) reads the user data from the URL.
```
#include
http(s)://<K2HR3 API FQDN>/v1/userdata/<path>
```

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/userdata/_userdata_path_

### Header(Request)
```
Content-Type: application/octet-stream
User-Agent: Cloud-Init 0.7.9
Accept-Encoding: gzip
```
- Content-Type  
Should be 'application/octet-stream'. Can be empty.  
- User-Agent  
Must include any 'Cloud-init' string. Will return a fatal error if no 'Cloud-Init' is included.  
- Accept-Encoding  
The 'gzip' can be specified. The API returns plain text data if no Accept-Encoding or the value without 'gzip' is specified.  
 

### URL Path
The "registerpath" value in K2HR3 ROLE API response data that contains the following json object, which is actually encoded by using JSON stringify().
```
{
    role:         <role name>
    token:        <role token string>
}
```
In addition, the value is encrypted, base64 encoded and encodeURI（+'/',':','?'） encoded.


### URL Arguments
Empty

### Response status
200、40x

### Response（Gzip/Text）
The response data is always in MIME Multi Part form.

The response data can be gzipped or plain text. The format doesn't determine the content.

#### Success
The following shows an example of a successful response data. Note that the URL path must contain a valid K2HR3 ROLE information.
```
$ npm run test:manual:apis:userdata_get

> k2hr3-api@0.0.1 test:manual:apis:userdata_get /home/nakatani/work/k2hr3_api
> test/manual_test.sh userdata_get

Response Type (gzip or text(default)) : gzip
Register URI path                     : olkKqFf2VdmsDeccSanw4%2F%2FtiDnPcVyQDf%2BUWBkgwt66BlLB9%2BolM1sn0w8F%2FN7jIGZcfPvuXBrFtQaQ1LJmyGEmi%2FzjWtcp3NmDx
HgXwYd99siENX9AT%2BvbIh28m5olORCLUm1zwR76fYt%2Ftezx7g%3D%3D
RESPONSE CODE = 200
RESPONSE BODY(GUNZIP) = <<<
Content-Type: multipart/mixed; boundary="================K2HR3INIT1539142345745=="
MIME-Version: 1.0
Number-Attachments: 2

--================K2HR3INIT1539142345745==
MIME-Version: 1.0
Content-Type: text/cloud-config; charset="us-ascii"
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="k2hr3-cloud-config.txt"

#cloud-config
#
# K2HR3
#
# Copyright 2018 Yahoo! JAPAN corporation.
#
# K2HR3 is K2hdkc based Resource and Roles and policy Rules, gathers
# common management information for the cloud.
# K2HR3 can dynamically manage information as "who", "what", "operate".
# These are stored as roles, resources, policies in K2hdkc, and the
# client system can dynamically read and modify these information.
#
# For the full copyright and license information, please view
# the license file that was distributed with this source code.
#
# AUTHOR:   Takeshi Nakatani
# CREATE:   Tue Oct 2 2018
# REVISION:
#
packages:
  - curl

#
# VIM modelines
#
# vim:set ts=4 fenc=utf-8:
#

--================K2HR3INIT1539142345745==
MIME-Version: 1.0
Content-Type: text/x-shellscript; charset="us-ascii"
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="k2hr3-init.sh"

#!/bin/sh
#
# K2HR3
#
# Copyright 2018 Yahoo! JAPAN corporation.
#
# K2HR3 is K2hdkc based Resource and Roles and policy Rules, gathers
# common management information for the cloud.
# K2HR3 can dynamically manage information as "who", "what", "operate".
# These are stored as roles, resources, policies in K2hdkc, and the
# client system can dynamically read and modify these information.
#
# For the full copyright and license information, please view
# the license file that was distributed with this source code.
#
# AUTHOR:   Takeshi Nakatani
# CREATE:   Tue Oct 2 2018
# REVISION:
#

SCRIPTNAME="k2hr3-init"
LOGFILE="/var/log/${SCRIPTNAME}.log"
CLOUDINIT_DATA_DIR="/var/lib/cloud/data"
INSTANCE_ID_FILE="${CLOUDINIT_DATA_DIR}/instance-id"
K2HR3_ROLE_FILE="${CLOUDINIT_DATA_DIR}/k2hr3-role"

K2HR3_USER_ROLE_TOKEN="16ac70ab586a65286624f0f98438a32"
K2HR3_API_HOST_URI="https://localhost/v1/role"
K2HR3_ROLE_NAME="yrn:yahoo:::33348:role:k2hr3_entest_obj_role_03"

echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[INFO]: Start to initialize information for k2hr3" | tee -a ${LOGFILE}

if [ ! -f ${INSTANCE_ID_FILE} ]; then
        echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[ERROR]: Could not read ${INSTANCE_ID_FILE}" | tee -a ${LOGFILE}
        exit 1
fi
INSTANCE_ID=`cat ${INSTANCE_ID_FILE}`
if [ "X${INSTANCE_ID}" = "X" ]; then
        echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[ERROR]: Unknown Instance Id in ${INSTANCE_ID_FILE}" | tee -a ${LOGFILE}
        exit 1
fi

CUK_PARAMETER="cuk=${INSTANCE_ID}"
EXTRA_PARAMETER="extra=openstack-auto-v1"

REGISTER_RESULT=`curl -s -S -X PUT -H "x-auth-token: R=${K2HR3_USER_ROLE_TOKEN}" "${K2HR3_API_HOST_URI}/${K2HR3_ROLE_NAME}?${CUK_PARAMETER}&${EXTRA_PARAMETER}" 2>&1`
if [ $? -ne 0 ];then
        echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[ERROR]: Could not register to role member with curl error" | tee -a ${LOGFILE}
        exit 1
fi
REGISTER_RESULT_VALUE=`echo ${REGISTER_RESULT} | python -m json.tool | grep result | cut -d':' -f2,2 | sed 's/^[ ,]\+\|[ ,]\+$//g' | tr '[:lower:]' '[:upper:]'`
if [ "X${REGISTER_RESULT_VALUE}" != "XTRUE" ]; then
        REGISTER_RESULT_MSG=`echo ${REGISTER_RESULT} | python -m json.tool | grep message | cut -d':' -f2,2 | sed 's/^[ ,]\+\|[ ,]\+$//g'`
        echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[ERROR]: Failed to put access for registering by ${REGISTER_RESULT_MSG}" | tee -a ${LOGFILE}
        exit 1
fi
echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[INFO]: Set this host to k2hr3 role(${K2HR3_ROLE_NAME})" | tee -a ${LOGFILE}

echo "${K2HR3_ROLE_NAME}" > ${K2HR3_ROLE_FILE}
if [ $? -ne 0 ]; then
        echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[ERROR]: Could not put k2hr3 role name(${K2HR3_ROLE_NAME}) to ${K2HR3_ROLE_FILE}" | tee -a ${LOGFILE}
        exit 1
fi
echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[INFO]: Create k2hr3 role(${K2HR3_ROLE_NAME}) file(${K2HR3_ROLE_FILE})" | tee -a ${LOGFILE}

chmod 444 ${K2HR3_ROLE_FILE}
if [ $? -ne 0 ]; then
        echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[WARN]: Could not change mode for ${K2HR3_ROLE_FILE}, but continue..." | tee -a ${LOGFILE}
fi
echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[INFO]: initialize host information for k2hr3" | tee -a ${LOGFILE}

exit 0

#
# VIM modelines
#
# vim:set ts=4 fenc=utf-8:
#
--================K2HR3INIT1539142345745==--
<<<
```
[cloud-init](https://cloudinit.readthedocs.io/en/latest/) will run by using this user data:
1. Installs the 'curl' package.
1. Calls the K2HR3 ROLE API with the instance unique id and the IP address.
1. Saves the K2HR3 ROLE to /var/lib/cloud/data/k2hr3-role the K2HR3 for future use.
1. Records the above in the /var/log/k2hr3-init.log file for later reference.

#### Error with 200 status
Returns a '200' HTTP status code if a 'right' URL Path is provided and an error is detected in cloud-init layer(including a shell script execution phase). Here is an example of a error response body.
```
Content-Type: multipart/mixed; boundary="================K2HR3INIT1539138817839=="
MIME-Version: 1.0
Number-Attachments: 1

--================K2HR3INIT1539138817839==
MIME-Version: 1.0
Content-Type: text/x-shellscript; charset="us-ascii"
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="k2hr3-init-error.sh"

#!/bin/sh
#
# K2HR3
#
# Copyright 2018 Yahoo! JAPAN corporation.
#
# K2HR3 is K2hdkc based Resource and Roles and policy Rules, gathers
# common management information for the cloud.
# K2HR3 can dynamically manage information as "who", "what", "operate".
# These are stored as roles, resources, policies in K2hdkc, and the
# client system can dynamically read and modify these information.
#
# For the full copyright and license information, please view
# the license file that was distributed with this source code.
#
# AUTHOR:   Takeshi Nakatani
# CREATE:   Tue Oct 2 2018
# REVISION:
#

SCRIPTNAME="k2hr3-init"
LOGFILE="/var/log/${SCRIPTNAME}.log"

echo "`date "+%Y-%m-%d %H:%M:%S,%3N"` - ${SCRIPTNAME}[ERROR]: Invalid userdata for creating k2hr3-init script was specified(detail error = Get userdata path is invalid.)" | tee -a ${LOGFILE}
exit 1

#
# VIM modelines
#
# vim:set ts=4 fenc=utf-8:
#

--================K2HR3INIT1539138817839==--
```
[cloud-init](https://cloudinit.readthedocs.io/en/latest/) will run by using this user data:
1. Records the reason for the error in the /var/log/k2hr3-init.log file for later reference.

#### Error
Returns a 40x HTTP status code if a fatal error is detected.
```
{
    result:       <false>
    message:      <error message string>
}
```
