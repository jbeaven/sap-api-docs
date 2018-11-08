# API: InfoApi

All URIs are relative to *https://demo.plossys-p5.com/v2*

## operation: **jobs_aggregate_put**
Create information aggregate of multiple print jobs

Aggregates count the number of objects matching a given query and aggregate results by values of given properties. Queries to this route must contain a json object describing the desired aggregate. The query will be processed and an aggregate json object returned. 


### Example
```abap
*** method InfoApi->jobs_aggregate_put example
*** Create information aggregate of multiple print jobs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the the result of the call is HTTP400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_InfoApi=>jobs_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_400 = gr_http400
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_AGGREGATERESPO)
      when 400.
*       do something with gr_http400 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[aggregatequery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-)**) | OK, an aggregate json object is returned
 400 | **e_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Missing required paramenter
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobs_count_get**
Count print jobs, filtered by OData query

This route provides access to the number of print jobs known in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method InfoApi->jobs_count_get example
*** Count print jobs, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_InfoApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing jobs to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_get**
List and search jobs

A GET query to this path provides access to the list of print jobs in PLOSSYS P5. Use OData queries to shape your query, and keep in mind that there may be billions of print jobs in the system. We mean it. 


### Example
```abap
*** method InfoApi->jobs_get example
*** List and search jobs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_get via HTTP GET
*** i_filter: OData query for searching jobs, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_InfoApi=>jobs_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching jobs, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB_TT (**[array](#markdown-header-model-)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_get**
Retrieve information on a specific print job

A GET query to this route returns a json object containing status information and links to sub-ressources (if any). 


### Example
```abap
*** method InfoApi->jobs_job_id_get example
*** Retrieve information on a specific print job

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_get via HTTP GET
*** i_job_id: jobID of the printjob to query
    /blck/p5_cl_InfoApi=>jobs_job_id_get(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | jobID of the printjob to query 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-)**) | OK, a json object is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_metadata_get**
Get PrintJob data model description

Returns a JSON object describing the PrintJob object model 


### Example
```abap
*** method InfoApi->jobs_metadata_get example
*** Get PrintJob data model description

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_metadata_get via HTTP GET
    /blck/p5_cl_InfoApi=>jobs_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_METADATA)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-)**) | Query OK, metadata document is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_aggregate_put**
Create information aggregate of multiple printers

Aggregates count the number of objects matching a given query and aggregate results by values of given properties. Queries agains this route must contain a json object describing the desired aggregate. The query will be processed and an aggregate json object returned. 


### Example
```abap
*** method InfoApi->printers_aggregate_put example
*** Create information aggregate of multiple printers

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the the result of the call is HTTP400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_InfoApi=>printers_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_400 = gr_http400
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_AGGREGATERESPO)
      when 400.
*       do something with gr_http400 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[aggregatequery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-)**) | OK, an aggregate json object is returned
 400 | **e_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Missing required paramenter
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **printers_count_get**
Count available printes, filtered by OData query

This route provides access to the number of printers registered in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method InfoApi->printers_count_get example
*** Count available printes, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_InfoApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing printers to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_get**
GetPrinter List

Retrieve a list of all known printers in PLOSSYS P5. A plain query to the endpoint will return a full list (keep in mind that this list may be *very* long). Use OData query parameters to search, filter and limit the list. A subset of OData query functions is supported, see PLOSSYS P5 documentation for details. 


### Example
```abap
*** method InfoApi->printers_get example
*** GetPrinter List

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_get via HTTP GET
*** i_filter: OData query for searching printers, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_InfoApi=>printers_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching printers, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER_TT (**[array](#markdown-header-model-)**) | Query OK; an array of printer objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_metadata_get**
Get Printer data model description

Returns a JSON object describing the Printer object model 


### Example
```abap
*** method InfoApi->printers_metadata_get example
*** Get Printer data model description

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_metadata_get via HTTP GET
    /blck/p5_cl_InfoApi=>printers_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_METADATA)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-)**) | Query OK, metadata document is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_printer_name_get**
Retrieve configuration of a given printer

Retrieves printer configuration of the printer with the given printerName and returns it as JSON object. 


### Example
```abap
*** method InfoApi->printers_printer_name_get example
*** Retrieve configuration of a given printer

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_get via HTTP GET
*** i_printer_name: Name (not ID!) of the printer
    /blck/p5_cl_InfoApi=>printers_printer_name_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name (not ID!) of the printer 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-)**) | Printer configuration
 404 | **e_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Printer not found
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_printer_name_logs_get**
Access to printer logs

Retrieve log entries for the given printer. 


### Example
```abap
*** method InfoApi->printers_printer_name_logs_get example
*** Access to printer logs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_InfoApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_404 = gr_http404
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_LOGS)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name of the printer to get logs for 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-)**) | OK, log entries are returned
 404 | **e_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | No log entries found
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternamestatusget**
Get Printer Status

Returns a PrinterStatus object describing the current status of the printer. 


### Example
```abap
*** method InfoApi->printersprinternamestatusget example
*** Get Printer Status

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER_STATUS
    data gr_http200 type /BLCK/P5_PRINTER_STATUS.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternamestatusget via HTTP GET
*** i_printer_name: Name (not ID) of the printer to query
    /blck/p5_cl_InfoApi=>printersprinternamestatusget(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_STATUS)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name (not ID) of the printer to query 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER_STATUS (**[PrinterStatus](#markdown-header-model-)**) | Query OK, status is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: JobsApi

All URIs are relative to *https://demo.plossys-p5.com/v2*

## operation: **jobs_aggregate_put**
Create information aggregate of multiple print jobs

Aggregates count the number of objects matching a given query and aggregate results by values of given properties. Queries to this route must contain a json object describing the desired aggregate. The query will be processed and an aggregate json object returned. 


### Example
```abap
*** method JobsApi->jobs_aggregate_put example
*** Create information aggregate of multiple print jobs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the the result of the call is HTTP400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_JobsApi=>jobs_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_400 = gr_http400
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_AGGREGATERESPO)
      when 400.
*       do something with gr_http400 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[aggregatequery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-)**) | OK, an aggregate json object is returned
 400 | **e_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Missing required paramenter
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobs_count_get**
Count print jobs, filtered by OData query

This route provides access to the number of print jobs known in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method JobsApi->jobs_count_get example
*** Count print jobs, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_JobsApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing jobs to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_get**
List and search jobs

A GET query to this path provides access to the list of print jobs in PLOSSYS P5. Use OData queries to shape your query, and keep in mind that there may be billions of print jobs in the system. We mean it. 


### Example
```abap
*** method JobsApi->jobs_get example
*** List and search jobs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_get via HTTP GET
*** i_filter: OData query for searching jobs, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_JobsApi=>jobs_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching jobs, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB_TT (**[array](#markdown-header-model-)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_delete**
Deletes a print job

A DELETE query to a job instance path stops and deletes the job. 


### Example
```abap
*** method JobsApi->jobs_job_id_delete example
*** Deletes a print job

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_delete via HTTP DELETE
*** i_job_id: jobID of the printjob to delete
    /blck/p5_cl_JobsApi=>jobs_job_id_delete(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_412 = gr_http412
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | jobID of the printjob to delete 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-)**) | OK, a json object is returned
 412 | **e_412** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Wrong Printer Status.
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_get**
Retrieve information on a specific print job

A GET query to this route returns a json object containing status information and links to sub-ressources (if any). 


### Example
```abap
*** method JobsApi->jobs_job_id_get example
*** Retrieve information on a specific print job

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_get via HTTP GET
*** i_job_id: jobID of the printjob to query
    /blck/p5_cl_JobsApi=>jobs_job_id_get(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | jobID of the printjob to query 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-)**) | OK, a json object is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_move_put**
Resume a paused print job.

A print job which has been suspended using the /jobs/{jobID}/pause function can be re-activated by a PUT query to this ressource. 


### Example
```abap
*** method JobsApi->jobs_job_id_move_put example
*** Resume a paused print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_JOB_TARGET
    data gm_body type /BLCK/P5_JOB_TARGET.

*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-target_printer = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-target_server = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_move_put via HTTP PUT
*** i_body: JSON object describing where to move the job
*** i_job_id: ID of the print job to move
    /blck/p5_cl_JobsApi=>jobs_job_id_move_put(
      exporting
        i_body = gm_body
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_JOB_TARGET (**[job_target](#markdown-header-model-job_target)**) | JSON object describing where to move the job 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to move 

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobs_job_id_pause_put**
Pause a print job.

Print job processing can be paused by a PUT query against this functional ressource. 


### Example
```abap
*** method JobsApi->jobs_job_id_pause_put example
*** Pause a print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_pause_put via HTTP PUT
*** i_job_id: ID of the print job to suspend
    /blck/p5_cl_JobsApi=>jobs_job_id_pause_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to suspend 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_repeat_put**
Repeat a print job.

A print job which has been printed before or failed can be repeated by a PUT query to this path. 


### Example
```abap
*** method JobsApi->jobs_job_id_repeat_put example
*** Repeat a print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_repeat_put via HTTP PUT
*** i_job_id: ID of the print job to repeat
    /blck/p5_cl_JobsApi=>jobs_job_id_repeat_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to repeat 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_resume_put**
Resume a paused print job.

A print job which has been suspended using the /jobs/{jobID}/pause function can be re-activated by a PUT query to this ressource. 


### Example
```abap
*** method JobsApi->jobs_job_id_resume_put example
*** Resume a paused print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_resume_put via HTTP PUT
*** i_job_id: ID of the print job to reactivate
    /blck/p5_cl_JobsApi=>jobs_job_id_resume_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to reactivate 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_metadata_get**
Get PrintJob data model description

Returns a JSON object describing the PrintJob object model 


### Example
```abap
*** method JobsApi->jobs_metadata_get example
*** Get PrintJob data model description

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_metadata_get via HTTP GET
    /blck/p5_cl_JobsApi=>jobs_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_METADATA)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-)**) | Query OK, metadata document is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: ManagementApi

All URIs are relative to *https://demo.plossys-p5.com/v2*

## operation: **jobs_job_id_delete**
Deletes a print job

A DELETE query to a job instance path stops and deletes the job. 


### Example
```abap
*** method ManagementApi->jobs_job_id_delete example
*** Deletes a print job

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_delete via HTTP DELETE
*** i_job_id: jobID of the printjob to delete
    /blck/p5_cl_ManagementApi=>jobs_job_id_delete(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_412 = gr_http412
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | jobID of the printjob to delete 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-)**) | OK, a json object is returned
 412 | **e_412** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Wrong Printer Status.
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_move_put**
Resume a paused print job.

A print job which has been suspended using the /jobs/{jobID}/pause function can be re-activated by a PUT query to this ressource. 


### Example
```abap
*** method ManagementApi->jobs_job_id_move_put example
*** Resume a paused print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_JOB_TARGET
    data gm_body type /BLCK/P5_JOB_TARGET.

*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-target_printer = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-target_server = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_move_put via HTTP PUT
*** i_body: JSON object describing where to move the job
*** i_job_id: ID of the print job to move
    /blck/p5_cl_ManagementApi=>jobs_job_id_move_put(
      exporting
        i_body = gm_body
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_JOB_TARGET (**[job_target](#markdown-header-model-job_target)**) | JSON object describing where to move the job 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to move 

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobs_job_id_pause_put**
Pause a print job.

Print job processing can be paused by a PUT query against this functional ressource. 


### Example
```abap
*** method ManagementApi->jobs_job_id_pause_put example
*** Pause a print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_pause_put via HTTP PUT
*** i_job_id: ID of the print job to suspend
    /blck/p5_cl_ManagementApi=>jobs_job_id_pause_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to suspend 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_repeat_put**
Repeat a print job.

A print job which has been printed before or failed can be repeated by a PUT query to this path. 


### Example
```abap
*** method ManagementApi->jobs_job_id_repeat_put example
*** Repeat a print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_repeat_put via HTTP PUT
*** i_job_id: ID of the print job to repeat
    /blck/p5_cl_ManagementApi=>jobs_job_id_repeat_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to repeat 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_resume_put**
Resume a paused print job.

A print job which has been suspended using the /jobs/{jobID}/pause function can be re-activated by a PUT query to this ressource. 


### Example
```abap
*** method ManagementApi->jobs_job_id_resume_put example
*** Resume a paused print job.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_resume_put via HTTP PUT
*** i_job_id: ID of the print job to reactivate
    /blck/p5_cl_ManagementApi=>jobs_job_id_resume_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/P5_STRING | ID of the print job to reactivate 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_post**
Register a new printer

Adds a new printer to the list of managed printers in PLOSSYS P5. The new printer needs a name (unique) and a connection string (arbitrary). An internal ID is generated automatically. 


### Example
```abap
*** method ManagementApi->printers_post example
*** Register a new printer

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_PRINTER
    data gr_http500 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_post via HTTP POST
*** i_body: A  JSON  object  describing the new printer. The 'printer' property needs to
*** contain  a  unique  name for the new printer (if the name is already in use,
*** the  POST  request  will  fail  (HTTP 409). The 'connection' parameter is an
*** arbitrary  string  (e.g. a URL) used to connect from PLOSSYS to the printer.
*** Example   {         \"printer\":   \"newPrinterName\",       \"connection\":
*** \"socket://HostOrIp:9100\" }
    /blck/p5_cl_ManagementApi=>printers_post(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_PRINTER)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[printer](#markdown-header-model-printer)**) | A JSON object describing the new printer. The &#x27;printer&#x27; property needs to contain a unique name for the new printer (if the name is already in use, the POST request will fail (HTTP 409). The &#x27;connection&#x27; parameter is an arbitrary string (e.g. a URL) used to connect from PLOSSYS to the printer. Example {   \&quot;printer\&quot;: \&quot;newPrinterName\&quot;,   \&quot;connection\&quot;: \&quot;socket://HostOrIp:9100\&quot; }  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-)**) | OK. The printer was created, details of the new printer are returned
 500 | **e_500** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-)**) | Error, e.g. in printer already exists
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **printers_printer_name_delete**
Delete a printer from the system

Deletes the printer with the given name; If the printer is found and deletion is possible, the printer is removed  from the list of managed printers. The ID will not be re-used. 


### Example
```abap
*** method ManagementApi->printers_printer_name_delete example
*** Delete a printer from the system

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_PRINTER
    data gr_http412 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_delete via HTTP DELETE
*** i_printer_name: name (not ID!) of the printer to delete
    /blck/p5_cl_ManagementApi=>printers_printer_name_delete(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 412.
*       do something with gr_http412 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to delete 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_put**
Modify/Reconfigure a printer

Modifies a printer, replacing the current configuration with the one given in the request body. 


### Example
```abap
*** method ManagementApi->printers_put example
*** Modify/Reconfigure a printer

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_put via HTTP PUT
*** i_body: JSON object containing updated printer object
    /blck/p5_cl_ManagementApi=>printers_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[printer](#markdown-header-model-printer)**) | JSON object containing updated printer object 

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **printersprinternamecreatetestj**
Creates a test page and sends it to the printer.

A predefined test sheet is generated and inserted into the printer queue. 


### Example
```abap
*** method ManagementApi->printersprinternamecreatetestj example
*** Creates a test page and sends it to the printer.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternamecreatetestj via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to test
    /blck/p5_cl_ManagementApi=>printersprinternamecreatetestj(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to test 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternamepauseput**
Pause a printer.

A printers operation can be paused by a PUT query against this functional ressource. 


### Example
```abap
*** method ManagementApi->printersprinternamepauseput example
*** Pause a printer.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternamepauseput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to pause
    /blck/p5_cl_ManagementApi=>printersprinternamepauseput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to pause 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternameredirectput**
Redirect a printer to another.

A printer can be redirected so that incoming print jobs for that printer are forwarded to another printer for output, e.g. if a printer is out of order. 


### Example
```abap
*** method ManagementApi->printersprinternameredirectput example
*** Redirect a printer to another.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternameredirectput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to redirect
    /blck/p5_cl_ManagementApi=>printersprinternameredirectput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to redirect 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternameresumeput**
Resume a paused printer.

A printer which has been suspended using the /printers/{printerName}/pause function can be re-activated by a PUT query to this ressource. 


### Example
```abap
*** method ManagementApi->printersprinternameresumeput example
*** Resume a paused printer.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternameresumeput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to reactivate
    /blck/p5_cl_ManagementApi=>printersprinternameresumeput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to reactivate 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: ODataApi

All URIs are relative to *https://demo.plossys-p5.com/v2*

## operation: **jobs_count_get**
Count print jobs, filtered by OData query

This route provides access to the number of print jobs known in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method ODataApi->jobs_count_get example
*** Count print jobs, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_ODataApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing jobs to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_get**
List and search jobs

A GET query to this path provides access to the list of print jobs in PLOSSYS P5. Use OData queries to shape your query, and keep in mind that there may be billions of print jobs in the system. We mean it. 


### Example
```abap
*** method ODataApi->jobs_get example
*** List and search jobs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_get via HTTP GET
*** i_filter: OData query for searching jobs, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_ODataApi=>jobs_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching jobs, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB_TT (**[array](#markdown-header-model-)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_count_get**
Count available printes, filtered by OData query

This route provides access to the number of printers registered in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method ODataApi->printers_count_get example
*** Count available printes, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_ODataApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing printers to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_get**
GetPrinter List

Retrieve a list of all known printers in PLOSSYS P5. A plain query to the endpoint will return a full list (keep in mind that this list may be *very* long). Use OData query parameters to search, filter and limit the list. A subset of OData query functions is supported, see PLOSSYS P5 documentation for details. 


### Example
```abap
*** method ODataApi->printers_get example
*** GetPrinter List

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_get via HTTP GET
*** i_filter: OData query for searching printers, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_ODataApi=>printers_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching printers, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER_TT (**[array](#markdown-header-model-)**) | Query OK; an array of printer objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_printer_name_logs_get**
Access to printer logs

Retrieve log entries for the given printer. 


### Example
```abap
*** method ODataApi->printers_printer_name_logs_get example
*** Access to printer logs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_ODataApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_404 = gr_http404
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_LOGS)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name of the printer to get logs for 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-)**) | OK, log entries are returned
 404 | **e_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | No log entries found
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: PrinterApi

All URIs are relative to *https://demo.plossys-p5.com/v2*

## operation: **printers_aggregate_put**
Create information aggregate of multiple printers

Aggregates count the number of objects matching a given query and aggregate results by values of given properties. Queries agains this route must contain a json object describing the desired aggregate. The query will be processed and an aggregate json object returned. 


### Example
```abap
*** method PrinterApi->printers_aggregate_put example
*** Create information aggregate of multiple printers

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the the result of the call is HTTP400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_PrinterApi=>printers_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_400 = gr_http400
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_AGGREGATERESPO)
      when 400.
*       do something with gr_http400 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[aggregatequery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-)**) | OK, an aggregate json object is returned
 400 | **e_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Missing required paramenter
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **printers_count_get**
Count available printes, filtered by OData query

This route provides access to the number of printers registered in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method PrinterApi->printers_count_get example
*** Count available printes, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_PrinterApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing printers to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_get**
GetPrinter List

Retrieve a list of all known printers in PLOSSYS P5. A plain query to the endpoint will return a full list (keep in mind that this list may be *very* long). Use OData query parameters to search, filter and limit the list. A subset of OData query functions is supported, see PLOSSYS P5 documentation for details. 


### Example
```abap
*** method PrinterApi->printers_get example
*** GetPrinter List

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_get via HTTP GET
*** i_filter: OData query for searching printers, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_PrinterApi=>printers_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching printers, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER_TT (**[array](#markdown-header-model-)**) | Query OK; an array of printer objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_metadata_get**
Get Printer data model description

Returns a JSON object describing the Printer object model 


### Example
```abap
*** method PrinterApi->printers_metadata_get example
*** Get Printer data model description

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_metadata_get via HTTP GET
    /blck/p5_cl_PrinterApi=>printers_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_METADATA)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-)**) | Query OK, metadata document is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_post**
Register a new printer

Adds a new printer to the list of managed printers in PLOSSYS P5. The new printer needs a name (unique) and a connection string (arbitrary). An internal ID is generated automatically. 


### Example
```abap
*** method PrinterApi->printers_post example
*** Register a new printer

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_PRINTER
    data gr_http500 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_post via HTTP POST
*** i_body: A  JSON  object  describing the new printer. The 'printer' property needs to
*** contain  a  unique  name for the new printer (if the name is already in use,
*** the  POST  request  will  fail  (HTTP 409). The 'connection' parameter is an
*** arbitrary  string  (e.g. a URL) used to connect from PLOSSYS to the printer.
*** Example   {         \"printer\":   \"newPrinterName\",       \"connection\":
*** \"socket://HostOrIp:9100\" }
    /blck/p5_cl_PrinterApi=>printers_post(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_PRINTER)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[printer](#markdown-header-model-printer)**) | A JSON object describing the new printer. The &#x27;printer&#x27; property needs to contain a unique name for the new printer (if the name is already in use, the POST request will fail (HTTP 409). The &#x27;connection&#x27; parameter is an arbitrary string (e.g. a URL) used to connect from PLOSSYS to the printer. Example {   \&quot;printer\&quot;: \&quot;newPrinterName\&quot;,   \&quot;connection\&quot;: \&quot;socket://HostOrIp:9100\&quot; }  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-)**) | OK. The printer was created, details of the new printer are returned
 500 | **e_500** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-)**) | Error, e.g. in printer already exists
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **printers_printer_name_delete**
Delete a printer from the system

Deletes the printer with the given name; If the printer is found and deletion is possible, the printer is removed  from the list of managed printers. The ID will not be re-used. 


### Example
```abap
*** method PrinterApi->printers_printer_name_delete example
*** Delete a printer from the system

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_PRINTER
    data gr_http412 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_delete via HTTP DELETE
*** i_printer_name: name (not ID!) of the printer to delete
    /blck/p5_cl_PrinterApi=>printers_printer_name_delete(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 412.
*       do something with gr_http412 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to delete 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_printer_name_get**
Retrieve configuration of a given printer

Retrieves printer configuration of the printer with the given printerName and returns it as JSON object. 


### Example
```abap
*** method PrinterApi->printers_printer_name_get example
*** Retrieve configuration of a given printer

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_get via HTTP GET
*** i_printer_name: Name (not ID!) of the printer
    /blck/p5_cl_PrinterApi=>printers_printer_name_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name (not ID!) of the printer 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-)**) | Printer configuration
 404 | **e_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Printer not found
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_printer_name_logs_get**
Access to printer logs

Retrieve log entries for the given printer. 


### Example
```abap
*** method PrinterApi->printers_printer_name_logs_get example
*** Access to printer logs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_PrinterApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_404 = gr_http404
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_LOGS)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name of the printer to get logs for 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-)**) | OK, log entries are returned
 404 | **e_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | No log entries found
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_put**
Modify/Reconfigure a printer

Modifies a printer, replacing the current configuration with the one given in the request body. 


### Example
```abap
*** method PrinterApi->printers_put example
*** Modify/Reconfigure a printer

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_put via HTTP PUT
*** i_body: JSON object containing updated printer object
    /blck/p5_cl_PrinterApi=>printers_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[printer](#markdown-header-model-printer)**) | JSON object containing updated printer object 

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **printersprinternamecreatetestj**
Creates a test page and sends it to the printer.

A predefined test sheet is generated and inserted into the printer queue. 


### Example
```abap
*** method PrinterApi->printersprinternamecreatetestj example
*** Creates a test page and sends it to the printer.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternamecreatetestj via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to test
    /blck/p5_cl_PrinterApi=>printersprinternamecreatetestj(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to test 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternamepauseput**
Pause a printer.

A printers operation can be paused by a PUT query against this functional ressource. 


### Example
```abap
*** method PrinterApi->printersprinternamepauseput example
*** Pause a printer.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternamepauseput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to pause
    /blck/p5_cl_PrinterApi=>printersprinternamepauseput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to pause 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternameredirectput**
Redirect a printer to another.

A printer can be redirected so that incoming print jobs for that printer are forwarded to another printer for output, e.g. if a printer is out of order. 


### Example
```abap
*** method PrinterApi->printersprinternameredirectput example
*** Redirect a printer to another.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternameredirectput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to redirect
    /blck/p5_cl_PrinterApi=>printersprinternameredirectput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to redirect 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternameresumeput**
Resume a paused printer.

A printer which has been suspended using the /printers/{printerName}/pause function can be re-activated by a PUT query to this ressource. 


### Example
```abap
*** method PrinterApi->printersprinternameresumeput example
*** Resume a paused printer.

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternameresumeput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to reactivate
    /blck/p5_cl_PrinterApi=>printersprinternameresumeput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_404 = gr_http404
        e_412 = gr_http412
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | name (not ID!) of the printer to reactivate 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printersprinternamestatusget**
Get Printer Status

Returns a PrinterStatus object describing the current status of the printer. 


### Example
```abap
*** method PrinterApi->printersprinternamestatusget example
*** Get Printer Status

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER_STATUS
    data gr_http200 type /BLCK/P5_PRINTER_STATUS.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printersprinternamestatusget via HTTP GET
*** i_printer_name: Name (not ID) of the printer to query
    /blck/p5_cl_PrinterApi=>printersprinternamestatusget(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_STATUS)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name (not ID) of the printer to query 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER_STATUS (**[PrinterStatus](#markdown-header-model-)**) | Query OK, status is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: SearchApi

All URIs are relative to *https://demo.plossys-p5.com/v2*

## operation: **jobs_aggregate_put**
Create information aggregate of multiple print jobs

Aggregates count the number of objects matching a given query and aggregate results by values of given properties. Queries to this route must contain a json object describing the desired aggregate. The query will be processed and an aggregate json object returned. 


### Example
```abap
*** method SearchApi->jobs_aggregate_put example
*** Create information aggregate of multiple print jobs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the the result of the call is HTTP400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_SearchApi=>jobs_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_400 = gr_http400
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_AGGREGATERESPO)
      when 400.
*       do something with gr_http400 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[aggregatequery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-)**) | OK, an aggregate json object is returned
 400 | **e_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Missing required paramenter
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobs_count_get**
Count print jobs, filtered by OData query

This route provides access to the number of print jobs known in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method SearchApi->jobs_count_get example
*** Count print jobs, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_SearchApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing jobs to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_get**
List and search jobs

A GET query to this path provides access to the list of print jobs in PLOSSYS P5. Use OData queries to shape your query, and keep in mind that there may be billions of print jobs in the system. We mean it. 


### Example
```abap
*** method SearchApi->jobs_get example
*** List and search jobs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_get via HTTP GET
*** i_filter: OData query for searching jobs, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_SearchApi=>jobs_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINT_JOB_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching jobs, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINT_JOB_TT (**[array](#markdown-header-model-)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_aggregate_put**
Create information aggregate of multiple printers

Aggregates count the number of objects matching a given query and aggregate results by values of given properties. Queries agains this route must contain a json object describing the desired aggregate. The query will be processed and an aggregate json object returned. 


### Example
```abap
*** method SearchApi->printers_aggregate_put example
*** Create information aggregate of multiple printers

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the the result of the call is HTTP400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_SearchApi=>printers_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_400 = gr_http400
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_AGGREGATERESPO)
      when 400.
*       do something with gr_http400 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[aggregatequery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-)**) | OK, an aggregate json object is returned
 400 | **e_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Missing required paramenter
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **printers_count_get**
Count available printes, filtered by OData query

This route provides access to the number of printers registered in PLOSSYS P5; either the overall number, or the number matching an OData _filter query. The result is returned as json object. 


### Example
```abap
*** method SearchApi->printers_count_get example
*** Count available printes, filtered by OData query

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_SearchApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_COUNT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query string describing printers to count [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-)**) | OK, a number is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_get**
GetPrinter List

Retrieve a list of all known printers in PLOSSYS P5. A plain query to the endpoint will return a full list (keep in mind that this list may be *very* long). Use OData query parameters to search, filter and limit the list. A subset of OData query functions is supported, see PLOSSYS P5 documentation for details. 


### Example
```abap
*** method SearchApi->printers_get example
*** GetPrinter List

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.

*   for parameter i_select:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_select type /BLCK/P5_STRING.

*   for parameter i_skip:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_skip type /BLCK/P5_INT.

*   for parameter i_top:
*   a simple ABAP primitive of type /BLCK/P5_INT
    data gvi_top type /BLCK/P5_INT.

*   for parameter i_orderby:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_orderby type /BLCK/P5_STRING.

*   for parameter i_inlinecount:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_inlinecount type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P5_ERROR
    data gr_http0 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_get via HTTP GET
*** i_filter: OData query for searching printers, see OData 3.0 Spec 
*** i_select: List of result properties, see OData 3.0 Spec 
*** i_skip: Number of results to skip (e.g. for paging), see OData 3.0 Spec 
*** i_top: Maximum number of results (e.g. for paging), see OData 3.0 Spec 
*** i_orderby: Column to use for sorting, see OData 3.0 Spec 
*** i_inlinecount: If  missing  or set to \"none\" the response is the result array.  If set to
*** \"allpages\" the response is an object with results as the result array  and
*** \"totalCount\"  with  the  total  count of entries found for this query, see
*** OData 3.0 Spec
    /blck/p5_cl_SearchApi=>printers_get(
      exporting
        i_filter = gvs_filter
        i_select = gvs_select
        i_skip = gvi_skip
        i_top = gvi_top
        i_orderby = gvs_orderby
        i_inlinecount = gvs_inlinecount
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_filter** | /BLCK/P5_STRING | OData query for searching printers, see OData 3.0 Spec  [optional]
 **i_select** | /BLCK/P5_STRING | List of result properties, see OData 3.0 Spec  [optional]
 **i_skip** | /BLCK/P5_INT | Number of results to skip (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_top** | /BLCK/P5_INT | Maximum number of results (e.g. for paging), see OData 3.0 Spec  [optional]
 **i_orderby** | /BLCK/P5_STRING | Column to use for sorting, see OData 3.0 Spec  [optional]
 **i_inlinecount** | /BLCK/P5_STRING | If missing or set to \&quot;none\&quot; the response is the result array.  If set to \&quot;allpages\&quot; the response is an object with results as the result array  and \&quot;totalCount\&quot; with the total count of entries found for this query, see OData 3.0 Spec  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_PRINTER_TT (**[array](#markdown-header-model-)**) | Query OK; an array of printer objects is returned
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error
 0 | **e_0** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **printers_printer_name_logs_get**
Access to printer logs

Retrieve log entries for the given printer. 


### Example
```abap
*** method SearchApi->printers_printer_name_logs_get example
*** Access to printer logs

  constants:
    gcc_basepath type string value 'https://demo.plossys-p5.com/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the the result of the call is HTTP404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_SearchApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_404 = gr_http404
        e_500 = gr_http500 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_LOGS)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name of the printer to get logs for 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-)**) | OK, log entries are returned
 404 | **e_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | No log entries found
 500 | **e_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-aggregatequery"></a> 

# Model: aggregatequery



### Example
```abap
*** model aggregatequery example
*** A query for an aggregate

* create our variables..
    data gcl_aggregatequery type ref to /blck/mdl_cl_aggregatequery.
    
* instantiate model and call the setters to set values..
    gcl_aggregatequery = /blck/mdl_cl_aggregatequery=>create( ).
    gcl_aggregatequery->set_match( 'ipsum lorem' ). " (type string)
    gcl_aggregatequery->set_aggregates( l_aggregates ). " (type /blck/api_string_tt)
    
* pass to example API method
    gcl_exampleapi->update_aggregatequery(
    	exporting
    		i_aggregatequery = gcl_aggregatequery ).
    		
    clear gcl_aggregatequery.
    
* fetch new instance from example API method
    gcl_aggregatequery = gcl_exampleapi->get_aggregatequery(
    	exporting
    		i_id = 1 ).
    		
    l_match = gcl_aggregatequery->get_match( ). " (type string)
    l_aggregates = gcl_aggregatequery->get_aggregates( ). " (type /blck/api_string_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**match** | string | Query-rules for objects to aggregate | [optional] [default to null]
**aggregates** | /blck/api_string_tt | List of aggregates to generate | [optional] [default to null]

* * *
<a name="markdown-header-model-aggregaterespo"></a> 

# Model: aggregaterespo



### Example
```abap
*** model aggregaterespo example
*** An aggregate generated by PLOSSYS P5

* create our variables..
    data gcl_aggregaterespo type ref to /blck/mdl_cl_aggregaterespo.
    
* instantiate model and call the setters to set values..
    gcl_aggregaterespo = /blck/mdl_cl_aggregaterespo=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_aggregaterespo(
    	exporting
    		i_aggregaterespo = gcl_aggregaterespo ).
    		
    clear gcl_aggregaterespo.
    
* fetch new instance from example API method
    gcl_aggregaterespo = gcl_exampleapi->get_aggregaterespo(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-model-count"></a> 

# Model: count



### Example
```abap
*** model count example
*** Key-Value pair containing a number

* create our variables..
    data gcl_count type ref to /blck/mdl_cl_count.
    
* instantiate model and call the setters to set values..
    gcl_count = /blck/mdl_cl_count=>create( ).
    gcl_count->set_count( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_count(
    	exporting
    		i_count = gcl_count ).
    		
    clear gcl_count.
    
* fetch new instance from example API method
    gcl_count = gcl_exampleapi->get_count(
    	exporting
    		i_id = 1 ).
    		
    l_count = gcl_count->get_count( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**count** | i | Counted number | [optional] [default to null]

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
    gcl_error->set_fields( 'ipsum lorem' ). " (type string)
    
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
    l_fields = gcl_error->get_fields( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | i |  | [optional] [default to null]
**message** | string |  | [optional] [default to null]
**fields** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-job_target"></a> 

# Model: job_target



### Example
```abap
*** model job_target example
*** Server and Printer for handling a job

* create our variables..
    data gcl_job_target type ref to /blck/mdl_cl_job_target.
    
* instantiate model and call the setters to set values..
    gcl_job_target = /blck/mdl_cl_job_target=>create( ).
    gcl_job_target->set_target_printer( 'ipsum lorem' ). " (type string)
    gcl_job_target->set_target_server( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_job_target(
    	exporting
    		i_job_target = gcl_job_target ).
    		
    clear gcl_job_target.
    
* fetch new instance from example API method
    gcl_job_target = gcl_exampleapi->get_job_target(
    	exporting
    		i_id = 1 ).
    		
    l_target_printer = gcl_job_target->get_target_printer( ). " (type string)
    l_target_server = gcl_job_target->get_target_server( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**target_printer** | string | PrinterName of the target printer | [optional] [default to null]
**target_server** | string | Name of the target PLOSSYS P5 server | [optional] [default to null]

* * *
<a name="markdown-header-model-logs"></a> 

# Model: logs



### Example
```abap
*** model logs example
*** List of Log entries for a printer

* create our variables..
    data gcl_logs type ref to /blck/mdl_cl_logs.
    
* instantiate model and call the setters to set values..
    gcl_logs = /blck/mdl_cl_logs=>create( ).
    gcl_logs->set_messages( l_messages ). " (type /blck/api_string_tt)
    
* pass to example API method
    gcl_exampleapi->update_logs(
    	exporting
    		i_logs = gcl_logs ).
    		
    clear gcl_logs.
    
* fetch new instance from example API method
    gcl_logs = gcl_exampleapi->get_logs(
    	exporting
    		i_id = 1 ).
    		
    l_messages = gcl_logs->get_messages( ). " (type /blck/api_string_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**messages** | /blck/api_string_tt | Array of Log entries | [optional] [default to null]

* * *
<a name="markdown-header-model-metadata"></a> 

# Model: metadata



### Example
```abap
*** model metadata example
*** Array of objects describing items in a JSON object used in this API. 

* create our variables..
    data gcl_metadata type ref to /blck/mdl_cl_metadata.
    
* instantiate model and call the setters to set values..
    gcl_metadata = /blck/mdl_cl_metadata=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_metadata(
    	exporting
    		i_metadata = gcl_metadata ).
    		
    clear gcl_metadata.
    
* fetch new instance from example API method
    gcl_metadata = gcl_exampleapi->get_metadata(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-model-print_job"></a> 

# Model: print_job



### Example
```abap
*** model print_job example
*** Status information about a print job

* create our variables..
    data gcl_print_job type ref to /blck/mdl_cl_print_job.
    
* instantiate model and call the setters to set values..
    gcl_print_job = /blck/mdl_cl_print_job=>create( ).
    gcl_print_job->set_id( 'ipsum lorem' ). " (type string)
    gcl_print_job->set_status( 'ipsum lorem' ). " (type string)
    gcl_print_job->set_current( 'ipsum lorem' ). " (type string)
    gcl_print_job->set_orig( 'ipsum lorem' ). " (type string)
    gcl_print_job->set_routing( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_print_job(
    	exporting
    		i_print_job = gcl_print_job ).
    		
    clear gcl_print_job.
    
* fetch new instance from example API method
    gcl_print_job = gcl_exampleapi->get_print_job(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_print_job->get_id( ). " (type string)
    l_status = gcl_print_job->get_status( ). " (type string)
    l_current = gcl_print_job->get_current( ). " (type string)
    l_orig = gcl_print_job->get_orig( ). " (type string)
    l_routing = gcl_print_job->get_routing( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | string | Job identifier | [optional] [default to null]
**status** | string | Current job status | [optional] [default to null]
**current** | string | Information about the job as it is used in PLOSSYS P5 at the present time. | [optional] [default to null]
**orig** | string | Information about the job as it was originally submitted to PLOSSYS P5 | [optional] [default to null]
**routing** | string | Information about the processor route of the job. | [optional] [default to null]

* * *
<a name="markdown-header-model-printer"></a> 

# Model: printer



### Example
```abap
*** model printer example

* create our variables..
    data gcl_printer type ref to /blck/mdl_cl_printer.
    
* instantiate model and call the setters to set values..
    gcl_printer = /blck/mdl_cl_printer=>create( ).
    gcl_printer->set_id( 'ipsum lorem' ). " (type string)
    gcl_printer->set_config( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_printer(
    	exporting
    		i_printer = gcl_printer ).
    		
    clear gcl_printer.
    
* fetch new instance from example API method
    gcl_printer = gcl_exampleapi->get_printer(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_printer->get_id( ). " (type string)
    l_config = gcl_printer->get_config( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | string | Internal ID of the printer, auto-generated by PLOSSYS P5 | [optional] [default to null]
**config** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-printer_status"></a> 

# Model: printer_status



### Example
```abap
*** model printer_status example
*** Ressource representing the current printer status.

* create our variables..
    data gcl_printer_status type ref to /blck/mdl_cl_printer_status.
    
* instantiate model and call the setters to set values..
    gcl_printer_status = /blck/mdl_cl_printer_status=>create( ).
    gcl_printer_status->set_mode( 'ipsum lorem' ). " (type string)
    gcl_printer_status->set_queue_length( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_printer_status(
    	exporting
    		i_printer_status = gcl_printer_status ).
    		
    clear gcl_printer_status.
    
* fetch new instance from example API method
    gcl_printer_status = gcl_exampleapi->get_printer_status(
    	exporting
    		i_id = 1 ).
    		
    l_mode = gcl_printer_status->get_mode( ). " (type string)
    l_queue_length = gcl_printer_status->get_queue_length( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**mode** | string | One of {ready, printing, paused, redirected, error} | [optional] [default to null]
**queue_length** | i |  | [optional] [default to null]

