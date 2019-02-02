# API: DefaultApi
## &nbsp; &nbsp; [Operation: lookup_get](#markdown-header-op-DefaultApi-lookup_get)
## &nbsp; &nbsp; [Operation: reverse_get](#markdown-header-op-DefaultApi-reverse_get)
## &nbsp; &nbsp; [Operation: search_get](#markdown-header-op-DefaultApi-search_get)
# Models and Enumerations

# API: DefaultApi

All URIs are relative to *http:// http://nominatim.openstreetmap.org*

<a name="markdown-header-op-DefaultApi-lookup_get"></a>

## operation: **lookup_get**
OSM - Address lookup

[Full description of the service:](http://wiki.openstreetmap.org/wiki/Nominatim#Address_lookup)


### Example
```abap
*** method DefaultApi->lookup_get example
*** OSM - Address lookup

  constants:
    gcc_basepath type string value 'http:// http://nominatim.openstreetmap.org'.
    
  data:  
    gvi_code type /blck/osm_int,
    gvs_msg  type /blck/osm_string.
    
*** create variables for input and output as needed
*   for parameter i_osm_ids:
*   a simple ABAP primitive of type /BLCK/OSM_STRING
    data gvs_osm_ids type /BLCK/OSM_STRING.
*   for parameter i_format:
*   a simple ABAP primitive of type /BLCK/OSM_STRING
    data gvs_format type /BLCK/OSM_STRING.
        
*** set data according to requirements of the API call
*   gvs_osm_ids = 'ipsum lorem'.
*   gvs_format = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/osm_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method lookup_get via HTTP GET
    /blck/osm_cl_DefaultApi=>lookup_get(
      exporting
        i_osm_ids = gvs_osm_ids
        i_format = gvs_format
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_osm_ids** | `/BLCK/OSM_STRING` |  
 **i_format** | `/BLCK/OSM_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-DefaultApi-reverse_get"></a>

## operation: **reverse_get**
OSM - Reverse

[Full description of the service:](http://wiki.openstreetmap.org/wiki/Nominatim#Reverse_Geocoding)


### Example
```abap
*** method DefaultApi->reverse_get example
*** OSM - Reverse

  constants:
    gcc_basepath type string value 'http:// http://nominatim.openstreetmap.org'.
    
  data:  
    gvi_code type /blck/osm_int,
    gvs_msg  type /blck/osm_string.
    
*** create variables for input and output as needed
*   for parameter i_format:
*   a simple ABAP primitive of type /BLCK/OSM_STRING
    data gvs_format type /BLCK/OSM_STRING.
*   for parameter i_lat:
*   a reference to model type /BLCK/OSM_NUMBER
    data gm_lat type /BLCK/OSM_NUMBER.
*   for parameter i_lon:
*   a reference to model type /BLCK/OSM_NUMBER
    data gm_lon type /BLCK/OSM_NUMBER.
        
*** set data according to requirements of the API call
*   gvs_format = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/osm_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method reverse_get via HTTP GET
    /blck/osm_cl_DefaultApi=>reverse_get(
      exporting
        i_format = gvs_format
        i_lat = gm_lat
        i_lon = gm_lon
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_format** | `/BLCK/OSM_STRING` |  
 **i_lat** | `/BLCK/OSM_NUMBER` (**[number](#markdown-header-model-number)**) |  
 **i_lon** | `/BLCK/OSM_NUMBER` (**[number](#markdown-header-model-number)**) |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-DefaultApi-search_get"></a>

## operation: **search_get**
OSM - Search

[Full documentation](http://wiki.openstreetmap.org/wiki/Nominatim#Search)


### Example
```abap
*** method DefaultApi->search_get example
*** OSM - Search

  constants:
    gcc_basepath type string value 'http:// http://nominatim.openstreetmap.org'.
    
  data:  
    gvi_code type /blck/osm_int,
    gvs_msg  type /blck/osm_string.
    
*** create variables for input and output as needed
*   for parameter i_format:
*   a simple ABAP primitive of type /BLCK/OSM_STRING
    data gvs_format type /BLCK/OSM_STRING.
*   for parameter i_q:
*   a simple ABAP primitive of type /BLCK/OSM_STRING
    data gvs_q type /BLCK/OSM_STRING.
        
*** set data according to requirements of the API call
*   gvs_format = 'ipsum lorem'.
*   gvs_q = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/osm_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method search_get via HTTP GET
    /blck/osm_cl_DefaultApi=>search_get(
      exporting
        i_format = gvs_format
        i_q = gvs_q
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_format** | `/BLCK/OSM_STRING` |  
 **i_q** | `/BLCK/OSM_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


