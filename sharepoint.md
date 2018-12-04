# API: DocumentsApi
## &nbsp; &nbsp; [Operation: get_doc_attr](#markdown-header-op-DocumentsApi-get_doc_attr)
## &nbsp; &nbsp; [Operation: get_doc_data](#markdown-header-op-DocumentsApi-get_doc_data)
## &nbsp; &nbsp; [Operation: get_docs](#markdown-header-op-DocumentsApi-get_docs)
## &nbsp; &nbsp; [Operation: set_doc_attr](#markdown-header-op-DocumentsApi-set_doc_attr)
# API: SearchApi
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
## &nbsp; &nbsp; [Model: Properties2](#markdown-header-model-properties2) (type `/blck/sp_properties2`)
## &nbsp; &nbsp; [Model: Query](#markdown-header-model-query) (type `/blck/sp_query`)

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

<a name="markdown-header-op-SearchApi-query"></a>

## operation: **query**


Query


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
*   for parameter i_selectproperties:
*   a simple ABAP primitive of type /BLCK/SP_STRING
    data gvs_selectproperties type /BLCK/SP_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SP_QUERY
    data gr_http200 type /BLCK/SP_QUERY.
        
*** set data according to requirements of the API call
*   gvs_querytext = 'ipsum lorem'.
*   gvs_selectproperties = 'ipsum lorem'.

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
*** i_querytext: querytext
*** i_selectproperties: selectproperties
    /blck/sp_cl_SearchApi=>query(
      exporting
        i_querytext = gvs_querytext
        i_selectproperties = gvs_selectproperties
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
 **i_querytext** | `/BLCK/SP_STRING` | querytext 
 **i_selectproperties** | `/BLCK/SP_STRING` | selectproperties [optional]

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
<a name="markdown-header-model-properties2"></a> 

# Model: Properties2



### Example
```abap
*** model properties2 example
*** Model for Properties2

* create our variables..
    data gr_properties2 type /blck/sp_properties2.
    
* fill model with data as appropriate..
    gr_properties2-key = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_properties2-value = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    gr_properties2-value_type = 'ipsum lorem'. " (type /BLCK/SP_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_properties2(
      exporting
        i_properties2 = gr_properties2 ).
    		
    clear gr_properties2.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_properties2(
      exporting
        i_id = 1
      importing 
        e_200 = gr_properties2 ).
    		
    write: gr_properties2-key. " (type /BLCK/SP_STRING)
    write: gr_properties2-value. " (type /BLCK/SP_STRING)
    write: gr_properties2-value_type. " (type /BLCK/SP_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**key** | `/BLCK/SP_STRING` | 
**value** | `/BLCK/SP_STRING` | 
**value_type** | `/BLCK/SP_STRING` | 

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
    gr_query-properties = l_properties. " (type /BLCK/SP_PROPERTIES2_TT)
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
    write: gr_query-properties. " (type /BLCK/SP_PROPERTIES2_TT)
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
**properties** | `/BLCK/SP_PROPERTIES2_TT` (**[array of Properties2](#markdown-header-model-properties2)**) | 
**secondary_query_results** | `/BLCK/SP_STRING_TT` | 
**spelling_suggestion** | `/BLCK/SP_STRING` | 
**triggered_rules** | `/BLCK/SP_STRING_TT` | 

