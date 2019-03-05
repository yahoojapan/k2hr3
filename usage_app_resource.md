---
layout: contents
language: en-us
title: App Resource
short_desc: K2Hdkc based Resource and Roles and policy Rules
lang_opp_file: usage_app_resourceja.html
lang_opp_word: To Japanese
prev_url: usage_app_tenant.html
prev_string: App Tenant
top_url: usage_app.html
top_string: Web Application
next_url: usage_app_policy.html
next_string: App Policy-Rule
---

# RESOURCE Usage for K2HR3 Web Application
This section explains how to operate **RESOURCE** using the **K2HR3 Web Application**.

## Display of RESOURCE
If **RESOURCE** has not yet been registered in **TENANT**(when using the K2HR3 system for the first time), registration of **RESOURCE** is required first.  
If **RESOURCE** data already exists, you can check registered **RESOURCE** by selecting **RESOURCE** in the **left tree**.  

![K2HR3 Usage Application - Resource Top](images/usage_app_resource_top.png)

## Registering RESOURCE
To register RESOURCE, select **RESOURCE** in the **left tree**, then click the ![K2HR3 Add Button](images/button_add.png) button next to **[RESOURCE]** at the top.  
To register a **hierarchical RESOURCE**(RESOURCE with parent), select the **existing RESOURCE to be made a parent** from the left tree and click the button.  

After clicking the button, a dialog for registering RESOURCE is displayed.  

![K2HR3 Usage Application - Resource Create Dialog](images/usage_app_resource_add.png)

Enter the **RESOURCE name** in the displayed dialog and click the ![K2HR3 OK Button](images/button_ok.png) button to register RESOURCE.  

Items displayed in dialog and their contents are shown below.  
- TENANT  
The **TENANT name*** for registering RESOURCE is displayed.
- TYPE  
**"resource"** indicating that it is RESOURCE is displayed.
- PARENT PATH  
**[YRN](detail_various.html) path** of the parent of RESOURCE to be registered is displayed.  
In the case of RESOURCE of top level(without parent) which is not layered, **"/"** is displayed.  
When registering under the parent RESOURCE, **[YRN](detail_various.html) path** of its parent RESOURCE is displayed.  
For example, if you register RESOURCE under the RESOURCE name **"toplevel"**, **"/toplevel"** is displayed.
- CREATE PATH  
Enter the name of the RESOURCE to be registered.

After registered **RESOURCE**, you can see by deploying **RESOURCE** in the left tree.

## Editing of RESOURCE
To edit the contents of already registered **RESOURCE**, first select RESOURCE to edit in the left tree.  
After selection, the data of the **RESOURCE data** is displayed in the main area of **K2HR3 Web Application**.  

You can directly edit, add, or delete this RESOURCE data.  
After editing, you can save the RESOURCE data by clicking the ![K2HR3 SAVE Button](images/button_save.png) button.
To discard the editing, please click the ![K2HR3 CANCEL Button](images/button_cancel.png) button.  

![K2HR3 Usage Application - Resource Page](images/usage_app_resource_all.png)

After selecting RESOURCE, the items displayed in the main area will be explained.  
- VALUE  
The value(data) of RESOURCE is displayed.  
  - Type of value(data)  
    Indicates the type of value(data).  
    A character string(Text String Type) or a JSON character string(Object(JSON) Type) is selected.
  - Value (data)  
    The value(data) is displayed. When editing, please input the value(data) directly as a character string.
- KEYS  
The registered **key-value pair** is displayed.  
Multiple pair registration is possible.  
When editing, you can directly change, add, or delete.
- ALIAS  
The registered ALIAS is displayed.  
ALIAS is displayed as **[YRN](detail_various.html) full path** to other RESOURCE.  
To edit/add as well, enter **[YRN](detail_various.html) full path**.

## Attribute information of RESOURCE
To display **RESOURCE attribute information**, first select RESOURCE in the left tree.  
After selection, click ![K2HR3 Path Button](images/button_path.png) on the left side of **[RESOURCE]** to display the RESOURCE attribute information(**Selected Path Information**) dialog.  
The attribute information of RESOURCE is displayed in this dialog.  

![K2HR3 Usage Application - Resource Information](images/usage_app_resource_info.png)

The following describes attribute information of RESOURCE.
- TENANT  
Displays the **TENANT name** to which RESOURCE belongs.
- TYPE  
**"resource"** is displayed.
- PATH  
**[YRN](detail_various.html) full path** to this RESOURCE is displayed.  
This **[YRN](detail_various.html) full path** is used for input to **POLICY-RULE** and **RESOURCE ALIAS** etc.

