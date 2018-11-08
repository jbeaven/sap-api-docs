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
*   when the the result of the call is HTTP200 we expect type /BLCK/SPS_QUERY
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
        e_200 = gr_http200 ).

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
 200 | **e_200** | /BLCK/SPS_QUERY (**[Query](#markdown-header-model-)**) | OK

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-cells"></a> 

# Model: cells



### Example
```abap
*** model cells example
*** Model for Cells

* create our variables..
    data gcl_cells type ref to /blck/mdl_cl_cells.
    
* instantiate model and call the setters to set values..
    gcl_cells = /blck/mdl_cl_cells=>create( ).
    gcl_cells->set_key( 'ipsum lorem' ). " (type string)
    gcl_cells->set_value( 'ipsum lorem' ). " (type string)
    gcl_cells->set_value_type( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_cells(
    	exporting
    		i_cells = gcl_cells ).
    		
    clear gcl_cells.
    
* fetch new instance from example API method
    gcl_cells = gcl_exampleapi->get_cells(
    	exporting
    		i_id = 1 ).
    		
    l_key = gcl_cells->get_key( ). " (type string)
    l_value = gcl_cells->get_value( ). " (type string)
    l_value_type = gcl_cells->get_value_type( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**key** | string |  | [default to null]
**value** | string |  | [optional] [default to null]
**value_type** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-properties"></a> 

# Model: properties



### Example
```abap
*** model properties example
*** Model for Properties

* create our variables..
    data gcl_properties type ref to /blck/mdl_cl_properties.
    
* instantiate model and call the setters to set values..
    gcl_properties = /blck/mdl_cl_properties=>create( ).
    gcl_properties->set_key( 'ipsum lorem' ). " (type string)
    gcl_properties->set_value( 'ipsum lorem' ). " (type string)
    gcl_properties->set_value_type( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_properties(
    	exporting
    		i_properties = gcl_properties ).
    		
    clear gcl_properties.
    
* fetch new instance from example API method
    gcl_properties = gcl_exampleapi->get_properties(
    	exporting
    		i_id = 1 ).
    		
    l_key = gcl_properties->get_key( ). " (type string)
    l_value = gcl_properties->get_value( ). " (type string)
    l_value_type = gcl_properties->get_value_type( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**key** | string |  | [default to null]
**value** | string |  | [optional] [default to null]
**value_type** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-rows"></a> 

# Model: rows



### Example
```abap
*** model rows example
*** Model for Rows

* create our variables..
    data gcl_rows type ref to /blck/mdl_cl_rows.
    
* instantiate model and call the setters to set values..
    gcl_rows = /blck/mdl_cl_rows=>create( ).
    gcl_rows->set_cells( l_cells ). " (type /BLCK/SPS_cells_tt)
    
* pass to example API method
    gcl_exampleapi->update_rows(
    	exporting
    		i_rows = gcl_rows ).
    		
    clear gcl_rows.
    
* fetch new instance from example API method
    gcl_rows = gcl_exampleapi->get_rows(
    	exporting
    		i_id = 1 ).
    		
    l_cells = gcl_rows->get_cells( ). " (type /BLCK/SPS_cells_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**cells** | /BLCK/SPS_cells_tt (**[array of cells](#markdown-header-model-cells)**) |  | [default to null]

* * *
<a name="markdown-header-model-table"></a> 

# Model: table



### Example
```abap
*** model table example
*** Model for Table

* create our variables..
    data gcl_table type ref to /blck/mdl_cl_table.
    
* instantiate model and call the setters to set values..
    gcl_table = /blck/mdl_cl_table=>create( ).
    gcl_table->set_rows( l_rows ). " (type /BLCK/SPS_rows_tt)
    
* pass to example API method
    gcl_exampleapi->update_table(
    	exporting
    		i_table = gcl_table ).
    		
    clear gcl_table.
    
* fetch new instance from example API method
    gcl_table = gcl_exampleapi->get_table(
    	exporting
    		i_id = 1 ).
    		
    l_rows = gcl_table->get_rows( ). " (type /BLCK/SPS_rows_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**rows** | /BLCK/SPS_rows_tt (**[array of rows](#markdown-header-model-rows)**) |  | [default to null]

* * *
<a name="markdown-header-model-relevantresult"></a> 

# Model: relevantresult



### Example
```abap
*** model relevantresult example
*** Model for RelevantResults

* create our variables..
    data gcl_relevantresult type ref to /blck/mdl_cl_relevantresult.
    
* instantiate model and call the setters to set values..
    gcl_relevantresult = /blck/mdl_cl_relevantresult=>create( ).
    gcl_relevantresult->set_group_template_id( 'ipsum lorem' ). " (type string)
    gcl_relevantresult->set_item_template_id( 'ipsum lorem' ). " (type string)
    gcl_relevantresult->set_properties( l_properties ). " (type /BLCK/SPS_properties_tt)
    gcl_relevantresult->set_result_title( 'ipsum lorem' ). " (type string)
    gcl_relevantresult->set_result_title_url( 'ipsum lorem' ). " (type string)
    gcl_relevantresult->set_row_count( 42 ). " (type i)
    gcl_relevantresult->set_table( l_table ). " (type /BLCK/SPS_table)
    gcl_relevantresult->set_total_rows( 42 ). " (type i)
    gcl_relevantresult->set_totalrowsincludingduplicat( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_relevantresult(
    	exporting
    		i_relevantresult = gcl_relevantresult ).
    		
    clear gcl_relevantresult.
    
* fetch new instance from example API method
    gcl_relevantresult = gcl_exampleapi->get_relevantresult(
    	exporting
    		i_id = 1 ).
    		
    l_group_template_id = gcl_relevantresult->get_group_template_id( ). " (type string)
    l_item_template_id = gcl_relevantresult->get_item_template_id( ). " (type string)
    l_properties = gcl_relevantresult->get_properties( ). " (type /BLCK/SPS_properties_tt)
    l_result_title = gcl_relevantresult->get_result_title( ). " (type string)
    l_result_title_url = gcl_relevantresult->get_result_title_url( ). " (type string)
    l_row_count = gcl_relevantresult->get_row_count( ). " (type i)
    l_table = gcl_relevantresult->get_table( ). " (type /BLCK/SPS_table)
    l_total_rows = gcl_relevantresult->get_total_rows( ). " (type i)
    l_totalrowsincludingduplicat = gcl_relevantresult->get_totalrowsincludingduplicat( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**group_template_id** | string |  | [default to null]
**item_template_id** | string |  | [optional] [default to null]
**properties** | /BLCK/SPS_properties_tt (**[array of properties](#markdown-header-model-properties)**) |  | [optional] [default to null]
**result_title** | string |  | [optional] [default to null]
**result_title_url** | string |  | [optional] [default to null]
**row_count** | i |  | [optional] [default to null]
**table** | /BLCK/SPS_table (**[table](#markdown-header-model-table)**) |  | [optional] [default to null]
**total_rows** | i |  | [optional] [default to null]
**totalrowsincludingduplicat** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-model-primaryqueryre"></a> 

# Model: primaryqueryre



### Example
```abap
*** model primaryqueryre example
*** Model for PrimaryQueryResult

* create our variables..
    data gcl_primaryqueryre type ref to /blck/mdl_cl_primaryqueryre.
    
* instantiate model and call the setters to set values..
    gcl_primaryqueryre = /blck/mdl_cl_primaryqueryre=>create( ).
    gcl_primaryqueryre->set_custom_results( l_custom_results ). " (type /blck/api_string_tt)
    gcl_primaryqueryre->set_query_id( 'ipsum lorem' ). " (type string)
    gcl_primaryqueryre->set_query_rule_id( 'ipsum lorem' ). " (type string)
    gcl_primaryqueryre->set_refinement_results( 'ipsum lorem' ). " (type string)
    gcl_primaryqueryre->set_relevant_results( l_relevant_results ). " (type /BLCK/SPS_relevantresult)
    gcl_primaryqueryre->set_special_term_results( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_primaryqueryre(
    	exporting
    		i_primaryqueryre = gcl_primaryqueryre ).
    		
    clear gcl_primaryqueryre.
    
* fetch new instance from example API method
    gcl_primaryqueryre = gcl_exampleapi->get_primaryqueryre(
    	exporting
    		i_id = 1 ).
    		
    l_custom_results = gcl_primaryqueryre->get_custom_results( ). " (type /blck/api_string_tt)
    l_query_id = gcl_primaryqueryre->get_query_id( ). " (type string)
    l_query_rule_id = gcl_primaryqueryre->get_query_rule_id( ). " (type string)
    l_refinement_results = gcl_primaryqueryre->get_refinement_results( ). " (type string)
    l_relevant_results = gcl_primaryqueryre->get_relevant_results( ). " (type /BLCK/SPS_relevantresult)
    l_special_term_results = gcl_primaryqueryre->get_special_term_results( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**custom_results** | /blck/api_string_tt |  | [default to null]
**query_id** | string |  | [optional] [default to null]
**query_rule_id** | string |  | [optional] [default to null]
**refinement_results** | string |  | [optional] [default to null]
**relevant_results** | /BLCK/SPS_relevantresult (**[relevantresult](#markdown-header-model-relevantresult)**) |  | [optional] [default to null]
**special_term_results** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-properties2"></a> 

# Model: properties2



### Example
```abap
*** model properties2 example
*** Model for Properties2

* create our variables..
    data gcl_properties2 type ref to /blck/mdl_cl_properties2.
    
* instantiate model and call the setters to set values..
    gcl_properties2 = /blck/mdl_cl_properties2=>create( ).
    gcl_properties2->set_key( 'ipsum lorem' ). " (type string)
    gcl_properties2->set_value( 'ipsum lorem' ). " (type string)
    gcl_properties2->set_value_type( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_properties2(
    	exporting
    		i_properties2 = gcl_properties2 ).
    		
    clear gcl_properties2.
    
* fetch new instance from example API method
    gcl_properties2 = gcl_exampleapi->get_properties2(
    	exporting
    		i_id = 1 ).
    		
    l_key = gcl_properties2->get_key( ). " (type string)
    l_value = gcl_properties2->get_value( ). " (type string)
    l_value_type = gcl_properties2->get_value_type( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**key** | string |  | [default to null]
**value** | string |  | [optional] [default to null]
**value_type** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-query"></a> 

# Model: query



### Example
```abap
*** model query example
*** Model for Query

* create our variables..
    data gcl_query type ref to /blck/mdl_cl_query.
    
* instantiate model and call the setters to set values..
    gcl_query = /blck/mdl_cl_query=>create( ).
    gcl_query->set_elapsed_time( 42 ). " (type i)
    gcl_query->set_odata_metadata( 'ipsum lorem' ). " (type string)
    gcl_query->set_primary_query_result( l_primary_query_result ). " (type /BLCK/SPS_primaryqueryre)
    gcl_query->set_properties( l_properties ). " (type /BLCK/SPS_properties2_tt)
    gcl_query->set_secondary_query_results( l_secondary_query_results ). " (type /blck/api_string_tt)
    gcl_query->set_spelling_suggestion( 'ipsum lorem' ). " (type string)
    gcl_query->set_triggered_rules( l_triggered_rules ). " (type /blck/api_string_tt)
    
* pass to example API method
    gcl_exampleapi->update_query(
    	exporting
    		i_query = gcl_query ).
    		
    clear gcl_query.
    
* fetch new instance from example API method
    gcl_query = gcl_exampleapi->get_query(
    	exporting
    		i_id = 1 ).
    		
    l_elapsed_time = gcl_query->get_elapsed_time( ). " (type i)
    l_odata_metadata = gcl_query->get_odata_metadata( ). " (type string)
    l_primary_query_result = gcl_query->get_primary_query_result( ). " (type /BLCK/SPS_primaryqueryre)
    l_properties = gcl_query->get_properties( ). " (type /BLCK/SPS_properties2_tt)
    l_secondary_query_results = gcl_query->get_secondary_query_results( ). " (type /blck/api_string_tt)
    l_spelling_suggestion = gcl_query->get_spelling_suggestion( ). " (type string)
    l_triggered_rules = gcl_query->get_triggered_rules( ). " (type /blck/api_string_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**elapsed_time** | i |  | [default to null]
**odata_metadata** | string |  | [optional] [default to null]
**primary_query_result** | /BLCK/SPS_primaryqueryre (**[primaryqueryre](#markdown-header-model-primaryqueryre)**) |  | [optional] [default to null]
**properties** | /BLCK/SPS_properties2_tt (**[array of properties2](#markdown-header-model-properties2)**) |  | [optional] [default to null]
**secondary_query_results** | /blck/api_string_tt |  | [optional] [default to null]
**spelling_suggestion** | string |  | [optional] [default to null]
**triggered_rules** | /blck/api_string_tt |  | [optional] [default to null]

