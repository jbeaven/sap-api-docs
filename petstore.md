# API: PetApi

All URIs are relative to *https://petstore.swagger.io/v2*

## operation: **add_pet**
Add a new pet to the store


### Example
```abap
*** method PetApi->add_pet example
*** Add a new pet to the store

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/PET_PET
    data gm_body type /BLCK/PET_PET.
        
*** set data according to requirements of the API call
*   gm_body-id = 42. " (type /BLCK/PET_INT)
*   gm_body-category = l_category. " (type /BLCK/PET_CATEGORY)
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-photo_urls = l_photo_urls. " (type /BLCK/PET_STRING_TT)
*   gm_body-tags = l_tags. " (type /BLCK/PET_TAG_TT)
*   gm_body-status = 'ipsum lorem'. " (type /BLCK/PET_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method add_pet via HTTP POST
*** i_body: Pet object that needs to be added to the store
    /blck/pet_cl_PetApi=>add_pet(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 405.
*       handle code 405
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/PET_PET (**[pet](#markdown-header-model-pet)**) | Pet object that needs to be added to the store 

### Return types


### HTTP request headers

 - **Content-Type**: application/json, application/xml
 - **Accept**: Not defined


## operation: **delete_pet**
Deletes a pet


### Example
```abap
*** method PetApi->delete_pet example
*** Deletes a pet

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_pet_id:
*   a simple ABAP primitive of type /BLCK/PET_INT
    data gvi_pet_id type /BLCK/PET_INT.
*   for parameter i_api_key:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_api_key type /BLCK/PET_STRING.
        
*** set data according to requirements of the API call
*   gvi_pet_id = 42.
*   gvs_api_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method delete_pet via HTTP DELETE
*** i_pet_id: Pet id to delete
    /blck/pet_cl_PetApi=>delete_pet(
      exporting
        i_pet_id = gvi_pet_id
        i_api_key = gvs_api_key
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pet_id** | /BLCK/PET_INT | Pet id to delete 
 **i_api_key** | /BLCK/PET_STRING |  [optional]

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


## operation: **find_pets_by_status**
Finds Pets by status

Multiple status values can be provided with comma separated strings


### Example
```abap
*** method PetApi->find_pets_by_status example
*** Finds Pets by status

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_status:
*   a table type /BLCK/PET_STRING_TT
    data gi_status type /BLCK/PET_STRING_TT.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_PET_TT
    data gr_http200 type /BLCK/PET_PET_TT.
        
*** set data according to requirements of the API call
*   data lr_status like line of gi_status.
*   lr_status = ...
*   append lr_status to gi_status.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method find_pets_by_status via HTTP GET
*** i_status: Status values that need to be considered for filter
    /blck/pet_cl_PetApi=>find_pets_by_status(
      exporting
        i_status = gi_status
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_PET_TT)
      when 400.
*       handle code 400
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_status** | /BLCK/PET_STRING_TT (**[array of ](#markdown-header-enum-)**) | Status values that need to be considered for filter 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_PET_TT (**[array](#markdown-header-model-pet)**) | successful operation
 400 | value not returned |  | Invalid status value

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/xml, application/json


## operation: **find_pets_by_tags**
Finds Pets by tags

Muliple tags can be provided with comma separated strings. Use tag1, tag2, tag3 for testing.


### Example
```abap
*** method PetApi->find_pets_by_tags example
*** Finds Pets by tags

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_tags:
*   a table type /BLCK/PET_STRING_TT
    data gi_tags type /BLCK/PET_STRING_TT.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_PET_TT
    data gr_http200 type /BLCK/PET_PET_TT.
        
*** set data according to requirements of the API call
*   data lr_tags like line of gi_tags.
*   lr_tags = ...
*   append lr_tags to gi_tags.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method find_pets_by_tags via HTTP GET
*** i_tags: Tags to filter by
    /blck/pet_cl_PetApi=>find_pets_by_tags(
      exporting
        i_tags = gi_tags
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_PET_TT)
      when 400.
*       handle code 400
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_tags** | /BLCK/PET_STRING_TT (**[array of ](#markdown-header-model-)**) | Tags to filter by 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_PET_TT (**[array](#markdown-header-model-pet)**) | successful operation
 400 | value not returned |  | Invalid tag value

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/xml, application/json


## operation: **get_pet_by_id**
Find pet by ID

Returns a single pet


### Example
```abap
*** method PetApi->get_pet_by_id example
*** Find pet by ID

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_pet_id:
*   a simple ABAP primitive of type /BLCK/PET_INT
    data gvi_pet_id type /BLCK/PET_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_PET
    data gr_http200 type /BLCK/PET_PET.
        
*** set data according to requirements of the API call
*   gvi_pet_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_pet_by_id via HTTP GET
*** i_pet_id: ID of pet to return
    /blck/pet_cl_PetApi=>get_pet_by_id(
      exporting
        i_pet_id = gvi_pet_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_PET)
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pet_id** | /BLCK/PET_INT | ID of pet to return 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_PET (**[Pet](#markdown-header-model-pet)**) | successful operation
 400 | value not returned |  | Invalid ID supplied
 404 | value not returned |  | Pet not found

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/xml, application/json


## operation: **update_pet**
Update an existing pet


### Example
```abap
*** method PetApi->update_pet example
*** Update an existing pet

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/PET_PET
    data gm_body type /BLCK/PET_PET.
        
*** set data according to requirements of the API call
*   gm_body-id = 42. " (type /BLCK/PET_INT)
*   gm_body-category = l_category. " (type /BLCK/PET_CATEGORY)
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-photo_urls = l_photo_urls. " (type /BLCK/PET_STRING_TT)
*   gm_body-tags = l_tags. " (type /BLCK/PET_TAG_TT)
*   gm_body-status = 'ipsum lorem'. " (type /BLCK/PET_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method update_pet via HTTP PUT
*** i_body: Pet object that needs to be added to the store
    /blck/pet_cl_PetApi=>update_pet(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when 405.
*       handle code 405
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/PET_PET (**[pet](#markdown-header-model-pet)**) | Pet object that needs to be added to the store 

### Return types


### HTTP request headers

 - **Content-Type**: application/json, application/xml
 - **Accept**: Not defined


## operation: **update_pet_with_form**
Updates a pet in the store with form data


### Example
```abap
*** method PetApi->update_pet_with_form example
*** Updates a pet in the store with form data

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_pet_id:
*   a simple ABAP primitive of type /BLCK/PET_INT
    data gvi_pet_id type /BLCK/PET_INT.
*   for parameter i_name:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_name type /BLCK/PET_STRING.
*   for parameter i_status:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_status type /BLCK/PET_STRING.
        
*** set data according to requirements of the API call
*   gvi_pet_id = 42.
*   gvs_name = 'ipsum lorem'.
*   gvs_status = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method update_pet_with_form via HTTP POST
*** i_pet_id: ID of pet that needs to be updated
    /blck/pet_cl_PetApi=>update_pet_with_form(
      exporting
        i_pet_id = gvi_pet_id
        i_name = gvs_name
        i_status = gvs_status
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 405.
*       handle code 405
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pet_id** | /BLCK/PET_INT | ID of pet that needs to be updated 
 **i_name** | /BLCK/PET_STRING |  [optional]
 **i_status** | /BLCK/PET_STRING |  [optional]

### Return types


### HTTP request headers

 - **Content-Type**: application/x-www-form-urlencoded
 - **Accept**: Not defined


## operation: **upload_file**
uploads an image


### Example
```abap
*** method PetApi->upload_file example
*** uploads an image

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_pet_id:
*   a simple ABAP primitive of type /BLCK/PET_INT
    data gvi_pet_id type /BLCK/PET_INT.
*   for parameter i_additional_metadata:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_additional_metadata type /BLCK/PET_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/PET_BINARY
    data gvs_file type /BLCK/PET_BINARY.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_API_RESPONSE
    data gr_http200 type /BLCK/PET_API_RESPONSE.
        
*** set data according to requirements of the API call
*   gvi_pet_id = 42.
*   gvs_additional_metadata = 'ipsum lorem'.
*   gvs_file = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_PetApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method upload_file via HTTP POST
*** i_pet_id: ID of pet to update
    /blck/pet_cl_PetApi=>upload_file(
      exporting
        i_pet_id = gvi_pet_id
        i_additional_metadata = gvs_additional_metadata
        i_file = gvs_file
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_API_RESPONSE)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_pet_id** | /BLCK/PET_INT | ID of pet to update 
 **i_additional_metadata** | /BLCK/PET_STRING |  [optional]
 **i_file** | /BLCK/PET_BINARY |  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_API_RESPONSE (**[ApiResponse](#markdown-header-model-api_response)**) | successful operation

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json


# API: StoreApi

All URIs are relative to *https://petstore.swagger.io/v2*

## operation: **delete_order**
Delete purchase order by ID

For valid response try integer IDs with positive integer value. Negative or non-integer values will generate API errors


### Example
```abap
*** method StoreApi->delete_order example
*** Delete purchase order by ID

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_order_id:
*   a simple ABAP primitive of type /BLCK/PET_INT
    data gvi_order_id type /BLCK/PET_INT.
        
*** set data according to requirements of the API call
*   gvi_order_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_StoreApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method delete_order via HTTP DELETE
*** i_order_id: ID of the order that needs to be deleted
    /blck/pet_cl_StoreApi=>delete_order(
      exporting
        i_order_id = gvi_order_id
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_order_id** | /BLCK/PET_INT | ID of the order that needs to be deleted 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


## operation: **get_inventory**
Returns pet inventories by status

Returns a map of status codes to quantities


### Example
```abap
*** method StoreApi->get_inventory example
*** Returns pet inventories by status

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/PET_INT_MT
    data gr_http200 type /BLCK/PET_INT_MT.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_StoreApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_inventory via HTTP GET
    /blck/pet_cl_StoreApi=>get_inventory(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_INT_MT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_INT_MT (**[map](#markdown-header-model-)**) | successful operation

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_order_by_id**
Find purchase order by ID

For valid response try integer IDs with value >= 1 and <= 10. Other values will generated exceptions


### Example
```abap
*** method StoreApi->get_order_by_id example
*** Find purchase order by ID

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_order_id:
*   a simple ABAP primitive of type /BLCK/PET_INT
    data gvi_order_id type /BLCK/PET_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_ORDER
    data gr_http200 type /BLCK/PET_ORDER.
        
*** set data according to requirements of the API call
*   gvi_order_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_StoreApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_order_by_id via HTTP GET
*** i_order_id: ID of pet that needs to be fetched
    /blck/pet_cl_StoreApi=>get_order_by_id(
      exporting
        i_order_id = gvi_order_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_ORDER)
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_order_id** | /BLCK/PET_INT | ID of pet that needs to be fetched 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_ORDER (**[Order](#markdown-header-model-order)**) | successful operation
 400 | value not returned |  | Invalid ID supplied
 404 | value not returned |  | Order not found

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/xml, application/json


## operation: **place_order**
Place an order for a pet


### Example
```abap
*** method StoreApi->place_order example
*** Place an order for a pet

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/PET_ORDER
    data gm_body type /BLCK/PET_ORDER.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_ORDER
    data gr_http200 type /BLCK/PET_ORDER.
        
*** set data according to requirements of the API call
*   gm_body-id = 42. " (type /BLCK/PET_INT)
*   gm_body-pet_id = 42. " (type /BLCK/PET_INT)
*   gm_body-quantity = 42. " (type /BLCK/PET_INT)
*   gm_body-ship_date = l_ship_date. " (type /BLCK/PET_TIMESTAMP)
*   gm_body-status = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-complete = 'X'. " (type /BLCK/PET_BOOL)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_StoreApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method place_order via HTTP POST
*** i_body: order placed for purchasing the pet
    /blck/pet_cl_StoreApi=>place_order(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_ORDER)
      when 400.
*       handle code 400
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/PET_ORDER (**[order](#markdown-header-model-order)**) | order placed for purchasing the pet 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_ORDER (**[Order](#markdown-header-model-order)**) | successful operation
 400 | value not returned |  | Invalid Order

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/xml, application/json


# API: UserApi

All URIs are relative to *https://petstore.swagger.io/v2*

## operation: **create_user**
Create user

This can only be done by the logged in user.


### Example
```abap
*** method UserApi->create_user example
*** Create user

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/PET_USER
    data gm_body type /BLCK/PET_USER.
        
*** set data according to requirements of the API call
*   gm_body-id = 42. " (type /BLCK/PET_INT)
*   gm_body-username = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-first_name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-last_name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-email = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-password = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-phone = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-user_status = 42. " (type /BLCK/PET_INT)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method create_user via HTTP POST
*** i_body: Created user object
    /blck/pet_cl_UserApi=>create_user(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 0.
*       handle code 0
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/PET_USER (**[user](#markdown-header-model-user)**) | Created user object 

### Return types


### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: Not defined


## operation: **create_users_with_array_input**
Creates list of users with given input array


### Example
```abap
*** method UserApi->create_users_with_array_input example
*** Creates list of users with given input array

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a table type /BLCK/PET_USER_TTT
    data gi_body type /BLCK/PET_USER_TTT.
        
*** set data according to requirements of the API call
*   data lr_body like line of gi_body.
*   lr_body = ...
*   append lr_body to gi_body.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method create_users_with_array_input via HTTP POST
*** i_body: List of user object
    /blck/pet_cl_UserApi=>create_users_with_array_input(
      exporting
        i_body = gi_body
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 0.
*       handle code 0
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/PET_USER_TTT (**[array of user](#markdown-header-model-)**) | List of user object 

### Return types


### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: Not defined


## operation: **create_users_with_list_input**
Creates list of users with given input array


### Example
```abap
*** method UserApi->create_users_with_list_input example
*** Creates list of users with given input array

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a table type /BLCK/PET_USER_TTT
    data gi_body type /BLCK/PET_USER_TTT.
        
*** set data according to requirements of the API call
*   data lr_body like line of gi_body.
*   lr_body = ...
*   append lr_body to gi_body.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method create_users_with_list_input via HTTP POST
*** i_body: List of user object
    /blck/pet_cl_UserApi=>create_users_with_list_input(
      exporting
        i_body = gi_body
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 0.
*       handle code 0
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/PET_USER_TTT (**[array of user](#markdown-header-model-)**) | List of user object 

### Return types


### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: Not defined


## operation: **delete_user**
Delete user

This can only be done by the logged in user.


### Example
```abap
*** method UserApi->delete_user example
*** Delete user

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_username:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_username type /BLCK/PET_STRING.
        
*** set data according to requirements of the API call
*   gvs_username = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method delete_user via HTTP DELETE
*** i_username: The name that needs to be deleted
    /blck/pet_cl_UserApi=>delete_user(
      exporting
        i_username = gvs_username
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_username** | /BLCK/PET_STRING | The name that needs to be deleted 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


## operation: **get_user_by_name**
Get user by user name


### Example
```abap
*** method UserApi->get_user_by_name example
*** Get user by user name

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_username:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_username type /BLCK/PET_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_USER
    data gr_http200 type /BLCK/PET_USER.
        
*** set data according to requirements of the API call
*   gvs_username = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_user_by_name via HTTP GET
*** i_username: The name that needs to be fetched. Use user1 for testing. 
    /blck/pet_cl_UserApi=>get_user_by_name(
      exporting
        i_username = gvs_username
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_USER)
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_username** | /BLCK/PET_STRING | The name that needs to be fetched. Use user1 for testing.  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_USER (**[User](#markdown-header-model-user)**) | successful operation
 400 | value not returned |  | Invalid username supplied
 404 | value not returned |  | User not found

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/xml, application/json


## operation: **login_user**
Logs user into the system


### Example
```abap
*** method UserApi->login_user example
*** Logs user into the system

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_username:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_username type /BLCK/PET_STRING.
*   for parameter i_password:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_password type /BLCK/PET_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/PET_STRING
    data gr_http200 type /BLCK/PET_STRING.
        
*** set data according to requirements of the API call
*   gvs_username = 'ipsum lorem'.
*   gvs_password = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method login_user via HTTP GET
*** i_username: The user name for login
*** i_password: The password for login in clear text
    /blck/pet_cl_UserApi=>login_user(
      exporting
        i_username = gvs_username
        i_password = gvs_password
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/PET_STRING)
      when 400.
*       handle code 400
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_username** | /BLCK/PET_STRING | The user name for login 
 **i_password** | /BLCK/PET_STRING | The password for login in clear text 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/PET_STRING | successful operation
 400 | value not returned |  | Invalid username/password supplied

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/xml, application/json


## operation: **logout_user**
Logs out current logged in user session


### Example
```abap
*** method UserApi->logout_user example
*** Logs out current logged in user session

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method logout_user via HTTP GET
    /blck/pet_cl_UserApi=>logout_user(
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 0.
*       handle code 0
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


## operation: **update_user**
Updated user

This can only be done by the logged in user.


### Example
```abap
*** method UserApi->update_user example
*** Updated user

  constants:
    gcc_basepath type string value 'https://petstore.swagger.io/v2'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/pet_int,
    gvs_msg  type /blck/pet_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/PET_USER
    data gm_body type /BLCK/PET_USER.
*   for parameter i_username:
*   a simple ABAP primitive of type /BLCK/PET_STRING
    data gvs_username type /BLCK/PET_STRING.
        
*** set data according to requirements of the API call
*   gm_body-id = 42. " (type /BLCK/PET_INT)
*   gm_body-username = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-first_name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-last_name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-email = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-password = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-phone = 'ipsum lorem'. " (type /BLCK/PET_STRING)
*   gm_body-user_status = 42. " (type /BLCK/PET_INT)
*   gvs_username = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/pet_cl_UserApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method update_user via HTTP PUT
*** i_body: Updated user object
*** i_username: name that need to be updated
    /blck/pet_cl_UserApi=>update_user(
      exporting
        i_body = gm_body
        i_username = gvs_username
      importing
        e_code = gvi_code
        e_message = gvs_msg ).

*** do something with the result if applicable..
    case gvi_code.
      when 400.
*       handle code 400
      when 404.
*       handle code 404
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/PET_USER (**[user](#markdown-header-model-user)**) | Updated user object 
 **i_username** | /BLCK/PET_STRING | name that need to be updated 

### Return types


### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: Not defined


* * *
<a name="markdown-header-model-api_response"></a> 

# Model: ApiResponse



### Example
```abap
*** model api_response example

* create our variables..
    data gr_api_response type /blck/pet_api_response.
    
* instantiate model and call the setters to set values..
    gr_api_response-code = 42. " (type /BLCK/PET_INT)

    gr_api_response-type = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_api_response-message = 'ipsum lorem'. " (type /BLCK/PET_STRING)
    
* pass to example API method
    gcl_exampleapi->update_api_response(
      exporting
        i_api_response = gr_api_response ).
    		
    clear gr_api_response.
    
* fetch new instance from example API method
    gcl_exampleapi->get_api_response(
      exporting
        i_id = 1
      importing 
        e_200 = gr_api_response ).
    		
    write: gr_api_response-code. " (type /BLCK/PET_INT)
    write: gr_api_response-type. " (type /BLCK/PET_STRING)
    write: gr_api_response-message. " (type /BLCK/PET_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**code** | /BLCK/PET_INT | 
**type** | /BLCK/PET_STRING | 
**message** | /BLCK/PET_STRING | 

* * *
<a name="markdown-header-model-category"></a> 

# Model: Category



### Example
```abap
*** model category example

* create our variables..
    data gr_category type /blck/pet_category.
    
* instantiate model and call the setters to set values..
    gr_category-id = 42. " (type /BLCK/PET_INT)

    gr_category-name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
    
* pass to example API method
    gcl_exampleapi->update_category(
      exporting
        i_category = gr_category ).
    		
    clear gr_category.
    
* fetch new instance from example API method
    gcl_exampleapi->get_category(
      exporting
        i_id = 1
      importing 
        e_200 = gr_category ).
    		
    write: gr_category-id. " (type /BLCK/PET_INT)
    write: gr_category-name. " (type /BLCK/PET_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/PET_INT | 
**name** | /BLCK/PET_STRING | 

* * *
<a name="markdown-header-model-order"></a> 

# Model: Order



### Example
```abap
*** model order example

* create our variables..
    data gr_order type /blck/pet_order.
    
* instantiate model and call the setters to set values..
    gr_order-id = 42. " (type /BLCK/PET_INT)

    gr_order-pet_id = 42. " (type /BLCK/PET_INT)

    gr_order-quantity = 42. " (type /BLCK/PET_INT)

    gr_order-ship_date = l_ship_date. " (type /BLCK/PET_TIMESTAMP)

    gr_order-status = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_order-complete = 'X'. " (type /BLCK/PET_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_order(
      exporting
        i_order = gr_order ).
    		
    clear gr_order.
    
* fetch new instance from example API method
    gcl_exampleapi->get_order(
      exporting
        i_id = 1
      importing 
        e_200 = gr_order ).
    		
    write: gr_order-id. " (type /BLCK/PET_INT)
    write: gr_order-pet_id. " (type /BLCK/PET_INT)
    write: gr_order-quantity. " (type /BLCK/PET_INT)
    write: gr_order-ship_date. " (type /BLCK/PET_TIMESTAMP)
    write: gr_order-status. " (type /BLCK/PET_STRING)
    write: gr_order-complete. " (type /BLCK/PET_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/PET_INT | 
**pet_id** | /BLCK/PET_INT | 
**quantity** | /BLCK/PET_INT | 
**ship_date** | /BLCK/PET_TIMESTAMP | 
**status** | /BLCK/PET_STRING | Order Status
**complete** | /BLCK/PET_BOOL | 

* * *
<a name="markdown-header-model-tag"></a> 

# Model: Tag



### Example
```abap
*** model tag example

* create our variables..
    data gr_tag type /blck/pet_tag.
    
* instantiate model and call the setters to set values..
    gr_tag-id = 42. " (type /BLCK/PET_INT)

    gr_tag-name = 'ipsum lorem'. " (type /BLCK/PET_STRING)
    
* pass to example API method
    gcl_exampleapi->update_tag(
      exporting
        i_tag = gr_tag ).
    		
    clear gr_tag.
    
* fetch new instance from example API method
    gcl_exampleapi->get_tag(
      exporting
        i_id = 1
      importing 
        e_200 = gr_tag ).
    		
    write: gr_tag-id. " (type /BLCK/PET_INT)
    write: gr_tag-name. " (type /BLCK/PET_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/PET_INT | 
**name** | /BLCK/PET_STRING | 

* * *
<a name="markdown-header-model-pet"></a> 

# Model: Pet



### Example
```abap
*** model pet example

* create our variables..
    data gr_pet type /blck/pet_pet.
    
* instantiate model and call the setters to set values..
    gr_pet-id = 42. " (type /BLCK/PET_INT)

    gr_pet-category = l_category. " (type /BLCK/PET_CATEGORY)

    gr_pet-name = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_pet-photo_urls = l_photo_urls. " (type /BLCK/PET_STRING_TT)

    gr_pet-tags = l_tags. " (type /BLCK/PET_TAG_TT)

    gr_pet-status = 'ipsum lorem'. " (type /BLCK/PET_STRING)
    
* pass to example API method
    gcl_exampleapi->update_pet(
      exporting
        i_pet = gr_pet ).
    		
    clear gr_pet.
    
* fetch new instance from example API method
    gcl_exampleapi->get_pet(
      exporting
        i_id = 1
      importing 
        e_200 = gr_pet ).
    		
    write: gr_pet-id. " (type /BLCK/PET_INT)
    write: gr_pet-category. " (type /BLCK/PET_CATEGORY)
    write: gr_pet-name. " (type /BLCK/PET_STRING)
    write: gr_pet-photo_urls. " (type /BLCK/PET_STRING_TT)
    write: gr_pet-tags. " (type /BLCK/PET_TAG_TT)
    write: gr_pet-status. " (type /BLCK/PET_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/PET_INT | 
**category** | /BLCK/PET_CATEGORY (**[category](#markdown-header-model-category)**) | 
**name** | /BLCK/PET_STRING | 
**photo_urls** | /BLCK/PET_STRING_TT | 
**tags** | /BLCK/PET_TAG_TT (**[array of tag](#markdown-header-model-tag)**) | 
**status** | /BLCK/PET_STRING | pet status in the store

* * *
<a name="markdown-header-model-user"></a> 

# Model: User



### Example
```abap
*** model user example

* create our variables..
    data gr_user type /blck/pet_user.
    
* instantiate model and call the setters to set values..
    gr_user-id = 42. " (type /BLCK/PET_INT)

    gr_user-username = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_user-first_name = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_user-last_name = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_user-email = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_user-password = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_user-phone = 'ipsum lorem'. " (type /BLCK/PET_STRING)

    gr_user-user_status = 42. " (type /BLCK/PET_INT)
    
* pass to example API method
    gcl_exampleapi->update_user(
      exporting
        i_user = gr_user ).
    		
    clear gr_user.
    
* fetch new instance from example API method
    gcl_exampleapi->get_user(
      exporting
        i_id = 1
      importing 
        e_200 = gr_user ).
    		
    write: gr_user-id. " (type /BLCK/PET_INT)
    write: gr_user-username. " (type /BLCK/PET_STRING)
    write: gr_user-first_name. " (type /BLCK/PET_STRING)
    write: gr_user-last_name. " (type /BLCK/PET_STRING)
    write: gr_user-email. " (type /BLCK/PET_STRING)
    write: gr_user-password. " (type /BLCK/PET_STRING)
    write: gr_user-phone. " (type /BLCK/PET_STRING)
    write: gr_user-user_status. " (type /BLCK/PET_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/PET_INT | 
**username** | /BLCK/PET_STRING | 
**first_name** | /BLCK/PET_STRING | 
**last_name** | /BLCK/PET_STRING | 
**email** | /BLCK/PET_STRING | 
**password** | /BLCK/PET_STRING | 
**phone** | /BLCK/PET_STRING | 
**user_status** | /BLCK/PET_INT | User Status

