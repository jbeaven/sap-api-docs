# API: DefaultApi

All URIs are relative to *https://s3alsystems.sharepoint.com/sites/job*

## operation: **get_doc_attr**
Get attribute of document


### Example
```abap
*** method DefaultApi->get_doc_attr example
*** Get attribute of document

  constants:
    gcc_basepath type string value 'https://s3alsystems.sharepoint.com/sites/job'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
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
*   when the the result of the call is HTTP200 we expect type /BLCK/SP_DOC_ATTR_VALUE
    data gr_http200 type /BLCK/SP_DOC_ATTR_VALUE.
        
*** set data according to requirements of the API call
*   gvs_title = 'ipsum lorem'.
*   gvi_doc_id = 42.
*   gvs_attr = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_DOC_ATTR_VALUE)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_title** | /BLCK/SP_STRING | Title of the document container 
 **i_doc_id** | /BLCK/SP_INT | Id of document 
 **i_attr** | /BLCK/SP_STRING | Name of attribute to change 
 **i_accept** | /BLCK/SP_STRING | an Accept header [default "application/json"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/SP_DOC_ATTR_VALUE (**[DocAttrValue](#markdown-header-model-)**) | successful operation
 405 | value not returned |  | Invalid input

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_doc_data**
Retrieve data of document


### Example
```abap
*** method DefaultApi->get_doc_data example
*** Retrieve data of document

  constants:
    gcc_basepath type string value 'https://s3alsystems.sharepoint.com/sites/job'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/sp_int,
    gvs_msg  type /blck/sp_string.
    
*** create variables for input and output as needed
*   for parameter i_title:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_title type /BLCK/SP_STRING.

*   for parameter i_doc_id:
*   a simple ABAP primitive of type /BLCK/SP_INT
    data gvi_doc_id type /BLCK/SP_INT.
*   when the the result of the call is HTTP200 we expect type /BLCK/SP_BINARY
    data gr_http200 type /BLCK/SP_BINARY.
        
*** set data according to requirements of the API call
*   gvs_title = 'ipsum lorem'.
*   gvi_doc_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_BINARY)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_title** | /BLCK/SP_STRING | Title of the document container 
 **i_doc_id** | /BLCK/SP_INT | Id of document 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/SP_BINARY | successful operation
 405 | value not returned |  | Invalid input

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octet-stream


## operation: **get_docs**
Retrieve list of documents matching criteria


### Example
```abap
*** method DefaultApi->get_docs example
*** Retrieve list of documents matching criteria

  constants:
    gcc_basepath type string value 'https://s3alsystems.sharepoint.com/sites/job'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
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
*   when the the result of the call is HTTP200 we expect type /BLCK/SP_SEAL_DOC_LIST
    data gr_http200 type /BLCK/SP_SEAL_DOC_LIST.
        
*** set data according to requirements of the API call
*   gvs_title = 'ipsum lorem'.
*   gvs_filter = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/SP_SEAL_DOC_LIST)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_title** | /BLCK/SP_STRING | Title of the document container 
 **i_filter** | /BLCK/SP_STRING | Filter the list of documents [optional]
 **i_accept** | /BLCK/SP_STRING | an Accept header [default "application/json"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/SP_SEAL_DOC_LIST (**[SEALDocList](#markdown-header-model-)**) | successful operation
 405 | value not returned |  | Invalid input

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


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
    gcl_auth type ref to /blck/api_cl_auth,
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


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/sp_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
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
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/SP_STRING |  
 **i_title** | /BLCK/SP_STRING | Title of the document container 
 **i_doc_id** | /BLCK/SP_INT | Id of document 
 **i_accept** | /BLCK/SP_STRING | an Accept header [default "application/json"]
 **i_content_type** | /BLCK/SP_STRING | a content type header [default "application/json"]
 **i_if_match** | /BLCK/SP_STRING | Default match header [default "*"]
 **i_x_http_method** | /BLCK/SP_STRING | Default method header [default "PATCH"]

### Return types


### HTTP request headers

 - **Content-Type**: text/plain
 - **Accept**: Not defined


* * *
<a name="markdown-header-model-doc_attr_value"></a> 

# Model: doc_attr_value



### Example
```abap
*** model doc_attr_value example

* create our variables..
    data gcl_doc_attr_value type ref to /blck/mdl_cl_doc_attr_value.
    
* instantiate model and call the setters to set values..
    gcl_doc_attr_value = /blck/mdl_cl_doc_attr_value=>create( ).
    gcl_doc_attr_value->set_value( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_doc_attr_value(
    	exporting
    		i_doc_attr_value = gcl_doc_attr_value ).
    		
    clear gcl_doc_attr_value.
    
* fetch new instance from example API method
    gcl_doc_attr_value = gcl_exampleapi->get_doc_attr_value(
    	exporting
    		i_id = 1 ).
    		
    l_value = gcl_doc_attr_value->get_value( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**value** | string |  | [default to null]

* * *
<a name="markdown-header-model-seal_doc"></a> 

# Model: seal_doc



### Example
```abap
*** model seal_doc example

* create our variables..
    data gcl_seal_doc type ref to /blck/mdl_cl_seal_doc.
    
* instantiate model and call the setters to set values..
    gcl_seal_doc = /blck/mdl_cl_seal_doc=>create( ).
    gcl_seal_doc->set_id( 42 ). " (type i)
    gcl_seal_doc->set_title( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_doknr( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_dokar( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_dokvr( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_doktl( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_description0( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_dir( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_sap_x0020_upload( 'ipsum lorem' ). " (type string)
    gcl_seal_doc->set_created( l_created ). " (type timestamp)
    gcl_seal_doc->set_author_id( 42 ). " (type i)
    gcl_seal_doc->set_modified( l_modified ). " (type timestamp)
    gcl_seal_doc->set_editor_id( 42 ). " (type i)
    gcl_seal_doc->set_guid( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_seal_doc(
    	exporting
    		i_seal_doc = gcl_seal_doc ).
    		
    clear gcl_seal_doc.
    
* fetch new instance from example API method
    gcl_seal_doc = gcl_exampleapi->get_seal_doc(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_seal_doc->get_id( ). " (type i)
    l_title = gcl_seal_doc->get_title( ). " (type string)
    l_doknr = gcl_seal_doc->get_doknr( ). " (type string)
    l_dokar = gcl_seal_doc->get_dokar( ). " (type string)
    l_dokvr = gcl_seal_doc->get_dokvr( ). " (type string)
    l_doktl = gcl_seal_doc->get_doktl( ). " (type string)
    l_description0 = gcl_seal_doc->get_description0( ). " (type string)
    l_dir = gcl_seal_doc->get_dir( ). " (type string)
    l_sap_x0020_upload = gcl_seal_doc->get_sap_x0020_upload( ). " (type string)
    l_created = gcl_seal_doc->get_created( ). " (type timestamp)
    l_author_id = gcl_seal_doc->get_author_id( ). " (type i)
    l_modified = gcl_seal_doc->get_modified( ). " (type timestamp)
    l_editor_id = gcl_seal_doc->get_editor_id( ). " (type i)
    l_guid = gcl_seal_doc->get_guid( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**title** | string |  | [optional] [default to null]
**doknr** | string |  | [optional] [default to null]
**dokar** | string |  | [optional] [default to null]
**dokvr** | string |  | [optional] [default to null]
**doktl** | string |  | [optional] [default to null]
**description0** | string |  | [optional] [default to null]
**dir** | string |  | [optional] [default to null]
**sap_x0020_upload** | string |  | [optional] [default to null]
**created** | timestamp |  | [optional] [default to null]
**author_id** | i |  | [optional] [default to null]
**modified** | timestamp |  | [optional] [default to null]
**editor_id** | i |  | [optional] [default to null]
**guid** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-seal_doc_list"></a> 

# Model: seal_doc_list



### Example
```abap
*** model seal_doc_list example

* create our variables..
    data gcl_seal_doc_list type ref to /blck/mdl_cl_seal_doc_list.
    
* instantiate model and call the setters to set values..
    gcl_seal_doc_list = /blck/mdl_cl_seal_doc_list=>create( ).
    gcl_seal_doc_list->set_value( l_value ). " (type /BLCK/SP_seal_doc_tt)
    
* pass to example API method
    gcl_exampleapi->update_seal_doc_list(
    	exporting
    		i_seal_doc_list = gcl_seal_doc_list ).
    		
    clear gcl_seal_doc_list.
    
* fetch new instance from example API method
    gcl_seal_doc_list = gcl_exampleapi->get_seal_doc_list(
    	exporting
    		i_id = 1 ).
    		
    l_value = gcl_seal_doc_list->get_value( ). " (type /BLCK/SP_seal_doc_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**value** | /BLCK/SP_seal_doc_tt (**[array of seal_doc](#markdown-header-model-seal_doc)**) |  | [default to null]

