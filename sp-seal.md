# API: DefaultApi
## &nbsp; &nbsp; [Operation: get_doc_attr](#markdown-header-op-DefaultApi-get_doc_attr)
## &nbsp; &nbsp; [Operation: get_doc_data](#markdown-header-op-DefaultApi-get_doc_data)
## &nbsp; &nbsp; [Operation: get_docs](#markdown-header-op-DefaultApi-get_docs)
## &nbsp; &nbsp; [Operation: set_doc_attr](#markdown-header-op-DefaultApi-set_doc_attr)
# Models and Enumerations
## &nbsp; &nbsp; [Model: DocAttrValue](#markdown-header-model-doc_attr_value) (type `/blck/sp_doc_attr_value`)
## &nbsp; &nbsp; [Model: SEALDoc](#markdown-header-model-seal_doc) (type `/blck/sp_seal_doc`)
## &nbsp; &nbsp; [Model: SEALDocList](#markdown-header-model-seal_doc_list) (type `/blck/sp_seal_doc_list`)

# API: DefaultApi

All URIs are relative to *https://s3alsystems.sharepoint.com/sites/job*

<a name="markdown-header-op-DefaultApi-get_doc_attr"></a>

## operation: **get_doc_attr**
Get attribute of document


### Example
```abap
*** method DefaultApi->get_doc_attr example
*** Get attribute of document

  constants:
    gcc_basepath type string value 'https://s3alsystems.sharepoint.com/sites/job'.
    
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


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method get_doc_attr via HTTP GET
*** i_title: Title of the document container
*** i_doc_id: Id of document
*** i_attr: Name of attribute to change
*** i_accept: an Accept header
    /blck/sp_cl_DefaultApi=>get_doc_attr(
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


<a name="markdown-header-op-DefaultApi-get_doc_data"></a>

## operation: **get_doc_data**
Retrieve data of document


### Example
```abap
*** method DefaultApi->get_doc_data example
*** Retrieve data of document

  constants:
    gcc_basepath type string value 'https://s3alsystems.sharepoint.com/sites/job'.
    
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


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method get_doc_data via HTTP GET
*** i_title: Title of the document container
*** i_doc_id: Id of document
    /blck/sp_cl_DefaultApi=>get_doc_data(
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


<a name="markdown-header-op-DefaultApi-get_docs"></a>

## operation: **get_docs**
Retrieve list of documents matching criteria


### Example
```abap
*** method DefaultApi->get_docs example
*** Retrieve list of documents matching criteria

  constants:
    gcc_basepath type string value 'https://s3alsystems.sharepoint.com/sites/job'.
    
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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SP_SEAL_DOC_LIST
    data gr_http200 type /BLCK/SP_SEAL_DOC_LIST.
        
*** set data according to requirements of the API call
*   gvs_title = 'ipsum lorem'.
*   gvs_filter = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method get_docs via HTTP GET
*** i_title: Title of the document container
*** i_filter: Filter the list of documents
*** i_accept: an Accept header
    /blck/sp_cl_DefaultApi=>get_docs(
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
*       do something with gr_http200 (type /BLCK/SP_SEAL_DOC_LIST)
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
 200 | **e_code_200** | `/BLCK/SP_SEAL_DOC_LIST` (**[SEALDocList](#markdown-header-model-seal_doc_list)**) | successful operation
 405 | value not returned |  | Invalid input

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


<a name="markdown-header-op-DefaultApi-set_doc_attr"></a>

## operation: **set_doc_attr**
Set properties of document

Pass in a json formatted body


### Example
```abap
*** method DefaultApi->set_doc_attr example
*** Set properties of document

  constants:
    gcc_basepath type string value 'https://s3alsystems.sharepoint.com/sites/job'.
    
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


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method set_doc_attr via HTTP POST
*** i_title: Title of the document container
*** i_doc_id: Id of document
*** i_accept: an Accept header
*** i_content_type: a content type header
*** i_if_match: Default match header
*** i_x_http_method: Default method header
    /blck/sp_cl_DefaultApi=>set_doc_attr(
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
<a name="markdown-header-model-seal_doc"></a> 

# Model: SEALDoc



### Example
```abap
*** model seal_doc example

* create our variables..
    data gr_seal_doc type /blck/sp_seal_doc.
    
* fill model with data as appropriate..
    gr_seal_doc-id = 42. " (type /BLCK/SP_INT)
    gr_seal_doc-title = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-doknr = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-dokar = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-dokvr = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-doktl = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-description0 = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-dir = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-sap_x0020_upload = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_seal_doc-created = l_created. " (type /BLCK/SP_TIMESTAMP)
    gr_seal_doc-author_id = 42. " (type /BLCK/SP_INT)
    gr_seal_doc-modified = l_modified. " (type /BLCK/SP_TIMESTAMP)
    gr_seal_doc-editor_id = 42. " (type /BLCK/SP_INT)
    gr_seal_doc-guid = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_seal_doc(
      exporting
        i_seal_doc = gr_seal_doc ).
    		
    clear gr_seal_doc.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_seal_doc(
      exporting
        i_id = 1
      importing 
        e_200 = gr_seal_doc ).
    		
    write: gr_seal_doc-id. " (type /BLCK/SP_INT)
    write: gr_seal_doc-title. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-doknr. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-dokar. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-dokvr. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-doktl. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-description0. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-dir. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-sap_x0020_upload. " (type /BLCK/SP_STRING)
    write: gr_seal_doc-created. " (type /BLCK/SP_TIMESTAMP)
    write: gr_seal_doc-author_id. " (type /BLCK/SP_INT)
    write: gr_seal_doc-modified. " (type /BLCK/SP_TIMESTAMP)
    write: gr_seal_doc-editor_id. " (type /BLCK/SP_INT)
    write: gr_seal_doc-guid. " (type /BLCK/SP_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | `/BLCK/SP_INT` | 
**title** | `/BLCK/SP_STRING` | 
**doknr** | `/BLCK/SP_STRING` | 
**dokar** | `/BLCK/SP_STRING` | 
**dokvr** | `/BLCK/SP_STRING` | 
**doktl** | `/BLCK/SP_STRING` | 
**description0** | `/BLCK/SP_STRING` | 
**dir** | `/BLCK/SP_STRING` | 
**sap_x0020_upload** | `/BLCK/SP_STRING` | 
**created** | `/BLCK/SP_TIMESTAMP` | 
**author_id** | `/BLCK/SP_INT` | 
**modified** | `/BLCK/SP_TIMESTAMP` | 
**editor_id** | `/BLCK/SP_INT` | 
**guid** | `/BLCK/SP_STRING` | 

* * *
<a name="markdown-header-model-seal_doc_list"></a> 

# Model: SEALDocList



### Example
```abap
*** model seal_doc_list example

* create our variables..
    data gr_seal_doc_list type /blck/sp_seal_doc_list.
    
* fill model with data as appropriate..
    gr_seal_doc_list-value = l_value. " (type /BLCK/SP_SEAL_DOC_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_seal_doc_list(
      exporting
        i_seal_doc_list = gr_seal_doc_list ).
    		
    clear gr_seal_doc_list.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_seal_doc_list(
      exporting
        i_id = 1
      importing 
        e_200 = gr_seal_doc_list ).
    		
    write: gr_seal_doc_list-value. " (type /BLCK/SP_SEAL_DOC_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**value** | `/BLCK/SP_SEAL_DOC_TT` (**[array of SEALDoc](#markdown-header-model-seal_doc)**) | 

