# API: DocumentsApi
## &nbsp; &nbsp; [Operation: get_doc_attr](#markdown-header-op-DocumentsApi-get_doc_attr)
## &nbsp; &nbsp; [Operation: get_doc_data](#markdown-header-op-DocumentsApi-get_doc_data)
## &nbsp; &nbsp; [Operation: get_docs](#markdown-header-op-DocumentsApi-get_docs)
## &nbsp; &nbsp; [Operation: set_doc_attr](#markdown-header-op-DocumentsApi-set_doc_attr)
# API: SearchApi
## &nbsp; &nbsp; [Operation: full_query](#markdown-header-op-SearchApi-full_query)
## &nbsp; &nbsp; [Operation: query](#markdown-header-op-SearchApi-query)
# Models and Enumerations
## &nbsp; &nbsp; [Model: Cells](#markdown-header-model-cells) (type `/blck/sp_cells`)
## &nbsp; &nbsp; [Model: DocAttrValue](#markdown-header-model-doc_attr_value) (type `/blck/sp_doc_attr_value`)
## &nbsp; &nbsp; [Model: Document](#markdown-header-model-document) (type `/blck/sp_document`)
## &nbsp; &nbsp; [Model: DocList](#markdown-header-model-doc_list) (type `/blck/sp_doc_list`)
## &nbsp; &nbsp; [Model: Properties](#markdown-header-model-properties) (type `/blck/sp_properties`)
## &nbsp; &nbsp; [Model: Rows](#markdown-header-model-rows) (type `/blck/sp_rows`)
## &nbsp; &nbsp; [Model: Table](#markdown-header-model-table) (type `/blck/sp_table`)
## &nbsp; &nbsp; [Model: RelevantResults](#markdown-header-model-relevantresult) (type `/blck/sp_relevantresult`)
## &nbsp; &nbsp; [Model: PrimaryQueryResult](#markdown-header-model-primaryqueryre) (type `/blck/sp_primaryqueryre`)
## &nbsp; &nbsp; [Model: Query](#markdown-header-model-query) (type `/blck/sp_query`)
## &nbsp; &nbsp; [Model: StringResultArray](#markdown-header-model-stringresultar) (type `/blck/sp_stringresultar`)
## &nbsp; &nbsp; [Model: QueryReqParams](#markdown-header-model-queryreqparams) (type `/blck/sp_queryreqparams`)
## &nbsp; &nbsp; [Model: QueryReq](#markdown-header-model-query_req) (type `/blck/sp_query_req`)

# API: DocumentsApi

All URIs are relative to *https://<site-collection>.sharepoint.com/sites/<site>*

<a name="markdown-header-op-DocumentsApi-get_doc_attr"></a>

## operation: **get_doc_attr**
Get attribute of document


### Example
```abap
*** method DocumentsApi->get_doc_attr example
*** Get attribute of document

  constants:
    gcc_basepath type string value 'https://<site-collection>.sharepoint.com/sites/<site>'.
    
  data:  
    gvi_code type /blck/sp_int,
    gvs_msg  type /blck/sp_string.
    
*** create variables for input and output as needed
*   for parameter i_title:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_title type /BLCK/SP_STRING.
*   for parameter i_doc_id:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_doc_id type /BLCK/SP_INT.
*   for parameter i_attr:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_attr type /BLCK/SP_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_accept type /BLCK/SP_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SP_DOC_ATTR_VALUE
    data gr_http200 type /BLCK/SP_DOC_ATTR_VALUE.
        
*** set data according to requirements of the API call
*   gvs_title = 'ipsum lorem'.
*   gvi_doc_id = 42.
*   gvs_attr = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.

*** pass auth credentials to the API as needed
    /blck/sp_cl_api=>set_credentials(
      exporting
        i_basic_auth_un = 'john'
        i_basic_auth_pw = 'pw' ).
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method get_doc_attr via HTTP GET
*** i_title: Title of the document container
*** i_doc_id: Id of document
*** i_attr: Name of attribute to change
*** i_accept: an Accept header
    /blck/sp_cl_DocumentsApi=>get_doc_attr(
      exporting
        i_title = gvs_title
        i_doc_id = gvi_doc_id
        i_attr = gvs_attr
        i_accept = gvs_accept
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_DOC_ATTR_VALUE)
      when 405.
*       handle code 405, e_message => gvs_msg
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_title** | `/BLCK/SP_STRING` | Title of the document container 
 **i_doc_id** | `/BLCK/SP_INT` | Id of document 
 **i_attr** | `/BLCK/SP_STRING` | Name of attribute to change 
 **i_accept** | `/BLCK/SP_STRING` | an Accept header [default "application/json"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/SP_DOC_ATTR_VALUE` (**[DocAttrValue](#markdown-header-model-doc_attr_value)**) | successful operation
 405 | value not returned |  | Invalid input

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


<a name="markdown-header-op-DocumentsApi-get_doc_data"></a>

## operation: **get_doc_data**
Retrieve data of document


### Example
```abap
*** method DocumentsApi->get_doc_data example
*** Retrieve data of document

  constants:
    gcc_basepath type string value 'https://<site-collection>.sharepoint.com/sites/<site>'.
    
  data:  
    gvi_code type /blck/sp_int,
    gvs_msg  type /blck/sp_string.
    
*** create variables for input and output as needed
*   for parameter i_title:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_title type /BLCK/SP_STRING.
*   for parameter i_doc_id:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_doc_id type /BLCK/SP_INT.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SP_BINARY
    data gr_http200 type /BLCK/SP_BINARY.
        
*** set data according to requirements of the API call
*   gvs_title = 'ipsum lorem'.
*   gvi_doc_id = 42.

*** pass auth credentials to the API as needed
    /blck/sp_cl_api=>set_credentials(
      exporting
        i_basic_auth_un = 'john'
        i_basic_auth_pw = 'pw' ).
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method get_doc_data via HTTP GET
*** i_title: Title of the document container
*** i_doc_id: Id of document
    /blck/sp_cl_DocumentsApi=>get_doc_data(
      exporting
        i_title = gvs_title
        i_doc_id = gvi_doc_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_BINARY)
      when 405.
*       handle code 405, e_message => gvs_msg
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_title** | `/BLCK/SP_STRING` | Title of the document container 
 **i_doc_id** | `/BLCK/SP_INT` | Id of document 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/SP_BINARY` | successful operation
 405 | value not returned |  | Invalid input

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octet-stream


<a name="markdown-header-op-DocumentsApi-get_docs"></a>

## operation: **get_docs**
Retrieve list of documents matching criteria


### Example
```abap
*** method DocumentsApi->get_docs example
*** Retrieve list of documents matching criteria

  constants:
    gcc_basepath type string value 'https://<site-collection>.sharepoint.com/sites/<site>'.
    
  data:  
    gvi_code type /blck/sp_int,
    gvs_msg  type /blck/sp_string.
    
*** create variables for input and output as needed
*   for parameter i_title:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_title type /BLCK/SP_STRING.
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_filter type /BLCK/SP_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_accept type /BLCK/SP_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SP_DOC_LIST
    data gr_http200 type /BLCK/SP_DOC_LIST.
        
*** set data according to requirements of the API call
*   gvs_title = 'ipsum lorem'.
*   gvs_filter = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.

*** pass auth credentials to the API as needed
    /blck/sp_cl_api=>set_credentials(
      exporting
        i_basic_auth_un = 'john'
        i_basic_auth_pw = 'pw' ).
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method get_docs via HTTP GET
*** i_title: Title of the document container
*** i_filter: Filter the list of documents
*** i_accept: an Accept header
    /blck/sp_cl_DocumentsApi=>get_docs(
      exporting
        i_title = gvs_title
        i_filter = gvs_filter
        i_accept = gvs_accept
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_DOC_LIST)
      when 405.
*       handle code 405, e_message => gvs_msg
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_title** | `/BLCK/SP_STRING` | Title of the document container 
 **i_filter** | `/BLCK/SP_STRING` | Filter the list of documents [optional]
 **i_accept** | `/BLCK/SP_STRING` | an Accept header [default "application/json"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/SP_DOC_LIST` (**[DocList](#markdown-header-model-doc_list)**) | successful operation
 405 | value not returned |  | Invalid input

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


<a name="markdown-header-op-DocumentsApi-set_doc_attr"></a>

## operation: **set_doc_attr**
Set properties of document

Pass in a json formatted body


### Example
```abap
*** method DocumentsApi->set_doc_attr example
*** Set properties of document

  constants:
    gcc_basepath type string value 'https://<site-collection>.sharepoint.com/sites/<site>'.
    
  data:  
    gvi_code type /blck/sp_int,
    gvs_msg  type /blck/sp_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_body type /BLCK/SP_STRING.
*   for parameter i_title:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_title type /BLCK/SP_STRING.
*   for parameter i_doc_id:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_doc_id type /BLCK/SP_INT.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_accept type /BLCK/SP_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_content_type type /BLCK/SP_STRING.
*   for parameter i_if_match:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_if_match type /BLCK/SP_STRING.
*   for parameter i_x_http_method:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_x_http_method type /BLCK/SP_STRING.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvs_title = 'ipsum lorem'.
*   gvi_doc_id = 42.
*   gvs_accept = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_if_match = 'ipsum lorem'.
*   gvs_x_http_method = 'ipsum lorem'.

*** pass auth credentials to the API as needed
    /blck/sp_cl_api=>set_credentials(
      exporting
        i_basic_auth_un = 'john'
        i_basic_auth_pw = 'pw' ).
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DocumentsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method set_doc_attr via HTTP POST
*** i_title: Title of the document container
*** i_doc_id: Id of document
*** i_accept: an Accept header
*** i_content_type: a content type header
*** i_if_match: Default match header
*** i_x_http_method: Default method header
    /blck/sp_cl_DocumentsApi=>set_doc_attr(
      exporting
        i_body = gvs_body
        i_title = gvs_title
        i_doc_id = gvi_doc_id
        i_accept = gvs_accept
        i_content_type = gvs_content_type
        i_if_match = gvs_if_match
        i_x_http_method = gvs_x_http_method
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when 405.
*       handle code 405, e_message => gvs_msg
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | `/BLCK/SP_STRING` |  
 **i_title** | `/BLCK/SP_STRING` | Title of the document container 
 **i_doc_id** | `/BLCK/SP_INT` | Id of document 
 **i_accept** | `/BLCK/SP_STRING` | an Accept header [default "application/json"]
 **i_content_type** | `/BLCK/SP_STRING` | a content type header [default "application/json"]
 **i_if_match** | `/BLCK/SP_STRING` | Default match header [default "*"]
 **i_x_http_method** | `/BLCK/SP_STRING` | Default method header [default "PATCH"]

### Return types


### HTTP request headers

 - **Content-Type**: text/plain
 - **Accept**: Not defined



# API: SearchApi

All URIs are relative to *https://<site-collection>.sharepoint.com/sites/<site>*

<a name="markdown-header-op-SearchApi-full_query"></a>

## operation: **full_query**


https://docs.microsoft.com/en-us/sharepoint/dev/general-development/sharepoint-search-rest-api-overview


### Example
```abap
*** method SearchApi->full_query example

  constants:
    gcc_basepath type string value 'https://<site-collection>.sharepoint.com/sites/<site>'.
    
  data:  
    gvi_code type /blck/sp_int,
    gvs_msg  type /blck/sp_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/SP_QUERY_REQ
    data gm_body type /BLCK/SP_QUERY_REQ.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_accept type /BLCK/SP_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SP_QUERY
    data gr_http200 type /BLCK/SP_QUERY.
        
*** set data according to requirements of the API call
*   gm_body-request = l_request. " (type /BLCK/SP_QUERYREQPARAMS)
*   gvs_accept = 'ipsum lorem'.

*** pass auth credentials to the API as needed
    /blck/sp_cl_api=>set_credentials(
      exporting
        i_basic_auth_un = 'john'
        i_basic_auth_pw = 'pw' ).
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method full_query via HTTP POST
*** i_accept: an accept header
    /blck/sp_cl_SearchApi=>full_query(
      exporting
        i_body = gm_body
        i_accept = gvs_accept
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_QUERY)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | `/BLCK/SP_QUERY_REQ` (**[QueryReq](#markdown-header-model-query_req)**) |  [optional]
 **i_accept** | `/BLCK/SP_STRING` | an accept header [default "application/json"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/SP_QUERY` (**[Query](#markdown-header-model-query)**) | OK

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


<a name="markdown-header-op-SearchApi-query"></a>

## operation: **query**


https://docs.microsoft.com/en-us/sharepoint/dev/general-development/sharepoint-search-rest-api-overview


### Example
```abap
*** method SearchApi->query example

  constants:
    gcc_basepath type string value 'https://<site-collection>.sharepoint.com/sites/<site>'.
    
  data:  
    gvi_code type /blck/sp_int,
    gvs_msg  type /blck/sp_string.
    
*** create variables for input and output as needed
*   for parameter i_querytext:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_querytext type /BLCK/SP_STRING.
*   for parameter i_querytemplate:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_querytemplate type /BLCK/SP_STRING.
*   for parameter i_enableinterleaving:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_enableinterleaving type /BLCK/SP_BOOL.
*   for parameter i_sourceid:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_sourceid type /BLCK/SP_STRING.
*   for parameter i_rankingmodelid:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_rankingmodelid type /BLCK/SP_STRING.
*   for parameter i_startrow:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_startrow type /BLCK/SP_INT.
*   for parameter i_rowlimit:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_rowlimit type /BLCK/SP_INT.
*   for parameter i_rowsperpage:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_rowsperpage type /BLCK/SP_INT.
*   for parameter i_selectproperties:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_selectproperties type /BLCK/SP_STRING.
*   for parameter i_culture:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_culture type /BLCK/SP_INT.
*   for parameter i_refinementfilters:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_refinementfilters type /BLCK/SP_STRING.
*   for parameter i_refiners:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_refiners type /BLCK/SP_STRING.
*   for parameter i_hiddenconstraints:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_hiddenconstraints type /BLCK/SP_STRING.
*   for parameter i_sortlist:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_sortlist type /BLCK/SP_STRING.
*   for parameter i_enablestemming:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_enablestemming type /BLCK/SP_BOOL.
*   for parameter i_trimduplicates:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_trimduplicates type /BLCK/SP_BOOL.
*   for parameter i_timeout:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_timeout type /BLCK/SP_INT.
*   for parameter i_enablenicknames:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_enablenicknames type /BLCK/SP_BOOL.
*   for parameter i_nnablephonetic:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_nnablephonetic type /BLCK/SP_BOOL.
*   for parameter i_enablefql:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_enablefql type /BLCK/SP_BOOL.
*   for parameter i_hithighlightedproperties:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_hithighlightedproperties type /BLCK/SP_STRING.
*   for parameter i_bypassresulttypes:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_bypassresulttypes type /BLCK/SP_BOOL.
*   for parameter i_processbestbets:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_processbestbets type /BLCK/SP_BOOL.
*   for parameter i_clienttype:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_clienttype type /BLCK/SP_STRING.
*   for parameter i_personalizationdata:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_personalizationdata type /BLCK/SP_STRING.
*   for parameter i_resultsurl:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_resultsurl type /BLCK/SP_STRING.
*   for parameter i_querytag:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_querytag type /BLCK/SP_STRING.
*   for parameter i_enablequeryrules:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_enablequeryrules type /BLCK/SP_BOOL.
*   for parameter i_processpersonalfavorites:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_processpersonalfavorites type /BLCK/SP_BOOL.
*   for parameter i_hithighlightedmultivalueprop:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_hithighlightedmultivalueprop type /BLCK/SP_INT.
*   for parameter i_enableorderinghithighlighted:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_enableorderinghithighlighted type /BLCK/SP_BOOL.
*   for parameter i_collapsespecification:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_collapsespecification type /BLCK/SP_STRING.
*   for parameter i_enablesorting:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_enablesorting type /BLCK/SP_BOOL.
*   for parameter i_generateblockranklog:
*   a simple ABAP primitive of type /BLCK/SP_BOOL
    data gv_generateblockranklog type /BLCK/SP_BOOL.
*   for parameter i_uilanguage:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_uilanguage type /BLCK/SP_INT.
*   for parameter i_desiredsnippetlength:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_desiredsnippetlength type /BLCK/SP_INT.
*   for parameter i_maxsnippetlength:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_maxsnippetlength type /BLCK/SP_INT.
*   for parameter i_summarylength:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_summarylength type /BLCK/SP_INT.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_accept type /BLCK/SP_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SP_QUERY
    data gr_http200 type /BLCK/SP_QUERY.
        
*** set data according to requirements of the API call
*   gvs_querytext = 'ipsum lorem'.
*   gvs_querytemplate = 'ipsum lorem'.
*   gv_enableinterleaving = 'X'.
*   gvs_sourceid = 'ipsum lorem'.
*   gvs_rankingmodelid = 'ipsum lorem'.
*   gvi_startrow = 42.
*   gvi_rowlimit = 42.
*   gvi_rowsperpage = 42.
*   gvs_selectproperties = 'ipsum lorem'.
*   gvi_culture = 42.
*   gvs_refinementfilters = 'ipsum lorem'.
*   gvs_refiners = 'ipsum lorem'.
*   gvs_hiddenconstraints = 'ipsum lorem'.
*   gvs_sortlist = 'ipsum lorem'.
*   gv_enablestemming = 'X'.
*   gv_trimduplicates = 'X'.
*   gvi_timeout = 42.
*   gv_enablenicknames = 'X'.
*   gv_nnablephonetic = 'X'.
*   gv_enablefql = 'X'.
*   gvs_hithighlightedproperties = 'ipsum lorem'.
*   gv_bypassresulttypes = 'X'.
*   gv_processbestbets = 'X'.
*   gvs_clienttype = 'ipsum lorem'.
*   gvs_personalizationdata = 'ipsum lorem'.
*   gvs_resultsurl = 'ipsum lorem'.
*   gvs_querytag = 'ipsum lorem'.
*   gv_enablequeryrules = 'X'.
*   gv_processpersonalfavorites = 'X'.
*   gvi_hithighlightedmultivalueprop = 42.
*   gv_enableorderinghithighlighted = 'X'.
*   gvs_collapsespecification = 'ipsum lorem'.
*   gv_enablesorting = 'X'.
*   gv_generateblockranklog = 'X'.
*   gvi_uilanguage = 42.
*   gvi_desiredsnippetlength = 42.
*   gvi_maxsnippetlength = 42.
*   gvi_summarylength = 42.
*   gvs_accept = 'ipsum lorem'.

*** pass auth credentials to the API as needed
    /blck/sp_cl_api=>set_credentials(
      exporting
        i_basic_auth_un = 'john'
        i_basic_auth_pw = 'pw' ).
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method query via HTTP GET
*** i_querytext: A string that contains the text for the search query.
*** i_querytemplate: A  string  that contains the text that replaces the query text, as part of a
*** query transform.
*** i_enableinterleaving: A  Boolean  value that specifies whether the result tables that are returned
*** for  the result block are mixed with the result tables that are returned for
*** the  original  query.  true  to  mix the ResultTables; otherwise, false. The
*** default  value  is  true. Change this value only if you want to provide your
*** own interleaving implementation.
*** i_sourceid: The result source ID to use for executing the search query.
*** i_rankingmodelid: The ID of the ranking model to use for the query.
*** i_startrow: The  first row that is included in the search results that are returned. You
*** use this parameter when you want to implement paging for search results.
*** i_rowlimit: The  maximum number of rows overall that are returned in the search results.
*** Compared  to  RowsPerPage,  RowLimit  is the maximum number of rows returned
*** overall.
*** i_rowsperpage: The  maximum  number  of  rows  to  return  per  page. Compared to RowLimit,
*** RowsPerPage  refers to the maximum number of rows to return per page, and is
*** used primarily when you want to implement paging for search results.
*** i_selectproperties: The  managed properties to return in the search results. To return a managed
*** property,  set the property's retrievable flag to true in the search schema.
*** Specify   the   SelectProperties   parameter   in   a  string  containing  a
*** comma-separated list of properties.
*** i_culture: The locale ID (LCID) for the query
*** i_refinementfilters: The  set  of  refinement  filters  used when issuing a refinement query. The
*** RefinementFilters parameter is specified as an FQL filter.
*** i_refiners: The set of refiners to return in a search result.
*** i_hiddenconstraints: The additional query terms to append to the query.
*** i_sortlist: The list of properties by which the search results are ordered.
*** i_enablestemming: A  Boolean  value  that  specifies  whether stemming is enabled. true if the
*** stemming is enabled; otherwise, false. The default value is true.
*** i_trimduplicates: A  Boolean value that specifies whether duplicate items are removed from the
*** results.  true  to remove the duplicate items; otherwise, false. The default
*** value is true.
*** i_timeout: The  amount  of time in milliseconds before the query request times out. The
*** default value is 30000.
*** i_enablenicknames: A  Boolean  value that specifies whether the exact terms in the search query
*** are  used  to find matches, or if nicknames are used also. true if nicknames
*** are used; otherwise, false. The default value is false.
*** i_nnablephonetic: A Boolean value that specifies whether the phonetic forms of the query terms
*** are used to find matches. true if phonetic forms are used; otherwise, false.
*** The default value is false.
*** i_enablefql: A  Boolean  value  that  specifies  whether  the  query  uses the FAST Query
*** Language  (FQL).  true  if  the query is an FQL query; otherwise, false. The
*** default value is false.
*** i_hithighlightedproperties: The  properties  to highlight in the search result summary when the property
*** value  matches  the  search  terms  entered by the user. Specify in a string
*** containing a comma-separated list of properties.
*** i_bypassresulttypes: A Boolean value that specifies whether to perform result type processing for
*** the  query.  true  to  perform result type processing; otherwise, false. The
*** default value is false.
*** i_processbestbets: A  Boolean  value  that specifies whether to return best bet results for the
*** query.  true  to  return best bets; otherwise, false. This parameter is used
*** only  when  EnableQueryRules  is  set  to true, otherwise it is ignored. The
*** default value is false.
*** i_clienttype: The type of the client that issued the query.
*** i_personalizationdata: The GUID for the user who submitted the search query.
*** i_resultsurl: The URL for the search results page.
*** i_querytag: Custom  tags  that  identify the query. You can specify multiple query tags,
*** separated by semicolons.
*** i_enablequeryrules: A  Boolean value that specifies whether to enable query rules for the query.
*** true to enable query rules; otherwise, false. The default value is true.
*** i_processpersonalfavorites: A Boolean value that specifies whether to return personal favorites with the
*** search results. true to return personal favorites; otherwise false.
*** i_hithighlightedmultivalueprop: The number of properties to show hit highlighting for in the search results.
*** i_enableorderinghithighlighted: A Boolean value that specifies whether the hit highlighted properties can be
*** ordered. true to enable ordering rules; otherwise false.
*** i_collapsespecification: The managed properties that are used to determine how to collapse individual
*** search  results.  Results  are  collapsed  into one or a specified number of
*** results  if they match any of the individual collapse specifications. Within
*** a  single  collapse specification, results are collapsed if their properties
*** match all individual properties in the collapse specification.
*** i_enablesorting: A  Boolean value that specifies whether to sort search results. true to sort
*** search  results  using  SortList,  or by rank if SortList is empty. false to
*** leave results unsorted.
*** i_generateblockranklog: A  Boolean value that specifies whether to return block rank log information
*** in  the  BlockRankLog property of the interleaved result table. A block rank
*** log  contains  the  textual information on the block score and the documents
*** that  were  de-duplicated.  true  to  return  block  rank  log  information;
*** otherwise, false.
*** i_uilanguage: The locale identifier (LCID) of the user interface
*** i_desiredsnippetlength: The preferred number of characters to display in the hit-highlighted summary
*** generated for a search result.
*** i_maxsnippetlength: The  maximum  number of characters to display in the hit-highlighted summary
*** generated for a search result.
*** i_summarylength: The  number  of  characters  to  display  in the result summary for a search
*** result.
*** i_accept: an accept header
    /blck/sp_cl_SearchApi=>query(
      exporting
        i_querytext = gvs_querytext
        i_querytemplate = gvs_querytemplate
        i_enableinterleaving = gv_enableinterleaving
        i_sourceid = gvs_sourceid
        i_rankingmodelid = gvs_rankingmodelid
        i_startrow = gvi_startrow
        i_rowlimit = gvi_rowlimit
        i_rowsperpage = gvi_rowsperpage
        i_selectproperties = gvs_selectproperties
        i_culture = gvi_culture
        i_refinementfilters = gvs_refinementfilters
        i_refiners = gvs_refiners
        i_hiddenconstraints = gvs_hiddenconstraints
        i_sortlist = gvs_sortlist
        i_enablestemming = gv_enablestemming
        i_trimduplicates = gv_trimduplicates
        i_timeout = gvi_timeout
        i_enablenicknames = gv_enablenicknames
        i_nnablephonetic = gv_nnablephonetic
        i_enablefql = gv_enablefql
        i_hithighlightedproperties = gvs_hithighlightedproperties
        i_bypassresulttypes = gv_bypassresulttypes
        i_processbestbets = gv_processbestbets
        i_clienttype = gvs_clienttype
        i_personalizationdata = gvs_personalizationdata
        i_resultsurl = gvs_resultsurl
        i_querytag = gvs_querytag
        i_enablequeryrules = gv_enablequeryrules
        i_processpersonalfavorites = gv_processpersonalfavorites
        i_hithighlightedmultivalueprop = gvi_hithighlightedmultivalueprop
        i_enableorderinghithighlighted = gv_enableorderinghithighlighted
        i_collapsespecification = gvs_collapsespecification
        i_enablesorting = gv_enablesorting
        i_generateblockranklog = gv_generateblockranklog
        i_uilanguage = gvi_uilanguage
        i_desiredsnippetlength = gvi_desiredsnippetlength
        i_maxsnippetlength = gvi_maxsnippetlength
        i_summarylength = gvi_summarylength
        i_accept = gvs_accept
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_QUERY)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_querytext** | `/BLCK/SP_STRING` | A string that contains the text for the search query. [optional]
 **i_querytemplate** | `/BLCK/SP_STRING` | A string that contains the text that replaces the query text, as part of a query transform. [optional]
 **i_enableinterleaving** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the result tables that are returned for the result block are mixed with the result tables that are returned for the original query. true to mix the ResultTables; otherwise, false. The default value is true. Change this value only if you want to provide your own interleaving implementation. [default "true"]
 **i_sourceid** | `/BLCK/SP_STRING` | The result source ID to use for executing the search query. [optional]
 **i_rankingmodelid** | `/BLCK/SP_STRING` | The ID of the ranking model to use for the query. [optional]
 **i_startrow** | `/BLCK/SP_INT` | The first row that is included in the search results that are returned. You use this parameter when you want to implement paging for search results. [optional]
 **i_rowlimit** | `/BLCK/SP_INT` | The maximum number of rows overall that are returned in the search results. Compared to RowsPerPage, RowLimit is the maximum number of rows returned overall. [optional]
 **i_rowsperpage** | `/BLCK/SP_INT` | The maximum number of rows to return per page. Compared to RowLimit, RowsPerPage refers to the maximum number of rows to return per page, and is used primarily when you want to implement paging for search results. [optional]
 **i_selectproperties** | `/BLCK/SP_STRING` | The managed properties to return in the search results. To return a managed property, set the property&#x27;s retrievable flag to true in the search schema. Specify the SelectProperties parameter in a string containing a comma-separated list of properties. [optional]
 **i_culture** | `/BLCK/SP_INT` | The locale ID (LCID) for the query [optional]
 **i_refinementfilters** | `/BLCK/SP_STRING` | The set of refinement filters used when issuing a refinement query. The RefinementFilters parameter is specified as an FQL filter. [optional]
 **i_refiners** | `/BLCK/SP_STRING` | The set of refiners to return in a search result. [optional]
 **i_hiddenconstraints** | `/BLCK/SP_STRING` | The additional query terms to append to the query. [optional]
 **i_sortlist** | `/BLCK/SP_STRING` | The list of properties by which the search results are ordered. [optional]
 **i_enablestemming** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether stemming is enabled. true if the stemming is enabled; otherwise, false. The default value is true. [default "true"]
 **i_trimduplicates** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether duplicate items are removed from the results. true to remove the duplicate items; otherwise, false. The default value is true. [default "true"]
 **i_timeout** | `/BLCK/SP_INT` | The amount of time in milliseconds before the query request times out. The default value is 30000. [optional]
 **i_enablenicknames** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the exact terms in the search query are used to find matches, or if nicknames are used also. true if nicknames are used; otherwise, false. The default value is false. [optional]
 **i_nnablephonetic** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the phonetic forms of the query terms are used to find matches. true if phonetic forms are used; otherwise, false. The default value is false. [optional]
 **i_enablefql** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the query uses the FAST Query Language (FQL). true if the query is an FQL query; otherwise, false. The default value is false. [optional]
 **i_hithighlightedproperties** | `/BLCK/SP_STRING` | The properties to highlight in the search result summary when the property value matches the search terms entered by the user. Specify in a string containing a comma-separated list of properties. [optional]
 **i_bypassresulttypes** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to perform result type processing for the query. true to perform result type processing; otherwise, false. The default value is false. [optional]
 **i_processbestbets** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to return best bet results for the query. true to return best bets; otherwise, false. This parameter is used only when EnableQueryRules is set to true, otherwise it is ignored. The default value is false. [optional]
 **i_clienttype** | `/BLCK/SP_STRING` | The type of the client that issued the query. [optional]
 **i_personalizationdata** | `/BLCK/SP_STRING` | The GUID for the user who submitted the search query. [optional]
 **i_resultsurl** | `/BLCK/SP_STRING` | The URL for the search results page. [optional]
 **i_querytag** | `/BLCK/SP_STRING` | Custom tags that identify the query. You can specify multiple query tags, separated by semicolons. [optional]
 **i_enablequeryrules** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to enable query rules for the query. true to enable query rules; otherwise, false. The default value is true. [default "true"]
 **i_processpersonalfavorites** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to return personal favorites with the search results. true to return personal favorites; otherwise false. [optional]
 **i_hithighlightedmultivalueprop** | `/BLCK/SP_INT` | The number of properties to show hit highlighting for in the search results. [optional]
 **i_enableorderinghithighlighted** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the hit highlighted properties can be ordered. true to enable ordering rules; otherwise false. [optional]
 **i_collapsespecification** | `/BLCK/SP_STRING` | The managed properties that are used to determine how to collapse individual search results. Results are collapsed into one or a specified number of results if they match any of the individual collapse specifications. Within a single collapse specification, results are collapsed if their properties match all individual properties in the collapse specification. [optional]
 **i_enablesorting** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to sort search results. true to sort search results using SortList, or by rank if SortList is empty. false to leave results unsorted. [optional]
 **i_generateblockranklog** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to return block rank log information in the BlockRankLog property of the interleaved result table. A block rank log contains the textual information on the block score and the documents that were de-duplicated. true to return block rank log information; otherwise, false. [optional]
 **i_uilanguage** | `/BLCK/SP_INT` | The locale identifier (LCID) of the user interface [optional]
 **i_desiredsnippetlength** | `/BLCK/SP_INT` | The preferred number of characters to display in the hit-highlighted summary generated for a search result. [optional]
 **i_maxsnippetlength** | `/BLCK/SP_INT` | The maximum number of characters to display in the hit-highlighted summary generated for a search result. [optional]
 **i_summarylength** | `/BLCK/SP_INT` | The number of characters to display in the result summary for a search result. [optional]
 **i_accept** | `/BLCK/SP_STRING` | an accept header [default "application/json"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/SP_QUERY` (**[Query](#markdown-header-model-query)**) | OK

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-cells"></a> 

# Model: Cells



### Example
```abap
*** model cells example
*** Model for Cells

* create our variables..
    data gr_cells type /blck/sp_cells.
    
* fill model with data as appropriate..
    gr_cells-key = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_cells-value = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_cells-value_type = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_cells(
      exporting
        i_cells = gr_cells ).
    		
    clear gr_cells.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_cells(
      exporting
        i_id = 1
      importing 
        e_200 = gr_cells ).
    		
    write: gr_cells-key. " (type /BLCK/SP_STRING)
    write: gr_cells-value. " (type /BLCK/SP_STRING)
    write: gr_cells-value_type. " (type /BLCK/SP_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**key** | `/BLCK/SP_STRING` | 
**value** | `/BLCK/SP_STRING` | 
**value_type** | `/BLCK/SP_STRING` | 

* * *
<a name="markdown-header-model-doc_attr_value"></a> 

# Model: DocAttrValue



### Example
```abap
*** model doc_attr_value example

* create our variables..
    data gr_doc_attr_value type /blck/sp_doc_attr_value.
    
* fill model with data as appropriate..
    gr_doc_attr_value-value = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_doc_attr_value(
      exporting
        i_doc_attr_value = gr_doc_attr_value ).
    		
    clear gr_doc_attr_value.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_doc_attr_value(
      exporting
        i_id = 1
      importing 
        e_200 = gr_doc_attr_value ).
    		
    write: gr_doc_attr_value-value. " (type /BLCK/SP_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**value** | `/BLCK/SP_STRING` | 

* * *
<a name="markdown-header-model-document"></a> 

# Model: Document



### Example
```abap
*** model document example

* create our variables..
    data gr_document type /blck/sp_document.
    
* fill model with data as appropriate..
    
* pass to example API method
    /blck/cl_example_api=>update_document(
      exporting
        i_document = gr_document ).
    		
    clear gr_document.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_document(
      exporting
        i_id = 1
      importing 
        e_200 = gr_document ).
    		

```

## Properties

Name | Type | Description
------------ | ------------- | -------------

* * *
<a name="markdown-header-model-doc_list"></a> 

# Model: DocList



### Example
```abap
*** model doc_list example

* create our variables..
    data gr_doc_list type /blck/sp_doc_list.
    
* fill model with data as appropriate..
    gr_doc_list-value = l_value. " (type /BLCK/SP_DOCUMENT_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_doc_list(
      exporting
        i_doc_list = gr_doc_list ).
    		
    clear gr_doc_list.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_doc_list(
      exporting
        i_id = 1
      importing 
        e_200 = gr_doc_list ).
    		
    write: gr_doc_list-value. " (type /BLCK/SP_DOCUMENT_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**value** | `/BLCK/SP_DOCUMENT_TT` (**[array of Document](#markdown-header-model-document)**) | 

* * *
<a name="markdown-header-model-properties"></a> 

# Model: Properties



### Example
```abap
*** model properties example
*** Model for Properties

* create our variables..
    data gr_properties type /blck/sp_properties.
    
* fill model with data as appropriate..
    gr_properties-key = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_properties-value = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_properties-value_type = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_properties(
      exporting
        i_properties = gr_properties ).
    		
    clear gr_properties.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_properties(
      exporting
        i_id = 1
      importing 
        e_200 = gr_properties ).
    		
    write: gr_properties-key. " (type /BLCK/SP_STRING)
    write: gr_properties-value. " (type /BLCK/SP_STRING)
    write: gr_properties-value_type. " (type /BLCK/SP_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**key** | `/BLCK/SP_STRING` | 
**value** | `/BLCK/SP_STRING` | 
**value_type** | `/BLCK/SP_STRING` | 

* * *
<a name="markdown-header-model-rows"></a> 

# Model: Rows



### Example
```abap
*** model rows example
*** Model for Rows

* create our variables..
    data gr_rows type /blck/sp_rows.
    
* fill model with data as appropriate..
    gr_rows-cells = l_cells. " (type /BLCK/SP_CELLS_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_rows(
      exporting
        i_rows = gr_rows ).
    		
    clear gr_rows.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_rows(
      exporting
        i_id = 1
      importing 
        e_200 = gr_rows ).
    		
    write: gr_rows-cells. " (type /BLCK/SP_CELLS_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**cells** | `/BLCK/SP_CELLS_TT` (**[array of Cells](#markdown-header-model-cells)**) | 

* * *
<a name="markdown-header-model-table"></a> 

# Model: Table



### Example
```abap
*** model table example
*** Model for Table

* create our variables..
    data gr_table type /blck/sp_table.
    
* fill model with data as appropriate..
    gr_table-rows = l_rows. " (type /BLCK/SP_ROWS_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_table(
      exporting
        i_table = gr_table ).
    		
    clear gr_table.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_table(
      exporting
        i_id = 1
      importing 
        e_200 = gr_table ).
    		
    write: gr_table-rows. " (type /BLCK/SP_ROWS_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**rows** | `/BLCK/SP_ROWS_TT` (**[array of Rows](#markdown-header-model-rows)**) | 

* * *
<a name="markdown-header-model-relevantresult"></a> 

# Model: RelevantResults



### Example
```abap
*** model relevantresult example
*** Model for RelevantResults

* create our variables..
    data gr_relevantresult type /blck/sp_relevantresult.
    
* fill model with data as appropriate..
    gr_relevantresult-group_template_id = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_relevantresult-item_template_id = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_relevantresult-properties = l_properties. " (type /BLCK/SP_PROPERTIES_TT)
    gr_relevantresult-result_title = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_relevantresult-result_title_url = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_relevantresult-row_count = 42. " (type /BLCK/SP_INT)
    gr_relevantresult-table = l_table. " (type /BLCK/SP_TABLE)
    gr_relevantresult-total_rows = 42. " (type /BLCK/SP_INT)
    gr_relevantresult-totalrowsincludingduplicat = 42. " (type /BLCK/SP_INT)
    
* pass to example API method
    /blck/cl_example_api=>update_relevantresult(
      exporting
        i_relevantresult = gr_relevantresult ).
    		
    clear gr_relevantresult.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_relevantresult(
      exporting
        i_id = 1
      importing 
        e_200 = gr_relevantresult ).
    		
    write: gr_relevantresult-group_template_id. " (type /BLCK/SP_STRING)
    write: gr_relevantresult-item_template_id. " (type /BLCK/SP_STRING)
    write: gr_relevantresult-properties. " (type /BLCK/SP_PROPERTIES_TT)
    write: gr_relevantresult-result_title. " (type /BLCK/SP_STRING)
    write: gr_relevantresult-result_title_url. " (type /BLCK/SP_STRING)
    write: gr_relevantresult-row_count. " (type /BLCK/SP_INT)
    write: gr_relevantresult-table. " (type /BLCK/SP_TABLE)
    write: gr_relevantresult-total_rows. " (type /BLCK/SP_INT)
    write: gr_relevantresult-totalrowsincludingduplicat. " (type /BLCK/SP_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**group_template_id** | `/BLCK/SP_STRING` | 
**item_template_id** | `/BLCK/SP_STRING` | 
**properties** | `/BLCK/SP_PROPERTIES_TT` (**[array of Properties](#markdown-header-model-properties)**) | 
**result_title** | `/BLCK/SP_STRING` | 
**result_title_url** | `/BLCK/SP_STRING` | 
**row_count** | `/BLCK/SP_INT` | 
**table** | `/BLCK/SP_TABLE` (**[Table](#markdown-header-model-table)**) | 
**total_rows** | `/BLCK/SP_INT` | 
**totalrowsincludingduplicat** | `/BLCK/SP_INT` | 

* * *
<a name="markdown-header-model-primaryqueryre"></a> 

# Model: PrimaryQueryResult



### Example
```abap
*** model primaryqueryre example
*** Model for PrimaryQueryResult

* create our variables..
    data gr_primaryqueryre type /blck/sp_primaryqueryre.
    
* fill model with data as appropriate..
    gr_primaryqueryre-custom_results = l_custom_results. " (type /BLCK/SP_STRING_TT)
    gr_primaryqueryre-query_id = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_primaryqueryre-query_rule_id = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_primaryqueryre-refinement_results = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_primaryqueryre-relevant_results = l_relevant_results. " (type /BLCK/SP_RELEVANTRESULT)
    gr_primaryqueryre-special_term_results = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_primaryqueryre(
      exporting
        i_primaryqueryre = gr_primaryqueryre ).
    		
    clear gr_primaryqueryre.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_primaryqueryre(
      exporting
        i_id = 1
      importing 
        e_200 = gr_primaryqueryre ).
    		
    write: gr_primaryqueryre-custom_results. " (type /BLCK/SP_STRING_TT)
    write: gr_primaryqueryre-query_id. " (type /BLCK/SP_STRING)
    write: gr_primaryqueryre-query_rule_id. " (type /BLCK/SP_STRING)
    write: gr_primaryqueryre-refinement_results. " (type /BLCK/SP_STRING)
    write: gr_primaryqueryre-relevant_results. " (type /BLCK/SP_RELEVANTRESULT)
    write: gr_primaryqueryre-special_term_results. " (type /BLCK/SP_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**custom_results** | `/BLCK/SP_STRING_TT` | 
**query_id** | `/BLCK/SP_STRING` | 
**query_rule_id** | `/BLCK/SP_STRING` | 
**refinement_results** | `/BLCK/SP_STRING` | 
**relevant_results** | `/BLCK/SP_RELEVANTRESULT` (**[RelevantResults](#markdown-header-model-relevantresult)**) | 
**special_term_results** | `/BLCK/SP_STRING` | 

* * *
<a name="markdown-header-model-query"></a> 

# Model: Query



### Example
```abap
*** model query example
*** Model for Query

* create our variables..
    data gr_query type /blck/sp_query.
    
* fill model with data as appropriate..
    gr_query-elapsed_time = 42. " (type /BLCK/SP_INT)
    gr_query-odata_metadata = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_query-primary_query_result = l_primary_query_result. " (type /BLCK/SP_PRIMARYQUERYRE)
    gr_query-properties = l_properties. " (type /BLCK/SP_PROPERTIES_TT)
    gr_query-secondary_query_results = l_secondary_query_results. " (type /BLCK/SP_STRING_TT)
    gr_query-spelling_suggestion = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_query-triggered_rules = l_triggered_rules. " (type /BLCK/SP_STRING_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_query(
      exporting
        i_query = gr_query ).
    		
    clear gr_query.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_query(
      exporting
        i_id = 1
      importing 
        e_200 = gr_query ).
    		
    write: gr_query-elapsed_time. " (type /BLCK/SP_INT)
    write: gr_query-odata_metadata. " (type /BLCK/SP_STRING)
    write: gr_query-primary_query_result. " (type /BLCK/SP_PRIMARYQUERYRE)
    write: gr_query-properties. " (type /BLCK/SP_PROPERTIES_TT)
    write: gr_query-secondary_query_results. " (type /BLCK/SP_STRING_TT)
    write: gr_query-spelling_suggestion. " (type /BLCK/SP_STRING)
    write: gr_query-triggered_rules. " (type /BLCK/SP_STRING_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**elapsed_time** | `/BLCK/SP_INT` | 
**odata_metadata** | `/BLCK/SP_STRING` | 
**primary_query_result** | `/BLCK/SP_PRIMARYQUERYRE` (**[PrimaryQueryResult](#markdown-header-model-primaryqueryre)**) | 
**properties** | `/BLCK/SP_PROPERTIES_TT` (**[array of Properties](#markdown-header-model-properties)**) | 
**secondary_query_results** | `/BLCK/SP_STRING_TT` | 
**spelling_suggestion** | `/BLCK/SP_STRING` | 
**triggered_rules** | `/BLCK/SP_STRING_TT` | 

* * *
<a name="markdown-header-model-stringresultar"></a> 

# Model: StringResultArray



### Example
```abap
*** model stringresultar example

* create our variables..
    data gr_stringresultar type /blck/sp_stringresultar.
    
* fill model with data as appropriate..
    gr_stringresultar-results = l_results. " (type /BLCK/SP_STRING_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_stringresultar(
      exporting
        i_stringresultar = gr_stringresultar ).
    		
    clear gr_stringresultar.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_stringresultar(
      exporting
        i_id = 1
      importing 
        e_200 = gr_stringresultar ).
    		
    write: gr_stringresultar-results. " (type /BLCK/SP_STRING_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**results** | `/BLCK/SP_STRING_TT` | 

* * *
<a name="markdown-header-model-queryreqparams"></a> 

# Model: QueryReqParams



### Example
```abap
*** model queryreqparams example
*** Request arguments for query operations

* create our variables..
    data gr_queryreqparams type /blck/sp_queryreqparams.
    
* fill model with data as appropriate..
    gr_queryreqparams-query_text = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-query_template = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-enable_interleaving = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-source_id = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-ranking_model_id = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-start_row = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-row_limit = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-rows_per_page = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-select_properties = l_select_properties. " (type /BLCK/SP_STRINGRESULTAR)
    gr_queryreqparams-culture = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-refinement_filters = l_refinement_filters. " (type /BLCK/SP_STRINGRESULTAR)
    gr_queryreqparams-refiners = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-hidden_constraints = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-sort_list = l_sort_list. " (type /BLCK/SP_STRINGRESULTAR)
    gr_queryreqparams-enable_stemming = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-trim_duplicates = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-timeout = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-enable_nicknames = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-enable_phonetic = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-enable_fql = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-hithighlighted_properties = l_hithighlighted_properties. " (type /BLCK/SP_STRINGRESULTAR)
    gr_queryreqparams-bypass_result_types = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-process_best_bets = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-client_type = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-personalization_data = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-results_url = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-query_tag = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-enable_query_rules = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-process_personal_favorites = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-hithighlightedmultivaluepr = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-enableorderinghithighlight = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-collapse_specification = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_queryreqparams-enable_sorting = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-generate_block_rank_log = 'X'. " (type /BLCK/SP_BOOL)
    gr_queryreqparams-u_ilanguage = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-desired_snippet_length = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-max_snippet_length = 42. " (type /BLCK/SP_INT)
    gr_queryreqparams-summary_length = 42. " (type /BLCK/SP_INT)
    
* pass to example API method
    /blck/cl_example_api=>update_queryreqparams(
      exporting
        i_queryreqparams = gr_queryreqparams ).
    		
    clear gr_queryreqparams.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_queryreqparams(
      exporting
        i_id = 1
      importing 
        e_200 = gr_queryreqparams ).
    		
    write: gr_queryreqparams-query_text. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-query_template. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-enable_interleaving. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-source_id. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-ranking_model_id. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-start_row. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-row_limit. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-rows_per_page. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-select_properties. " (type /BLCK/SP_STRINGRESULTAR)
    write: gr_queryreqparams-culture. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-refinement_filters. " (type /BLCK/SP_STRINGRESULTAR)
    write: gr_queryreqparams-refiners. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-hidden_constraints. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-sort_list. " (type /BLCK/SP_STRINGRESULTAR)
    write: gr_queryreqparams-enable_stemming. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-trim_duplicates. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-timeout. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-enable_nicknames. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-enable_phonetic. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-enable_fql. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-hithighlighted_properties. " (type /BLCK/SP_STRINGRESULTAR)
    write: gr_queryreqparams-bypass_result_types. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-process_best_bets. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-client_type. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-personalization_data. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-results_url. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-query_tag. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-enable_query_rules. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-process_personal_favorites. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-hithighlightedmultivaluepr. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-enableorderinghithighlight. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-collapse_specification. " (type /BLCK/SP_STRING)
    write: gr_queryreqparams-enable_sorting. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-generate_block_rank_log. " (type /BLCK/SP_BOOL)
    write: gr_queryreqparams-u_ilanguage. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-desired_snippet_length. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-max_snippet_length. " (type /BLCK/SP_INT)
    write: gr_queryreqparams-summary_length. " (type /BLCK/SP_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**query_text** | `/BLCK/SP_STRING` | A string that contains the text for the search query.
**query_template** | `/BLCK/SP_STRING` | A string that contains the text that replaces the query text, as part of a query transform.
**enable_interleaving** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the result tables that are returned for the result block are mixed with the result tables that are returned for the original query. true to mix the ResultTables; otherwise, false. The default value is true. Change this value only if you want to provide your own interleaving implementation.
**source_id** | `/BLCK/SP_STRING` | The result source ID to use for executing the search query.
**ranking_model_id** | `/BLCK/SP_STRING` | The ID of the ranking model to use for the query.
**start_row** | `/BLCK/SP_INT` | The first row that is included in the search results that are returned. You use this parameter when you want to implement paging for search results.
**row_limit** | `/BLCK/SP_INT` | The maximum number of rows overall that are returned in the search results. Compared to RowsPerPage, RowLimit is the maximum number of rows returned overall.
**rows_per_page** | `/BLCK/SP_INT` | The maximum number of rows to return per page. Compared to RowLimit, RowsPerPage refers to the maximum number of rows to return per page, and is used primarily when you want to implement paging for search results.
**select_properties** | `/BLCK/SP_STRINGRESULTAR` (**[StringResultArray](#markdown-header-model-stringresultar)**) | 
**culture** | `/BLCK/SP_INT` | The locale ID (LCID) for the query
**refinement_filters** | `/BLCK/SP_STRINGRESULTAR` (**[StringResultArray](#markdown-header-model-stringresultar)**) | 
**refiners** | `/BLCK/SP_STRING` | The set of refiners to return in a search result.
**hidden_constraints** | `/BLCK/SP_STRING` | The additional query terms to append to the query.
**sort_list** | `/BLCK/SP_STRINGRESULTAR` (**[StringResultArray](#markdown-header-model-stringresultar)**) | 
**enable_stemming** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether stemming is enabled. true if the stemming is enabled; otherwise, false. The default value is true.
**trim_duplicates** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether duplicate items are removed from the results. true to remove the duplicate items; otherwise, false. The default value is true.
**timeout** | `/BLCK/SP_INT` | The amount of time in milliseconds before the query request times out. The default value is 30000.
**enable_nicknames** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the exact terms in the search query are used to find matches, or if nicknames are used also. true if nicknames are used; otherwise, false. The default value is false.
**enable_phonetic** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the phonetic forms of the query terms are used to find matches. true if phonetic forms are used; otherwise, false. The default value is false.
**enable_fql** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the query uses the FAST Query Language (FQL). true if the query is an FQL query; otherwise, false. The default value is false.
**hithighlighted_properties** | `/BLCK/SP_STRINGRESULTAR` (**[StringResultArray](#markdown-header-model-stringresultar)**) | 
**bypass_result_types** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to perform result type processing for the query. true to perform result type processing; otherwise, false. The default value is false.
**process_best_bets** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to return best bet results for the query. true to return best bets; otherwise, false. This parameter is used only when EnableQueryRules is set to true, otherwise it is ignored. The default value is false.
**client_type** | `/BLCK/SP_STRING` | The type of the client that issued the query.
**personalization_data** | `/BLCK/SP_STRING` | The GUID for the user who submitted the search query.
**results_url** | `/BLCK/SP_STRING` | The URL for the search results page.
**query_tag** | `/BLCK/SP_STRING` | Custom tags that identify the query. You can specify multiple query tags, separated by semicolons.
**enable_query_rules** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to enable query rules for the query. true to enable query rules; otherwise, false. The default value is true.
**process_personal_favorites** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to return personal favorites with the search results. true to return personal favorites; otherwise false.
**hithighlightedmultivaluepr** | `/BLCK/SP_INT` | The number of properties to show hit highlighting for in the search results.
**enableorderinghithighlight** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether the hit highlighted properties can be ordered. true to enable ordering rules; otherwise false.
**collapse_specification** | `/BLCK/SP_STRING` | The managed properties that are used to determine how to collapse individual search results. Results are collapsed into one or a specified number of results if they match any of the individual collapse specifications. Within a single collapse specification, results are collapsed if their properties match all individual properties in the collapse specification.
**enable_sorting** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to sort search results. true to sort search results using SortList, or by rank if SortList is empty. false to leave results unsorted.
**generate_block_rank_log** | `/BLCK/SP_BOOL` | A Boolean value that specifies whether to return block rank log information in the BlockRankLog property of the interleaved result table. A block rank log contains the textual information on the block score and the documents that were de-duplicated. true to return block rank log information; otherwise, false.
**u_ilanguage** | `/BLCK/SP_INT` | The locale identifier (LCID) of the user interface
**desired_snippet_length** | `/BLCK/SP_INT` | The preferred number of characters to display in the hit-highlighted summary generated for a search result.
**max_snippet_length** | `/BLCK/SP_INT` | The maximum number of characters to display in the hit-highlighted summary generated for a search result.
**summary_length** | `/BLCK/SP_INT` | The number of characters to display in the result summary for a search result.

* * *
<a name="markdown-header-model-query_req"></a> 

# Model: QueryReq



### Example
```abap
*** model query_req example
*** Request arguments for query operations

* create our variables..
    data gr_query_req type /blck/sp_query_req.
    
* fill model with data as appropriate..
    gr_query_req-request = l_request. " (type /BLCK/SP_QUERYREQPARAMS)
    
* pass to example API method
    /blck/cl_example_api=>update_query_req(
      exporting
        i_query_req = gr_query_req ).
    		
    clear gr_query_req.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_query_req(
      exporting
        i_id = 1
      importing 
        e_200 = gr_query_req ).
    		
    write: gr_query_req-request. " (type /BLCK/SP_QUERYREQPARAMS)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**request** | `/BLCK/SP_QUERYREQPARAMS` (**[QueryReqParams](#markdown-header-model-queryreqparams)**) | 

