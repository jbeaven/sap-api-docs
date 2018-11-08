# API: CollectionsApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **services_sid_repo_command_post**
Create new command resource.

Creates a new record in the command resource. It returns a JSON object containing a command id for tracking status of asynchronous commands. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_command_post example
*** Create new command resource.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_COMMAND
    data gm_body type /BLCK/OP4_COMMAND.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_COMMAND_STATUS
    data gr_http200 type /BLCK/OP4_COMMAND_STATUS.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-action = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-parameter = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_command_post via HTTP POST
*** i_body: The  command  entry  and  it's  parameter to be created. Currently supported
*** commands  are `copy` and `move`. The parameters for both commands: ```json {
*** \"action\":  \"copy|move\",      \"parameter\":  {      \"source\": \"source
*** href\",       \"parent\": \"uuid of target parent\"   } } ``` The source may
*** be  a  remote  repository  in  later implementations, so an `href` is needed
*** here.
*** i_sid: ID of the current service.
    /blck/op4_cl_CollectionsApi=>services_sid_repo_command_post(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_COMMAND_STATUS)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_COMMAND (**[command](#markdown-header-model-command)**) | The command entry and it&#x27;s parameter to be created. Currently supported  commands are &#x60;copy&#x60; and &#x60;move&#x60;. The parameters for both commands: &#x60;&#x60;&#x60;json {   \&quot;action\&quot;: \&quot;copy|move\&quot;,   \&quot;parameter\&quot;: {     \&quot;source\&quot;: \&quot;source href\&quot;,     \&quot;parent\&quot;: \&quot;uuid of target parent\&quot;   } } &#x60;&#x60;&#x60; The source may be a remote repository in later implementations, so an &#x60;href&#x60; is needed here.  
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_COMMAND_STATUS (**[CommandStatus](#markdown-header-model-)**) | OK, entry created. Command id will be returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide commands
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_repo_get**
Access the document repository within a service

Some services (not all) expose access to documents. All documents available through a Service are accessible via the 'repo' route. This route provides access to the repository root collection, containing documents and/or child collections. Use metadata property names and regular expressions in URL query string to search for entries (documents or collections) and the offset and limit parameters to control the number of results returned. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_get example
*** Access the document repository within a service

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_offset:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_offset type /BLCK/OP4_INT.

*   for parameter i_limit:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_limit type /BLCK/OP4_INT.

*   for parameter i_sort:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sort type /BLCK/OP4_STRING.

*   for parameter i_scope:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_scope type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY_TT
    data gr_http200 type /BLCK/OP4_REPO_ENTRY_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvi_offset = 42.
*   gvi_limit = 42.
*   gvs_sort = 'ipsum lorem'.
*   gvs_scope = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_get via HTTP GET
*** i_sid: ID of the current repository.
*** i_offset: Index of first result to return.
*** i_limit: Number of results to return. Maximum is 500.
*** i_sort: Sort  query  results.  Comma separated list of property names, prefixed with
*** '-' for descending sort order. Example: 'sort=date,-name'
*** i_scope: Set  the  scope when searching for documents. Possible values are `root` and
*** `all`, default is `all`.
*** i_embed: Include  sub-ressource  or sub-collection data in response. \"permissions\":
*** include  access  rights  records  for  each entry. \"thumb\": include base64
*** encoded   thumbnail   image   for  each  entry,  e.g.  ```  \"embedded\":  {
*** \"content-type\": \"image/png\"   \"thumb\": \"A9cX0...\" } ```
    /blck/op4_cl_CollectionsApi=>services_sid_repo_get(
      exporting
        i_sid = gvs_sid
        i_offset = gvi_offset
        i_limit = gvi_limit
        i_sort = gvs_sort
        i_scope = gvs_scope
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current repository. 
 **i_offset** | /BLCK/OP4_INT | Index of first result to return. [default "0"]
 **i_limit** | /BLCK/OP4_INT | Number of results to return. Maximum is 500. [default "50"]
 **i_sort** | /BLCK/OP4_STRING | Sort query results. Comma separated list of property names, prefixed with &#x27;-&#x27; for descending sort order. Example: &#x27;sort&#x3D;date,-name&#x27;  [optional]
 **i_scope** | /BLCK/OP4_STRING | Set the scope when searching for documents. Possible values are &#x60;root&#x60; and &#x60;all&#x60;, default is &#x60;all&#x60;.  [default "all"]
 **i_embed** | /BLCK/OP4_STRING | Include sub-ressource or sub-collection data in response. \&quot;permissions\&quot;: include access rights records for each entry. \&quot;thumb\&quot;: include base64 encoded thumbnail image for each entry, e.g. &#x60;&#x60;&#x60; \&quot;embedded\&quot;: {   \&quot;content-type\&quot;: \&quot;image/png\&quot;   \&quot;thumb\&quot;: \&quot;A9cX0...\&quot; } &#x60;&#x60;&#x60;  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY_TT (**[array](#markdown-header-model-)**) | OK, collection of entries is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide a repository
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_repo_post**
Create new entry in the root collection of the repository.

Creates a new record in the current Repository, inside the root collection, and assigns the posted metadata. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_post example
*** Create new entry in the root collection of the repository.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_BASEREPOENTRY
    data gm_body type /BLCK/OP4_BASEREPOENTRY.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_post via HTTP POST
*** i_body: metadata of the entry to be created
*** i_sid: ID of the current service.
    /blck/op4_cl_CollectionsApi=>services_sid_repo_post(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_BASEREPOENTRY (**[baserepoentry](#markdown-header-model-baserepoentry)**) | metadata of the entry to be created 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry created. Entry metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide a repository
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_delete**
Delete the current entry.

Removes the current entry from the repository. This will not only remove the reference within Operator, but the actual record and content in the target system. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_uuid_delete example
*** Delete the current entry.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.

*   for parameter i_force:
*   a simple ABAP primitive of type /BLCK/OP4_BOOL
    data gv_force type /BLCK/OP4_BOOL.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_TASK_TT
    data gr_http409 type /BLCK/OP4_TASK_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.
*   gv_force = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_delete via HTTP DELETE
*** i_sid: ID of the current Service.
*** i_uuid: UUID of the entry to delete
*** i_force: Delete document even if it's still in use by one or more tasks.
    /blck/op4_cl_CollectionsApi=>services_sid_repo_uuid_delete(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
        i_force = gv_force
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_TASK_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current Service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the entry to delete 
 **i_force** | /BLCK/OP4_BOOL | Delete document even if it&#x27;s still in use by one or more tasks. [optional]

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_get**
Retrieve metadata of a specific entry (document or collection).

Given a 'uuid' parameter, this route retrieves an entry's metadata. The entry may be either a document or a collection. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_uuid_get example
*** Retrieve metadata of a specific entry (document or collection).

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_get via HTTP GET
*** i_sid: ID of the current service.
*** i_uuid: ID of the repository entry
    /blck/op4_cl_CollectionsApi=>services_sid_repo_uuid_get(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_uuid** | /BLCK/OP4_STRING | ID of the repository entry 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The given uuid was not found.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_patch**
Update entry metadata (partial, merge)

Update the given entry's metadata. Only data given with the patch will be changed/added; no entries removed. Only core metadata can be updated; internal auto-generated metadata (links, embedded), if given, are ignored. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_uuid_patch example
*** Update entry metadata (partial, merge)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_BASEREPOENTRY
    data gm_body type /BLCK/OP4_BASEREPOENTRY.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_patch via HTTP PATCH
*** i_body: New entry metadata.
*** i_sid: ID of the current service.
*** i_uuid: UUID of the entry
    /blck/op4_cl_CollectionsApi=>services_sid_repo_uuid_patch(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_BASEREPOENTRY (**[baserepoentry](#markdown-header-model-baserepoentry)**) | New entry metadata. 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the entry 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry metadata replaced, new metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | No entry found at the given &#x27;uuid&#x27;.
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_post**
Create a new entry in the current collection (collections only).

If the entry under the given uuid is a collection, then a POST request to this route will create a new entry in this collection. Whether the created entry will be a document or another collection depends on the metadata enclosed in the request body. See RepoEntry data model. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_uuid_post example
*** Create a new entry in the current collection (collections only).

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_BASEREPOENTRY
    data gm_body type /BLCK/OP4_BASEREPOENTRY.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP405 we expect type /BLCK/OP4_ERROR
    data gr_http405 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_post via HTTP POST
*** i_body: Metadata of the entry to create
*** i_sid: ID of the current Service.
*** i_uuid: UUID of the collection
    /blck/op4_cl_CollectionsApi=>services_sid_repo_uuid_post(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_405 = gr_http405
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 405.
*       do something with gr_http405 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_BASEREPOENTRY (**[baserepoentry](#markdown-header-model-baserepoentry)**) | Metadata of the entry to create 
 **i_sid** | /BLCK/OP4_STRING | ID of the current Service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the collection 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, new entry created, metadata of the entry returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | No entry found at the given &#x27;uuid&#x27;.
 405 | **e_405** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Method not allowed. The entry under &#x27;uuid&#x27; is not a collection. 
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_put**
Update entry metadata (complete, replace)

Completely replace the metadata record of the given entry. Only record metadata can be replaced; internal auto-generated metadata (links, embedded), if given, are ignored. 


### Example
```abap
*** method CollectionsApi->services_sid_repo_uuid_put example
*** Update entry metadata (complete, replace)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_BASEREPOENTRY
    data gm_body type /BLCK/OP4_BASEREPOENTRY.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_put via HTTP PUT
*** i_body: New  entry  metadata.  Note  that changing the entry type is not possible by
*** updating metadata.
*** i_sid: ID of the current repository.
*** i_uuid: UUID of the entry
    /blck/op4_cl_CollectionsApi=>services_sid_repo_uuid_put(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_BASEREPOENTRY (**[baserepoentry](#markdown-header-model-baserepoentry)**) | New entry metadata. Note that changing the entry type is not possible by updating metadata.  
 **i_sid** | /BLCK/OP4_STRING | ID of the current repository. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the entry 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry metadata replaced, new metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | No entry found under the given &#x27;uuid&#x27;.
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidrepocommandcidget**
Access a command resource within a service

Returns a JSON object containing the status of the command. Command resources are automatically deleted after a final state (success or failure) was delivered once to the client or it's expired. 


### Example
```abap
*** method CollectionsApi->servicessidrepocommandcidget example
*** Access a command resource within a service

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_cid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_cid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_COMMAND_STATUS
    data gr_http200 type /BLCK/OP4_COMMAND_STATUS.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_cid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidrepocommandcidget via HTTP GET
*** i_sid: ID of the current service.
*** i_cid: ID of the command.
    /blck/op4_cl_CollectionsApi=>servicessidrepocommandcidget(
      exporting
        i_sid = gvs_sid
        i_cid = gvs_cid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_COMMAND_STATUS)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_cid** | /BLCK/OP4_STRING | ID of the command. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_COMMAND_STATUS (**[CommandStatus](#markdown-header-model-)**) | OK, status of command resource is returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide the given resource.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidrepouuidchildrenget**
Access a collections children.

Some services (not all) expose access to documents. All documents available through a Service are accessible via the 'repo' route. This route provides access to the children of a collection, containing documents and/or collections. Use metadata property names and regular expressions in URL query string to search for entries (documents or collections) ae offset and limit parameters to control the number of results returned. 


### Example
```abap
*** method CollectionsApi->servicessidrepouuidchildrenget example
*** Access a collections children.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.

*   for parameter i_offset:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_offset type /BLCK/OP4_INT.

*   for parameter i_limit:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_limit type /BLCK/OP4_INT.

*   for parameter i_sort:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sort type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY_TT
    data gr_http200 type /BLCK/OP4_REPO_ENTRY_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.
*   gvi_offset = 42.
*   gvi_limit = 42.
*   gvs_sort = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_CollectionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidrepouuidchildrenget via HTTP GET
*** i_sid: ID of the current repository.
*** i_uuid: UUID of the parent collection
*** i_offset: Index of first result to return.
*** i_limit: Number of results to return. Maximum is 500.
*** i_sort: Sort  query  results.  Comma separated list of property names, prefixed with
*** '-' for descending sort order. Example: 'sort=date,-name'
*** i_embed: Include  sub-ressource  or sub-collection data in response. \"permissions\":
*** include  access  rights  records for each entry. \"icon\": include icon-font
*** and   value   for   each  entry,  e.g.  ```  \"embedded\":  {      \"icon\":
*** \"material:play\"  }  ```  \"thumb\": include base64 encoded thumbnail image
*** for  each  entry, e.g. ``` \"embedded\": {   \"content-type\": \"image/png\"
*** \"thumb\": \"A9cX0...\" } ```
    /blck/op4_cl_CollectionsApi=>servicessidrepouuidchildrenget(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
        i_offset = gvi_offset
        i_limit = gvi_limit
        i_sort = gvs_sort
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current repository. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the parent collection 
 **i_offset** | /BLCK/OP4_INT | Index of first result to return. [default "0"]
 **i_limit** | /BLCK/OP4_INT | Number of results to return. Maximum is 500. [default "50"]
 **i_sort** | /BLCK/OP4_STRING | Sort query results. Comma separated list of property names, prefixed with &#x27;-&#x27; for descending sort order. Example: &#x27;sort&#x3D;date,-name&#x27;  [optional]
 **i_embed** | /BLCK/OP4_STRING | Include sub-ressource or sub-collection data in response. \&quot;permissions\&quot;: include access rights records for each entry. \&quot;icon\&quot;: include icon-font and value for each entry, e.g. &#x60;&#x60;&#x60; \&quot;embedded\&quot;: {   \&quot;icon\&quot;: \&quot;material:play\&quot; } &#x60;&#x60;&#x60; \&quot;thumb\&quot;: include base64 encoded thumbnail image for each entry, e.g. &#x60;&#x60;&#x60; \&quot;embedded\&quot;: {   \&quot;content-type\&quot;: \&quot;image/png\&quot;   \&quot;thumb\&quot;: \&quot;A9cX0...\&quot; } &#x60;&#x60;&#x60;  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY_TT (**[array](#markdown-header-model-)**) | OK, collection of entries is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide a repository
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: ConfigurationApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **config_delete**
Delete a configuration item

Deletes a single ConfigItem at the given path or all ConfigItems in the whole tree below if path does not point to an actual item. 


### Example
```abap
*** method ConfigurationApi->config_delete example
*** Delete a configuration item

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_path:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_path type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_path = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConfigurationApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method config_delete via HTTP DELETE
*** i_path: Path/to/config/item
    /blck/op4_cl_ConfigurationApi=>config_delete(
      exporting
        i_path = gvs_path
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/OP4_STRING | Path/to/config/item 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, configuration deleted.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | value not returned |  | Forbidden. User lacks access rights to change configuration. schema:   _ref: &#x27;#/definitions/Error&#x27; 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **config_get**
Access a configuration item or path

Use this route to browse the configuration. Configuration is structured unix file-system like, in a path/to/item way. Use path/to/item as 'path' parameter to access a specific item or together with 'keys' parameter for retrieving only keys. 


### Example
```abap
*** method ConfigurationApi->config_get example
*** Access a configuration item or path

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_path:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_path type /BLCK/OP4_STRING.

*   for parameter i_keys:
*   a simple ABAP primitive of type /BLCK/OP4_BOOL
    data gv_keys type /BLCK/OP4_BOOL.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_STRING
    data gr_http200 type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_path = 'ipsum lorem'.
*   gv_keys = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConfigurationApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method config_get via HTTP GET
*** i_path: Path/to/config/item
*** i_keys: Return an array of strings containing all recursively fetched keys below the
*** given  'path'.  Without  or an empty 'path' all available keys are returned.
*** **Example      response:**     ```     [     \"key1\",     \"path/to/key2\",
*** \"some/other/path/to/key3\" ] ```
    /blck/op4_cl_ConfigurationApi=>config_get(
      exporting
        i_path = gvs_path
        i_keys = gv_keys
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_STRING)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/OP4_STRING | Path/to/config/item [optional]
 **i_keys** | /BLCK/OP4_BOOL | Return an array of strings containing all recursively fetched keys below the given &#x27;path&#x27;. Without or an empty &#x27;path&#x27; all available keys are returned.   **Example response:** &#x60;&#x60;&#x60; [ \&quot;key1\&quot;, \&quot;path/to/key2\&quot;, \&quot;some/other/path/to/key3\&quot; ] &#x60;&#x60;&#x60;  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_STRING | OK, configuration items returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The given ConfigItem was not found.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **config_put**
Store a configuration item

Stores the ConfigItem in the request body at the given path. 


### Example
```abap
*** method ConfigurationApi->config_put example
*** Store a configuration item

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_body type /BLCK/OP4_STRING.

*   for parameter i_path:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_path type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvs_path = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConfigurationApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method config_put via HTTP PUT
*** i_path: Path/to/config/item
    /blck/op4_cl_ConfigurationApi=>config_put(
      exporting
        i_body = gvs_body
        i_path = gvs_path
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_STRING |  
 **i_path** | /BLCK/OP4_STRING | Path/to/config/item [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, configuration stored.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | value not returned |  | Forbidden. User lacks access rights to change configuration. schema:   _ref: &#x27;#/definitions/Error&#x27; 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


# API: ConnectorsApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **services_sid_get**
Retrieve service metadata

FIXME 


### Example
```abap
*** method ConnectorsApi->services_sid_get example
*** Retrieve service metadata

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_SERVICE
    data gr_http200 type /BLCK/OP4_SERVICE.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConnectorsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_get via HTTP GET
*** i_sid: ID of the current service.
    /blck/op4_cl_ConnectorsApi=>services_sid_get(
      exporting
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_SERVICE)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_SERVICE (**[Service](#markdown-header-model-)**) | OK, service metadata is returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service metadata. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The requested Service was not found.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidconnectortaskspost**
Handle jobs in backend system

A POST call to this route will create new jobs and return their connector id's (cid's). 


### Example
```abap
*** method ConnectorsApi->servicessidconnectortaskspost example
*** Handle jobs in backend system

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_CID_COMMAND
    data gm_body type /BLCK/OP4_CID_COMMAND.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CID_STATUS
    data gr_http200 type /BLCK/OP4_CID_STATUS.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-action = l_action. " (type /BLCK/OP4_ACTION)
*   gm_body-data = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConnectorsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidconnectortaskspost via HTTP POST
*** i_body: Action to be performed (start, abort, pause, resume)
*** i_sid: ID of the Service managing the current Task
    /blck/op4_cl_ConnectorsApi=>servicessidconnectortaskspost(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CID_STATUS)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_CID_COMMAND (**[cid_command](#markdown-header-model-cid_command)**) | Action to be performed (start, abort, pause, resume) 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CID_STATUS (**[CidStatus](#markdown-header-model-)**) | OK, task data for update is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service list. 
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidconnectortasksput**
Get status and output files

A PUT call to this route returns an array with status and output listItems for all given cid's. 


### Example
```abap
*** method ConnectorsApi->servicessidconnectortasksput example
*** Get status and output files

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a table type /BLCK/OP4_CID_TASKDATA_TTT
    data gi_body type /BLCK/OP4_CID_TASKDATA_TTT.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CID_STATUS_TT
    data gr_http200 type /BLCK/OP4_CID_STATUS_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   data lr_body like line of gi_body.
*   lr_body = ...
*   append lr_body to gi_body.
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConnectorsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidconnectortasksput via HTTP PUT
*** i_body: List of task cids for which to retrieve status
*** i_sid: ID of the Service managing the current Task
    /blck/op4_cl_ConnectorsApi=>servicessidconnectortasksput(
      exporting
        i_body = gi_body
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CID_STATUS_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_CID_TASKDATA_TTT (**[array of cid_taskdata](#markdown-header-model-)**) | List of task cids for which to retrieve status 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CID_STATUS_TT (**[array](#markdown-header-model-)**) | OK, array of task data for update is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service list. 
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **ui_get**
Retrieve list of default UI panels available to the user.

The SEAL Operator user interface provides the user with a set of default panels to use. A GET call to this route returns a list of panels available to the current user. Default panels cannot be edited or deleted. 


### Example
```abap
*** method ConnectorsApi->ui_get example
*** Retrieve list of default UI panels available to the user.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_PANEL_ITEM_TT
    data gr_http200 type /BLCK/OP4_PANEL_ITEM_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConnectorsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method ui_get via HTTP GET
    /blck/op4_cl_ConnectorsApi=>ui_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_PANEL_ITEM_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_PANEL_ITEM_TT (**[array](#markdown-header-model-)**) | OK, list of UI panel configurations returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **ui_pid_get**
Retrieve the default configuration of a UI panel.

A GET call to this route returns a JSON object containing the default configuration of the panel. 


### Example
```abap
*** method ConnectorsApi->ui_pid_get example
*** Retrieve the default configuration of a UI panel.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_pid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_pid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_pid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ConnectorsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method ui_pid_get via HTTP GET
    /blck/op4_cl_ConnectorsApi=>ui_pid_get(
      exporting
        i_pid = gvs_pid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pid** | /BLCK/OP4_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, panel configuration is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: DocumentsApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **services_sid_repo_command_post**
Create new command resource.

Creates a new record in the command resource. It returns a JSON object containing a command id for tracking status of asynchronous commands. 


### Example
```abap
*** method DocumentsApi->services_sid_repo_command_post example
*** Create new command resource.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_COMMAND
    data gm_body type /BLCK/OP4_COMMAND.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_COMMAND_STATUS
    data gr_http200 type /BLCK/OP4_COMMAND_STATUS.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-action = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-parameter = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_command_post via HTTP POST
*** i_body: The  command  entry  and  it's  parameter to be created. Currently supported
*** commands  are `copy` and `move`. The parameters for both commands: ```json {
*** \"action\":  \"copy|move\",      \"parameter\":  {      \"source\": \"source
*** href\",       \"parent\": \"uuid of target parent\"   } } ``` The source may
*** be  a  remote  repository  in  later implementations, so an `href` is needed
*** here.
*** i_sid: ID of the current service.
    /blck/op4_cl_DocumentsApi=>services_sid_repo_command_post(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_COMMAND_STATUS)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_COMMAND (**[command](#markdown-header-model-command)**) | The command entry and it&#x27;s parameter to be created. Currently supported  commands are &#x60;copy&#x60; and &#x60;move&#x60;. The parameters for both commands: &#x60;&#x60;&#x60;json {   \&quot;action\&quot;: \&quot;copy|move\&quot;,   \&quot;parameter\&quot;: {     \&quot;source\&quot;: \&quot;source href\&quot;,     \&quot;parent\&quot;: \&quot;uuid of target parent\&quot;   } } &#x60;&#x60;&#x60; The source may be a remote repository in later implementations, so an &#x60;href&#x60; is needed here.  
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_COMMAND_STATUS (**[CommandStatus](#markdown-header-model-)**) | OK, entry created. Command id will be returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide commands
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_repo_get**
Access the document repository within a service

Some services (not all) expose access to documents. All documents available through a Service are accessible via the 'repo' route. This route provides access to the repository root collection, containing documents and/or child collections. Use metadata property names and regular expressions in URL query string to search for entries (documents or collections) and the offset and limit parameters to control the number of results returned. 


### Example
```abap
*** method DocumentsApi->services_sid_repo_get example
*** Access the document repository within a service

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_offset:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_offset type /BLCK/OP4_INT.

*   for parameter i_limit:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_limit type /BLCK/OP4_INT.

*   for parameter i_sort:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sort type /BLCK/OP4_STRING.

*   for parameter i_scope:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_scope type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY_TT
    data gr_http200 type /BLCK/OP4_REPO_ENTRY_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvi_offset = 42.
*   gvi_limit = 42.
*   gvs_sort = 'ipsum lorem'.
*   gvs_scope = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_get via HTTP GET
*** i_sid: ID of the current repository.
*** i_offset: Index of first result to return.
*** i_limit: Number of results to return. Maximum is 500.
*** i_sort: Sort  query  results.  Comma separated list of property names, prefixed with
*** '-' for descending sort order. Example: 'sort=date,-name'
*** i_scope: Set  the  scope when searching for documents. Possible values are `root` and
*** `all`, default is `all`.
*** i_embed: Include  sub-ressource  or sub-collection data in response. \"permissions\":
*** include  access  rights  records  for  each entry. \"thumb\": include base64
*** encoded   thumbnail   image   for  each  entry,  e.g.  ```  \"embedded\":  {
*** \"content-type\": \"image/png\"   \"thumb\": \"A9cX0...\" } ```
    /blck/op4_cl_DocumentsApi=>services_sid_repo_get(
      exporting
        i_sid = gvs_sid
        i_offset = gvi_offset
        i_limit = gvi_limit
        i_sort = gvs_sort
        i_scope = gvs_scope
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current repository. 
 **i_offset** | /BLCK/OP4_INT | Index of first result to return. [default "0"]
 **i_limit** | /BLCK/OP4_INT | Number of results to return. Maximum is 500. [default "50"]
 **i_sort** | /BLCK/OP4_STRING | Sort query results. Comma separated list of property names, prefixed with &#x27;-&#x27; for descending sort order. Example: &#x27;sort&#x3D;date,-name&#x27;  [optional]
 **i_scope** | /BLCK/OP4_STRING | Set the scope when searching for documents. Possible values are &#x60;root&#x60; and &#x60;all&#x60;, default is &#x60;all&#x60;.  [default "all"]
 **i_embed** | /BLCK/OP4_STRING | Include sub-ressource or sub-collection data in response. \&quot;permissions\&quot;: include access rights records for each entry. \&quot;thumb\&quot;: include base64 encoded thumbnail image for each entry, e.g. &#x60;&#x60;&#x60; \&quot;embedded\&quot;: {   \&quot;content-type\&quot;: \&quot;image/png\&quot;   \&quot;thumb\&quot;: \&quot;A9cX0...\&quot; } &#x60;&#x60;&#x60;  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY_TT (**[array](#markdown-header-model-)**) | OK, collection of entries is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide a repository
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_repo_post**
Create new entry in the root collection of the repository.

Creates a new record in the current Repository, inside the root collection, and assigns the posted metadata. 


### Example
```abap
*** method DocumentsApi->services_sid_repo_post example
*** Create new entry in the root collection of the repository.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_BASEREPOENTRY
    data gm_body type /BLCK/OP4_BASEREPOENTRY.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_post via HTTP POST
*** i_body: metadata of the entry to be created
*** i_sid: ID of the current service.
    /blck/op4_cl_DocumentsApi=>services_sid_repo_post(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_BASEREPOENTRY (**[baserepoentry](#markdown-header-model-baserepoentry)**) | metadata of the entry to be created 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry created. Entry metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide a repository
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_delete**
Delete the current entry.

Removes the current entry from the repository. This will not only remove the reference within Operator, but the actual record and content in the target system. 


### Example
```abap
*** method DocumentsApi->services_sid_repo_uuid_delete example
*** Delete the current entry.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.

*   for parameter i_force:
*   a simple ABAP primitive of type /BLCK/OP4_BOOL
    data gv_force type /BLCK/OP4_BOOL.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_TASK_TT
    data gr_http409 type /BLCK/OP4_TASK_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.
*   gv_force = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_delete via HTTP DELETE
*** i_sid: ID of the current Service.
*** i_uuid: UUID of the entry to delete
*** i_force: Delete document even if it's still in use by one or more tasks.
    /blck/op4_cl_DocumentsApi=>services_sid_repo_uuid_delete(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
        i_force = gv_force
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_TASK_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current Service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the entry to delete 
 **i_force** | /BLCK/OP4_BOOL | Delete document even if it&#x27;s still in use by one or more tasks. [optional]

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_get**
Retrieve metadata of a specific entry (document or collection).

Given a 'uuid' parameter, this route retrieves an entry's metadata. The entry may be either a document or a collection. 


### Example
```abap
*** method DocumentsApi->services_sid_repo_uuid_get example
*** Retrieve metadata of a specific entry (document or collection).

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_get via HTTP GET
*** i_sid: ID of the current service.
*** i_uuid: ID of the repository entry
    /blck/op4_cl_DocumentsApi=>services_sid_repo_uuid_get(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_uuid** | /BLCK/OP4_STRING | ID of the repository entry 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The given uuid was not found.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_patch**
Update entry metadata (partial, merge)

Update the given entry's metadata. Only data given with the patch will be changed/added; no entries removed. Only core metadata can be updated; internal auto-generated metadata (links, embedded), if given, are ignored. 


### Example
```abap
*** method DocumentsApi->services_sid_repo_uuid_patch example
*** Update entry metadata (partial, merge)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_BASEREPOENTRY
    data gm_body type /BLCK/OP4_BASEREPOENTRY.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_patch via HTTP PATCH
*** i_body: New entry metadata.
*** i_sid: ID of the current service.
*** i_uuid: UUID of the entry
    /blck/op4_cl_DocumentsApi=>services_sid_repo_uuid_patch(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_BASEREPOENTRY (**[baserepoentry](#markdown-header-model-baserepoentry)**) | New entry metadata. 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the entry 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry metadata replaced, new metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | No entry found at the given &#x27;uuid&#x27;.
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_repo_uuid_put**
Update entry metadata (complete, replace)

Completely replace the metadata record of the given entry. Only record metadata can be replaced; internal auto-generated metadata (links, embedded), if given, are ignored. 


### Example
```abap
*** method DocumentsApi->services_sid_repo_uuid_put example
*** Update entry metadata (complete, replace)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_BASEREPOENTRY
    data gm_body type /BLCK/OP4_BASEREPOENTRY.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_REPO_ENTRY
    data gr_http200 type /BLCK/OP4_REPO_ENTRY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_repo_uuid_put via HTTP PUT
*** i_body: New  entry  metadata.  Note  that changing the entry type is not possible by
*** updating metadata.
*** i_sid: ID of the current repository.
*** i_uuid: UUID of the entry
    /blck/op4_cl_DocumentsApi=>services_sid_repo_uuid_put(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_REPO_ENTRY)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_BASEREPOENTRY (**[baserepoentry](#markdown-header-model-baserepoentry)**) | New entry metadata. Note that changing the entry type is not possible by updating metadata.  
 **i_sid** | /BLCK/OP4_STRING | ID of the current repository. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the entry 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_REPO_ENTRY (**[RepoEntry](#markdown-header-model-)**) | OK, entry metadata replaced, new metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | No entry found under the given &#x27;uuid&#x27;.
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidrepocommandcidget**
Access a command resource within a service

Returns a JSON object containing the status of the command. Command resources are automatically deleted after a final state (success or failure) was delivered once to the client or it's expired. 


### Example
```abap
*** method DocumentsApi->servicessidrepocommandcidget example
*** Access a command resource within a service

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_cid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_cid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_COMMAND_STATUS
    data gr_http200 type /BLCK/OP4_COMMAND_STATUS.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_cid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidrepocommandcidget via HTTP GET
*** i_sid: ID of the current service.
*** i_cid: ID of the command.
    /blck/op4_cl_DocumentsApi=>servicessidrepocommandcidget(
      exporting
        i_sid = gvs_sid
        i_cid = gvs_cid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_COMMAND_STATUS)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_cid** | /BLCK/OP4_STRING | ID of the command. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_COMMAND_STATUS (**[CommandStatus](#markdown-header-model-)**) | OK, status of command resource is returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide the given resource.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidrepouuidcontentdele**
Delete document binary content (documents only)

Deletes the binary content of a document, leaving metadata only. Note that some repositories will not allow this operation. To delete binary content from such repositories, you will need to delete the entire document. Deleting binary content is not supported by collection type entries. 


### Example
```abap
*** method DocumentsApi->servicessidrepouuidcontentdele example
*** Delete document binary content (documents only)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP405 we expect type /BLCK/OP4_ERROR
    data gr_http405 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_TASK_TT
    data gr_http409 type /BLCK/OP4_TASK_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidrepouuidcontentdele via HTTP DELETE
*** i_sid: ID of the current service.
*** i_uuid: UUID of the document
    /blck/op4_cl_DocumentsApi=>servicessidrepouuidcontentdele(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_405 = gr_http405
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 405.
*       do something with gr_http405 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_TASK_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the document 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidrepouuidcontentget**
Retrieve binary content (documents only)

If the entry under 'uuid' is a document, then this route provides access to the binary content (i.e. the actual file). 


### Example
```abap
*** method DocumentsApi->servicessidrepouuidcontentget example
*** Retrieve binary content (documents only)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidrepouuidcontentget via HTTP GET
*** i_sid: ID of the current Service.
*** i_uuid: UUID of the document
    /blck/op4_cl_DocumentsApi=>servicessidrepouuidcontentget(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current Service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the document 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application-octed/stream


## operation: **servicessidrepouuidcontentput**
Create or update document binary content (documents only)

Upload binary content of a document. Create if none exists, or replace existing file. Uploading binary content to collection type entries is not supported. 


### Example
```abap
*** method DocumentsApi->servicessidrepouuidcontentput example
*** Create or update document binary content (documents only)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.

*   for parameter i_content:
*   a simple ABAP primitive of type /BLCK/OP4_BINARY
    data gvs_content type /BLCK/OP4_BINARY.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP406 we expect type /BLCK/OP4_ERROR
    data gr_http406 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.
*   gvs_content = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidrepouuidcontentput via HTTP PUT
*** i_sid: ID of the current service.
*** i_uuid: UUID of the document
    /blck/op4_cl_DocumentsApi=>servicessidrepouuidcontentput(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
        i_content = gvs_content
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_406 = gr_http406
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 406.
*       do something with gr_http406 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the document 
 **i_content** | /BLCK/OP4_BINARY |  [optional]

### Return types


### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json


## operation: **servicessidrepouuidpreviewget**
Retrieve preview of binary content (documents only)

If the entry under 'uuid' is a document, then this route provides access to the preview content. 


### Example
```abap
*** method DocumentsApi->servicessidrepouuidpreviewget example
*** Retrieve preview of binary content (documents only)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidrepouuidpreviewget via HTTP GET
*** i_sid: ID of the current Service.
*** i_uuid: UUID of the document
    /blck/op4_cl_DocumentsApi=>servicessidrepouuidpreviewget(
      exporting
        i_sid = gvs_sid
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current Service. 
 **i_uuid** | /BLCK/OP4_STRING | UUID of the document 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: image/jpeg


# API: FunctionsApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **services_sid_function_fid_post**
Access a connector specific function

This route triggers a connector specific function and returns the result. The function routes are synchronous calls in contrary to the asynchronous commands. 


### Example
```abap
*** method FunctionsApi->services_sid_function_fid_post example
*** Access a connector specific function

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_fid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_fid type /BLCK/OP4_STRING.

*   for parameter i_params:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_params type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_fid = 'ipsum lorem'.
*   gvs_params = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_FunctionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_function_fid_post via HTTP POST
*** i_sid: ID of the current repository.
*** i_fid: Name of the function to calls
*** i_params: String  with  a  list  of  function  specific  parameter as key value pairs.
*** Syntax: ``` params=\"key::value[;key::value]*\" ```
    /blck/op4_cl_FunctionsApi=>services_sid_function_fid_post(
      exporting
        i_sid = gvs_sid
        i_fid = gvs_fid
        i_params = gvs_params
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current repository. 
 **i_fid** | /BLCK/OP4_STRING | Name of the function to calls 
 **i_params** | /BLCK/OP4_STRING | String with a list of function specific parameter as key value pairs. Syntax: &#x60;&#x60;&#x60; params&#x3D;\&quot;key::value[;key::value]*\&quot; &#x60;&#x60;&#x60;  [optional]

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_function_get**
List connector specific functions

For panels static configuration data is sometimes not sufficient, dynamically retrieved data from the backend system is needed. The function routes allows the connector to make dynamic data and functionality available to the client. The function routes are synchronous calls in contrary to the asynchronous commands. This route returns all supported functions. 


### Example
```abap
*** method FunctionsApi->services_sid_function_get example
*** List connector specific functions

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_FUNCTIONS
    data gr_http200 type /BLCK/OP4_FUNCTIONS.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_FunctionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_function_get via HTTP GET
*** i_sid: ID of the current repository.
    /blck/op4_cl_FunctionsApi=>services_sid_function_get(
      exporting
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_FUNCTIONS)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current repository. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_FUNCTIONS (**[Functions](#markdown-header-model-)**) | OK, list of entries is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide functions
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: ListsApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **lists_get**
Get collection of available Lists.

This is the list of Lists of the authenticated user. Use metadata property names and regular expressions in URL query string to search for entries and the offset and limit parameters to control the number of results returned. 


### Example
```abap
*** method ListsApi->lists_get example
*** Get collection of available Lists.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_offset:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_offset type /BLCK/OP4_INT.

*   for parameter i_limit:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_limit type /BLCK/OP4_INT.

*   for parameter i_sort:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sort type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_TT
    data gr_http200 type /BLCK/OP4_LIST_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvi_offset = 42.
*   gvi_limit = 42.
*   gvs_sort = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_get via HTTP GET
*** i_offset: Index of first result to return.
*** i_limit: Number of results to return. Maximum is 500.
*** i_sort: Sort  query  results.  Comma separated list of property names, prefixed with
*** '-' for descending sort order. Example: 'sort=date,-name'
*** i_embed: Include information about collection members. - \"items\": Include item data
*** -  \"permissions\":  User  access rights on each List - \"metadata\": Return
*** list  of  lists metadata. Example:   ```   {     exportTypes: [{       name:
*** 'csv',          description: 'Export a CSV file',       mimeType: 'text/csv'
*** }],          importTypes: [{       name: 'csv',       description: 'Import a
*** CSV file',       mimeType: 'text/csv'     }]   }   ```
    /blck/op4_cl_ListsApi=>lists_get(
      exporting
        i_offset = gvi_offset
        i_limit = gvi_limit
        i_sort = gvs_sort
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_offset** | /BLCK/OP4_INT | Index of first result to return. [default "0"]
 **i_limit** | /BLCK/OP4_INT | Number of results to return. Maximum is 500. [default "50"]
 **i_sort** | /BLCK/OP4_STRING | Sort query results. Comma separated list of property names, prefixed with &#x27;-&#x27; for descending sort order. Example: &#x27;sort&#x3D;date,-name&#x27;  [optional]
 **i_embed** | /BLCK/OP4_STRING | Include information about collection members. - \&quot;items\&quot;: Include item data - \&quot;permissions\&quot;: User access rights on each List - \&quot;metadata\&quot;: Return list of lists metadata. Example:   &#x60;&#x60;&#x60;   {     exportTypes: [{       name: &#x27;csv&#x27;,       description: &#x27;Export a CSV file&#x27;,       mimeType: &#x27;text/csv&#x27;     }],     importTypes: [{       name: &#x27;csv&#x27;,       description: &#x27;Import a CSV file&#x27;,       mimeType: &#x27;text/csv&#x27;     }]   }   &#x60;&#x60;&#x60;  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_TT (**[array](#markdown-header-model-)**) | OK, collection of lists is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | No lists available
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **lists_lid_delete**
Delete the current list

Deletes the current list inclusive all it's items, but not the documents. 


### Example
```abap
*** method ListsApi->lists_lid_delete example
*** Delete the current list

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_delete via HTTP DELETE
*** i_lid: ID of the current list.
    /blck/op4_cl_ListsApi=>lists_lid_delete(
      exporting
        i_lid = gvs_lid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **lists_lid_get**
Retrieve metadata for the current List.

This is the root record for a given list. It contains List-level metadata. Use the 'embed' parameter to include information about sub-ressource like items or access rights. The client controls the exported data format with the `Accept` HTTP header field. Default is JSON. 


### Example
```abap
*** method ListsApi->lists_lid_get example
*** Retrieve metadata for the current List.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_get via HTTP GET
*** i_lid: ID of the current list.
*** i_embed: Include information about collection members or sub-ressources. - \"items\":
*** Include  item  data  -  \"permissions\":  Include user access rights for the
*** current user.
    /blck/op4_cl_ListsApi=>lists_lid_get(
      exporting
        i_lid = gvs_lid
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_embed** | /BLCK/OP4_STRING | Include information about collection members or sub-ressources. - \&quot;items\&quot;: Include item data - \&quot;permissions\&quot;: Include user access rights for the current user.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, metadata is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **lists_lid_items_get**
Get List items.

This is the collection of items currently in the List. For performance reasons, only references are returned by default. Use metadata property names and regular expressions in URL query string to search for entries and the offset and limit parameters to control the number of results returned. 


### Example
```abap
*** method ListsApi->lists_lid_items_get example
*** Get List items.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_offset:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_offset type /BLCK/OP4_INT.

*   for parameter i_limit:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_limit type /BLCK/OP4_INT.

*   for parameter i_sort:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sort type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM_TT
    data gr_http200 type /BLCK/OP4_LIST_ITEM_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gvi_offset = 42.
*   gvi_limit = 42.
*   gvs_sort = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_items_get via HTTP GET
*** i_lid: ID of the current list.
*** i_offset: Index of first result to return.
*** i_limit: Number of results to return. Maximum is 500.
*** i_sort: Sort  query  results.  Comma separated list of property names, prefixed with
*** '-' for descending sort order. Example: 'sort=href,-index'
*** i_embed: Sub-ressources to include in the response. - \"items\": Include metadata for
*** each List - \"permissions\": Include user access rights
    /blck/op4_cl_ListsApi=>lists_lid_items_get(
      exporting
        i_lid = gvs_lid
        i_offset = gvi_offset
        i_limit = gvi_limit
        i_sort = gvs_sort
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_offset** | /BLCK/OP4_INT | Index of first result to return. [default "0"]
 **i_limit** | /BLCK/OP4_INT | Number of results to return. Maximum is 500. [default "50"]
 **i_sort** | /BLCK/OP4_STRING | Sort query results. Comma separated list of property names, prefixed with &#x27;-&#x27; for descending sort order. Example: &#x27;sort&#x3D;href,-index&#x27;  [optional]
 **i_embed** | /BLCK/OP4_STRING | Sub-ressources to include in the response. - \&quot;items\&quot;: Include metadata for each List - \&quot;permissions\&quot;: Include user access rights  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM_TT (**[array](#markdown-header-model-)**) | OK, collection of list items is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **lists_lid_items_id_delete**
Remove the current element from the list

Deletes an entry from a list. Only the list entry is removed, not the document. Note that id is NOT the index of an item in the List. The index is part of item metadata. 


### Example
```abap
*** method ListsApi->lists_lid_items_id_delete example
*** Remove the current element from the list

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_items_id_delete via HTTP DELETE
*** i_lid: ID of the current list.
*** i_id: ID of the current element.
    /blck/op4_cl_ListsApi=>lists_lid_items_id_delete(
      exporting
        i_lid = gvs_lid
        i_id = gvs_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_id** | /BLCK/OP4_STRING | ID of the current element. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **lists_lid_items_id_get**
Retrieve item data of the current list element

Get metadata record of a list item. Note that the 'id' is NOT the index, which is part of item metadata. 


### Example
```abap
*** method ListsApi->lists_lid_items_id_get example
*** Retrieve item data of the current list element

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_items_id_get via HTTP GET
*** i_lid: ID of the current list.
*** i_id: ID of the current element.
    /blck/op4_cl_ListsApi=>lists_lid_items_id_get(
      exporting
        i_lid = gvs_lid
        i_id = gvs_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_id** | /BLCK/OP4_STRING | ID of the current element. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, List item data is returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **lists_lid_items_id_patch**
Update current list item (partial, merge)

Update the metadata record of the current list item, adding missing entries but removing nothing. Note that the ID is NOT the index of the item in the list. The index is part of item metadata. 


### Example
```abap
*** method ListsApi->lists_lid_items_id_patch example
*** Update current list item (partial, merge)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.

*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST_ITEM
    data gm_body type /BLCK/OP4_LIST_ITEM.

*   for parameter i_href:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_href type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.
*   gm_body-index = 42. " (type /BLCK/OP4_INT)
*   gm_body-href = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_href = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_items_id_patch via HTTP PATCH
*** i_lid: ID of the current list.
*** i_id: ID of the current element.
*** i_body: New  link  data  to replace existing entry. Use EITHER item OR href; if both
*** are present, item is used.
*** i_href: Relative  URL of document to link. This is a convenient way of just updating
*** the href property of the existing List item.
    /blck/op4_cl_ListsApi=>lists_lid_items_id_patch(
      exporting
        i_lid = gvs_lid
        i_id = gvs_id
        i_body = gm_body
        i_href = gvs_href
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_id** | /BLCK/OP4_STRING | ID of the current element. 
 **i_body** | /BLCK/OP4_LIST_ITEM (**[list_item](#markdown-header-model-list_item)**) | New link data to replace existing entry. Use EITHER item OR href; if both are present, item is used.  [optional]
 **i_href** | /BLCK/OP4_STRING | Relative URL of document to link. This is a convenient way of just updating the href property of the existing List item.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, List item is updated, item data returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **lists_lid_items_id_put**
Update current list item (complete, replace)

Update and replace the entire metadata record of the current list item. Note that the ID is NOT the index of the item in the List. The index is part of item metadata. 


### Example
```abap
*** method ListsApi->lists_lid_items_id_put example
*** Update current list item (complete, replace)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST_ITEM
    data gm_body type /BLCK/OP4_LIST_ITEM.

*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-index = 42. " (type /BLCK/OP4_INT)
*   gm_body-href = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_lid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_items_id_put via HTTP PUT
*** i_body: New item data to replace existing entry 
*** i_lid: ID of the current list.
*** i_id: ID of the current element.
    /blck/op4_cl_ListsApi=>lists_lid_items_id_put(
      exporting
        i_body = gm_body
        i_lid = gvs_lid
        i_id = gvs_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_LIST_ITEM (**[list_item](#markdown-header-model-list_item)**) | New item data to replace existing entry  
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_id** | /BLCK/OP4_STRING | ID of the current element. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, List item is updated, item data returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **lists_lid_items_post**
Appended and item to the list.

Lists are are ordered sets, items have consecutive indices (0..n). Posting this route will append a new item to the List. 


### Example
```abap
*** method ListsApi->lists_lid_items_post example
*** Appended and item to the list.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST_ITEM
    data gm_body type /BLCK/OP4_LIST_ITEM.

*   for parameter i_href:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_href type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gm_body-index = 42. " (type /BLCK/OP4_INT)
*   gm_body-href = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_href = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_items_post via HTTP POST
*** i_lid: ID of the current list.
*** i_body: Use EITHER href OR item. If both are present, item is used. 
*** i_href: Relative URL of the document instance to add to the list 
    /blck/op4_cl_ListsApi=>lists_lid_items_post(
      exporting
        i_lid = gvs_lid
        i_body = gm_body
        i_href = gvs_href
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_body** | /BLCK/OP4_LIST_ITEM (**[list_item](#markdown-header-model-list_item)**) | Use EITHER href OR item. If both are present, item is used.  [optional]
 **i_href** | /BLCK/OP4_STRING | Relative URL of the document instance to add to the list  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, document reference has been added to the list.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **lists_lid_patch**
Update List metadata (partial, merge)

Updates or adds part of the List metadata. Only given metadata will be replaced or added, no metadata will be removed. Note that only List metadata can be updated; internal auto-generated metadata (links, embedded), if present, are ignored. 


### Example
```abap
*** method ListsApi->lists_lid_patch example
*** Update List metadata (partial, merge)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST
    data gm_body type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gm_body-uuid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-created = 42. " (type /BLCK/OP4_INT)
*   gm_body-last_modified = 42. " (type /BLCK/OP4_INT)
*   gm_body-list_length = 42. " (type /BLCK/OP4_INT)
*   gm_body-links = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-embedded = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_patch via HTTP PATCH
*** i_lid: ID of the current list.
*** i_body: New Metadata for the list 
    /blck/op4_cl_ListsApi=>lists_lid_patch(
      exporting
        i_lid = gvs_lid
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_body** | /BLCK/OP4_LIST (**[list](#markdown-header-model-list)**) | New Metadata for the list  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, document list updated. New metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **lists_lid_put**
Update List metadata (complete, replace)

This will completely replace the existing List metadata (if any) by the given metadata. Note that only List metadata itself can be updated. Internal auto-generated metadata (links; embedded), if present, are ignored. 


### Example
```abap
*** method ListsApi->lists_lid_put example
*** Update List metadata (complete, replace)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_lid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_lid type /BLCK/OP4_STRING.

*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST
    data gm_body type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_lid = 'ipsum lorem'.
*   gm_body-uuid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-created = 42. " (type /BLCK/OP4_INT)
*   gm_body-last_modified = 42. " (type /BLCK/OP4_INT)
*   gm_body-list_length = 42. " (type /BLCK/OP4_INT)
*   gm_body-links = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-embedded = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_lid_put via HTTP PUT
*** i_lid: ID of the current list.
*** i_body: New Metadata for the list 
    /blck/op4_cl_ListsApi=>lists_lid_put(
      exporting
        i_lid = gvs_lid
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_lid** | /BLCK/OP4_STRING | ID of the current list. 
 **i_body** | /BLCK/OP4_LIST (**[list](#markdown-header-model-list)**) | New Metadata for the list  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, document list updated. New metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **lists_post**
Create new List

Creates a new entry in the list of Lists. The `Content-Type` HTTP header defines the format of the import data. Default is JSON. If a URL is given in query as parameter `href` the list to import is retrieved from that URL. 


### Example
```abap
*** method ListsApi->lists_post example
*** Create new List

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST
    data gm_body type /BLCK/OP4_LIST.

*   for parameter i_href:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_href type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-uuid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-created = 42. " (type /BLCK/OP4_INT)
*   gm_body-last_modified = 42. " (type /BLCK/OP4_INT)
*   gm_body-list_length = 42. " (type /BLCK/OP4_INT)
*   gm_body-links = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-embedded = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_href = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ListsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method lists_post via HTTP POST
*** i_body: metadata of the document list to create.
*** i_href: URL of the list to add. Example: `http://somehost:3456/path/to/mylist.csv` 
    /blck/op4_cl_ListsApi=>lists_post(
      exporting
        i_body = gm_body
        i_href = gvs_href
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_LIST (**[list](#markdown-header-model-list)**) | metadata of the document list to create. 
 **i_href** | /BLCK/OP4_STRING | URL of the list to add. Example: &#x60;http://somehost:3456/path/to/mylist.csv&#x60;  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, list created. List metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


# API: MessagesApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **messages_get**
Access the users messages

Every user has his own list of messages containing info, warning and error messages of various panels and actions. The messages are stored on server until they expire. This route provides access to the messages. Use property names and regular expressions in URL query string to search for entries and the offset and limit parameters to control the number of results returned. 


### Example
```abap
*** method MessagesApi->messages_get example
*** Access the users messages

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_offset:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_offset type /BLCK/OP4_INT.

*   for parameter i_limit:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_limit type /BLCK/OP4_INT.

*   for parameter i_sort:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sort type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_MESSAGE_TT
    data gr_http200 type /BLCK/OP4_MESSAGE_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvi_offset = 42.
*   gvi_limit = 42.
*   gvs_sort = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_MessagesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method messages_get via HTTP GET
*** i_offset: Index of first result to return.
*** i_limit: Number of results to return. Maximum is 500.
*** i_sort: Sort  query  results.  Comma separated list of property names, prefixed with
*** '-' for descending sort order. Example: 'sort=date,-type'
    /blck/op4_cl_MessagesApi=>messages_get(
      exporting
        i_offset = gvi_offset
        i_limit = gvi_limit
        i_sort = gvs_sort
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_MESSAGE_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_offset** | /BLCK/OP4_INT | Index of first result to return. [default "0"]
 **i_limit** | /BLCK/OP4_INT | Number of results to return. Maximum is 500. [default "25"]
 **i_sort** | /BLCK/OP4_STRING | Sort query results. Comma separated list of property names, prefixed with &#x27;-&#x27; for descending sort order. Example: &#x27;sort&#x3D;date,-type&#x27;  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_MESSAGE_TT (**[array](#markdown-header-model-)**) | OK, list of entries is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide messages
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **messages_post**
Create new message entry.

Creates a new record in the message list and assigns the posted data. The server adds a uuid and a creation date to each entry if not already present. 


### Example
```abap
*** method MessagesApi->messages_post example
*** Create new message entry.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_MESSAGE
    data gm_body type /BLCK/OP4_MESSAGE.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_MESSAGE
    data gr_http200 type /BLCK/OP4_MESSAGE.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-uuid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-text = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-date = 42. " (type /BLCK/OP4_INT)
*   gm_body-source = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-read = 'X'. " (type /BLCK/OP4_BOOL)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_MessagesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method messages_post via HTTP POST
*** i_body: metadata of the entry to be created
    /blck/op4_cl_MessagesApi=>messages_post(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_MESSAGE)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_MESSAGE (**[message](#markdown-header-model-message)**) | metadata of the entry to be created 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_MESSAGE (**[Message](#markdown-header-model-)**) | OK, entry created. Entry metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide messages
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **messages_uuid_patch**
Update a message entry.

Update a message entry. Only data given with the patch will be  changed/added; no entries removed. Updating uuid and creation date is prohibited. 


### Example
```abap
*** method MessagesApi->messages_uuid_patch example
*** Update a message entry.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_MESSAGE
    data gm_body type /BLCK/OP4_MESSAGE.

*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_uuid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_MESSAGE
    data gr_http200 type /BLCK/OP4_MESSAGE.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-uuid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-type = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-text = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-date = 42. " (type /BLCK/OP4_INT)
*   gm_body-source = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-read = 'X'. " (type /BLCK/OP4_BOOL)
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_MessagesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method messages_uuid_patch via HTTP PATCH
*** i_body: metadata of the entry to be created
*** i_uuid: ID of the message entry
    /blck/op4_cl_MessagesApi=>messages_uuid_patch(
      exporting
        i_body = gm_body
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_MESSAGE)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_MESSAGE (**[message](#markdown-header-model-message)**) | metadata of the entry to be created 
 **i_uuid** | /BLCK/OP4_STRING | ID of the message entry 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_MESSAGE (**[Message](#markdown-header-model-)**) | OK, message entry updated, new message returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The service does not provide messages
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


# API: PanelsApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **panels_get**
Retrieve list of UI panels available to the user.

The SEAL Operator user interface provides the user with a set of panels to use. A GET call to this route returns a list of user defined panels available to the current user. User-defined configurations can be stored using a POST request; these can also be edited and deleted later. 


### Example
```abap
*** method PanelsApi->panels_get example
*** Retrieve list of UI panels available to the user.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM_TT
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_PanelsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method panels_get via HTTP GET
    /blck/op4_cl_PanelsApi=>panels_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM_TT (**[array](#markdown-header-model-)**) | OK, list of UI panel configurations returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **panels_pid_delete**
Delete a stored panel configuration

User-defined panel configurations can be delete by a DELETE request to this route. 


### Example
```abap
*** method PanelsApi->panels_pid_delete example
*** Delete a stored panel configuration

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_pid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_pid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_pid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_PanelsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method panels_pid_delete via HTTP DELETE
*** i_pid: ID of the panel configuration to remove.
    /blck/op4_cl_PanelsApi=>panels_pid_delete(
      exporting
        i_pid = gvs_pid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pid** | /BLCK/OP4_STRING | ID of the panel configuration to remove. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, panel configuration was deleted, return deleted configuration.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | value not returned |  | Forbidden. The current user lacks access rights, or is trying to delete a read-only default configuration. schema:   _ref: &#x27;#/definitions/Error&#x27; 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **panels_pid_get**
Retrieve a specific panel configuration

Returns a ConfigItem containing configuration for a stored panel. 


### Example
```abap
*** method PanelsApi->panels_pid_get example
*** Retrieve a specific panel configuration

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_pid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_pid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_pid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_PanelsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method panels_pid_get via HTTP GET
*** i_pid: ID of the panel
    /blck/op4_cl_PanelsApi=>panels_pid_get(
      exporting
        i_pid = gvs_pid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pid** | /BLCK/OP4_STRING | ID of the panel 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, configuration returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found. The given pid is unknown.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **panels_pid_put**
Updates a saved panel configuration

A PUT request to a panel configuration will replace the entire stored configuration with the one contained in the request body. It's possible to use a different value for the \"name\" key in order to rename the saved configuration; however, the new name must not be in use. Note that only user-defined panel configurations can be updated. 


### Example
```abap
*** method PanelsApi->panels_pid_put example
*** Updates a saved panel configuration

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_body type /BLCK/OP4_STRING.

*   for parameter i_pid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_pid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvs_pid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_PanelsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method panels_pid_put via HTTP PUT
*** i_body: ConfigItem containing the configuration to store. 
*** i_pid: ID of the panel
    /blck/op4_cl_PanelsApi=>panels_pid_put(
      exporting
        i_body = gvs_body
        i_pid = gvs_pid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_STRING | ConfigItem containing the configuration to store.  
 **i_pid** | /BLCK/OP4_STRING | ID of the panel 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, configuration updated.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | value not returned |  | Forbidden. The current user lacks access rights, or is trying to update a read-only default configuration. schema:   _ref: &#x27;#/definitions/Error&#x27; 
 409 | value not returned |  | Conflict. A panel configuration under the \&quot;name\&quot; given in the ConfigItem already exists. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **panels_post**
Save a (user-specific) panel configuration.

Users can save panel configurations they intend to (re-)use in later sessions under a name. If the ConfigItem does not contain a \"name\" key, a name for the configuration will be auto-generated. 


### Example
```abap
*** method PanelsApi->panels_post example
*** Save a (user-specific) panel configuration.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_body type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_PanelsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method panels_post via HTTP POST
*** i_body: ConfigItem containing the configuration to store. 
    /blck/op4_cl_PanelsApi=>panels_post(
      exporting
        i_body = gvs_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_STRING | ConfigItem containing the configuration to store.  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, configuration was saved. The returned configItem contains the generated ID. 
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 409 | value not returned |  | Conflict. A panel configuration under the \&quot;name\&quot; given in the ConfigItem already exists. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **ui_get**
Retrieve list of default UI panels available to the user.

The SEAL Operator user interface provides the user with a set of default panels to use. A GET call to this route returns a list of panels available to the current user. Default panels cannot be edited or deleted. 


### Example
```abap
*** method PanelsApi->ui_get example
*** Retrieve list of default UI panels available to the user.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_PANEL_ITEM_TT
    data gr_http200 type /BLCK/OP4_PANEL_ITEM_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_PanelsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method ui_get via HTTP GET
    /blck/op4_cl_PanelsApi=>ui_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_PANEL_ITEM_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_PANEL_ITEM_TT (**[array](#markdown-header-model-)**) | OK, list of UI panel configurations returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **ui_pid_get**
Retrieve the default configuration of a UI panel.

A GET call to this route returns a JSON object containing the default configuration of the panel. 


### Example
```abap
*** method PanelsApi->ui_pid_get example
*** Retrieve the default configuration of a UI panel.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_pid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_pid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_CONFIG_ITEM
    data gr_http200 type /BLCK/OP4_CONFIG_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_pid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_PanelsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method ui_pid_get via HTTP GET
    /blck/op4_cl_PanelsApi=>ui_pid_get(
      exporting
        i_pid = gvs_pid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_CONFIG_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pid** | /BLCK/OP4_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_CONFIG_ITEM (**[ConfigItem](#markdown-header-model-)**) | OK, panel configuration is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: ServicesApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **services_get**
Get list of available services

A GET call to this route will return a list of active services currently available through the API. 


### Example
```abap
*** method ServicesApi->services_get example
*** Get list of available services

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_SERVICE_TT
    data gr_http200 type /BLCK/OP4_SERVICE_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ServicesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_get via HTTP GET
    /blck/op4_cl_ServicesApi=>services_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_SERVICE_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_SERVICE_TT (**[array](#markdown-header-model-)**) | OK, collection of services is returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service list. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_get**
Retrieve service metadata

FIXME 


### Example
```abap
*** method ServicesApi->services_sid_get example
*** Retrieve service metadata

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_SERVICE
    data gr_http200 type /BLCK/OP4_SERVICE.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_ServicesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_get via HTTP GET
*** i_sid: ID of the current service.
    /blck/op4_cl_ServicesApi=>services_sid_get(
      exporting
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_SERVICE)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_SERVICE (**[Service](#markdown-header-model-)**) | OK, service metadata is returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service metadata. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | The requested Service was not found.
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: SessionsApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **sessions_get**
Get session information

Get number of currently established sessions of user 


### Example
```abap
*** method SessionsApi->sessions_get example
*** Get session information

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_SESSION_INFO
    data gr_http200 type /BLCK/OP4_SESSION_INFO.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_SessionsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method sessions_get via HTTP GET
    /blck/op4_cl_SessionsApi=>sessions_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_SESSION_INFO)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_SESSION_INFO (**[SessionInfo](#markdown-header-model-)**) | OK, return object with session information
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service list. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: TasksApi

All URIs are relative to *https://operator-seal.cloudapp.net:3008/v1*

## operation: **services_sid_tasks_get**
Retrieve collection of tasks managed by the service.

This route provides access to the root collection of known tasks for the current service. Use property names and regular expressions in URL query string to search for tasks and the offset and limit parameters to control the number of results returned. Use the 'embed' parameter to include information about instances and sub-ressources. 


### Example
```abap
*** method TasksApi->services_sid_tasks_get example
*** Retrieve collection of tasks managed by the service.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_offset:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_offset type /BLCK/OP4_INT.

*   for parameter i_limit:
*   a simple ABAP primitive of type /BLCK/OP4_INT
    data gvi_limit type /BLCK/OP4_INT.

*   for parameter i_sort:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sort type /BLCK/OP4_STRING.

*   for parameter i_input_document:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_input_document type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.

*   for parameter i_inline_count:
*   a simple ABAP primitive of type /BLCK/OP4_BOOL
    data gv_inline_count type /BLCK/OP4_BOOL.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_TASK_TT
    data gr_http200 type /BLCK/OP4_TASK_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvi_offset = 42.
*   gvi_limit = 42.
*   gvs_sort = 'ipsum lorem'.
*   gvs_input_document = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.
*   gv_inline_count = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_tasks_get via HTTP GET
*** i_sid: ID of the Service managing the tasks
*** i_offset: Index of first result to return.
*** i_limit: Number of results to return. Maximum is 500.
*** i_sort: Sort  query  results.  Comma separated list of property names, prefixed with
*** '-' for descending sort order. Example: 'sort=date,-name'
*** i_input_document: A document UUID queried for in all lists of input documents of all tasks.
*** i_embed: Information  about  sub-collections  and/or sub-ressources to include in the
*** response.  -  \"permissions\":  include  user  access rights for each Task -
*** \"metadata\":  include  Task  metadata.  -  \"input\":  include  input lists
*** (metadata  only)  -  \"output\":  include  output  lists  (metadata  only) -
*** \"cstats\": connector specific job id's and states
*** i_inline_count: Return  a JSON object containing the number of tasks found, according to the
*** query parameters, instead of an array with tasks.
    /blck/op4_cl_TasksApi=>services_sid_tasks_get(
      exporting
        i_sid = gvs_sid
        i_offset = gvi_offset
        i_limit = gvi_limit
        i_sort = gvs_sort
        i_input_document = gvs_input_document
        i_embed = gvs_embed
        i_inline_count = gv_inline_count
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_TASK_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the tasks 
 **i_offset** | /BLCK/OP4_INT | Index of first result to return. [default "0"]
 **i_limit** | /BLCK/OP4_INT | Number of results to return. Maximum is 500. [default "50"]
 **i_sort** | /BLCK/OP4_STRING | Sort query results. Comma separated list of property names, prefixed with &#x27;-&#x27; for descending sort order. Example: &#x27;sort&#x3D;date,-name&#x27;  [optional]
 **i_input_document** | /BLCK/OP4_STRING | A document UUID queried for in all lists of input documents of all tasks. [optional]
 **i_embed** | /BLCK/OP4_STRING | Information about sub-collections and/or sub-ressources to include in the response. - \&quot;permissions\&quot;: include user access rights for each Task - \&quot;metadata\&quot;: include Task metadata. - \&quot;input\&quot;: include input lists (metadata only) - \&quot;output\&quot;: include output lists (metadata only) - \&quot;cstats\&quot;: connector specific job id&#x27;s and states  [optional]
 **i_inline_count** | /BLCK/OP4_BOOL | Return a JSON object containing the number of tasks found, according to the query parameters, instead of an array with tasks.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_TASK_TT (**[array](#markdown-header-model-)**) | OK, collection of tasks or count is returned. Example for count: &#x60;&#x60;&#x60; {   count: 0 } &#x60;&#x60;&#x60; 
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_tasks_post**
Create new task.

Adds a new Task to the collection. Given metadata is assigned, input list must be filled after creation. 


### Example
```abap
*** method TasksApi->services_sid_tasks_post example
*** Create new task.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_TASK
    data gm_body type /BLCK/OP4_TASK.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_TASK
    data gr_http200 type /BLCK/OP4_TASK.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-sid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-tid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-created = 42. " (type /BLCK/OP4_INT)
*   gm_body-started = 42. " (type /BLCK/OP4_INT)
*   gm_body-finished = 42. " (type /BLCK/OP4_INT)
*   gm_body-input_list_length = 42. " (type /BLCK/OP4_INT)
*   gm_body-output_list_length = 42. " (type /BLCK/OP4_INT)
*   gm_body-status = l_status. " (type /BLCK/OP4_STATUS_TYPE)
*   gm_body-links = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-embedded = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_tasks_post via HTTP POST
*** i_body: Task metadata
*** i_sid: ID of the Service managing the current Task
    /blck/op4_cl_TasksApi=>services_sid_tasks_post(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_TASK)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_TASK (**[task](#markdown-header-model-task)**) | Task metadata 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_TASK (**[Task](#markdown-header-model-)**) | OK, task created. Task metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_tasks_tid_delete**
Delete a Task.

Deletes a Task from the collection. This is only possible if the Task is not currently active and if the user has sufficient access rights. 


### Example
```abap
*** method TasksApi->services_sid_tasks_tid_delete example
*** Delete a Task.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_tasks_tid_delete via HTTP DELETE
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the Task to delete.
    /blck/op4_cl_TasksApi=>services_sid_tasks_tid_delete(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the Task to delete. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_tasks_tid_get**
Retrieve metadata of current task.

This route provides access to a Task's root record. The record contains taks metadata (such as parameters controlling it), details are available via sub-ressources and sub-collections. 


### Example
```abap
*** method TasksApi->services_sid_tasks_tid_get example
*** Retrieve metadata of current task.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.

*   for parameter i_force:
*   a simple ABAP primitive of type /BLCK/OP4_BOOL
    data gv_force type /BLCK/OP4_BOOL.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_TASK
    data gr_http200 type /BLCK/OP4_TASK.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.
*   gv_force = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_tasks_tid_get via HTTP GET
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_embed: Embed  sub-ressources  in  the  response. - \"input\": include list of input
*** documents - \"output\": include list of output documents
*** i_force: Force status update from backend system.
    /blck/op4_cl_TasksApi=>services_sid_tasks_tid_get(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_embed = gvs_embed
        i_force = gv_force
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_TASK)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_embed** | /BLCK/OP4_STRING | Embed sub-ressources in the response. - \&quot;input\&quot;: include list of input documents - \&quot;output\&quot;: include list of output documents  [optional]
 **i_force** | /BLCK/OP4_BOOL | Force status update from backend system. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_TASK (**[Task](#markdown-header-model-)**) | OK. Task metadata returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **services_sid_tasks_tid_patch**
Update Task metadata (partial, merge)

Does a partial update to the Task metadata. Given metadata replaces existing one, or is added to the record if not yet present. No metadata is deleted. 


### Example
```abap
*** method TasksApi->services_sid_tasks_tid_patch example
*** Update Task metadata (partial, merge)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_TASK_METADATA
    data gm_body type /BLCK/OP4_TASK_METADATA.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_TASK
    data gr_http200 type /BLCK/OP4_TASK.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_tasks_tid_patch via HTTP PATCH
*** i_body: New metadata for the task
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the Task to update.
    /blck/op4_cl_TasksApi=>services_sid_tasks_tid_patch(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_tid = gvs_tid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_TASK)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_TASK_METADATA (**[task_metadata](#markdown-header-model-task_metadata)**) | New metadata for the task 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the Task to update. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_TASK (**[Task](#markdown-header-model-)**) | OK, task updated and returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **services_sid_tasks_tid_put**
Update task metadata (complete, replace)

A put call to the task root record completely replaces task metadata, but does not affect sub-ressources or sub-collections. 


### Example
```abap
*** method TasksApi->services_sid_tasks_tid_put example
*** Update task metadata (complete, replace)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_TASK_METADATA
    data gm_body type /BLCK/OP4_TASK_METADATA.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_TASK
    data gr_http200 type /BLCK/OP4_TASK.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method services_sid_tasks_tid_put via HTTP PUT
*** i_body: New metadata for the task
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the task to update.
    /blck/op4_cl_TasksApi=>services_sid_tasks_tid_put(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_tid = gvs_tid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_TASK)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_TASK_METADATA (**[task_metadata](#markdown-header-model-task_metadata)**) | New metadata for the task 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the task to update. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_TASK (**[Task](#markdown-header-model-)**) | OK, task updated and returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidtaskstidactionpost**
Trigger an action

Trigger a new action on the current task. Currently supported actions are `start`, `abort`, `pause` and `resume`. 


### Example
```abap
*** method TasksApi->servicessidtaskstidactionpost example
*** Trigger an action

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_ACTION
    data gm_body type /BLCK/OP4_ACTION.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-action = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidactionpost via HTTP POST
*** i_body: The body contains a JSON object with the name of the action. 
*** i_sid: ID of the current service.
*** i_tid: ID of the current task.
    /blck/op4_cl_TasksApi=>servicessidtaskstidactionpost(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_tid = gvs_tid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_ACTION (**[action](#markdown-header-model-action)**) | The body contains a JSON object with the name of the action.  
 **i_sid** | /BLCK/OP4_STRING | ID of the current service. 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidtaskstidinputget**
Retrieve list of task input items

This route provides access to a Task's list of input documents. Input lists of Tasks are structure-wise identical with Lists in general, they differ in that they are Task-internal and hence not available via the /lists route. Input lists can have list-level metadata, and each list item can have metadata as well. A call to this route will provide the list-level metadata and an inventory of the collection. Access input list items via the 'items' sub-collection. Use the 'embed' parameter to include item metadata in the result. 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputget example
*** Retrieve list of task input items

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputget via HTTP GET
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_embed: Use  'embed'  to include sub-collection metadata in the result. - \"items\":
*** Include list-item metadata.
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputget(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_embed** | /BLCK/OP4_STRING | Use &#x27;embed&#x27; to include sub-collection metadata in the result. - \&quot;items\&quot;: Include list-item metadata.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, collection of input list items returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidtaskstidinputiddele**
Delete a task input list item

Deletes an item from a Task's input list. The deleted ID is permanently orphaned, other list items keep their IDs. 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputiddele example
*** Delete a task input list item

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputiddele via HTTP DELETE
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_id: ID of the input list item to delete
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputiddele(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_id = gvs_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_id** | /BLCK/OP4_STRING | ID of the input list item to delete 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidtaskstidinputidget**
Retrieve task item details

FIXME 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputidget example
*** Retrieve task item details

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputidget via HTTP GET
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_id: ID of the input list item
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputidget(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_id = gvs_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_id** | /BLCK/OP4_STRING | ID of the input list item 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, input list item data returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidtaskstidinputidpatc**
Update a task input list item (partial, merge)

Updates task input list item metadata, replacing present entries and adding missing ones. No metadata is deleted by the patch. 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputidpatc example
*** Update a task input list item (partial, merge)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.

*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST_ITEM
    data gm_body type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.
*   gm_body-index = 42. " (type /BLCK/OP4_INT)
*   gm_body-href = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputidpatc via HTTP PATCH
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_id: ID of the task input list item to update
*** i_body: (Partial) metadata of an input list item. 
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputidpatc(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_id = gvs_id
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_id** | /BLCK/OP4_STRING | ID of the task input list item to update 
 **i_body** | /BLCK/OP4_LIST_ITEM (**[list_item](#markdown-header-model-list_item)**) | (Partial) metadata of an input list item.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, task input list item updated. Item data returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidtaskstidinputidput**
Update the current task input list item (complete, replace)

Replaces the task input list item's metadata, including the document reference. 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputidput example
*** Update the current task input list item (complete, replace)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.

*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST_ITEM
    data gm_body type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.
*   gm_body-index = 42. " (type /BLCK/OP4_INT)
*   gm_body-href = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputidput via HTTP PUT
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_id: ID of the input list item
*** i_body: complete item metadata for the task item. 
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputidput(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_id = gvs_id
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_id** | /BLCK/OP4_STRING | ID of the input list item 
 **i_body** | /BLCK/OP4_LIST_ITEM (**[list_item](#markdown-header-model-list_item)**) | complete item metadata for the task item.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, list item updated. Item data returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidtaskstidinputpatch**
Update input list metadata (partial, merge)

Does a partial update to the input list metadata. Given metadata replaces existing one, or is added to the record if not yet present. No metadata is deleted. 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputpatch example
*** Update input list metadata (partial, merge)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST
    data gm_body type /BLCK/OP4_LIST.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-uuid = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-created = 42. " (type /BLCK/OP4_INT)
*   gm_body-last_modified = 42. " (type /BLCK/OP4_INT)
*   gm_body-list_length = 42. " (type /BLCK/OP4_INT)
*   gm_body-links = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-embedded = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputpatch via HTTP PATCH
*** i_body: New metadata for the input list.
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the Task to update.
*** i_embed: Use  'embed'  to  include sub-collection metadata for updating. - \"items\":
*** Include list-item data including indices for reordering.
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputpatch(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_LIST (**[list](#markdown-header-model-list)**) | New metadata for the input list. 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the Task to update. 
 **i_embed** | /BLCK/OP4_STRING | Use &#x27;embed&#x27; to include sub-collection metadata for updating. - \&quot;items\&quot;: Include list-item data including indices for reordering.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, input list updated and returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidtaskstidinputpost**
Append a new item to the input list of the task.

Creates a new entry in the given Task's input list. Given metadata is assigned to the new list item. 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputpost example
*** Append a new item to the input list of the task.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_body:
*   a reference to model type /BLCK/OP4_LIST_ITEM
    data gm_body type /BLCK/OP4_LIST_ITEM.

*   for parameter i_href:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_href type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gm_body-index = 42. " (type /BLCK/OP4_INT)
*   gm_body-href = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_href = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputpost via HTTP POST
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_body: Complete list item metadata for the new task input list item. Use EITHER doc
*** OR item parameter; if both are present, item is used.
*** i_href: URL  of  the  document to add. This is a convenient way of adding a document
*** without constructing a list item first.
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputpost(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_body = gm_body
        i_href = gvs_href
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_body** | /BLCK/OP4_LIST_ITEM (**[list_item](#markdown-header-model-list_item)**) | Complete list item metadata for the new task input list item. Use EITHER doc OR item parameter; if both are present, item is used.  [optional]
 **i_href** | /BLCK/OP4_STRING | URL of the document to add. This is a convenient way of adding a document without constructing a list item first.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, task input list item created, item data returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidtaskstidinputput**
Update input list metadata (complete, replace)

A put call to the input list root record completely replaces the metadata, but does not affect sub-collections. 


### Example
```abap
*** method TasksApi->servicessidtaskstidinputput example
*** Update input list metadata (complete, replace)

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/OP4_TASK_METADATA
    data gm_body type /BLCK/OP4_TASK_METADATA.

*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/OP4_ERROR
    data gr_http409 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/OP4_STRING)
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidinputput via HTTP PUT
*** i_body: New metadata for the task input list
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the task to update.
    /blck/op4_cl_TasksApi=>servicessidtaskstidinputput(
      exporting
        i_body = gm_body
        i_sid = gvs_sid
        i_tid = gvs_tid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/OP4_TASK_METADATA (**[task_metadata](#markdown-header-model-task_metadata)**) | New metadata for the task input list 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the task to update. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, input list updated and returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 409 | **e_409** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, resource could not be updated. See error message for details. 
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **servicessidtaskstidoutputget**
Retrieve list of task output items

This route provides access to a Task's list of output documents. Output lists of Tasks are structure-wise identical with Lists in general, they differ in that they are Task-internal and hence not available via the /lists route. Output lists can have list-level metadata, and each list item can have metadata as well. A call to this route will provide the list-level metadata and an inventory of the collection. Access output list items via the 'items' sub-collection. Use the 'embed' parameter to include item metadata in the result. 


### Example
```abap
*** method TasksApi->servicessidtaskstidoutputget example
*** Retrieve list of task output items

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST
    data gr_http200 type /BLCK/OP4_LIST.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidoutputget via HTTP GET
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_embed: Use  'embed'  to include sub-collection metadata in the result. - \"items\":
*** Include list-item metadata.
    /blck/op4_cl_TasksApi=>servicessidtaskstidoutputget(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_embed = gvs_embed
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_embed** | /BLCK/OP4_STRING | Use &#x27;embed&#x27; to include sub-collection metadata in the result. - \&quot;items\&quot;: Include list-item metadata.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST (**[List](#markdown-header-model-)**) | OK, collection of output list items returned
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **servicessidtaskstidoutputidget**
Retrieve task output list item details

This route provides access to individual task output items. 


### Example
```abap
*** method TasksApi->servicessidtaskstidoutputidget example
*** Retrieve task output list item details

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_sid type /BLCK/OP4_STRING.

*   for parameter i_tid:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_tid type /BLCK/OP4_STRING.

*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_id type /BLCK/OP4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_LIST_ITEM
    data gr_http200 type /BLCK/OP4_LIST_ITEM.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_sid = 'ipsum lorem'.
*   gvs_tid = 'ipsum lorem'.
*   gvs_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method servicessidtaskstidoutputidget via HTTP GET
*** i_sid: ID of the Service managing the current Task
*** i_tid: ID of the current task.
*** i_id: ID of the output list item
    /blck/op4_cl_TasksApi=>servicessidtaskstidoutputidget(
      exporting
        i_sid = gvs_sid
        i_tid = gvs_tid
        i_id = gvs_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_LIST_ITEM)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_sid** | /BLCK/OP4_STRING | ID of the Service managing the current Task 
 **i_tid** | /BLCK/OP4_STRING | ID of the current task. 
 **i_id** | /BLCK/OP4_STRING | ID of the output list item 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_LIST_ITEM (**[ListItem](#markdown-header-model-)**) | OK, output list item data returned.
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **tasks_get**
Retrieve collection of tasks managed by all services.

This route provides access to the root collection of known tasks for all services supporting tasks. Use property names and regular expressions in URL query string to search for tasks. Use the 'embed' parameter to include information about instances and sub-ressources. Use the 'inputDocument' parameter to search for a task containing a special document and use 'inlineCount' to get the number of found tasks. 


### Example
```abap
*** method TasksApi->tasks_get example
*** Retrieve collection of tasks managed by all services.

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net:3008/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/op4_int,
    gvs_msg  type /blck/op4_string.
    
*** create variables for input and output as needed
*   for parameter i_input_document:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_input_document type /BLCK/OP4_STRING.

*   for parameter i_embed:
*   a simple ABAP primitive of type /BLCK/OP4_STRING
    data gvs_embed type /BLCK/OP4_STRING.

*   for parameter i_inline_count:
*   a simple ABAP primitive of type /BLCK/OP4_BOOL
    data gv_inline_count type /BLCK/OP4_BOOL.
*   when the the result of the call is HTTP200 we expect type /BLCK/OP4_TASK_TT
    data gr_http200 type /BLCK/OP4_TASK_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/OP4_ERROR
    data gr_http401 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/OP4_ERROR
    data gr_http403 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/OP4_ERROR
    data gr_http404 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/OP4_ERROR
    data gr_http500 type /BLCK/OP4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/OP4_ERROR
    data gr_http0 type /BLCK/OP4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_input_document = 'ipsum lorem'.
*   gvs_embed = 'ipsum lorem'.
*   gv_inline_count = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/op4_cl_TasksApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method tasks_get via HTTP GET
*** i_input_document: A document UUID queried for in all lists of input documents of all tasks.
*** i_embed: Information  about  sub-collections  and/or sub-ressources to include in the
*** response.  -  \"permissions\":  include  user  access rights for each Task -
*** \"metadata\":  include  Task  metadata.  -  \"input\":  include  input lists
*** (metadata  only)  -  \"output\":  include  output  lists  (metadata  only) -
*** \"cstats\": connector specific job id's and states
*** i_inline_count: Return  a JSON object containing the number of tasks found, according to the
*** query parameters, instead of an array with tasks.
    /blck/op4_cl_TasksApi=>tasks_get(
      exporting
        i_input_document = gvs_input_document
        i_embed = gvs_embed
        i_inline_count = gv_inline_count
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/OP4_TASK_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/OP4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/OP4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/OP4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/OP4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/OP4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_input_document** | /BLCK/OP4_STRING | A document UUID queried for in all lists of input documents of all tasks. [optional]
 **i_embed** | /BLCK/OP4_STRING | Information about sub-collections and/or sub-ressources to include in the response. - \&quot;permissions\&quot;: include user access rights for each Task - \&quot;metadata\&quot;: include Task metadata. - \&quot;input\&quot;: include input lists (metadata only) - \&quot;output\&quot;: include output lists (metadata only) - \&quot;cstats\&quot;: connector specific job id&#x27;s and states  [optional]
 **i_inline_count** | /BLCK/OP4_BOOL | Return a JSON object containing the number of tasks found, according to the query parameters, instead of an array with tasks.  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/OP4_TASK_TT (**[array](#markdown-header-model-)**) | OK, collection of tasks or count is returned. Example for count: &#x60;&#x60;&#x60; {   count: 0 } &#x60;&#x60;&#x60; 
 401 | **e_401** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks rights to access the data. 
 404 | **e_404** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/OP4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-action"></a> 

# Model: action



### Example
```abap
*** model action example
*** A  JSON  object  containing  the  name  of  the  command to execute and it&#x27;s
*** paramters.

* create our variables..
    data gcl_action type ref to /blck/mdl_cl_action.
    
* instantiate model and call the setters to set values..
    gcl_action = /blck/mdl_cl_action=>create( ).
    gcl_action->set_action( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_action(
    	exporting
    		i_action = gcl_action ).
    		
    clear gcl_action.
    
* fetch new instance from example API method
    gcl_action = gcl_exampleapi->get_action(
    	exporting
    		i_id = 1 ).
    		
    l_action = gcl_action->get_action( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**action** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-baserepoentry"></a> 

# Model: baserepoentry



### Example
```abap
*** model baserepoentry example
*** A  RepoEntry  contains  user  defined  metadata with any number of arbitrary
*** properties and two mandatory properties &#x27;name&#x27; and &#x27;type&#x27;.

* create our variables..
    data gcl_baserepoentry type ref to /blck/mdl_cl_baserepoentry.
    
* instantiate model and call the setters to set values..
    gcl_baserepoentry = /blck/mdl_cl_baserepoentry=>create( ).
    gcl_baserepoentry->set_name( 'ipsum lorem' ). " (type string)
    gcl_baserepoentry->set_type( 'ipsum lorem' ). " (type string)
    gcl_baserepoentry->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_baserepoentry(
    	exporting
    		i_baserepoentry = gcl_baserepoentry ).
    		
    clear gcl_baserepoentry.
    
* fetch new instance from example API method
    gcl_baserepoentry = gcl_exampleapi->get_baserepoentry(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_baserepoentry->get_name( ). " (type string)
    l_type = gcl_baserepoentry->get_type( ). " (type string)
    l_metadata = gcl_baserepoentry->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string | (File) name of the Entry | [optional] [default to null]
**type** | string | Type of RepoEntry. | [optional] [default to null]
**metadata** | string | Metadata assigned to the entry | [optional] [default to null]

* * *
<a name="markdown-header-model-cid"></a> 

# Model: cid



### Example
```abap
*** model cid example
*** An arbitrary id representing a job in the backend system.

* create our variables..
    data gcl_cid type ref to /blck/mdl_cl_cid.
    
* instantiate model and call the setters to set values..
    gcl_cid = /blck/mdl_cl_cid=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_cid(
    	exporting
    		i_cid = gcl_cid ).
    		
    clear gcl_cid.
    
* fetch new instance from example API method
    gcl_cid = gcl_exampleapi->get_cid(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-model-cid_command"></a> 

# Model: cid_command



### Example
```abap
*** model cid_command example
*** A task action and it&#x27;s parameters

* create our variables..
    data gcl_cid_command type ref to /blck/mdl_cl_cid_command.
    
* instantiate model and call the setters to set values..
    gcl_cid_command = /blck/mdl_cl_cid_command=>create( ).
    gcl_cid_command->set_action( l_action ). " (type /BLCK/OP4_action)
    gcl_cid_command->set_data( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_cid_command(
    	exporting
    		i_cid_command = gcl_cid_command ).
    		
    clear gcl_cid_command.
    
* fetch new instance from example API method
    gcl_cid_command = gcl_exampleapi->get_cid_command(
    	exporting
    		i_id = 1 ).
    		
    l_action = gcl_cid_command->get_action( ). " (type /BLCK/OP4_action)
    l_data = gcl_cid_command->get_data( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**action** | /BLCK/OP4_action (**[action](#markdown-header-model-action)**) |  | [optional] [default to null]
**data** | string | Data depending on the action. - start: &#x60;data&#x60; contains complete task data in operator-server internal structure - abort: &#x60;data&#x60; contains tid and cids part of task data to abort - pause: &#x60;data&#x60; contains tid and cids part of task data to pause - resume: &#x60;data&#x60; contains tid and cids part of task data to resume  | [optional] [default to null]

* * *
<a name="markdown-header-model-list_item"></a> 

# Model: list_item



### Example
```abap
*** model list_item example

* create our variables..
    data gcl_list_item type ref to /blck/mdl_cl_list_item.
    
* instantiate model and call the setters to set values..
    gcl_list_item = /blck/mdl_cl_list_item=>create( ).
    gcl_list_item->set_index( 42 ). " (type i)
    gcl_list_item->set_href( 'ipsum lorem' ). " (type string)
    gcl_list_item->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_list_item(
    	exporting
    		i_list_item = gcl_list_item ).
    		
    clear gcl_list_item.
    
* fetch new instance from example API method
    gcl_list_item = gcl_exampleapi->get_list_item(
    	exporting
    		i_id = 1 ).
    		
    l_index = gcl_list_item->get_index( ). " (type i)
    l_href = gcl_list_item->get_href( ). " (type string)
    l_metadata = gcl_list_item->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**index** | i | This is the index of an item in a List. The index is maintained by the SEAL Operator backend. Setting the index to a value beyond the end of the list will move the item to the end of the list. Setting the index to 0 will move th item to the top of the list. Setting the index to a value in use by another item will replace this item, moving it (and all with higher indices) one space down in the list, by increasing their index values.  | [optional] [default to null]
**href** | string | URL location of linked ressource | [optional] [default to null]
**metadata** | string | Additional data to be stored with the link | [optional] [default to null]

* * *
<a name="markdown-header-enum-status_type"></a> 

# Enum: status_type



### Example
```abap
*** model status_type example
*** Definition of allowed status names

* create our variables..
    data gcl_status_type type ref to /blck/mdl_cl_status_type.
    
* instantiate model relevant to the enum value we want
    gcl_status_type = /blck/mdl_cl_status_type=>enum_open( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_status_type_state(
    	exporting
    		i_status_type = gcl_status_type ).
    		
    clear gcl_status_type.
    
* fetch result from example API method
    gcl_status_type = gcl_exampleapi->get_status_type_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_status_type->is_open( ) eq 'X'.
*   do something specific to open case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_status_type->get_value( ).
    when /blck/mdl_cl_status_type=>mce_open.
*     do something specific to open case..
    when /blck/mdl_cl_status_type=>mce_processing.
*     do something specific to processing case..
    when /blck/mdl_cl_status_type=>mce_completed.
*     do something specific to completed case..
    when /blck/mdl_cl_status_type=>mce_paused.
*     do something specific to paused case..
    when /blck/mdl_cl_status_type=>mce_aborted.
*     do something specific to aborted case..
    when /blck/mdl_cl_status_type=>mce_failed.
*     do something specific to failed case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**open** | open | /blck/mdl_cl_status_type=>enum_open( ).
**processing** | processing | /blck/mdl_cl_status_type=>enum_processing( ).
**completed** | completed | /blck/mdl_cl_status_type=>enum_completed( ).
**paused** | paused | /blck/mdl_cl_status_type=>enum_paused( ).
**aborted** | aborted | /blck/mdl_cl_status_type=>enum_aborted( ).
**failed** | failed | /blck/mdl_cl_status_type=>enum_failed( ).

* * *
<a name="markdown-header-model-cid_status"></a> 

# Model: cid_status



### Example
```abap
*** model cid_status example
*** The status of a cid job

* create our variables..
    data gcl_cid_status type ref to /blck/mdl_cl_cid_status.
    
* instantiate model and call the setters to set values..
    gcl_cid_status = /blck/mdl_cl_cid_status=>create( ).
    gcl_cid_status->set_tid( 'ipsum lorem' ). " (type string)
    gcl_cid_status->set_status( l_status ). " (type /BLCK/OP4_status_type)
    gcl_cid_status->set_started( 42 ). " (type i)
    gcl_cid_status->set_finished( 42 ). " (type i)
    gcl_cid_status->set_cids( l_cids ). " (type /BLCK/OP4_cid_tt)
    gcl_cid_status->set_cstats( l_cstats ). " (type /blck/api_string_tt)
    gcl_cid_status->set_list_items( l_list_items ). " (type /BLCK/OP4_list_item_tt)
    
* pass to example API method
    gcl_exampleapi->update_cid_status(
    	exporting
    		i_cid_status = gcl_cid_status ).
    		
    clear gcl_cid_status.
    
* fetch new instance from example API method
    gcl_cid_status = gcl_exampleapi->get_cid_status(
    	exporting
    		i_id = 1 ).
    		
    l_tid = gcl_cid_status->get_tid( ). " (type string)
    l_status = gcl_cid_status->get_status( ). " (type /BLCK/OP4_status_type)
    l_started = gcl_cid_status->get_started( ). " (type i)
    l_finished = gcl_cid_status->get_finished( ). " (type i)
    l_cids = gcl_cid_status->get_cids( ). " (type /BLCK/OP4_cid_tt)
    l_cstats = gcl_cid_status->get_cstats( ). " (type /blck/api_string_tt)
    l_list_items = gcl_cid_status->get_list_items( ). " (type /BLCK/OP4_list_item_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**tid** | string |  | [optional] [default to null]
**status** | /BLCK/OP4_status_type (**[status_type](#markdown-header-enum-status_type)**) |  | [optional] [default to null]
**started** | i | Timestamp when the cid job started | [optional] [default to null]
**finished** | i | Timestamp when the cid job finished | [optional] [default to null]
**cids** | /BLCK/OP4_cid_tt (**[array of cid](#markdown-header-model-cid)**) | list of cid&#x27;s | [optional] [default to null]
**cstats** | /blck/api_string_tt | list with status for each cid | [optional] [default to null]
**list_items** | /BLCK/OP4_list_item_tt (**[array of list_item](#markdown-header-model-list_item)**) | Output documents list | [optional] [default to null]

* * *
<a name="markdown-header-model-cid_taskdata"></a> 

# Model: cid_taskdata



### Example
```abap
*** model cid_taskdata example
*** Object containing a list of cid&#x27;s 

* create our variables..
    data gcl_cid_taskdata type ref to /blck/mdl_cl_cid_taskdata.
    
* instantiate model and call the setters to set values..
    gcl_cid_taskdata = /blck/mdl_cl_cid_taskdata=>create( ).
    gcl_cid_taskdata->set_tid( 'ipsum lorem' ). " (type string)
    gcl_cid_taskdata->set_cids( l_cids ). " (type /BLCK/OP4_cid_tt)
    
* pass to example API method
    gcl_exampleapi->update_cid_taskdata(
    	exporting
    		i_cid_taskdata = gcl_cid_taskdata ).
    		
    clear gcl_cid_taskdata.
    
* fetch new instance from example API method
    gcl_cid_taskdata = gcl_exampleapi->get_cid_taskdata(
    	exporting
    		i_id = 1 ).
    		
    l_tid = gcl_cid_taskdata->get_tid( ). " (type string)
    l_cids = gcl_cid_taskdata->get_cids( ). " (type /BLCK/OP4_cid_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**tid** | string | Task id | [optional] [default to null]
**cids** | /BLCK/OP4_cid_tt (**[array of cid](#markdown-header-model-cid)**) | list of cid&#x27;s | [optional] [default to null]

* * *
<a name="markdown-header-model-command"></a> 

# Model: command



### Example
```abap
*** model command example
*** A  JSON  object  containing  the  name  of  the  command to execute and it&#x27;s
*** paramters.

* create our variables..
    data gcl_command type ref to /blck/mdl_cl_command.
    
* instantiate model and call the setters to set values..
    gcl_command = /blck/mdl_cl_command=>create( ).
    gcl_command->set_action( 'ipsum lorem' ). " (type string)
    gcl_command->set_parameter( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_command(
    	exporting
    		i_command = gcl_command ).
    		
    clear gcl_command.
    
* fetch new instance from example API method
    gcl_command = gcl_exampleapi->get_command(
    	exporting
    		i_id = 1 ).
    		
    l_action = gcl_command->get_action( ). " (type string)
    l_parameter = gcl_command->get_parameter( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**action** | string |  | [optional] [default to null]
**parameter** | string | Command specific parameter, e.g. href&#x27;s of documents  | [optional] [default to null]

* * *
<a name="markdown-header-model-command_status"></a> 

# Model: command_status



### Example
```abap
*** model command_status example
*** A JSON object containing a command and it&#x27;s current status

* create our variables..
    data gcl_command_status type ref to /blck/mdl_cl_command_status.
    
* instantiate model and call the setters to set values..
    gcl_command_status = /blck/mdl_cl_command_status=>create( ).
    gcl_command_status->set_cid( 'ipsum lorem' ). " (type string)
    gcl_command_status->set_status( l_status ). " (type /BLCK/OP4_status_type)
    gcl_command_status->set_command( l_command ). " (type /BLCK/OP4_command)
    
* pass to example API method
    gcl_exampleapi->update_command_status(
    	exporting
    		i_command_status = gcl_command_status ).
    		
    clear gcl_command_status.
    
* fetch new instance from example API method
    gcl_command_status = gcl_exampleapi->get_command_status(
    	exporting
    		i_id = 1 ).
    		
    l_cid = gcl_command_status->get_cid( ). " (type string)
    l_status = gcl_command_status->get_status( ). " (type /BLCK/OP4_status_type)
    l_command = gcl_command_status->get_command( ). " (type /BLCK/OP4_command)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**cid** | string |  | [optional] [default to null]
**status** | /BLCK/OP4_status_type (**[status_type](#markdown-header-enum-status_type)**) |  | [optional] [default to null]
**command** | /BLCK/OP4_command (**[command](#markdown-header-model-command)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-config_item"></a> 

# Model: config_item



### Example
```abap
*** model config_item example
*** A JSON object containing key-value pairs representing the configuration. 

* create our variables..
    data gcl_config_item type ref to /blck/mdl_cl_config_item.
    
* instantiate model and call the setters to set values..
    gcl_config_item = /blck/mdl_cl_config_item=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_config_item(
    	exporting
    		i_config_item = gcl_config_item ).
    		
    clear gcl_config_item.
    
* fetch new instance from example API method
    gcl_config_item = gcl_exampleapi->get_config_item(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-model-error"></a> 

# Model: error



### Example
```abap
*** model error example

* create our variables..
    data gcl_error type ref to /blck/mdl_cl_error.
    
* instantiate model and call the setters to set values..
    gcl_error = /blck/mdl_cl_error=>create( ).
    gcl_error->set_code( 42 ). " (type i)
    gcl_error->set_message( 'ipsum lorem' ). " (type string)
    gcl_error->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_error(
    	exporting
    		i_error = gcl_error ).
    		
    clear gcl_error.
    
* fetch new instance from example API method
    gcl_error = gcl_exampleapi->get_error(
    	exporting
    		i_id = 1 ).
    		
    l_code = gcl_error->get_code( ). " (type i)
    l_message = gcl_error->get_message( ). " (type string)
    l_metadata = gcl_error->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | i |  | [optional] [default to null]
**message** | string |  | [optional] [default to null]
**metadata** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-functions"></a> 

# Model: functions



### Example
```abap
*** model functions example
*** Contains  for  each  available  function  one  object  with  an  href to the
*** function. Key of each object is the function name.

* create our variables..
    data gcl_functions type ref to /blck/mdl_cl_functions.
    
* instantiate model and call the setters to set values..
    gcl_functions = /blck/mdl_cl_functions=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_functions(
    	exporting
    		i_functions = gcl_functions ).
    		
    clear gcl_functions.
    
* fetch new instance from example API method
    gcl_functions = gcl_exampleapi->get_functions(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-model-list"></a> 

# Model: list



### Example
```abap
*** model list example
*** A  List  is  an  ordered  sequence of documents as list items. Each List can
*** contain  arbitrary  metadata.  List  items  may also have metadata assigned,
*** which  does not replace but complement document metadata. A document may not
*** be  unique within a List, i.e. a List can contain several items all pointing
*** to the same document (but most likely with different item metadata).

* create our variables..
    data gcl_list type ref to /blck/mdl_cl_list.
    
* instantiate model and call the setters to set values..
    gcl_list = /blck/mdl_cl_list=>create( ).
    gcl_list->set_uuid( 'ipsum lorem' ). " (type string)
    gcl_list->set_name( 'ipsum lorem' ). " (type string)
    gcl_list->set_created( 42 ). " (type i)
    gcl_list->set_last_modified( 42 ). " (type i)
    gcl_list->set_list_length( 42 ). " (type i)
    gcl_list->set_links( 'ipsum lorem' ). " (type string)
    gcl_list->set_embedded( 'ipsum lorem' ). " (type string)
    gcl_list->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_list(
    	exporting
    		i_list = gcl_list ).
    		
    clear gcl_list.
    
* fetch new instance from example API method
    gcl_list = gcl_exampleapi->get_list(
    	exporting
    		i_id = 1 ).
    		
    l_uuid = gcl_list->get_uuid( ). " (type string)
    l_name = gcl_list->get_name( ). " (type string)
    l_created = gcl_list->get_created( ). " (type i)
    l_last_modified = gcl_list->get_last_modified( ). " (type i)
    l_list_length = gcl_list->get_list_length( ). " (type i)
    l_links = gcl_list->get_links( ). " (type string)
    l_embedded = gcl_list->get_embedded( ). " (type string)
    l_metadata = gcl_list->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**uuid** | string | Unique identifier of the list, generated by SEAL Operator. | [optional] [default to null]
**name** | string | User defined name for the list. Doesn&#x27;t have to be unique. | [optional] [default to null]
**created** | i | Timestamp of list creation | [optional] [default to null]
**last_modified** | i | Timestamp of list creation | [optional] [default to null]
**list_length** | i | Number of items in list | [optional] [default to null]
**links** | string | If requested by MIME type, the links section contains hrefs to - \&quot;self\&quot;: the List itself  | [optional] [default to null]
**embedded** | string | Embedded sub-ressources or sub-collections, as requested throught the \&quot;embed\&quot; query parameter  | [optional] [default to null]
**metadata** | string | List metadata. Note that these do not contain item metadata. | [optional] [default to null]

* * *
<a name="markdown-header-model-message"></a> 

# Model: message



### Example
```abap
*** model message example
*** A JSON object containing a message 

* create our variables..
    data gcl_message type ref to /blck/mdl_cl_message.
    
* instantiate model and call the setters to set values..
    gcl_message = /blck/mdl_cl_message=>create( ).
    gcl_message->set_uuid( 'ipsum lorem' ). " (type string)
    gcl_message->set_type( 'ipsum lorem' ). " (type string)
    gcl_message->set_text( 'ipsum lorem' ). " (type string)
    gcl_message->set_date( 42 ). " (type i)
    gcl_message->set_source( 'ipsum lorem' ). " (type string)
    gcl_message->set_read( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_message(
    	exporting
    		i_message = gcl_message ).
    		
    clear gcl_message.
    
* fetch new instance from example API method
    gcl_message = gcl_exampleapi->get_message(
    	exporting
    		i_id = 1 ).
    		
    l_uuid = gcl_message->get_uuid( ). " (type string)
    l_type = gcl_message->get_type( ). " (type string)
    l_text = gcl_message->get_text( ). " (type string)
    l_date = gcl_message->get_date( ). " (type i)
    l_source = gcl_message->get_source( ). " (type string)
    l_read = gcl_message->get_read( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**uuid** | string | A server side defined uuid for each new entry | [optional] [default to null]
**type** | string | The message type | [optional] [default to null]
**text** | string | The message text | [optional] [default to null]
**date** | i | The creation time of the message as timestamp | [optional] [default to null]
**source** | string | Name of the panel which created the message | [optional] [default to null]
**read** | flag | Flag if the message has already been read by user | [optional] [default to null]

* * *
<a name="markdown-header-model-panel_item"></a> 

# Model: panel_item



### Example
```abap
*** model panel_item example
*** A JSON object containing name and id of a PanelListItem

* create our variables..
    data gcl_panel_item type ref to /blck/mdl_cl_panel_item.
    
* instantiate model and call the setters to set values..
    gcl_panel_item = /blck/mdl_cl_panel_item=>create( ).
    gcl_panel_item->set_pid( 'ipsum lorem' ). " (type string)
    gcl_panel_item->set_name( 'ipsum lorem' ). " (type string)
    gcl_panel_item->set_type( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_panel_item(
    	exporting
    		i_panel_item = gcl_panel_item ).
    		
    clear gcl_panel_item.
    
* fetch new instance from example API method
    gcl_panel_item = gcl_exampleapi->get_panel_item(
    	exporting
    		i_id = 1 ).
    		
    l_pid = gcl_panel_item->get_pid( ). " (type string)
    l_name = gcl_panel_item->get_name( ). " (type string)
    l_type = gcl_panel_item->get_type( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**pid** | string | unique id of the PanelListItem | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**type** | string | the panel type the configuration is for, e.g. scratch, p4,... | [optional] [default to null]

* * *
<a name="markdown-header-model-repo_entry"></a> 

# Model: repo_entry



### Example
```abap
*** model repo_entry example
*** A  RepoEntry  represents a record within the Repository part of a Service. A
*** RepoEntry  may  be  either  a  document or a collection. All RepoEntries may
*** contain  metadata  and user permission records. collections may also contain
*** children, while documents may have binary content.

* create our variables..
    data gcl_repo_entry type ref to /blck/mdl_cl_repo_entry.
    
* instantiate model and call the setters to set values..
    gcl_repo_entry = /blck/mdl_cl_repo_entry=>create( ).
    gcl_repo_entry->set_id( 'ipsum lorem' ). " (type string)
    gcl_repo_entry->set_uuid( 'ipsum lorem' ). " (type string)
    gcl_repo_entry->set_name( 'ipsum lorem' ). " (type string)
    gcl_repo_entry->set_type( 'ipsum lorem' ). " (type string)
    gcl_repo_entry->set_links( 'ipsum lorem' ). " (type string)
    gcl_repo_entry->set_embedded( 'ipsum lorem' ). " (type string)
    gcl_repo_entry->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_repo_entry(
    	exporting
    		i_repo_entry = gcl_repo_entry ).
    		
    clear gcl_repo_entry.
    
* fetch new instance from example API method
    gcl_repo_entry = gcl_exampleapi->get_repo_entry(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_repo_entry->get_id( ). " (type string)
    l_uuid = gcl_repo_entry->get_uuid( ). " (type string)
    l_name = gcl_repo_entry->get_name( ). " (type string)
    l_type = gcl_repo_entry->get_type( ). " (type string)
    l_links = gcl_repo_entry->get_links( ). " (type string)
    l_embedded = gcl_repo_entry->get_embedded( ). " (type string)
    l_metadata = gcl_repo_entry->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | string | Local ID of the document within the repository. | [optional] [default to null]
**uuid** | string | Global ID of the document, created by SEAL Operator | [optional] [default to null]
**name** | string | (File) name of the Entry | [optional] [default to null]
**type** | string | Type of RepoEntry. | [optional] [default to null]
**links** | string | If requested by MIME type, the links section contains hrefs to - \&quot;self\&quot;: the document itself - \&quot;parent\&quot;: the collection containing the document - \&quot;permissions\&quot;: an object describing user permissions on the document  | [optional] [default to null]
**embedded** | string | Embedded sub-ressources as requested through the \&quot;embed\&quot; query parameter, e.g. \&quot;permissions\&quot;, \&quot;icon\&quot;, \&quot;thumb\&quot;.  | [optional] [default to null]
**metadata** | string | Metadata assigned to the entry | [optional] [default to null]

* * *
<a name="markdown-header-model-service"></a> 

# Model: service



### Example
```abap
*** model service example
*** A  Service  represents  a  target  system  connected  to  the  SEAL Operator
*** framework.  It  may  be  able  to  process  tasks  and/or  provide access to
*** documents, under its /tasks and /repo routes.

* create our variables..
    data gcl_service type ref to /blck/mdl_cl_service.
    
* instantiate model and call the setters to set values..
    gcl_service = /blck/mdl_cl_service=>create( ).
    gcl_service->set_id( 'ipsum lorem' ). " (type string)
    gcl_service->set_name( 'ipsum lorem' ). " (type string)
    gcl_service->set_metadata( 'ipsum lorem' ). " (type string)
    gcl_service->set_links( 'ipsum lorem' ). " (type string)
    gcl_service->set_embedded( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_service(
    	exporting
    		i_service = gcl_service ).
    		
    clear gcl_service.
    
* fetch new instance from example API method
    gcl_service = gcl_exampleapi->get_service(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_service->get_id( ). " (type string)
    l_name = gcl_service->get_name( ). " (type string)
    l_metadata = gcl_service->get_metadata( ). " (type string)
    l_links = gcl_service->get_links( ). " (type string)
    l_embedded = gcl_service->get_embedded( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | string | Identifier of the Service within the SEAL Operator | [optional] [default to null]
**name** | string | Label describing the Service | [optional] [default to null]
**metadata** | string | Metadata of the Service | [optional] [default to null]
**links** | string | If requested by MIME type, the links section contains hrefs to - \&quot;self\&quot;: The Service itself - \&quot;permissions\&quot;: User permissions on the Service  | [optional] [default to null]
**embedded** | string | Sub-collections and/or sub-ressources requested through the embed query parameter.  | [optional] [default to null]

* * *
<a name="markdown-header-model-session_info"></a> 

# Model: session_info



### Example
```abap
*** model session_info example
*** Informations about users sessions

* create our variables..
    data gcl_session_info type ref to /blck/mdl_cl_session_info.
    
* instantiate model and call the setters to set values..
    gcl_session_info = /blck/mdl_cl_session_info=>create( ).
    gcl_session_info->set_false( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_session_info(
    	exporting
    		i_session_info = gcl_session_info ).
    		
    clear gcl_session_info.
    
* fetch new instance from example API method
    gcl_session_info = gcl_exampleapi->get_session_info(
    	exporting
    		i_id = 1 ).
    		
    l_false = gcl_session_info->get_false( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**false** | i | number of currently open sessions of this user | [optional] [default to null]

* * *
<a name="markdown-header-model-task"></a> 

# Model: task



### Example
```abap
*** model task example

* create our variables..
    data gcl_task type ref to /blck/mdl_cl_task.
    
* instantiate model and call the setters to set values..
    gcl_task = /blck/mdl_cl_task=>create( ).
    gcl_task->set_name( 'ipsum lorem' ). " (type string)
    gcl_task->set_sid( 'ipsum lorem' ). " (type string)
    gcl_task->set_tid( 'ipsum lorem' ). " (type string)
    gcl_task->set_metadata( 'ipsum lorem' ). " (type string)
    gcl_task->set_created( 42 ). " (type i)
    gcl_task->set_started( 42 ). " (type i)
    gcl_task->set_finished( 42 ). " (type i)
    gcl_task->set_input_list_length( 42 ). " (type i)
    gcl_task->set_output_list_length( 42 ). " (type i)
    gcl_task->set_status( l_status ). " (type /BLCK/OP4_status_type)
    gcl_task->set_links( 'ipsum lorem' ). " (type string)
    gcl_task->set_embedded( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_task(
    	exporting
    		i_task = gcl_task ).
    		
    clear gcl_task.
    
* fetch new instance from example API method
    gcl_task = gcl_exampleapi->get_task(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_task->get_name( ). " (type string)
    l_sid = gcl_task->get_sid( ). " (type string)
    l_tid = gcl_task->get_tid( ). " (type string)
    l_metadata = gcl_task->get_metadata( ). " (type string)
    l_created = gcl_task->get_created( ). " (type i)
    l_started = gcl_task->get_started( ). " (type i)
    l_finished = gcl_task->get_finished( ). " (type i)
    l_input_list_length = gcl_task->get_input_list_length( ). " (type i)
    l_output_list_length = gcl_task->get_output_list_length( ). " (type i)
    l_status = gcl_task->get_status( ). " (type /BLCK/OP4_status_type)
    l_links = gcl_task->get_links( ). " (type string)
    l_embedded = gcl_task->get_embedded( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string |  | [optional] [default to null]
**sid** | string |  | [optional] [default to null]
**tid** | string |  | [optional] [default to null]
**metadata** | string | Task metadata. Note that these do not contain item metadata. | [optional] [default to null]
**created** | i | Timestamp of task creation | [optional] [default to null]
**started** | i | Timestamp of task started | [optional] [default to null]
**finished** | i | Timestamp of task finished | [optional] [default to null]
**input_list_length** | i | Number of items in input list | [optional] [default to null]
**output_list_length** | i | Number of items in output list | [optional] [default to null]
**status** | /BLCK/OP4_status_type (**[status_type](#markdown-header-enum-status_type)**) |  | [optional] [default to null]
**links** | string | If requested, the links section contains hrefs to - \&quot;self\&quot;: the Task itself - \&quot;input\&quot;: input documents - \&quot;output\&quot;: output documents  | [optional] [default to null]
**embedded** | string | Embedded sub-ressources or sub-collections, as requested throught the \&quot;embed\&quot; query parameter  | [optional] [default to null]

* * *
<a name="markdown-header-model-task_metadata"></a> 

# Model: task_metadata



### Example
```abap
*** model task_metadata example
*** A  task  metadata  object  contains user defined metadata with any number of
*** arbitrary properties and the optional property &#x27;name&#x27;.

* create our variables..
    data gcl_task_metadata type ref to /blck/mdl_cl_task_metadata.
    
* instantiate model and call the setters to set values..
    gcl_task_metadata = /blck/mdl_cl_task_metadata=>create( ).
    gcl_task_metadata->set_name( 'ipsum lorem' ). " (type string)
    gcl_task_metadata->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_task_metadata(
    	exporting
    		i_task_metadata = gcl_task_metadata ).
    		
    clear gcl_task_metadata.
    
* fetch new instance from example API method
    gcl_task_metadata = gcl_exampleapi->get_task_metadata(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_task_metadata->get_name( ). " (type string)
    l_metadata = gcl_task_metadata->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string | Name of the Task | [optional] [default to null]
**metadata** | string | Metadata assigned to the task | [optional] [default to null]

