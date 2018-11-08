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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_PET_TT
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
 200 | **e_200** | /BLCK/PET_PET_TT (**[array](#markdown-header-model-)**) | successful operation
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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_PET_TT
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
 200 | **e_200** | /BLCK/PET_PET_TT (**[array](#markdown-header-model-)**) | successful operation
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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_PET
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
 200 | **e_200** | /BLCK/PET_PET (**[Pet](#markdown-header-model-)**) | successful operation
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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_API_RESPONSE
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
 200 | **e_200** | /BLCK/PET_API_RESPONSE (**[ApiResponse](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/PET_INT_MT
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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_ORDER
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
 200 | **e_200** | /BLCK/PET_ORDER (**[Order](#markdown-header-model-)**) | successful operation
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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_ORDER
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
 200 | **e_200** | /BLCK/PET_ORDER (**[Order](#markdown-header-model-)**) | successful operation
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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_USER
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
 200 | **e_200** | /BLCK/PET_USER (**[User](#markdown-header-model-)**) | successful operation
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
*   when the the result of the call is HTTP200 we expect type /BLCK/PET_STRING
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

# Model: api_response



### Example
```abap
*** model api_response example

* create our variables..
    data gcl_api_response type ref to /blck/mdl_cl_api_response.
    
* instantiate model and call the setters to set values..
    gcl_api_response = /blck/mdl_cl_api_response=>create( ).
    gcl_api_response->set_code( 42 ). " (type i)
    gcl_api_response->set_type( 'ipsum lorem' ). " (type string)
    gcl_api_response->set_message( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_api_response(
    	exporting
    		i_api_response = gcl_api_response ).
    		
    clear gcl_api_response.
    
* fetch new instance from example API method
    gcl_api_response = gcl_exampleapi->get_api_response(
    	exporting
    		i_id = 1 ).
    		
    l_code = gcl_api_response->get_code( ). " (type i)
    l_type = gcl_api_response->get_type( ). " (type string)
    l_message = gcl_api_response->get_message( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | i |  | [optional] [default to null]
**type** | string |  | [optional] [default to null]
**message** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-category"></a> 

# Model: category



### Example
```abap
*** model category example

* create our variables..
    data gcl_category type ref to /blck/mdl_cl_category.
    
* instantiate model and call the setters to set values..
    gcl_category = /blck/mdl_cl_category=>create( ).
    gcl_category->set_id( 42 ). " (type i)
    gcl_category->set_name( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_category(
    	exporting
    		i_category = gcl_category ).
    		
    clear gcl_category.
    
* fetch new instance from example API method
    gcl_category = gcl_exampleapi->get_category(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_category->get_id( ). " (type i)
    l_name = gcl_category->get_name( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-order"></a> 

# Model: order



### Example
```abap
*** model order example

* create our variables..
    data gcl_order type ref to /blck/mdl_cl_order.
    
* instantiate model and call the setters to set values..
    gcl_order = /blck/mdl_cl_order=>create( ).
    gcl_order->set_id( 42 ). " (type i)
    gcl_order->set_pet_id( 42 ). " (type i)
    gcl_order->set_quantity( 42 ). " (type i)
    gcl_order->set_ship_date( l_ship_date ). " (type timestamp)
    gcl_order->set_status( 'ipsum lorem' ). " (type string)
    gcl_order->set_complete( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_order(
    	exporting
    		i_order = gcl_order ).
    		
    clear gcl_order.
    
* fetch new instance from example API method
    gcl_order = gcl_exampleapi->get_order(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_order->get_id( ). " (type i)
    l_pet_id = gcl_order->get_pet_id( ). " (type i)
    l_quantity = gcl_order->get_quantity( ). " (type i)
    l_ship_date = gcl_order->get_ship_date( ). " (type timestamp)
    l_status = gcl_order->get_status( ). " (type string)
    l_complete = gcl_order->get_complete( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**pet_id** | i |  | [optional] [default to null]
**quantity** | i |  | [optional] [default to null]
**ship_date** | timestamp |  | [optional] [default to null]
**status** | string | Order Status | [optional] [default to null]
**complete** | flag |  | [optional] [default to false]

* * *
<a name="markdown-header-model-tag"></a> 

# Model: tag



### Example
```abap
*** model tag example

* create our variables..
    data gcl_tag type ref to /blck/mdl_cl_tag.
    
* instantiate model and call the setters to set values..
    gcl_tag = /blck/mdl_cl_tag=>create( ).
    gcl_tag->set_id( 42 ). " (type i)
    gcl_tag->set_name( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_tag(
    	exporting
    		i_tag = gcl_tag ).
    		
    clear gcl_tag.
    
* fetch new instance from example API method
    gcl_tag = gcl_exampleapi->get_tag(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_tag->get_id( ). " (type i)
    l_name = gcl_tag->get_name( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-pet"></a> 

# Model: pet



### Example
```abap
*** model pet example

* create our variables..
    data gcl_pet type ref to /blck/mdl_cl_pet.
    
* instantiate model and call the setters to set values..
    gcl_pet = /blck/mdl_cl_pet=>create( ).
    gcl_pet->set_id( 42 ). " (type i)
    gcl_pet->set_category( l_category ). " (type /BLCK/PET_category)
    gcl_pet->set_name( 'ipsum lorem' ). " (type string)
    gcl_pet->set_photo_urls( l_photo_urls ). " (type /blck/api_string_tt)
    gcl_pet->set_tags( l_tags ). " (type /BLCK/PET_tag_tt)
    gcl_pet->set_status( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_pet(
    	exporting
    		i_pet = gcl_pet ).
    		
    clear gcl_pet.
    
* fetch new instance from example API method
    gcl_pet = gcl_exampleapi->get_pet(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_pet->get_id( ). " (type i)
    l_category = gcl_pet->get_category( ). " (type /BLCK/PET_category)
    l_name = gcl_pet->get_name( ). " (type string)
    l_photo_urls = gcl_pet->get_photo_urls( ). " (type /blck/api_string_tt)
    l_tags = gcl_pet->get_tags( ). " (type /BLCK/PET_tag_tt)
    l_status = gcl_pet->get_status( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**category** | /BLCK/PET_category (**[category](#markdown-header-model-category)**) |  | [optional] [default to null]
**name** | string |  | [default to null]
**photo_urls** | /blck/api_string_tt |  | [default to null]
**tags** | /BLCK/PET_tag_tt (**[array of tag](#markdown-header-model-tag)**) |  | [optional] [default to null]
**status** | string | pet status in the store | [optional] [default to null]

* * *
<a name="markdown-header-model-user"></a> 

# Model: user



### Example
```abap
*** model user example

* create our variables..
    data gcl_user type ref to /blck/mdl_cl_user.
    
* instantiate model and call the setters to set values..
    gcl_user = /blck/mdl_cl_user=>create( ).
    gcl_user->set_id( 42 ). " (type i)
    gcl_user->set_username( 'ipsum lorem' ). " (type string)
    gcl_user->set_first_name( 'ipsum lorem' ). " (type string)
    gcl_user->set_last_name( 'ipsum lorem' ). " (type string)
    gcl_user->set_email( 'ipsum lorem' ). " (type string)
    gcl_user->set_password( 'ipsum lorem' ). " (type string)
    gcl_user->set_phone( 'ipsum lorem' ). " (type string)
    gcl_user->set_user_status( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_user(
    	exporting
    		i_user = gcl_user ).
    		
    clear gcl_user.
    
* fetch new instance from example API method
    gcl_user = gcl_exampleapi->get_user(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_user->get_id( ). " (type i)
    l_username = gcl_user->get_username( ). " (type string)
    l_first_name = gcl_user->get_first_name( ). " (type string)
    l_last_name = gcl_user->get_last_name( ). " (type string)
    l_email = gcl_user->get_email( ). " (type string)
    l_password = gcl_user->get_password( ). " (type string)
    l_phone = gcl_user->get_phone( ). " (type string)
    l_user_status = gcl_user->get_user_status( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**username** | string |  | [optional] [default to null]
**first_name** | string |  | [optional] [default to null]
**last_name** | string |  | [optional] [default to null]
**email** | string |  | [optional] [default to null]
**password** | string |  | [optional] [default to null]
**phone** | string |  | [optional] [default to null]
**user_status** | i | User Status | [optional] [default to null]

