# API: SearchApi

All URIs are relative to *https://<<SITEURL.SHAREPOINT.COM>>/_api*

## operation: **query**


Query


### Example
```abap
*** method SearchApi->query example

  constants:
    gcc_basepath type string value 'https://<<SITEURL.SHAREPOINT.COM>>/_api'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/sps_int,
    gvs_msg  type /blck/sps_string.
    
*** create variables for input and output as needed
*   for parameter i_querytext:
*   a simple ABAP primitive of type /BLCK/SPS_STRING
    data gvs_querytext type /BLCK/SPS_STRING.
*   for parameter i_selectproperties:
*   a simple ABAP primitive of type /BLCK/SPS_STRING
    data gvs_selectproperties type /BLCK/SPS_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/SPS_QUERY
    data gr_http200 type /BLCK/SPS_QUERY.
        
*** set data according to requirements of the API call
*   gvs_querytext = 'ipsum lorem'.
*   gvs_selectproperties = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/sps_cl_SearchApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method query via HTTP GET
*** i_querytext: querytext
*** i_selectproperties: selectproperties
    /blck/sps_cl_SearchApi=>query(
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
*       do something with gr_http200 (type /BLCK/SPS_QUERY)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_querytext** | /BLCK/SPS_STRING | querytext 
 **i_selectproperties** | /BLCK/SPS_STRING | selectproperties [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/SPS_QUERY (**[Query](#markdown-header-model-query)**) | OK

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
    data gr_cells type /blck/sps_cells.
    
* fill model with data as appropriate..
    gr_cells-key = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_cells-value = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_cells-value_type = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    
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
    		
    write: gr_cells-key. " (type /BLCK/SPS_STRING)
    write: gr_cells-value. " (type /BLCK/SPS_STRING)
    write: gr_cells-value_type. " (type /BLCK/SPS_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**key** | /BLCK/SPS_STRING | 
**value** | /BLCK/SPS_STRING | 
**value_type** | /BLCK/SPS_STRING | 

* * *
<a name="markdown-header-model-properties"></a> 

# Model: Properties



### Example
```abap
*** model properties example
*** Model for Properties

* create our variables..
    data gr_properties type /blck/sps_properties.
    
* fill model with data as appropriate..
    gr_properties-key = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_properties-value = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_properties-value_type = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    
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
    		
    write: gr_properties-key. " (type /BLCK/SPS_STRING)
    write: gr_properties-value. " (type /BLCK/SPS_STRING)
    write: gr_properties-value_type. " (type /BLCK/SPS_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**key** | /BLCK/SPS_STRING | 
**value** | /BLCK/SPS_STRING | 
**value_type** | /BLCK/SPS_STRING | 

* * *
<a name="markdown-header-model-rows"></a> 

# Model: Rows



### Example
```abap
*** model rows example
*** Model for Rows

* create our variables..
    data gr_rows type /blck/sps_rows.
    
* fill model with data as appropriate..
    gr_rows-cells = l_cells. " (type /BLCK/SPS_CELLS_TT)
    
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
    		
    write: gr_rows-cells. " (type /BLCK/SPS_CELLS_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**cells** | /BLCK/SPS_CELLS_TT (**[array of Cells](#markdown-header-model-cells)**) | 

* * *
<a name="markdown-header-model-table"></a> 

# Model: Table



### Example
```abap
*** model table example
*** Model for Table

* create our variables..
    data gr_table type /blck/sps_table.
    
* fill model with data as appropriate..
    gr_table-rows = l_rows. " (type /BLCK/SPS_ROWS_TT)
    
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
    		
    write: gr_table-rows. " (type /BLCK/SPS_ROWS_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**rows** | /BLCK/SPS_ROWS_TT (**[array of Rows](#markdown-header-model-rows)**) | 

* * *
<a name="markdown-header-model-relevantresult"></a> 

# Model: RelevantResults



### Example
```abap
*** model relevantresult example
*** Model for RelevantResults

* create our variables..
    data gr_relevantresult type /blck/sps_relevantresult.
    
* fill model with data as appropriate..
    gr_relevantresult-group_template_id = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_relevantresult-item_template_id = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_relevantresult-properties = l_properties. " (type /BLCK/SPS_PROPERTIES_TT)
    gr_relevantresult-result_title = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_relevantresult-result_title_url = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_relevantresult-row_count = 42. " (type /BLCK/SPS_INT)
    gr_relevantresult-table = l_table. " (type /BLCK/SPS_TABLE)
    gr_relevantresult-total_rows = 42. " (type /BLCK/SPS_INT)
    gr_relevantresult-totalrowsincludingduplicat = 42. " (type /BLCK/SPS_INT)
    
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
    		
    write: gr_relevantresult-group_template_id. " (type /BLCK/SPS_STRING)
    write: gr_relevantresult-item_template_id. " (type /BLCK/SPS_STRING)
    write: gr_relevantresult-properties. " (type /BLCK/SPS_PROPERTIES_TT)
    write: gr_relevantresult-result_title. " (type /BLCK/SPS_STRING)
    write: gr_relevantresult-result_title_url. " (type /BLCK/SPS_STRING)
    write: gr_relevantresult-row_count. " (type /BLCK/SPS_INT)
    write: gr_relevantresult-table. " (type /BLCK/SPS_TABLE)
    write: gr_relevantresult-total_rows. " (type /BLCK/SPS_INT)
    write: gr_relevantresult-totalrowsincludingduplicat. " (type /BLCK/SPS_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**group_template_id** | /BLCK/SPS_STRING | 
**item_template_id** | /BLCK/SPS_STRING | 
**properties** | /BLCK/SPS_PROPERTIES_TT (**[array of Properties](#markdown-header-model-properties)**) | 
**result_title** | /BLCK/SPS_STRING | 
**result_title_url** | /BLCK/SPS_STRING | 
**row_count** | /BLCK/SPS_INT | 
**table** | /BLCK/SPS_TABLE (**[Table](#markdown-header-model-table)**) | 
**total_rows** | /BLCK/SPS_INT | 
**totalrowsincludingduplicat** | /BLCK/SPS_INT | 

* * *
<a name="markdown-header-model-primaryqueryre"></a> 

# Model: PrimaryQueryResult



### Example
```abap
*** model primaryqueryre example
*** Model for PrimaryQueryResult

* create our variables..
    data gr_primaryqueryre type /blck/sps_primaryqueryre.
    
* fill model with data as appropriate..
    gr_primaryqueryre-custom_results = l_custom_results. " (type /BLCK/SPS_STRING_TT)
    gr_primaryqueryre-query_id = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_primaryqueryre-query_rule_id = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_primaryqueryre-refinement_results = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_primaryqueryre-relevant_results = l_relevant_results. " (type /BLCK/SPS_RELEVANTRESULT)
    gr_primaryqueryre-special_term_results = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    
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
    		
    write: gr_primaryqueryre-custom_results. " (type /BLCK/SPS_STRING_TT)
    write: gr_primaryqueryre-query_id. " (type /BLCK/SPS_STRING)
    write: gr_primaryqueryre-query_rule_id. " (type /BLCK/SPS_STRING)
    write: gr_primaryqueryre-refinement_results. " (type /BLCK/SPS_STRING)
    write: gr_primaryqueryre-relevant_results. " (type /BLCK/SPS_RELEVANTRESULT)
    write: gr_primaryqueryre-special_term_results. " (type /BLCK/SPS_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**custom_results** | /BLCK/SPS_STRING_TT | 
**query_id** | /BLCK/SPS_STRING | 
**query_rule_id** | /BLCK/SPS_STRING | 
**refinement_results** | /BLCK/SPS_STRING | 
**relevant_results** | /BLCK/SPS_RELEVANTRESULT (**[RelevantResults](#markdown-header-model-relevantresult)**) | 
**special_term_results** | /BLCK/SPS_STRING | 

* * *
<a name="markdown-header-model-properties2"></a> 

# Model: Properties2



### Example
```abap
*** model properties2 example
*** Model for Properties2

* create our variables..
    data gr_properties2 type /blck/sps_properties2.
    
* fill model with data as appropriate..
    gr_properties2-key = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_properties2-value = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_properties2-value_type = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    
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
    		
    write: gr_properties2-key. " (type /BLCK/SPS_STRING)
    write: gr_properties2-value. " (type /BLCK/SPS_STRING)
    write: gr_properties2-value_type. " (type /BLCK/SPS_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**key** | /BLCK/SPS_STRING | 
**value** | /BLCK/SPS_STRING | 
**value_type** | /BLCK/SPS_STRING | 

* * *
<a name="markdown-header-model-query"></a> 

# Model: Query



### Example
```abap
*** model query example
*** Model for Query

* create our variables..
    data gr_query type /blck/sps_query.
    
* fill model with data as appropriate..
    gr_query-elapsed_time = 42. " (type /BLCK/SPS_INT)
    gr_query-odata_metadata = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_query-primary_query_result = l_primary_query_result. " (type /BLCK/SPS_PRIMARYQUERYRE)
    gr_query-properties = l_properties. " (type /BLCK/SPS_PROPERTIES2_TT)
    gr_query-secondary_query_results = l_secondary_query_results. " (type /BLCK/SPS_STRING_TT)
    gr_query-spelling_suggestion = 'ipsum lorem'. " (type /BLCK/SPS_STRING)
    gr_query-triggered_rules = l_triggered_rules. " (type /BLCK/SPS_STRING_TT)
    
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
    		
    write: gr_query-elapsed_time. " (type /BLCK/SPS_INT)
    write: gr_query-odata_metadata. " (type /BLCK/SPS_STRING)
    write: gr_query-primary_query_result. " (type /BLCK/SPS_PRIMARYQUERYRE)
    write: gr_query-properties. " (type /BLCK/SPS_PROPERTIES2_TT)
    write: gr_query-secondary_query_results. " (type /BLCK/SPS_STRING_TT)
    write: gr_query-spelling_suggestion. " (type /BLCK/SPS_STRING)
    write: gr_query-triggered_rules. " (type /BLCK/SPS_STRING_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**elapsed_time** | /BLCK/SPS_INT | 
**odata_metadata** | /BLCK/SPS_STRING | 
**primary_query_result** | /BLCK/SPS_PRIMARYQUERYRE (**[PrimaryQueryResult](#markdown-header-model-primaryqueryre)**) | 
**properties** | /BLCK/SPS_PROPERTIES2_TT (**[array of Properties2](#markdown-header-model-properties2)**) | 
**secondary_query_results** | /BLCK/SPS_STRING_TT | 
**spelling_suggestion** | /BLCK/SPS_STRING | 
**triggered_rules** | /BLCK/SPS_STRING_TT | 

