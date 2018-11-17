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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the result of the call is HTTP Code: 400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_InfoApi=>jobs_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_400 = gr_http400
        e_code_500 = gr_http500 ).

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
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[AggregateQuery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-aggregaterespo)**) | OK, an aggregate json object is returned
 400 | **e_code_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Missing required paramenter
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_InfoApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB_TT (**[array of PrintJob](#markdown-header-model-print_job)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_get via HTTP GET
*** i_job_id: jobID of the printjob to query
    /blck/p5_cl_InfoApi=>jobs_job_id_get(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-print_job)**) | OK, a json object is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_metadata_get via HTTP GET
    /blck/p5_cl_InfoApi=>jobs_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-metadata)**) | Query OK, metadata document is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the result of the call is HTTP Code: 400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_InfoApi=>printers_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_400 = gr_http400
        e_code_500 = gr_http500 ).

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
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[AggregateQuery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-aggregaterespo)**) | OK, an aggregate json object is returned
 400 | **e_code_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Missing required paramenter
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_InfoApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
 200 | **e_code_200** | /BLCK/P5_PRINTER_TT (**[array of Printer](#markdown-header-model-printer)**) | Query OK; an array of printer objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_metadata_get via HTTP GET
    /blck/p5_cl_InfoApi=>printers_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-metadata)**) | Query OK, metadata document is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_get via HTTP GET
*** i_printer_name: Name (not ID!) of the printer
    /blck/p5_cl_InfoApi=>printers_printer_name_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name (not ID!) of the printer 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | Printer configuration
 404 | **e_code_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Printer not found
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_InfoApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_404 = gr_http404
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-logs)**) | OK, log entries are returned
 404 | **e_code_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | No log entries found
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER_STATUS
    data gr_http200 type /BLCK/P5_PRINTER_STATUS.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_InfoApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternamestatusget via HTTP GET
*** i_printer_name: Name (not ID) of the printer to query
    /blck/p5_cl_InfoApi=>printersprinternamestatusget(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINTER_STATUS (**[PrinterStatus](#markdown-header-model-printer_status)**) | Query OK, status is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the result of the call is HTTP Code: 400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_JobsApi=>jobs_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_400 = gr_http400
        e_code_500 = gr_http500 ).

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
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[AggregateQuery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-aggregaterespo)**) | OK, an aggregate json object is returned
 400 | **e_code_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Missing required paramenter
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_JobsApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB_TT (**[array of PrintJob](#markdown-header-model-print_job)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_delete via HTTP DELETE
*** i_job_id: jobID of the printjob to delete
    /blck/p5_cl_JobsApi=>jobs_job_id_delete(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_412 = gr_http412
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-print_job)**) | OK, a json object is returned
 412 | **e_code_412** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Wrong Printer Status.
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_get via HTTP GET
*** i_job_id: jobID of the printjob to query
    /blck/p5_cl_JobsApi=>jobs_job_id_get(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-print_job)**) | OK, a json object is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_JOB_TARGET
    data gm_body type /BLCK/P5_JOB_TARGET.
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-target_printer = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-target_server = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_JOB_TARGET (**[JobTarget](#markdown-header-model-job_target)**) | JSON object describing where to move the job 
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_pause_put via HTTP PUT
*** i_job_id: ID of the print job to suspend
    /blck/p5_cl_JobsApi=>jobs_job_id_pause_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_repeat_put via HTTP PUT
*** i_job_id: ID of the print job to repeat
    /blck/p5_cl_JobsApi=>jobs_job_id_repeat_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_resume_put via HTTP PUT
*** i_job_id: ID of the print job to reactivate
    /blck/p5_cl_JobsApi=>jobs_job_id_resume_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_metadata_get via HTTP GET
    /blck/p5_cl_JobsApi=>jobs_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-metadata)**) | Query OK, metadata document is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB
    data gr_http200 type /BLCK/P5_PRINT_JOB.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_delete via HTTP DELETE
*** i_job_id: jobID of the printjob to delete
    /blck/p5_cl_ManagementApi=>jobs_job_id_delete(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_412 = gr_http412
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB (**[PrintJob](#markdown-header-model-print_job)**) | OK, a json object is returned
 412 | **e_code_412** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Wrong Printer Status.
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_JOB_TARGET
    data gm_body type /BLCK/P5_JOB_TARGET.
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-target_printer = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-target_server = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_JOB_TARGET (**[JobTarget](#markdown-header-model-job_target)**) | JSON object describing where to move the job 
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_pause_put via HTTP PUT
*** i_job_id: ID of the print job to suspend
    /blck/p5_cl_ManagementApi=>jobs_job_id_pause_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_repeat_put via HTTP PUT
*** i_job_id: ID of the print job to repeat
    /blck/p5_cl_ManagementApi=>jobs_job_id_repeat_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_job_id type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_job_id_resume_put via HTTP PUT
*** i_job_id: ID of the print job to reactivate
    /blck/p5_cl_ManagementApi=>jobs_job_id_resume_put(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_PRINTER
    data gr_http500 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_PRINTER)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | A JSON object describing the new printer. The &#x27;printer&#x27; property needs to contain a unique name for the new printer (if the name is already in use, the POST request will fail (HTTP 409). The &#x27;connection&#x27; parameter is an arbitrary string (e.g. a URL) used to connect from PLOSSYS to the printer. Example {   \&quot;printer\&quot;: \&quot;newPrinterName\&quot;,   \&quot;connection\&quot;: \&quot;socket://HostOrIp:9100\&quot; }  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | OK. The printer was created, details of the new printer are returned
 500 | **e_code_500** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | Error, e.g. in printer already exists
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_PRINTER
    data gr_http412 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_delete via HTTP DELETE
*** i_printer_name: name (not ID!) of the printer to delete
    /blck/p5_cl_ManagementApi=>printers_printer_name_delete(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 412.
*       do something with gr_http412 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_put via HTTP PUT
*** i_body: JSON object containing updated printer object
    /blck/p5_cl_ManagementApi=>printers_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | JSON object containing updated printer object 

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternamecreatetestj via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to test
    /blck/p5_cl_ManagementApi=>printersprinternamecreatetestj(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternamepauseput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to pause
    /blck/p5_cl_ManagementApi=>printersprinternamepauseput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternameredirectput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to redirect
    /blck/p5_cl_ManagementApi=>printersprinternameredirectput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ManagementApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternameresumeput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to reactivate
    /blck/p5_cl_ManagementApi=>printersprinternameresumeput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_ODataApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB_TT (**[array of PrintJob](#markdown-header-model-print_job)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_ODataApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
 200 | **e_code_200** | /BLCK/P5_PRINTER_TT (**[array of Printer](#markdown-header-model-printer)**) | Query OK; an array of printer objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_ODataApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_ODataApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_404 = gr_http404
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-logs)**) | OK, log entries are returned
 404 | **e_code_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | No log entries found
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the result of the call is HTTP Code: 400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_PrinterApi=>printers_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_400 = gr_http400
        e_code_500 = gr_http500 ).

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
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[AggregateQuery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-aggregaterespo)**) | OK, an aggregate json object is returned
 400 | **e_code_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Missing required paramenter
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_PrinterApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
 200 | **e_code_200** | /BLCK/P5_PRINTER_TT (**[array of Printer](#markdown-header-model-printer)**) | Query OK; an array of printer objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_METADATA
    data gr_http200 type /BLCK/P5_METADATA.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_metadata_get via HTTP GET
    /blck/p5_cl_PrinterApi=>printers_metadata_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_METADATA (**[Metadata](#markdown-header-model-metadata)**) | Query OK, metadata document is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_PRINTER
    data gr_http500 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_PRINTER)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | A JSON object describing the new printer. The &#x27;printer&#x27; property needs to contain a unique name for the new printer (if the name is already in use, the POST request will fail (HTTP 409). The &#x27;connection&#x27; parameter is an arbitrary string (e.g. a URL) used to connect from PLOSSYS to the printer. Example {   \&quot;printer\&quot;: \&quot;newPrinterName\&quot;,   \&quot;connection\&quot;: \&quot;socket://HostOrIp:9100\&quot; }  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | OK. The printer was created, details of the new printer are returned
 500 | **e_code_500** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | Error, e.g. in printer already exists
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_PRINTER
    data gr_http412 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_delete via HTTP DELETE
*** i_printer_name: name (not ID!) of the printer to delete
    /blck/p5_cl_PrinterApi=>printers_printer_name_delete(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 412.
*       do something with gr_http412 (type /BLCK/P5_PRINTER)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER
    data gr_http200 type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_get via HTTP GET
*** i_printer_name: Name (not ID!) of the printer
    /blck/p5_cl_PrinterApi=>printers_printer_name_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER)
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_printer_name** | /BLCK/P5_STRING | Name (not ID!) of the printer 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | Printer configuration
 404 | **e_code_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Printer not found
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_PrinterApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_404 = gr_http404
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-logs)**) | OK, log entries are returned
 404 | **e_code_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | No log entries found
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_PRINTER
    data gm_body type /BLCK/P5_PRINTER.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_put via HTTP PUT
*** i_body: JSON object containing updated printer object
    /blck/p5_cl_PrinterApi=>printers_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P5_PRINTER (**[Printer](#markdown-header-model-printer)**) | JSON object containing updated printer object 

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternamecreatetestj via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to test
    /blck/p5_cl_PrinterApi=>printersprinternamecreatetestj(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternamepauseput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to pause
    /blck/p5_cl_PrinterApi=>printersprinternamepauseput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternameredirectput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to redirect
    /blck/p5_cl_PrinterApi=>printersprinternameredirectput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 412 we expect type /BLCK/P5_ERROR
    data gr_http412 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternameresumeput via HTTP PUT
*** i_printer_name: name (not ID!) of the printer to reactivate
    /blck/p5_cl_PrinterApi=>printersprinternameresumeput(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_404 = gr_http404
        e_code_412 = gr_http412
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 404.
*       do something with gr_http404 (type /BLCK/P5_ERROR)
      when 412.
*       do something with gr_http412 (type /BLCK/P5_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER_STATUS
    data gr_http200 type /BLCK/P5_PRINTER_STATUS.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_PrinterApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printersprinternamestatusget via HTTP GET
*** i_printer_name: Name (not ID) of the printer to query
    /blck/p5_cl_PrinterApi=>printersprinternamestatusget(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINTER_STATUS (**[PrinterStatus](#markdown-header-model-printer_status)**) | Query OK, status is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the result of the call is HTTP Code: 400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_SearchApi=>jobs_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_400 = gr_http400
        e_code_500 = gr_http500 ).

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
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[AggregateQuery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-aggregaterespo)**) | OK, an aggregate json object is returned
 400 | **e_code_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Missing required paramenter
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method jobs_count_get via HTTP GET
*** i_filter: OData query string describing jobs to count
    /blck/p5_cl_SearchApi=>jobs_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINT_JOB_TT
    data gr_http200 type /BLCK/P5_PRINT_JOB_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_PRINT_JOB_TT (**[array of PrintJob](#markdown-header-model-print_job)**) | Query OK; an array of PrintJob objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/P5_AGGREGATEQUERY
    data gm_body type /BLCK/P5_AGGREGATEQUERY.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_AGGREGATERESPO
    data gr_http200 type /BLCK/P5_AGGREGATERESPO.
*   when the result of the call is HTTP Code: 400 we expect type /BLCK/P5_ERROR
    data gr_http400 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
*   gm_body-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_aggregate_put via HTTP PUT
*** i_body: Query object containing definition of the requested aggregate 
    /blck/p5_cl_SearchApi=>printers_aggregate_put(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_400 = gr_http400
        e_code_500 = gr_http500 ).

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
 **i_body** | /BLCK/P5_AGGREGATEQUERY (**[AggregateQuery](#markdown-header-model-aggregatequery)**) | Query object containing definition of the requested aggregate  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P5_AGGREGATERESPO (**[AggregateResponse](#markdown-header-model-aggregaterespo)**) | OK, an aggregate json object is returned
 400 | **e_code_400** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Missing required paramenter
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_filter type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_COUNT
    data gr_http200 type /BLCK/P5_COUNT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_count_get via HTTP GET
*** i_filter: OData query string describing printers to count
    /blck/p5_cl_SearchApi=>printers_count_get(
      exporting
        i_filter = gvs_filter
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_COUNT (**[Count](#markdown-header-model-count)**) | OK, a number is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_PRINTER_TT
    data gr_http200 type /BLCK/P5_PRINTER_TT.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P5_ERROR
    data gr_httpother type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_filter = 'ipsum lorem'.
*   gvs_select = 'ipsum lorem'.
*   gvi_skip = 42.
*   gvi_top = 42.
*   gvs_orderby = 'ipsum lorem'.
*   gvs_inlinecount = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
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
        e_code_200 = gr_http200
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P5_PRINTER_TT)
      when 500.
*       do something with gr_http500 (type /BLCK/P5_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P5_ERROR)
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
 200 | **e_code_200** | /BLCK/P5_PRINTER_TT (**[array of Printer](#markdown-header-model-printer)**) | Query OK; an array of printer objects is returned
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error
 other | **e_code_other** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gvi_code type /blck/p5_int,
    gvs_msg  type /blck/p5_string.
    
*** create variables for input and output as needed
*   for parameter i_printer_name:
*   a simple ABAP primitive of type /BLCK/P5_STRING
    data gvs_printer_name type /BLCK/P5_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P5_LOGS
    data gr_http200 type /BLCK/P5_LOGS.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P5_ERROR
    data gr_http404 type /BLCK/P5_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P5_ERROR
    data gr_http500 type /BLCK/P5_ERROR.
        
*** set data according to requirements of the API call
*   gvs_printer_name = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*   so the following call is only necessary if the url should be different
    /blck/p5_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method printers_printer_name_logs_get via HTTP GET
*** i_printer_name: Name of the printer to get logs for
    /blck/p5_cl_SearchApi=>printers_printer_name_logs_get(
      exporting
        i_printer_name = gvs_printer_name
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_404 = gr_http404
        e_code_500 = gr_http500 ).

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
 200 | **e_code_200** | /BLCK/P5_LOGS (**[Logs](#markdown-header-model-logs)**) | OK, log entries are returned
 404 | **e_code_404** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | No log entries found
 500 | **e_code_500** | /BLCK/P5_ERROR (**[Error](#markdown-header-model-error)**) | Internal Server Error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-aggregatequery"></a> 

# Model: AggregateQuery



### Example
```abap
*** model aggregatequery example
*** A query for an aggregate

* create our variables..
    data gr_aggregatequery type /blck/p5_aggregatequery.
    
* fill model with data as appropriate..
    gr_aggregatequery-match = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_aggregatequery-aggregates = l_aggregates. " (type /BLCK/P5_STRING_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_aggregatequery(
      exporting
        i_aggregatequery = gr_aggregatequery ).
    		
    clear gr_aggregatequery.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_aggregatequery(
      exporting
        i_id = 1
      importing 
        e_200 = gr_aggregatequery ).
    		
    write: gr_aggregatequery-match. " (type /BLCK/P5_STRING)
    write: gr_aggregatequery-aggregates. " (type /BLCK/P5_STRING_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**match** | /BLCK/P5_STRING | Query-rules for objects to aggregate
**aggregates** | /BLCK/P5_STRING_TT | List of aggregates to generate

* * *
<a name="markdown-header-model-aggregaterespo"></a> 

# Model: AggregateResponse



### Example
```abap
*** model aggregaterespo example
*** An aggregate generated by PLOSSYS P5

* create our variables..
    data gr_aggregaterespo type /blck/p5_aggregaterespo.
    
* fill model with data as appropriate..
    
* pass to example API method
    /blck/cl_example_api=>update_aggregaterespo(
      exporting
        i_aggregaterespo = gr_aggregaterespo ).
    		
    clear gr_aggregaterespo.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_aggregaterespo(
      exporting
        i_id = 1
      importing 
        e_200 = gr_aggregaterespo ).
    		

```

## Properties

Name | Type | Description
------------ | ------------- | -------------

* * *
<a name="markdown-header-model-count"></a> 

# Model: Count



### Example
```abap
*** model count example
*** Key-Value pair containing a number

* create our variables..
    data gr_count type /blck/p5_count.
    
* fill model with data as appropriate..
    gr_count-count = 42. " (type /BLCK/P5_INT)
    
* pass to example API method
    /blck/cl_example_api=>update_count(
      exporting
        i_count = gr_count ).
    		
    clear gr_count.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_count(
      exporting
        i_id = 1
      importing 
        e_200 = gr_count ).
    		
    write: gr_count-count. " (type /BLCK/P5_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**count** | /BLCK/P5_INT | Counted number

* * *
<a name="markdown-header-model-error"></a> 

# Model: Error



### Example
```abap
*** model error example

* create our variables..
    data gr_error type /blck/p5_error.
    
* fill model with data as appropriate..
    gr_error-code = 42. " (type /BLCK/P5_INT)
    gr_error-message = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_error-fields = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_error(
      exporting
        i_error = gr_error ).
    		
    clear gr_error.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_error(
      exporting
        i_id = 1
      importing 
        e_200 = gr_error ).
    		
    write: gr_error-code. " (type /BLCK/P5_INT)
    write: gr_error-message. " (type /BLCK/P5_STRING)
    write: gr_error-fields. " (type /BLCK/P5_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**code** | /BLCK/P5_INT | 
**message** | /BLCK/P5_STRING | 
**fields** | /BLCK/P5_STRING | 

* * *
<a name="markdown-header-model-job_target"></a> 

# Model: JobTarget



### Example
```abap
*** model job_target example
*** Server and Printer for handling a job

* create our variables..
    data gr_job_target type /blck/p5_job_target.
    
* fill model with data as appropriate..
    gr_job_target-target_printer = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_job_target-target_server = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_job_target(
      exporting
        i_job_target = gr_job_target ).
    		
    clear gr_job_target.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_job_target(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_target ).
    		
    write: gr_job_target-target_printer. " (type /BLCK/P5_STRING)
    write: gr_job_target-target_server. " (type /BLCK/P5_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**target_printer** | /BLCK/P5_STRING | PrinterName of the target printer
**target_server** | /BLCK/P5_STRING | Name of the target PLOSSYS P5 server

* * *
<a name="markdown-header-model-logs"></a> 

# Model: Logs



### Example
```abap
*** model logs example
*** List of Log entries for a printer

* create our variables..
    data gr_logs type /blck/p5_logs.
    
* fill model with data as appropriate..
    gr_logs-messages = l_messages. " (type /BLCK/P5_STRING_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_logs(
      exporting
        i_logs = gr_logs ).
    		
    clear gr_logs.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_logs(
      exporting
        i_id = 1
      importing 
        e_200 = gr_logs ).
    		
    write: gr_logs-messages. " (type /BLCK/P5_STRING_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**messages** | /BLCK/P5_STRING_TT | Array of Log entries

* * *
<a name="markdown-header-model-metadata"></a> 

# Model: Metadata



### Example
```abap
*** model metadata example
*** Array of objects describing items in a JSON object used in this API. 

* create our variables..
    data gr_metadata type /blck/p5_metadata.
    
* fill model with data as appropriate..
    
* pass to example API method
    /blck/cl_example_api=>update_metadata(
      exporting
        i_metadata = gr_metadata ).
    		
    clear gr_metadata.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_metadata(
      exporting
        i_id = 1
      importing 
        e_200 = gr_metadata ).
    		

```

## Properties

Name | Type | Description
------------ | ------------- | -------------

* * *
<a name="markdown-header-model-print_job"></a> 

# Model: PrintJob



### Example
```abap
*** model print_job example
*** Status information about a print job

* create our variables..
    data gr_print_job type /blck/p5_print_job.
    
* fill model with data as appropriate..
    gr_print_job-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_print_job-status = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_print_job-current = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_print_job-orig = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_print_job-routing = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_print_job(
      exporting
        i_print_job = gr_print_job ).
    		
    clear gr_print_job.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_print_job(
      exporting
        i_id = 1
      importing 
        e_200 = gr_print_job ).
    		
    write: gr_print_job-id. " (type /BLCK/P5_STRING)
    write: gr_print_job-status. " (type /BLCK/P5_STRING)
    write: gr_print_job-current. " (type /BLCK/P5_STRING)
    write: gr_print_job-orig. " (type /BLCK/P5_STRING)
    write: gr_print_job-routing. " (type /BLCK/P5_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/P5_STRING | Job identifier
**status** | /BLCK/P5_STRING | Current job status
**current** | /BLCK/P5_STRING | Information about the job as it is used in PLOSSYS P5 at the present time.
**orig** | /BLCK/P5_STRING | Information about the job as it was originally submitted to PLOSSYS P5
**routing** | /BLCK/P5_STRING | Information about the processor route of the job.

* * *
<a name="markdown-header-model-printer"></a> 

# Model: Printer



### Example
```abap
*** model printer example

* create our variables..
    data gr_printer type /blck/p5_printer.
    
* fill model with data as appropriate..
    gr_printer-id = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_printer-config = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_printer(
      exporting
        i_printer = gr_printer ).
    		
    clear gr_printer.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_printer(
      exporting
        i_id = 1
      importing 
        e_200 = gr_printer ).
    		
    write: gr_printer-id. " (type /BLCK/P5_STRING)
    write: gr_printer-config. " (type /BLCK/P5_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/P5_STRING | Internal ID of the printer, auto-generated by PLOSSYS P5
**config** | /BLCK/P5_STRING | 

* * *
<a name="markdown-header-model-printer_status"></a> 

# Model: PrinterStatus



### Example
```abap
*** model printer_status example
*** Ressource representing the current printer status.

* create our variables..
    data gr_printer_status type /blck/p5_printer_status.
    
* fill model with data as appropriate..
    gr_printer_status-mode = 'ipsum lorem'. " (type /BLCK/P5_STRING)
    gr_printer_status-queue_length = 42. " (type /BLCK/P5_INT)
    
* pass to example API method
    /blck/cl_example_api=>update_printer_status(
      exporting
        i_printer_status = gr_printer_status ).
    		
    clear gr_printer_status.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_printer_status(
      exporting
        i_id = 1
      importing 
        e_200 = gr_printer_status ).
    		
    write: gr_printer_status-mode. " (type /BLCK/P5_STRING)
    write: gr_printer_status-queue_length. " (type /BLCK/P5_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**mode** | /BLCK/P5_STRING | One of {ready, printing, paused, redirected, error}
**queue_length** | /BLCK/P5_INT | 

