---
layout: contents
language: ja
title: USERDATA API
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: api_userdata.html
lang_opp_word: To English
prev_url: api_acrja.html
prev_string: ACR API
top_url: apija.html
top_string: REST API
next_url: 
next_string: 
---

# USERDATA API
K2HR3 REST APIのOpenStack連携用のUSER DATA SCRIPTに関連するAPI群です。

## GET（Userdata）
OpenStack インスタンス起動時にCloud-Initが利用するUserdataを取得します。  
K2HR3が提供するUserdata（USER DATA SCRIPT）は、以下の形式となっており、この#includeキーワードに指定されたURLからCloud-Initが真のUserdataを取得します。
```
#include
http(s)://<K2HR3 API FQDN>/v1/userdata/<path>
```
本USERDATA APIは上記USER DATA SCRIPT中に記載されるURIの処理を提供するエントリポイントです。

### Endpoint(URL)
http(s)://_API SERVER:PORT_/v1/userdata/_userdata_path_

### Header
```
Content-Type: application/octet-stream
User-Agent: Cloud-Init 0.7.9
Accept-Encoding: gzip
```
- Content-Type  
'application/octet-stream'を期待します。  
ただし、このヘッダーは必須ではありません。
- User-Agent  
必須のヘッダーであり、値に'Cloud-Init'が含まれていなければなりません。（Cloud-Init以外からのリクエストは致命的なエラーとなります）
- Accept-Encoding  
任意のヘッダーであり、指定する場合には'gzip'を含む必要があります。  
レスポンスをGzip圧縮する場合に指定してください。  
このヘッダーが指定されていない（もしくはgzipを含まない）場合には、レスポンスはtextで返されます。  
_レスポンスは常にMIME Multipartで返されます。_

### URL Path
ROLE APIのRoleToken取得のAPIから返された文字列（registerpath値）を指定します。

### URL Arguments
なし

### Response status
200、40x

### Response（Gzip/Text）
Gzip圧縮された場合とTextの場合は共に内容は同じです。（Gzip圧縮されたかどうかだけの違いです）  
#### レスポンス（正常）
正しいURIパスが指定され、ROLE名、ROLEトークンも問題がない場合には、以下のレスポンスが返されます。
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
このUserdataでは、Cloud-Initにより、以下の処理が行われるようになっています。
1. curlのロード
1. ROLE APIを呼び出しInstance ID、IPアドレスを登録
1. K2HR3 ROLE名を/var/lib/cloud/data/k2hr3-roleファイルに出力
1. 上記の動作を/var/log/k2hr3-init.logに記録

#### レスポンス（エラー時）
正しいURIパスが指定されたが、何がしかのエラーによりUserdata Script等が実行できない状況にある場合には、本APIは200（正常レスポンス）を返し、レスポンスボディは以下の内容を返します。
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
このUserdataでは、Cloud-Initにより、以下の処理が行われるようになっています。
1. USERDATA API呼び出しのエラーの事由を/var/log/k2hr3-init.logに記録

#### レスポンス（致命的エラー時）
致命的なエラーが発生した場合には、40x系ステータスと以下のボディを返します。
```
{
    result:       <false>
    message:      <error message string>
}
```
