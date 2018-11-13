# API: FavoritesApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **add_favorite**
Adds an object to the favorites.


### Example
```abap
*** method FavoritesApi->add_favorite example
*** Adds an object to the favorites.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_OBJ_ID
    data gm_body type /BLCK/MFI_OBJ_ID.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-id = 42. " (type /BLCK/MFI_INT)
*   gm_body-type = 42. " (type /BLCK/MFI_INT)
*   gm_body-external_repository_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-externalrepositoryobjectid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_FavoritesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method add_favorite via HTTP POST
    /blck/mfi_cl_FavoritesApi=>add_favorite(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJ_ID (**[ObjID](#markdown-header-model-obj_id)**) |  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **get_favorite**
Retrieves object version information on the favorite object


### Example
```abap
*** method FavoritesApi->get_favorite example
*** Retrieves object version information on the favorite object

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_objectid type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvs_objectid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_FavoritesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_favorite via HTTP GET
    /blck/mfi_cl_FavoritesApi=>get_favorite(
      exporting
        i_type = gvi_type
        i_objectid = gvs_objectid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_favorites**
Retrieves favorite objects.


### Example
```abap
*** method FavoritesApi->get_favorites example
*** Retrieves favorite objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_FavoritesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_favorites via HTTP GET
    /blck/mfi_cl_FavoritesApi=>get_favorites(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **remove_favorite**
Removes an object from favorites.


### Example
```abap
*** method FavoritesApi->remove_favorite example
*** Removes an object from favorites.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_objectid type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvs_objectid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_FavoritesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method remove_favorite via HTTP DELETE
    /blck/mfi_cl_FavoritesApi=>remove_favorite(
      exporting
        i_type = gvi_type
        i_objectid = gvs_objectid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: FilesApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **upload**
Sets the current vault.

Stores a temporary file on the server and assigns an ID for it. Once uploaded the file can be used in object creation. https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/


### Example
```abap
*** method FilesApi->upload example
*** Sets the current vault.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_body type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_UPLOAD_INFO
    data gr_http200 type /BLCK/MFI_UPLOAD_INFO.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_FilesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method upload via HTTP POST
    /blck/mfi_cl_FilesApi=>upload(
      exporting
        i_body = gvs_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_UPLOAD_INFO)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_UPLOAD_INFO (**[UploadInfo](#markdown-header-model-upload_info)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


# API: ObjectsApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **add_comment**
Adds a comment to an object


### Example
```abap
*** method ObjectsApi->add_comment example
*** Adds a comment to an object

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_body type /BLCK/MFI_STRING.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method add_comment via HTTP PUT
*** i_body: Comment to add to object
    /blck/mfi_cl_ObjectsApi=>add_comment(
      exporting
        i_body = gvs_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING | Comment to add to object 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **add_file_content**
Adds a new file to the object.


### Example
```abap
*** method ObjectsApi->add_file_content example
*** Adds a new file to the object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_body type /BLCK/MFI_STRING.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method add_file_content via HTTP PUT
*** i_body: Binary file data
    /blck/mfi_cl_ObjectsApi=>add_file_content(
      exporting
        i_body = gvs_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING | Binary file data 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **create_object**
Creates a new object of type.


### Example
```abap
*** method ObjectsApi->create_object example
*** Creates a new object of type.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_OBJECTCREATION
    data gm_body type /BLCK/MFI_OBJECTCREATION.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-property_values = l_property_values. " (type /BLCK/MFI_PROPERTY_VALUE_TT)
*   gm_body-files = l_files. " (type /BLCK/MFI_UPLOAD_INFO_TT)
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method create_object via HTTP POST
    /blck/mfi_cl_ObjectsApi=>create_object(
      exporting
        i_body = gm_body
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJECTCREATION (**[ObjectCreationInfo](#markdown-header-model-objectcreation)**) |  
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **demote_objects**
Demotes external objects that have been previously promoted.


### Example
```abap
*** method ObjectsApi->demote_objects example
*** Demotes external objects that have been previously promoted.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a table type /BLCK/MFI_OBJ_ID_TTT
    data gi_body type /BLCK/MFI_OBJ_ID_TTT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT_TT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   data lr_body like line of gi_body.
*   lr_body = ...
*   append lr_body to gi_body.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method demote_objects via HTTP PUT
*** i_body: Holds file upload ids and property values for fetching automatic metadata.
    /blck/mfi_cl_ObjectsApi=>demote_objects(
      exporting
        i_body = gi_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJ_ID_TTT (**[array of ObjID](#markdown-header-model-obj_id)**) | Holds file upload ids and property values for fetching automatic metadata. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT_TT (**[array of ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **destroy_object_version**
Destroys the object version. 

As checked in versions cannot be destroyed this can only be performed on a checked out version and is equivalent to an undo checkout. Returns the new ObjectVersion information if it is still visible to the user.


### Example
```abap
*** method ObjectsApi->destroy_object_version example
*** Destroys the object version. 

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_force:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_force type /BLCK/MFI_BOOL.
*   for parameter i_all_versions:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_all_versions type /BLCK/MFI_BOOL.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gv_force = 'X'.
*   gv_all_versions = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method destroy_object_version via HTTP DELETE
*** i_force: If  true,  DELETE  will  perform  an  undo checkout even if the object isn’t
*** checked out to the current user on this computer.
*** i_all_versions: If  true,  DELETE  will destroy the whole object. Unlike normal DELETE, this
*** will not require the object to be checked out.
    /blck/mfi_cl_ObjectsApi=>destroy_object_version(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_force = gv_force
        i_all_versions = gv_all_versions
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_force** | /BLCK/MFI_BOOL | If true, DELETE will perform an undo checkout even if the object isn’t checked out to the current user on this computer. [optional]
 **i_all_versions** | /BLCK/MFI_BOOL | If true, DELETE will destroy the whole object. Unlike normal DELETE, this will not require the object to be checked out. [optional]

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_automatic_metadata**
Retrieves automatic metadata based on specified request info.


### Example
```abap
*** method ObjectsApi->get_automatic_metadata example
*** Retrieves automatic metadata based on specified request info.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_AUTOMATICMETAD
    data gm_body type /BLCK/MFI_AUTOMATICMETAD.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTYVALUES_TT
    data gr_http200 type /BLCK/MFI_PROPERTYVALUES_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-upload_ids = l_upload_ids. " (type /BLCK/MFI_INT_TT)
*   gm_body-property_values = l_property_values. " (type /BLCK/MFI_PROPERTY_VALUE_TT)
*   gm_body-obj_ver = l_obj_ver. " (type /BLCK/MFI_OBJ_VER)
*   gm_body-object_type = 42. " (type /BLCK/MFI_INT)
*   gm_body-metadata_provider_ids = l_metadata_provider_ids. " (type /BLCK/MFI_STRING_TT)
*   gm_body-custom_data = 'ipsum lorem'. " (type /BLCK/MFI_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_automatic_metadata via HTTP POST
*** i_body: Holds file upload ids and property values for fetching automatic metadata.
    /blck/mfi_cl_ObjectsApi=>get_automatic_metadata(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTYVALUES_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_AUTOMATICMETAD (**[AutomaticMetadataRequestInfo](#markdown-header-model-automaticmetad)**) | Holds file upload ids and property values for fetching automatic metadata. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_PROPERTYVALUES_TT (**[array of PropertyValueSuggestion](#markdown-header-model-propertyvalues)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **get_checkout_status**
Retrieves the current check out status.


### Example
```abap
*** method ObjectsApi->get_checkout_status example
*** Retrieves the current check out status.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_MFCHECKOUTSTAT
    data gr_http200 type /BLCK/MFI_MFCHECKOUTSTAT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_checkout_status via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_checkout_status(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_MFCHECKOUTSTAT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_MFCHECKOUTSTAT (**[MFCheckOutStatus](#markdown-header-model-mfcheckoutstat)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_comments**
Retrieves the comments written on the object.


### Example
```abap
*** method ObjectsApi->get_comments example
*** Retrieves the comments written on the object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VERSIONCOMMENT_TT
    data gr_http200 type /BLCK/MFI_VERSIONCOMMENT_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_comments via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_comments(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VERSIONCOMMENT_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VERSIONCOMMENT_TT (**[array of VersionComment](#markdown-header-model-versioncomment)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_deleted_state**
Retrieves the deleted status of the object.


### Example
```abap
*** method ObjectsApi->get_deleted_state example
*** Retrieves the deleted status of the object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_BOOL
    data gr_http200 type /BLCK/MFI_BOOL.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_deleted_state via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_deleted_state(
      exporting
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BOOL)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_BOOL | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_file_content**
Retrieves the object file contents.


### Example
```abap
*** method ObjectsApi->get_file_content example
*** Retrieves the object file contents.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_file type /BLCK/MFI_INT.
*   for parameter i_x_hmac:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_x_hmac type /BLCK/MFI_STRING.
*   for parameter i_mac:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_mac type /BLCK/MFI_BOOL.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_file = 42.
*   gvs_x_hmac = 'ipsum lorem'.
*   gv_mac = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_file_content via HTTP GET
*** i_x_hmac: Specifies the HMAC key
*** i_mac: If  true,  appends  a  SHA-512 message authentication code at the end of the
*** stream.
    /blck/mfi_cl_ObjectsApi=>get_file_content(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_file = gvi_file
        i_x_hmac = gvs_x_hmac
        i_mac = gv_mac
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  
 **i_x_hmac** | /BLCK/MFI_STRING | Specifies the HMAC key [optional]
 **i_mac** | /BLCK/MFI_BOOL | If true, appends a SHA-512 message authentication code at the end of the stream. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_BINARY | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_file_info**
Retrieves the object file information for the specific object file.


### Example
```abap
*** method ObjectsApi->get_file_info example
*** Retrieves the object file information for the specific object file.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_file type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_FILE
    data gr_http200 type /BLCK/MFI_OBJECT_FILE.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_file = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_file_info via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_file_info(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_file = gvi_file
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_FILE)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_FILE (**[ObjectFile](#markdown-header-model-object_file)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_file_thumbnail**
Retrieves the file preview.


### Example
```abap
*** method ObjectsApi->get_file_thumbnail example
*** Retrieves the file preview.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_file type /BLCK/MFI_INT.
*   for parameter i_force:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_force type /BLCK/MFI_BOOL.
*   for parameter i_size:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_size type /BLCK/MFI_INT.
*   for parameter i_width:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_width type /BLCK/MFI_INT.
*   for parameter i_height:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_height type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_file = 42.
*   gv_force = 'X'.
*   gvi_size = 42.
*   gvi_width = 42.
*   gvi_height = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_file_thumbnail via HTTP GET
*** i_force: If  true, the server streams an empty image instead of giving a 404 response
*** if the preview cannot be generated.
*** i_size: Specifies  square  dimensions.  Defaults  to  32.  This  also works with the
*** force-parameter by forcing the empty image to have the specified dimensions.
*** i_width: Specifies preview width. Overrides size.
*** i_height: Specifies preview height. Overrides size.
    /blck/mfi_cl_ObjectsApi=>get_file_thumbnail(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_file = gvi_file
        i_force = gv_force
        i_size = gvi_size
        i_width = gvi_width
        i_height = gvi_height
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when 404.
*       handle code 404, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  
 **i_force** | /BLCK/MFI_BOOL | If true, the server streams an empty image instead of giving a 404 response if the preview cannot be generated. [optional]
 **i_size** | /BLCK/MFI_INT | Specifies square dimensions. Defaults to 32. This also works with the force-parameter by forcing the empty image to have the specified dimensions. [optional]
 **i_width** | /BLCK/MFI_INT | Specifies preview width. Overrides size. [optional]
 **i_height** | /BLCK/MFI_INT | Specifies preview height. Overrides size. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_BINARY | successful operation
 404 | value not returned |  | If a preview cannot be generated the service responds with a 404.
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_filename**
Retrieves the current object file name.


### Example
```abap
*** method ObjectsApi->get_filename example
*** Retrieves the current object file name.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_file type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_file = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_filename via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_filename(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_file = gvi_file
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_STRING | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_files_info**
Retrieves the object file information for all the files on an object.


### Example
```abap
*** method ObjectsApi->get_files_info example
*** Retrieves the object file information for all the files on an object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_FILE_TT
    data gr_http200 type /BLCK/MFI_OBJECT_FILE_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_files_info via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_files_info(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_FILE_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_FILE_TT (**[array of ObjectFile](#markdown-header-model-object_file)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_multi_obj_props**
Retrieves properties of multiple objects.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/properties/


### Example
```abap
*** method ObjectsApi->get_multi_obj_props example
*** Retrieves properties of multiple objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_object_ids:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_object_ids type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_object_ids = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_multi_obj_props via HTTP GET
*** i_object_ids: The   object   versions  are  specified,  seperated  with  semicolons,  e.g.
*** 0/5/6;0/112/latest;136/2/3
    /blck/mfi_cl_ObjectsApi=>get_multi_obj_props(
      exporting
        i_object_ids = gvs_object_ids
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_object_ids** | /BLCK/MFI_STRING | The object versions are specified, seperated with semicolons, e.g. 0/5/6;0/112/latest;136/2/3 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_name**
Retrieves the object name

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/title/


### Example
```abap
*** method ObjectsApi->get_name example
*** Retrieves the object name

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_name via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_name(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_STRING | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_object_info**
Retrieves the object information.

Parameters: ?include - A list of additional fields to include in the ExtendedObjectVersion. Currently only properties is supported. properties includes the Properties field in the returned object.


### Example
```abap
*** method ObjectsApi->get_object_info example
*** Retrieves the object information.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_include:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_include type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvs_include = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_info via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_object_info(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_include = gvs_include
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_include** | /BLCK/MFI_STRING |  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_object_thumbnail**
Retrieves the object preview.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/preview/


### Example
```abap
*** method ObjectsApi->get_object_thumbnail example
*** Retrieves the object preview.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_force:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_force type /BLCK/MFI_BOOL.
*   for parameter i_size:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_size type /BLCK/MFI_INT.
*   for parameter i_width:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_width type /BLCK/MFI_INT.
*   for parameter i_height:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_height type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gv_force = 'X'.
*   gvi_size = 42.
*   gvi_width = 42.
*   gvi_height = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_thumbnail via HTTP GET
*** i_force: If  true, the server streams an empty image instead of giving a 404 response
*** if the preview cannot be generated.
*** i_size: Specifies  square  dimensions.  Defaults  to  32.  This  also works with the
*** force-parameter by forcing the empty image to have the specified dimensions.
*** i_width: Specifies preview width. Overrides size.
*** i_height: Specifies preview height. Overrides size.
    /blck/mfi_cl_ObjectsApi=>get_object_thumbnail(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_force = gv_force
        i_size = gvi_size
        i_width = gvi_width
        i_height = gvi_height
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when 404.
*       handle code 404, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_force** | /BLCK/MFI_BOOL | If true, the server streams an empty image instead of giving a 404 response if the preview cannot be generated. [optional]
 **i_size** | /BLCK/MFI_INT | Specifies square dimensions. Defaults to 32. This also works with the force-parameter by forcing the empty image to have the specified dimensions. [optional]
 **i_width** | /BLCK/MFI_INT | Specifies preview width. Overrides size. [optional]
 **i_height** | /BLCK/MFI_INT | Specifies preview height. Overrides size. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_BINARY | successful operation
 404 | value not returned |  | If a preview cannot be generated the service responds with a 404.
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_object_versions**
Retrieves all the available versions of the object.


### Example
```abap
*** method ObjectsApi->get_object_versions example
*** Retrieves all the available versions of the object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_versions via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_object_versions(
      exporting
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_objects**
Retrieves objects.

The amount of returned objects is limited by the server, by default to 500 items.


### Example
```abap
*** method ObjectsApi->get_objects example
*** Retrieves objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSOBJECTV
    data gr_http200 type /BLCK/MFI_RESULTSOBJECTV.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_objects via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_objects(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSOBJECTV)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_RESULTSOBJECTV (**[ResultsObjectVersion](#markdown-header-model-resultsobjectv)**) | Retrieves objects. The amount of returned objects is limited by the server, by default to 500 items.
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_objects_of_type**
Collection of objects filtered by object type.


### Example
```abap
*** method ObjectsApi->get_objects_of_type example
*** Collection of objects filtered by object type.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSOBJECTV
    data gr_http200 type /BLCK/MFI_RESULTSOBJECTV.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_objects_of_type via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_objects_of_type(
      exporting
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSOBJECTV)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_RESULTSOBJECTV (**[ResultsObjectVersion](#markdown-header-model-resultsobjectv)**) | Retrieves objects of the given type. The amount of returned objects is limited by the server.
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_properties**
Retrieves the object properties

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/properties/


### Example
```abap
*** method ObjectsApi->get_properties example
*** Retrieves the object properties

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_for_display:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_for_display type /BLCK/MFI_BOOL.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_VALUE_TT
    data gr_http200 type /BLCK/MFI_PROPERTY_VALUE_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gv_for_display = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_properties via HTTP GET
*** i_for_display: If  true,  the response will be filtered and sorted for display. Each object
*** has several built-in properties which usually aren’t shown to the user. This
*** parameter can be used to leave those out.
    /blck/mfi_cl_ObjectsApi=>get_properties(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_for_display = gv_for_display
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_VALUE_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_for_display** | /BLCK/MFI_BOOL | If true, the response will be filtered and sorted for display. Each object has several built-in properties which usually aren’t shown to the user. This parameter can be used to leave those out. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_PROPERTY_VALUE_TT (**[array of PropertyValue](#markdown-header-model-property_value)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_property**
Retrieves a single property value

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/properties/id/


### Example
```abap
*** method ObjectsApi->get_property example
*** Retrieves a single property value

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_VALUE
    data gr_http200 type /BLCK/MFI_PROPERTY_VALUE.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_property via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_property(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_VALUE)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-property_value)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_relationship_count**
Retrieves the number of related objects.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/relationships/count/


### Example
```abap
*** method ObjectsApi->get_relationship_count example
*** Retrieves the number of related objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_objtype:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objtype type /BLCK/MFI_INT.
*   for parameter i_direction:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_direction type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_objtype = 42.
*   gvs_direction = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_relationship_count via HTTP GET
*** i_objtype: Only returns related objects of a certain object type.
*** i_direction: Only  returns  related objects with the specified direction of relationship.
*** from  considers  only  the relationships specified on the current object. to
*** considers  only  the  relationships  originating  from  the related objects.
*** ‘both’ is the default behaviour which considers both directions.
    /blck/mfi_cl_ObjectsApi=>get_relationship_count(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_objtype = gvi_objtype
        i_direction = gvs_direction
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_objtype** | /BLCK/MFI_INT | Only returns related objects of a certain object type. [optional]
 **i_direction** | /BLCK/MFI_STRING | Only returns related objects with the specified direction of relationship. from considers only the relationships specified on the current object. to considers only the relationships originating from the related objects. ‘both’ is the default behaviour which considers both directions. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_INT | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_relationships**
Retrieves related objects.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/relationships/


### Example
```abap
*** method ObjectsApi->get_relationships example
*** Retrieves related objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_objtype:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objtype type /BLCK/MFI_INT.
*   for parameter i_direction:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_direction type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_objtype = 42.
*   gvs_direction = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_relationships via HTTP GET
*** i_objtype: Only returns related objects of a certain object type.
*** i_direction: Only  returns  related objects with the specified direction of relationship.
*** from  considers  only  the relationships specified on the current object. to
*** considers  only  the  relationships  originating  from  the related objects.
*** ‘both’ is the default behaviour which considers both directions.
    /blck/mfi_cl_ObjectsApi=>get_relationships(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_objtype = gvi_objtype
        i_direction = gvs_direction
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_objtype** | /BLCK/MFI_INT | Only returns related objects of a certain object type. [optional]
 **i_direction** | /BLCK/MFI_STRING | Only returns related objects with the specified direction of relationship. from considers only the relationships specified on the current object. to considers only the relationships originating from the related objects. ‘both’ is the default behaviour which considers both directions. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_state**
Retrieves the current workflow state.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/workflowstate/


### Example
```abap
*** method ObjectsApi->get_state example
*** Retrieves the current workflow state.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECTWORKFLOW
    data gr_http200 type /BLCK/MFI_OBJECTWORKFLOW.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_state via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_state(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECTWORKFLOW)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECTWORKFLOW (**[ObjectWorkflowState](#markdown-header-model-objectworkflow)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_sub_object_count**
Retrieves the number of sub-objects.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/subobjects/count/


### Example
```abap
*** method ObjectsApi->get_sub_object_count example
*** Retrieves the number of sub-objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_sub_object_count via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_sub_object_count(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_INT | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_sub_objects**
Retrieves a collection of sub-objects.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/subobjects/


### Example
```abap
*** method ObjectsApi->get_sub_objects example
*** Retrieves a collection of sub-objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_sub_objects via HTTP GET
    /blck/mfi_cl_ObjectsApi=>get_sub_objects(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **remove_file**
Removes the file from the object.


### Example
```abap
*** method ObjectsApi->remove_file example
*** Removes the file from the object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_file type /BLCK/MFI_INT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_file = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method remove_file via HTTP DELETE
    /blck/mfi_cl_ObjectsApi=>remove_file(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_file = gvi_file
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 203.
*       handle code 203, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **remove_property**
Removes a single property value

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/properties/id/


### Example
```abap
*** method ObjectsApi->remove_property example
*** Removes a single property value

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method remove_property via HTTP DELETE
    /blck/mfi_cl_ObjectsApi=>remove_property(
      exporting
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **set_checkout_status**
Sets the check out status. This is allowed only when the object isn't checked out to someone else, that is when the check out status isn't CheckedOut.


### Example
```abap
*** method ObjectsApi->set_checkout_status example
*** Sets  the  check  out  status.  This  is  allowed only when the object isn&#x27;t
*** checked  out  to  someone  else,  that  is  when  the check out status isn&#x27;t
*** CheckedOut.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_body type /BLCK/MFI_INT.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP204 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http204 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_body = 42.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_checkout_status via HTTP PUT
    /blck/mfi_cl_ObjectsApi=>set_checkout_status(
      exporting
        i_body = gvi_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_204 = gr_http204
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       do something with gr_http204 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_INT |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 204 | **e_code_204** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_deleted_state**
Sets the deleted status of the object.


### Example
```abap
*** method ObjectsApi->set_deleted_state example
*** Sets the deleted status of the object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_body type /BLCK/MFI_BOOL.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gv_body = 'X'.
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_deleted_state via HTTP POST
    /blck/mfi_cl_ObjectsApi=>set_deleted_state(
      exporting
        i_body = gv_body
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_BOOL |  
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_file_contents**
Replaces the object file contents.


### Example
```abap
*** method ObjectsApi->set_file_contents example
*** Replaces the object file contents.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_body type /BLCK/MFI_STRING.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_file type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_file = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_file_contents via HTTP PUT
*** i_body: Binary file data
    /blck/mfi_cl_ObjectsApi=>set_file_contents(
      exporting
        i_body = gvs_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_file = gvi_file
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING | Binary file data 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_filename**
Sets the name on the object file.


### Example
```abap
*** method ObjectsApi->set_filename example
*** Sets the name on the object file.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_body type /BLCK/MFI_STRING.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_file:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_file type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_file = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_filename via HTTP PUT
*** i_body: New filename for file
    /blck/mfi_cl_ObjectsApi=>set_filename(
      exporting
        i_body = gvs_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_file = gvi_file
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING | New filename for file 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_multi_obj_props**
Sets properties in multiple objects in one HTTP call. Can also be used to promote an unmanaged external object.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/setmultipleobjproperties/


### Example
```abap
*** method ObjectsApi->set_multi_obj_props example
*** Sets  properties  in  multiple objects in one HTTP call. Can also be used to
*** promote an unmanaged external object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_OBJECTSUPDATEI
    data gm_body type /BLCK/MFI_OBJECTSUPDATEI.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT_TT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-multiple_object_info = l_multiple_object_info. " (type /BLCK/MFI_OBJECTVERSIONU)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_multi_obj_props via HTTP PUT
    /blck/mfi_cl_ObjectsApi=>set_multi_obj_props(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJECTSUPDATEI (**[ObjectsUpdateInfo](#markdown-header-model-objectsupdatei)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT_TT (**[array of ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_name**
Sets the object name

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/title/


### Example
```abap
*** method ObjectsApi->set_name example
*** Sets the object name

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_body type /BLCK/MFI_STRING.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_name via HTTP PUT
*** i_body: New name for object
    /blck/mfi_cl_ObjectsApi=>set_name(
      exporting
        i_body = gvs_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when 401.
*       handle code 401, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING | New name for object 
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 401 | value not returned |  | If the object has an automatic title PUT will result in 401.
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_properties**
Sets the object properties. Properties not included in the request are removed from the object.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/properties/


### Example
```abap
*** method ObjectsApi->set_properties example
*** Sets  the  object  properties.  Properties  not  included in the request are
*** removed from the object.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a table type /BLCK/MFI_PROPERTY_VALUE_TTT
    data gi_body type /BLCK/MFI_PROPERTY_VALUE_TTT.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   data lr_body like line of gi_body.
*   lr_body = ...
*   append lr_body to gi_body.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_properties via HTTP PUT
    /blck/mfi_cl_ObjectsApi=>set_properties(
      exporting
        i_body = gi_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_PROPERTY_VALUE_TTT (**[array of PropertyValue](#markdown-header-model-property_value)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_property**
  Sets a single property value

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/properties/id/


### Example
```abap
*** method ObjectsApi->set_property example
***   Sets a single property value

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_PROPERTY_VALUE
    data gm_body type /BLCK/MFI_PROPERTY_VALUE.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-property_def = 42. " (type /BLCK/MFI_INT)
*   gm_body-typed_value = l_typed_value. " (type /BLCK/MFI_TYPED_VALUE)
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.
*   gvi_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_property via HTTP PUT
    /blck/mfi_cl_ObjectsApi=>set_property(
      exporting
        i_body = gm_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-property_value)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_workflow_state**
Sets the workflow state.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/workflowstate/


### Example
```abap
*** method ObjectsApi->set_workflow_state example
*** Sets the workflow state.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_OBJECTWORKFLOW
    data gm_body type /BLCK/MFI_OBJECTWORKFLOW.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-state = l_state. " (type /BLCK/MFI_PROPERTY_VALUE)
*   gm_body-state_id = 42. " (type /BLCK/MFI_INT)
*   gm_body-state_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-workflow = l_workflow. " (type /BLCK/MFI_PROPERTY_VALUE)
*   gm_body-workflow_id = 42. " (type /BLCK/MFI_INT)
*   gm_body-workflow_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-version_comment = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_workflow_state via HTTP PUT
    /blck/mfi_cl_ObjectsApi=>set_workflow_state(
      exporting
        i_body = gm_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when 401.
*       handle code 401, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJECTWORKFLOW (**[ObjectWorkflowState](#markdown-header-model-objectworkflow)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 401 | value not returned |  | If the object has an automatic workflow state PUT will result in 401.
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **update_properties**
Sets the posted properties on the object. If the object already has a value for the sent properties this value will be overridden.

https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/type/objectid/version/properties/


### Example
```abap
*** method ObjectsApi->update_properties example
*** Sets  the posted properties on the object. If the object already has a value
*** for the sent properties this value will be overridden.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a table type /BLCK/MFI_PROPERTY_VALUE_TTT
    data gi_body type /BLCK/MFI_PROPERTY_VALUE_TTT.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   for parameter i_version:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_version type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   data lr_body like line of gi_body.
*   lr_body = ...
*   append lr_body to gi_body.
*   gvi_type = 42.
*   gvi_objectid = 42.
*   gvs_version = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ObjectsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method update_properties via HTTP POST
    /blck/mfi_cl_ObjectsApi=>update_properties(
      exporting
        i_body = gi_body
        i_type = gvi_type
        i_objectid = gvi_objectid
        i_version = gvs_version
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_PROPERTY_VALUE_TTT (**[array of PropertyValue](#markdown-header-model-property_value)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


# API: RecentApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **add_recent_object**
Notifies object access and adds the object to the recently accessed objects.

https://developer.m-files.com/APIs/REST-API/Reference/resources/recentlyaccessedbyme/


### Example
```abap
*** method RecentApi->add_recent_object example
*** Notifies object access and adds the object to the recently accessed objects.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_OBJ_ID
    data gm_body type /BLCK/MFI_OBJ_ID.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-id = 42. " (type /BLCK/MFI_INT)
*   gm_body-type = 42. " (type /BLCK/MFI_INT)
*   gm_body-external_repository_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-externalrepositoryobjectid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_RecentApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method add_recent_object via HTTP POST
    /blck/mfi_cl_RecentApi=>add_recent_object(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJ_ID (**[ObjID](#markdown-header-model-obj_id)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-extendedobject)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **get_recent_objects**
A collection of objects recently accessed by the current user.

https://developer.m-files.com/APIs/REST-API/Reference/resources/recentlyaccessedbyme/


### Example
```abap
*** method RecentApi->get_recent_objects example
*** A collection of objects recently accessed by the current user.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_RecentApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_recent_objects via HTTP GET
    /blck/mfi_cl_RecentApi=>get_recent_objects(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: RepositoriesApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **get_repositories**
Array of repository authentication target objects showing the current external repository connections and their authentication states.

https://developer.m-files.com/APIs/REST-API/Reference/resources/repositories/


### Example
```abap
*** method RepositoriesApi->get_repositories example
*** Array  of  repository  authentication  target  objects  showing  the current
*** external repository connections and their authentication states.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_REPOSITORYAUTH_TT
    data gr_http200 type /BLCK/MFI_REPOSITORYAUTH_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_RepositoriesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_repositories via HTTP GET
    /blck/mfi_cl_RepositoriesApi=>get_repositories(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_REPOSITORYAUTH_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_REPOSITORYAUTH_TT (**[array of RepositoryAuthenticationTarget](#markdown-header-model-repositoryauth)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **log_in_repo**
Logs into the specified external repository connection using the provided authentication data.

https://developer.m-files.com/APIs/REST-API/Reference/resources/repositories/session/


### Example
```abap
*** method RepositoriesApi->log_in_repo example
*** Logs  into  the  specified external repository connection using the provided
*** authentication data.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_REPOSITORYAUT3
    data gm_body type /BLCK/MFI_REPOSITORYAUT3.
*   for parameter i_targetid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_targetid type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_REPOSITORYAUT2
    data gr_http200 type /BLCK/MFI_REPOSITORYAUT2.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-configuration_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-username = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-password = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-authentication_token = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-refresh_token = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gvi_targetid = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_RepositoriesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method log_in_repo via HTTP POST
    /blck/mfi_cl_RepositoriesApi=>log_in_repo(
      exporting
        i_body = gm_body
        i_targetid = gvi_targetid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_REPOSITORYAUT2)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_REPOSITORYAUT3 (**[RepositoryAuthentication](#markdown-header-model-repositoryaut3)**) |  
 **i_targetid** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_REPOSITORYAUT2 (**[RepositoryAuthenticationStatus](#markdown-header-model-repositoryaut2)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **log_out_repo**
Logs out from specified external repository connection.

https://developer.m-files.com/APIs/REST-API/Reference/resources/repositories/session/


### Example
```abap
*** method RepositoriesApi->log_out_repo example
*** Logs out from specified external repository connection.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_targetid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_targetid type /BLCK/MFI_INT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_targetid = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_RepositoriesApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method log_out_repo via HTTP DELETE
    /blck/mfi_cl_RepositoriesApi=>log_out_repo(
      exporting
        i_targetid = gvi_targetid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_targetid** | /BLCK/MFI_INT |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: ServerApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **authenticate**
Creates a new authentication token based on the authentication information. See Getting started for more information on authenticating.

https://developer.m-files.com/APIs/REST-API/Reference/resources/server/authenticationtokens/


### Example
```abap
*** method ServerApi->authenticate example
*** Creates  a new authentication token based on the authentication information.
*** See Getting started for more information on authenticating.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_AUTHENTICATION
    data gm_body type /BLCK/MFI_AUTHENTICATION.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-username = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-password = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-domain = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-windows_user = 'X'. " (type /BLCK/MFI_BOOL)
*   gm_body-computer_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-vault_guid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-expiration = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-read_only = 'X'. " (type /BLCK/MFI_BOOL)
*   gm_body-url = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-method = 'ipsum lorem'. " (type /BLCK/MFI_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ServerApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method authenticate via HTTP POST
    /blck/mfi_cl_ServerApi=>authenticate(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_AUTHENTICATION (**[Authentication](#markdown-header-model-authentication)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_STRING | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **get_public_key**
Used to encrypt secure information before sending it to the server.

https://developer.m-files.com/APIs/REST-API/Reference/resources/server/publickey/


### Example
```abap
*** method ServerApi->get_public_key example
*** Used to encrypt secure information before sending it to the server.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_PUBLIC_KEY
    data gr_http200 type /BLCK/MFI_PUBLIC_KEY.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ServerApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_public_key via HTTP GET
    /blck/mfi_cl_ServerApi=>get_public_key(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PUBLIC_KEY)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_PUBLIC_KEY (**[PublicKey](#markdown-header-model-public_key)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_status**
Retrieves the server status. If the M-Files server is unavailable the service responds with 503.

https://developer.m-files.com/APIs/REST-API/Reference/resources/server/status/


### Example
```abap
*** method ServerApi->get_status example
*** Retrieves  the  server  status.  If  the  M-Files  server is unavailable the
*** service responds with 503.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_STATUSRESPONSE
    data gr_http200 type /BLCK/MFI_STATUSRESPONSE.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ServerApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_status via HTTP GET
    /blck/mfi_cl_ServerApi=>get_status(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STATUSRESPONSE)
      when 503.
*       handle code 503, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_STATUSRESPONSE (**[StatusResponse](#markdown-header-model-statusresponse)**) | successful operation
 503 | value not returned |  | the M-Files server is unavailable
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_vaults**
Retrieves the vaults from the server

https://developer.m-files.com/APIs/REST-API/Reference/resources/server/vaults/


### Example
```abap
*** method ServerApi->get_vaults example
*** Retrieves the vaults from the server

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_online:
*   a simple ABAP primitive of type /BLCK/MFI_BOOL
    data gv_online type /BLCK/MFI_BOOL.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_REPOSITORYAUTH_TT
    data gr_http200 type /BLCK/MFI_REPOSITORYAUTH_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gv_online = 'X'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ServerApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_vaults via HTTP GET
*** i_online: If true, return only online vaults.
    /blck/mfi_cl_ServerApi=>get_vaults(
      exporting
        i_online = gv_online
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_REPOSITORYAUTH_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_online** | /BLCK/MFI_BOOL | If true, return only online vaults. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_REPOSITORYAUTH_TT (**[array of RepositoryAuthenticationTarget](#markdown-header-model-repositoryauth)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: SessionApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **get_auth_token**
Retrieves the authentication token for the current session.

https://developer.m-files.com/APIs/REST-API/Reference/resources/session/authenticationtoken/


### Example
```abap
*** method SessionApi->get_auth_token example
*** Retrieves the authentication token for the current session.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_SessionApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_auth_token via HTTP GET
    /blck/mfi_cl_SessionApi=>get_auth_token(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_STRING | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_session_info**
Retrieves the current session information.

https://developer.m-files.com/APIs/REST-API/Reference/resources/session/


### Example
```abap
*** method SessionApi->get_session_info example
*** Retrieves the current session information.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_SESSION_INFO
    data gr_http200 type /BLCK/MFI_SESSION_INFO.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_SessionApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_session_info via HTTP GET
    /blck/mfi_cl_SessionApi=>get_session_info(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_SESSION_INFO)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_SESSION_INFO (**[SessionInfo](#markdown-header-model-session_info)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_user_id**
Returns current logged in user ID.

https://developer.m-files.com/APIs/REST-API/Reference/resources/session/userid/


### Example
```abap
*** method SessionApi->get_user_id example
*** Returns current logged in user ID.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_PRIMITIVETYPEI
    data gr_http200 type /BLCK/MFI_PRIMITIVETYPEI.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_SessionApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_user_id via HTTP GET
    /blck/mfi_cl_SessionApi=>get_user_id(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PRIMITIVETYPEI)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_PRIMITIVETYPEI (**[PrimitiveTypeInt](#markdown-header-model-primitivetypei)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_vault_info**
Retrieves the current session information.

https://developer.m-files.com/APIs/REST-API/Reference/resources/session/vault/


### Example
```abap
*** method SessionApi->get_vault_info example
*** Retrieves the current session information.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VAULT
    data gr_http200 type /BLCK/MFI_VAULT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_SessionApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_vault_info via HTTP GET
    /blck/mfi_cl_SessionApi=>get_vault_info(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VAULT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VAULT (**[Vault](#markdown-header-model-vault)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **log_in**
Performs login using the credentials in the request.

https://developer.m-files.com/APIs/REST-API/Reference/resources/session/


### Example
```abap
*** method SessionApi->log_in example
*** Performs login using the credentials in the request.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_AUTHENTICATION
    data gm_body type /BLCK/MFI_AUTHENTICATION.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VAULT_TT
    data gr_http200 type /BLCK/MFI_VAULT_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-username = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-password = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-domain = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-windows_user = 'X'. " (type /BLCK/MFI_BOOL)
*   gm_body-computer_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-vault_guid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-expiration = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-read_only = 'X'. " (type /BLCK/MFI_BOOL)
*   gm_body-url = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-method = 'ipsum lorem'. " (type /BLCK/MFI_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_SessionApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method log_in via HTTP PUT
    /blck/mfi_cl_SessionApi=>log_in(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VAULT_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_AUTHENTICATION (**[Authentication](#markdown-header-model-authentication)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VAULT_TT (**[array of Vault](#markdown-header-model-vault)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **log_out**
Performs a logout for the session.

https://developer.m-files.com/APIs/REST-API/Reference/resources/session/


### Example
```abap
*** method SessionApi->log_out example
*** Performs a logout for the session.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_SessionApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method log_out via HTTP DELETE
    /blck/mfi_cl_SessionApi=>log_out(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **set_vault_info**
Sets the current vault.

The request must have either the GUID or the Name of the vault filled. In case both of these are filled the GUID is used. If only the name is filled and there are multiple vaults with the same name, the server will respond with 409. https://developer.m-files.com/APIs/REST-API/Reference/resources/session/vault/


### Example
```abap
*** method SessionApi->set_vault_info example
*** Sets the current vault.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_VAULT
    data gm_body type /BLCK/MFI_VAULT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VAULT
    data gr_http200 type /BLCK/MFI_VAULT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-guid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-authentication = 'ipsum lorem'. " (type /BLCK/MFI_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_SessionApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_vault_info via HTTP PUT
    /blck/mfi_cl_SessionApi=>set_vault_info(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VAULT)
      when 409.
*       handle code 409, e_message => gvs_msg
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_VAULT (**[Vault](#markdown-header-model-vault)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VAULT (**[Vault](#markdown-header-model-vault)**) | successful operation
 409 | value not returned |  | there are multiple vaults with the same name
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


# API: VaultApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **add_item**
Creates a new value list item in the value list.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/id/items/


### Example
```abap
*** method VaultApi->add_item example
*** Creates a new value list item in the value list.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/MFI_VALUELISTITEM
    data gm_body type /BLCK/MFI_VALUELISTITEM.
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
    data gr_http200 type /BLCK/MFI_VALUELISTITEM.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gm_body-display_id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-has_owner = 'X'. " (type /BLCK/MFI_BOOL)
*   gm_body-has_parent = 'X'. " (type /BLCK/MFI_BOOL)
*   gm_body-id = 42. " (type /BLCK/MFI_INT)
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
*   gm_body-owner_id = 42. " (type /BLCK/MFI_INT)
*   gm_body-parent_id = 42. " (type /BLCK/MFI_INT)
*   gm_body-value_list_id = 42. " (type /BLCK/MFI_INT)
*   gvi_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method add_item via HTTP POST
    /blck/mfi_cl_VaultApi=>add_item(
      exporting
        i_body = gm_body
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VALUELISTITEM)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-valuelistitem)**) |  
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-valuelistitem)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **get_class_icon**
Retrieves the object class icon.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/classes/id/icon/


### Example
```abap
*** method VaultApi->get_class_icon example
*** Retrieves the object class icon.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_size:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_size type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvi_size = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_class_icon via HTTP GET
*** i_size: Icon dimension. Default is 16.
    /blck/mfi_cl_VaultApi=>get_class_icon(
      exporting
        i_id = gvi_id
        i_size = gvi_size
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_size** | /BLCK/MFI_INT | Icon dimension. Default is 16. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_BINARY | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/png


## operation: **get_class_id**
Retrieves the ID of the class with the given GUID.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/classes/itemidbyguid/


### Example
```abap
*** method VaultApi->get_class_id example
*** Retrieves the ID of the class with the given GUID.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_guid:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_guid type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_guid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_class_id via HTTP GET
    /blck/mfi_cl_VaultApi=>get_class_id(
      exporting
        i_guid = gvs_guid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_guid** | /BLCK/MFI_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_INT | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_class_info**
Retrieves information on an object class.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/classes/id/


### Example
```abap
*** method VaultApi->get_class_info example
*** Retrieves information on an object class.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_include:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_include type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJEC2
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJEC2.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvs_include = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_class_info via HTTP GET
*** i_include: Comma  separated  list  of  additional  data  sets to return. Currently only
*** templates  is supported which will will cause the response to include a list
*** of available templates available to the class.
    /blck/mfi_cl_VaultApi=>get_class_info(
      exporting
        i_id = gvi_id
        i_include = gvs_include
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJEC2)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_include** | /BLCK/MFI_STRING | Comma separated list of additional data sets to return. Currently only templates is supported which will will cause the response to include a list of available templates available to the class. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_EXTENDEDOBJEC2 (**[ExtendedObjectClass](#markdown-header-model-extendedobjec2)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_item**
Retrieves a single value list item information.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/id/items/objectid/


### Example
```abap
*** method VaultApi->get_item example
*** Retrieves a single value list item information.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
    data gr_http200 type /BLCK/MFI_VALUELISTITEM.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvi_objectid = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_item via HTTP GET
    /blck/mfi_cl_VaultApi=>get_item(
      exporting
        i_id = gvi_id
        i_objectid = gvi_objectid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VALUELISTITEM)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-valuelistitem)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_item_title**
Retrieves the value list item title.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/id/items/objectid/title/


### Example
```abap
*** method VaultApi->get_item_title example
*** Retrieves the value list item title.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvi_objectid = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_item_title via HTTP GET
    /blck/mfi_cl_VaultApi=>get_item_title(
      exporting
        i_id = gvi_id
        i_objectid = gvi_objectid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_STRING | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_items**
Retrieves value list item information.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/id/items/


### Example
```abap
*** method VaultApi->get_items example
*** Retrieves value list item information.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_filter:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_filter type /BLCK/MFI_STRING.
*   for parameter i_filter_item:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_filter_item type /BLCK/MFI_STRING.
*   for parameter i_condition_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_condition_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSVALUELI
    data gr_http200 type /BLCK/MFI_RESULTSVALUELI.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvs_filter = 'ipsum lorem'.
*   gvs_filter_item = 'ipsum lorem'.
*   gvi_condition_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_items via HTTP GET
*** i_filter: Filter using name. Supports wildcards.
*** i_filter_item: Filter using name. Supports wildcards.
*** i_condition_type: One  of  the  following  values:  1  =  'Equal  to', 2 = 'Not equal to', 3 =
*** 'Greater than', 4 = 'Less than.
    /blck/mfi_cl_VaultApi=>get_items(
      exporting
        i_id = gvi_id
        i_filter = gvs_filter
        i_filter_item = gvs_filter_item
        i_condition_type = gvi_condition_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSVALUELI)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_filter** | /BLCK/MFI_STRING | Filter using name. Supports wildcards. [optional]
 **i_filter_item** | /BLCK/MFI_STRING | Filter using name. Supports wildcards. [optional]
 **i_condition_type** | /BLCK/MFI_INT | One of the following values: 1 &#x3D; &#x27;Equal to&#x27;, 2 &#x3D; &#x27;Not equal to&#x27;, 3 &#x3D; &#x27;Greater than&#x27;, 4 &#x3D; &#x27;Less than. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_RESULTSVALUELI (**[ResultsValueListItem](#markdown-header-model-resultsvalueli)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_object_classes**
Retrieves information on all object classes.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/classes/


### Example
```abap
*** method VaultApi->get_object_classes example
*** Retrieves information on all object classes.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_objtype:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objtype type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_CLASS_TT
    data gr_http200 type /BLCK/MFI_OBJECT_CLASS_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_objtype = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_classes via HTTP GET
*** i_objtype: Object  type  ID.  Filters the returned classes by object type. Only classes
*** belonging to the object type are returned.
    /blck/mfi_cl_VaultApi=>get_object_classes(
      exporting
        i_objtype = gvi_objtype
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_CLASS_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_objtype** | /BLCK/MFI_INT | Object type ID. Filters the returned classes by object type. Only classes belonging to the object type are returned. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_CLASS_TT (**[array of ObjectClass](#markdown-header-model-object_class)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_object_type**
Retrieves information on an object type.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/objecttypes/type/


### Example
```abap
*** method VaultApi->get_object_type example
*** Retrieves information on an object type.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE
    data gr_http200 type /BLCK/MFI_OBJ_TYPE.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_type via HTTP GET
    /blck/mfi_cl_VaultApi=>get_object_type(
      exporting
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJ_TYPE (**[ObjType](#markdown-header-model-obj_type)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_object_type_classes**
Retrieves a collection of object classes for the provided object type.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/objecttypes/type/classes/


### Example
```abap
*** method VaultApi->get_object_type_classes example
*** Retrieves a collection of object classes for the provided object type.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_CLASS_TT
    data gr_http200 type /BLCK/MFI_OBJECT_CLASS_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_type_classes via HTTP GET
    /blck/mfi_cl_VaultApi=>get_object_type_classes(
      exporting
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_CLASS_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJECT_CLASS_TT (**[array of ObjectClass](#markdown-header-model-object_class)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_object_type_icon**
Retrieves the object type icon.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/objecttypes/type/icon/


### Example
```abap
*** method VaultApi->get_object_type_icon example
*** Retrieves the object type icon.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_type_icon via HTTP GET
    /blck/mfi_cl_VaultApi=>get_object_type_icon(
      exporting
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_BINARY | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/png


## operation: **get_object_types**
Retrieves information on real object types.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/objecttypes/


### Example
```abap
*** method VaultApi->get_object_types example
*** Retrieves information on real object types.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE_TT
    data gr_http200 type /BLCK/MFI_OBJ_TYPE_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_object_types via HTTP GET
    /blck/mfi_cl_VaultApi=>get_object_types(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJ_TYPE_TT (**[array of ObjType](#markdown-header-model-obj_type)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_value_list**
Retrieves information on a single value list.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/id/


### Example
```abap
*** method VaultApi->get_value_list example
*** Retrieves information on a single value list.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE
    data gr_http200 type /BLCK/MFI_OBJ_TYPE.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_value_list via HTTP GET
    /blck/mfi_cl_VaultApi=>get_value_list(
      exporting
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJ_TYPE (**[ObjType](#markdown-header-model-obj_type)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_value_lists**
  Retrieves information on all value lists.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/


### Example
```abap
*** method VaultApi->get_value_lists example
***   Retrieves information on all value lists.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE_TT
    data gr_http200 type /BLCK/MFI_OBJ_TYPE_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_value_lists via HTTP GET
    /blck/mfi_cl_VaultApi=>get_value_lists(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_OBJ_TYPE_TT (**[array of ObjType](#markdown-header-model-obj_type)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_vault_properties**
Retrieves information on all property definitions.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/properties/


### Example
```abap
*** method VaultApi->get_vault_properties example
*** Retrieves information on all property definitions.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_DEF_TT
    data gr_http200 type /BLCK/MFI_PROPERTY_DEF_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_vault_properties via HTTP GET
    /blck/mfi_cl_VaultApi=>get_vault_properties(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_DEF_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_PROPERTY_DEF_TT (**[array of PropertyDef](#markdown-header-model-property_def)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_vault_property**
Retrieves information on a single property definition.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/properties/id/


### Example
```abap
*** method VaultApi->get_vault_property example
*** Retrieves information on a single property definition.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_DEF
    data gr_http200 type /BLCK/MFI_PROPERTY_DEF.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_vault_property via HTTP GET
    /blck/mfi_cl_VaultApi=>get_vault_property(
      exporting
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_DEF)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_PROPERTY_DEF (**[PropertyDef](#markdown-header-model-property_def)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_workflow**
Retrieves information on a single workflow.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/workflows/


### Example
```abap
*** method VaultApi->get_workflow example
*** Retrieves information on a single workflow.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW
    data gr_http200 type /BLCK/MFI_WORKFLOW.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_workflow via HTTP GET
    /blck/mfi_cl_VaultApi=>get_workflow(
      exporting
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_WORKFLOW (**[Workflow](#markdown-header-model-workflow)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_workflow_state**
Retrieves information on the specific workflow state.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/workflows/id/states/id/


### Example
```abap
*** method VaultApi->get_workflow_state example
*** Retrieves information on the specific workflow state.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_sid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_sid type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_STATE
    data gr_http200 type /BLCK/MFI_WORKFLOW_STATE.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvi_sid = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_workflow_state via HTTP GET
*** i_id: Workflow ID
*** i_sid: State ID
    /blck/mfi_cl_VaultApi=>get_workflow_state(
      exporting
        i_id = gvi_id
        i_sid = gvi_sid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_STATE)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT | Workflow ID 
 **i_sid** | /BLCK/MFI_INT | State ID 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_WORKFLOW_STATE (**[WorkflowState](#markdown-header-model-workflow_state)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_workflow_states**
Retrieves information on all workflow states of the given workflow.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/workflows/id/states/


### Example
```abap
*** method VaultApi->get_workflow_states example
*** Retrieves information on all workflow states of the given workflow.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_currentstate:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_currentstate type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_STATE_TT
    data gr_http200 type /BLCK/MFI_WORKFLOW_STATE_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvi_currentstate = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_workflow_states via HTTP GET
*** i_currentstate: state  ID. Restricts the list of returned states to those that are available
*** as valid states from the current state.
    /blck/mfi_cl_VaultApi=>get_workflow_states(
      exporting
        i_id = gvi_id
        i_currentstate = gvi_currentstate
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_STATE_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_currentstate** | /BLCK/MFI_INT | state ID. Restricts the list of returned states to those that are available as valid states from the current state. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_WORKFLOW_STATE_TT (**[array of WorkflowState](#markdown-header-model-workflow_state)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_workflow_transitions**
Retrieves information on valid state transitions in the current workflow.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/workflows/id/statetransitions/


### Example
```abap
*** method VaultApi->get_workflow_transitions example
*** Retrieves information on valid state transitions in the current workflow.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_currentstate:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_currentstate type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_STATE_TT
    data gr_http200 type /BLCK/MFI_WORKFLOW_STATE_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvi_currentstate = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_workflow_transitions via HTTP GET
*** i_currentstate: state  ID. Restricts the list of returned states to those that are available
*** as valid states from the current state.
    /blck/mfi_cl_VaultApi=>get_workflow_transitions(
      exporting
        i_id = gvi_id
        i_currentstate = gvi_currentstate
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_STATE_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_currentstate** | /BLCK/MFI_INT | state ID. Restricts the list of returned states to those that are available as valid states from the current state. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_WORKFLOW_STATE_TT (**[array of WorkflowState](#markdown-header-model-workflow_state)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_workflows**
Retrieves information on all workflows.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/workflows/


### Example
```abap
*** method VaultApi->get_workflows example
*** Retrieves information on all workflows.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_TT
    data gr_http200 type /BLCK/MFI_WORKFLOW_TT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_workflows via HTTP GET
    /blck/mfi_cl_VaultApi=>get_workflows(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_TT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_WORKFLOW_TT (**[array of Workflow](#markdown-header-model-workflow)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **remove_item**
Deletes a value list item.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/id/items/objectid/


### Example
```abap
*** method VaultApi->remove_item example
*** Deletes a value list item.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
    data gr_http200 type /BLCK/MFI_VALUELISTITEM.
        
*** set data according to requirements of the API call
*   gvi_id = 42.
*   gvi_objectid = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method remove_item via HTTP DELETE
    /blck/mfi_cl_VaultApi=>remove_item(
      exporting
        i_id = gvi_id
        i_objectid = gvi_objectid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VALUELISTITEM)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-valuelistitem)**) | successful operation

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **set_item_title**
Changes the value list item title.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/valuelists/id/items/objectid/title/


### Example
```abap
*** method VaultApi->set_item_title example
*** Changes the value list item title.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_body type /BLCK/MFI_STRING.
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   for parameter i_objectid:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_objectid type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
    data gr_http200 type /BLCK/MFI_VALUELISTITEM.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.
*   gvi_id = 42.
*   gvi_objectid = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_item_title via HTTP PUT
    /blck/mfi_cl_VaultApi=>set_item_title(
      exporting
        i_body = gvs_body
        i_id = gvi_id
        i_objectid = gvi_objectid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VALUELISTITEM)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING |  
 **i_id** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-valuelistitem)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


## operation: **set_refresh_status**
Sets the refresh status to either Full or Quick.

https://developer.m-files.com/APIs/REST-API/Reference/resources/structure/objecttypes/type/refreshstatus/


### Example
```abap
*** method VaultApi->set_refresh_status example
*** Sets the refresh status to either Full or Quick.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_body type /BLCK/MFI_INT.
*   for parameter i_type:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_type type /BLCK/MFI_INT.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_MFREFRESHSTATU
    data gr_http200 type /BLCK/MFI_MFREFRESHSTATU.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvi_body = 42.
*   gvi_type = 42.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_VaultApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method set_refresh_status via HTTP PUT
    /blck/mfi_cl_VaultApi=>set_refresh_status(
      exporting
        i_body = gvi_body
        i_type = gvi_type
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_MFREFRESHSTATU)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_INT |  
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_MFREFRESHSTATU (**[MFRefreshStatus](#markdown-header-model-mfrefreshstatu)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: */*
 - **Accept**: application/json


# API: ViewsApi

All URIs are relative to *https://kb.cloudvault.m-files.com/REST*

## operation: **get_view_contents**
Retrieves the view contents

https://developer.m-files.com/APIs/REST-API/Reference/resources/views/path/items/


### Example
```abap
*** method ViewsApi->get_view_contents example
*** Retrieves the view contents

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_path:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_path type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_FOLDERCONTENTI
    data gr_http200 type /BLCK/MFI_FOLDERCONTENTI.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_path = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ViewsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_view_contents via HTTP GET
*** i_path: Any number of path segments separated with '/'.
    /blck/mfi_cl_ViewsApi=>get_view_contents(
      exporting
        i_path = gvs_path
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_FOLDERCONTENTI)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/MFI_STRING | Any number of path segments separated with &#x27;/&#x27;. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_FOLDERCONTENTI (**[FolderContentItems](#markdown-header-model-foldercontenti)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_view_contents_count**
Retrieves the amount of items in the view.

https://developer.m-files.com/APIs/REST-API/Reference/resources/views/path/items/count/


### Example
```abap
*** method ViewsApi->get_view_contents_count example
*** Retrieves the amount of items in the view.

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_path:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_path type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_path = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ViewsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_view_contents_count via HTTP GET
*** i_path: Any number of path segments separated with '/'.
    /blck/mfi_cl_ViewsApi=>get_view_contents_count(
      exporting
        i_path = gvs_path
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/MFI_STRING | Any number of path segments separated with &#x27;/&#x27;. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_INT | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **get_view_objects**
Searches for objects within the view

https://developer.m-files.com/APIs/REST-API/Reference/resources/views/path/objects/


### Example
```abap
*** method ViewsApi->get_view_objects example
*** Searches for objects within the view

  constants:
    gcc_basepath type string value 'https://kb.cloudvault.m-files.com/REST'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/mfi_int,
    gvs_msg  type /blck/mfi_string.
    
*** create variables for input and output as needed
*   for parameter i_path:
*   a simple ABAP primitive of type /BLCK/MFI_STRING
    data gvs_path type /BLCK/MFI_STRING.
*   when the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSOBJECTV
    data gr_http200 type /BLCK/MFI_RESULTSOBJECTV.
*   when the result of the call is HTTPother we expect type /BLCK/MFI_WEBSERVICEERRO
    data gr_httpother type /BLCK/MFI_WEBSERVICEERRO.
        
*** set data according to requirements of the API call
*   gvs_path = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/mfi_cl_ViewsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method get_view_objects via HTTP GET
*** i_path: Any number of path segments separated with '/'.
    /blck/mfi_cl_ViewsApi=>get_view_objects(
      exporting
        i_path = gvs_path
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_code_200 = gr_http200
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSOBJECTV)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/MFI_WEBSERVICEERRO)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/MFI_STRING | Any number of path segments separated with &#x27;/&#x27;. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/MFI_RESULTSOBJECTV (**[ResultsObjectVersion](#markdown-header-model-resultsobjectv)**) | successful operation
 other | **e_code_other** | /BLCK/MFI_WEBSERVICEERRO (**[WebServiceError](#markdown-header-model-webserviceerro)**) | an error occurred

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-associatedprop"></a> 

# Model: AssociatedPropertyDef



### Example
```abap
*** model associatedprop example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~AssociatedPropertyDef.html

* create our variables..
    data gr_associatedprop type /blck/mfi_associatedprop.
    
* instantiate model and call the setters to set values..
    gr_associatedprop-property_def = 42. " (type /BLCK/MFI_INT)

    gr_associatedprop-required = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_associatedprop(
      exporting
        i_associatedprop = gr_associatedprop ).
    		
    clear gr_associatedprop.
    
* fetch new instance from example API method
    gcl_exampleapi->get_associatedprop(
      exporting
        i_id = 1
      importing 
        e_200 = gr_associatedprop ).
    		
    write: gr_associatedprop-property_def. " (type /BLCK/MFI_INT)
    write: gr_associatedprop-required. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**property_def** | /BLCK/MFI_INT | 
**required** | /BLCK/MFI_BOOL | 

* * *
<a name="markdown-header-model-authentication"></a> 

# Model: Authentication



### Example
```abap
*** model authentication example
*** Structures the details used for authentication with the M-Files Web Service.

* create our variables..
    data gr_authentication type /blck/mfi_authentication.
    
* instantiate model and call the setters to set values..
    gr_authentication-username = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_authentication-password = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_authentication-domain = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_authentication-windows_user = 'X'. " (type /BLCK/MFI_BOOL)

    gr_authentication-computer_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_authentication-vault_guid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_authentication-expiration = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_authentication-read_only = 'X'. " (type /BLCK/MFI_BOOL)

    gr_authentication-url = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_authentication-method = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_authentication(
      exporting
        i_authentication = gr_authentication ).
    		
    clear gr_authentication.
    
* fetch new instance from example API method
    gcl_exampleapi->get_authentication(
      exporting
        i_id = 1
      importing 
        e_200 = gr_authentication ).
    		
    write: gr_authentication-username. " (type /BLCK/MFI_STRING)
    write: gr_authentication-password. " (type /BLCK/MFI_STRING)
    write: gr_authentication-domain. " (type /BLCK/MFI_STRING)
    write: gr_authentication-windows_user. " (type /BLCK/MFI_BOOL)
    write: gr_authentication-computer_name. " (type /BLCK/MFI_STRING)
    write: gr_authentication-vault_guid. " (type /BLCK/MFI_STRING)
    write: gr_authentication-expiration. " (type /BLCK/MFI_STRING)
    write: gr_authentication-read_only. " (type /BLCK/MFI_BOOL)
    write: gr_authentication-url. " (type /BLCK/MFI_STRING)
    write: gr_authentication-method. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**username** | /BLCK/MFI_STRING | 
**password** | /BLCK/MFI_STRING | 
**domain** | /BLCK/MFI_STRING | 
**windows_user** | /BLCK/MFI_BOOL | 
**computer_name** | /BLCK/MFI_STRING | 
**vault_guid** | /BLCK/MFI_STRING | 
**expiration** | /BLCK/MFI_STRING | 
**read_only** | /BLCK/MFI_BOOL | 
**url** | /BLCK/MFI_STRING | 
**method** | /BLCK/MFI_STRING | 

* * *
<a name="markdown-header-model-obj_ver"></a> 

# Model: ObjVer



### Example
```abap
*** model obj_ver example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjVer.html

* create our variables..
    data gr_obj_ver type /blck/mfi_obj_ver.
    
* instantiate model and call the setters to set values..
    gr_obj_ver-id = 42. " (type /BLCK/MFI_INT)

    gr_obj_ver-type = 42. " (type /BLCK/MFI_INT)

    gr_obj_ver-version = 42. " (type /BLCK/MFI_INT)

    gr_obj_ver-external_repository_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_obj_ver-externalrepositoryobjectid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_obj_ver-externalrepositoryobjectve = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_obj_ver(
      exporting
        i_obj_ver = gr_obj_ver ).
    		
    clear gr_obj_ver.
    
* fetch new instance from example API method
    gcl_exampleapi->get_obj_ver(
      exporting
        i_id = 1
      importing 
        e_200 = gr_obj_ver ).
    		
    write: gr_obj_ver-id. " (type /BLCK/MFI_INT)
    write: gr_obj_ver-type. " (type /BLCK/MFI_INT)
    write: gr_obj_ver-version. " (type /BLCK/MFI_INT)
    write: gr_obj_ver-external_repository_name. " (type /BLCK/MFI_STRING)
    write: gr_obj_ver-externalrepositoryobjectid. " (type /BLCK/MFI_STRING)
    write: gr_obj_ver-externalrepositoryobjectve. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/MFI_INT | 
**type** | /BLCK/MFI_INT | 
**version** | /BLCK/MFI_INT | 
**external_repository_name** | /BLCK/MFI_STRING | (for external objects only)
**externalrepositoryobjectid** | /BLCK/MFI_STRING | (for external objects only)
**externalrepositoryobjectve** | /BLCK/MFI_STRING | 

* * *
<a name="markdown-header-model-lookup"></a> 

# Model: Lookup



### Example
```abap
*** model lookup example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~Lookup.html

* create our variables..
    data gr_lookup type /blck/mfi_lookup.
    
* instantiate model and call the setters to set values..
    gr_lookup-deleted = 'X'. " (type /BLCK/MFI_BOOL)

    gr_lookup-display_value = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_lookup-hidden = 'X'. " (type /BLCK/MFI_BOOL)

    gr_lookup-item = 42. " (type /BLCK/MFI_INT)

    gr_lookup-version = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_lookup(
      exporting
        i_lookup = gr_lookup ).
    		
    clear gr_lookup.
    
* fetch new instance from example API method
    gcl_exampleapi->get_lookup(
      exporting
        i_id = 1
      importing 
        e_200 = gr_lookup ).
    		
    write: gr_lookup-deleted. " (type /BLCK/MFI_BOOL)
    write: gr_lookup-display_value. " (type /BLCK/MFI_STRING)
    write: gr_lookup-hidden. " (type /BLCK/MFI_BOOL)
    write: gr_lookup-item. " (type /BLCK/MFI_INT)
    write: gr_lookup-version. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**deleted** | /BLCK/MFI_BOOL | 
**display_value** | /BLCK/MFI_STRING | 
**hidden** | /BLCK/MFI_BOOL | 
**item** | /BLCK/MFI_INT | 
**version** | /BLCK/MFI_INT | 

* * *
<a name="markdown-header-enum-mf_data_type"></a> 

# Enum: MFDataType



### Example
```abap
*** model mf_data_type example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFDataType.html
*** 0: Uninitialized 1: Text 2: Integer 3: Floating 5: Date 6: Time 7: Timestamp
*** 8:  Boolean  9:  Lookup 10: MultiSelectLookup 11: Integer64 12: FILETIME 13:
*** MultiLineText 14: ACL

* create our variables..
    data gv_mf_data_type type /blck/mfi_mf_data_type.
    
* set the enum value we want
    gv_mf_data_type = /blck/mfi_cl_model=>mf_data_type-uninitialized.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mf_data_type_state(
      exporting
        i_mf_data_type = gv_mf_data_type ).
    		
    clear gv_mf_data_type.
    
* fetch result from example API method
    gcl_exampleapi->get_mf_data_type_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mf_data_type ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mf_data_type.
    when /blck/mfi_cl_model=>mf_data_type-uninitialized.
*     do something specific to uninitialized case..
    when /blck/mfi_cl_model=>mf_data_type-text.
*     do something specific to text case..
    when /blck/mfi_cl_model=>mf_data_type-integer.
*     do something specific to integer case..
    when /blck/mfi_cl_model=>mf_data_type-floating.
*     do something specific to floating case..
    when /blck/mfi_cl_model=>mf_data_type-date.
*     do something specific to date case..
    when /blck/mfi_cl_model=>mf_data_type-time.
*     do something specific to time case..
    when /blck/mfi_cl_model=>mf_data_type-timestamp.
*     do something specific to timestamp case..
    when /blck/mfi_cl_model=>mf_data_type-boolean.
*     do something specific to boolean case..
    when /blck/mfi_cl_model=>mf_data_type-lookup.
*     do something specific to lookup case..
    when /blck/mfi_cl_model=>mf_data_type-multi_select_lookup.
*     do something specific to multi_select_lookup case..
    when /blck/mfi_cl_model=>mf_data_type-integer64.
*     do something specific to integer64 case..
    when /blck/mfi_cl_model=>mf_data_type-filetime.
*     do something specific to filetime case..
    when /blck/mfi_cl_model=>mf_data_type-multi_line_text.
*     do something specific to multi_line_text case..
    when /blck/mfi_cl_model=>mf_data_type-acl.
*     do something specific to acl case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**uninitialized** | 0 | /blck/mfi_cl_model=>mf_data_type-uninitialized.
**text** | 1 | /blck/mfi_cl_model=>mf_data_type-text.
**integer** | 2 | /blck/mfi_cl_model=>mf_data_type-integer.
**floating** | 3 | /blck/mfi_cl_model=>mf_data_type-floating.
**date** | 5 | /blck/mfi_cl_model=>mf_data_type-date.
**time** | 6 | /blck/mfi_cl_model=>mf_data_type-time.
**timestamp** | 7 | /blck/mfi_cl_model=>mf_data_type-timestamp.
**boolean** | 8 | /blck/mfi_cl_model=>mf_data_type-boolean.
**lookup** | 9 | /blck/mfi_cl_model=>mf_data_type-lookup.
**multi_select_lookup** | 10 | /blck/mfi_cl_model=>mf_data_type-multi_select_lookup.
**integer64** | 11 | /blck/mfi_cl_model=>mf_data_type-integer64.
**filetime** | 12 | /blck/mfi_cl_model=>mf_data_type-filetime.
**multi_line_text** | 13 | /blck/mfi_cl_model=>mf_data_type-multi_line_text.
**acl** | 14 | /blck/mfi_cl_model=>mf_data_type-acl.

* * *
<a name="markdown-header-model-typed_value"></a> 

# Model: TypedValue



### Example
```abap
*** model typed_value example
*** A  &#x27;typed  value&#x27;  represents  a value, such as text, number, date or lookup
*** item.                                                                       
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~TypedValue.html

* create our variables..
    data gr_typed_value type /blck/mfi_typed_value.
    
* instantiate model and call the setters to set values..
    gr_typed_value-data_type = l_data_type. " (type /BLCK/MFI_MF_DATA_TYPE)

    gr_typed_value-has_value = 'X'. " (type /BLCK/MFI_BOOL)

    gr_typed_value-value = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_typed_value-lookup = l_lookup. " (type /BLCK/MFI_LOOKUP)

    gr_typed_value-lookups = l_lookups. " (type /BLCK/MFI_LOOKUP_TT)

    gr_typed_value-display_value = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_typed_value-sorting_key = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_typed_value-serialized_value = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_typed_value(
      exporting
        i_typed_value = gr_typed_value ).
    		
    clear gr_typed_value.
    
* fetch new instance from example API method
    gcl_exampleapi->get_typed_value(
      exporting
        i_id = 1
      importing 
        e_200 = gr_typed_value ).
    		
    write: gr_typed_value-data_type. " (type /BLCK/MFI_MF_DATA_TYPE)
    write: gr_typed_value-has_value. " (type /BLCK/MFI_BOOL)
    write: gr_typed_value-value. " (type /BLCK/MFI_STRING)
    write: gr_typed_value-lookup. " (type /BLCK/MFI_LOOKUP)
    write: gr_typed_value-lookups. " (type /BLCK/MFI_LOOKUP_TT)
    write: gr_typed_value-display_value. " (type /BLCK/MFI_STRING)
    write: gr_typed_value-sorting_key. " (type /BLCK/MFI_STRING)
    write: gr_typed_value-serialized_value. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**data_type** | /BLCK/MFI_MF_DATA_TYPE (**[MFDataType](#markdown-header-enum-mf_data_type)**) | 
**has_value** | /BLCK/MFI_BOOL | Specifies whether the typed value contains a real value.
**value** | /BLCK/MFI_STRING | Specifies the string, number or boolean value when the DataType is not a lookup type.
**lookup** | /BLCK/MFI_LOOKUP (**[Lookup](#markdown-header-model-lookup)**) | 
**lookups** | /BLCK/MFI_LOOKUP_TT (**[array of Lookup](#markdown-header-model-lookup)**) | Specifies the collection of Lookups when the DataType is MultiSelectLookup.
**display_value** | /BLCK/MFI_STRING | Provides the value formatted for display.
**sorting_key** | /BLCK/MFI_STRING | Provides a key that can be used to sort TypedValues
**serialized_value** | /BLCK/MFI_STRING | Provides the typed value in a serialized format suitable to be used in URIs.

* * *
<a name="markdown-header-model-property_value"></a> 

# Model: PropertyValue



### Example
```abap
*** model property_value example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~PropertyValue.html

* create our variables..
    data gr_property_value type /blck/mfi_property_value.
    
* instantiate model and call the setters to set values..
    gr_property_value-property_def = 42. " (type /BLCK/MFI_INT)

    gr_property_value-typed_value = l_typed_value. " (type /BLCK/MFI_TYPED_VALUE)
    
* pass to example API method
    gcl_exampleapi->update_property_value(
      exporting
        i_property_value = gr_property_value ).
    		
    clear gr_property_value.
    
* fetch new instance from example API method
    gcl_exampleapi->get_property_value(
      exporting
        i_id = 1
      importing 
        e_200 = gr_property_value ).
    		
    write: gr_property_value-property_def. " (type /BLCK/MFI_INT)
    write: gr_property_value-typed_value. " (type /BLCK/MFI_TYPED_VALUE)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**property_def** | /BLCK/MFI_INT | 
**typed_value** | /BLCK/MFI_TYPED_VALUE (**[TypedValue](#markdown-header-model-typed_value)**) | 

* * *
<a name="markdown-header-model-automaticmetad"></a> 

# Model: AutomaticMetadataRequestInfo



### Example
```abap
*** model automaticmetad example
*** Holds  file  upload ids and property values for fetching automatic metadata.
*** This struct is used when automatic metadata is fetched from server.

* create our variables..
    data gr_automaticmetad type /blck/mfi_automaticmetad.
    
* instantiate model and call the setters to set values..
    gr_automaticmetad-upload_ids = l_upload_ids. " (type /BLCK/MFI_INT_TT)

    gr_automaticmetad-property_values = l_property_values. " (type /BLCK/MFI_PROPERTY_VALUE_TT)

    gr_automaticmetad-obj_ver = l_obj_ver. " (type /BLCK/MFI_OBJ_VER)

    gr_automaticmetad-object_type = 42. " (type /BLCK/MFI_INT)

    gr_automaticmetad-metadata_provider_ids = l_metadata_provider_ids. " (type /BLCK/MFI_STRING_TT)

    gr_automaticmetad-custom_data = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_automaticmetad(
      exporting
        i_automaticmetad = gr_automaticmetad ).
    		
    clear gr_automaticmetad.
    
* fetch new instance from example API method
    gcl_exampleapi->get_automaticmetad(
      exporting
        i_id = 1
      importing 
        e_200 = gr_automaticmetad ).
    		
    write: gr_automaticmetad-upload_ids. " (type /BLCK/MFI_INT_TT)
    write: gr_automaticmetad-property_values. " (type /BLCK/MFI_PROPERTY_VALUE_TT)
    write: gr_automaticmetad-obj_ver. " (type /BLCK/MFI_OBJ_VER)
    write: gr_automaticmetad-object_type. " (type /BLCK/MFI_INT)
    write: gr_automaticmetad-metadata_provider_ids. " (type /BLCK/MFI_STRING_TT)
    write: gr_automaticmetad-custom_data. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**upload_ids** | /BLCK/MFI_INT_TT | List of temporary file upload ids.
**property_values** | /BLCK/MFI_PROPERTY_VALUE_TT (**[array of PropertyValue](#markdown-header-model-property_value)**) | Array of object’s current property values.
**obj_ver** | /BLCK/MFI_OBJ_VER (**[ObjVer](#markdown-header-model-obj_ver)**) | 
**object_type** | /BLCK/MFI_INT | The object type of the new object.
**metadata_provider_ids** | /BLCK/MFI_STRING_TT | List of metadata provider ids.
**custom_data** | /BLCK/MFI_STRING | Custom data provided to the providers.

* * *
<a name="markdown-header-model-class_group"></a> 

# Model: ClassGroup



### Example
```abap
*** model class_group example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ClassGroup.html

* create our variables..
    data gr_class_group type /blck/mfi_class_group.
    
* instantiate model and call the setters to set values..
    gr_class_group-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_class_group(
      exporting
        i_class_group = gr_class_group ).
    		
    clear gr_class_group.
    
* fetch new instance from example API method
    gcl_exampleapi->get_class_group(
      exporting
        i_id = 1
      importing 
        e_200 = gr_class_group ).
    		
    write: gr_class_group-name. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**name** | /BLCK/MFI_STRING | 

* * *
<a name="markdown-header-model-stacktraceelem"></a> 

# Model: StackTraceElement



### Example
```abap
*** model stacktraceelem example
*** M-Files Web Service error stack trace element.

* create our variables..
    data gr_stacktraceelem type /blck/mfi_stacktraceelem.
    
* instantiate model and call the setters to set values..
    gr_stacktraceelem-file_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_stacktraceelem-line_number = 42. " (type /BLCK/MFI_INT)

    gr_stacktraceelem-class_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_stacktraceelem-method_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_stacktraceelem(
      exporting
        i_stacktraceelem = gr_stacktraceelem ).
    		
    clear gr_stacktraceelem.
    
* fetch new instance from example API method
    gcl_exampleapi->get_stacktraceelem(
      exporting
        i_id = 1
      importing 
        e_200 = gr_stacktraceelem ).
    		
    write: gr_stacktraceelem-file_name. " (type /BLCK/MFI_STRING)
    write: gr_stacktraceelem-line_number. " (type /BLCK/MFI_INT)
    write: gr_stacktraceelem-class_name. " (type /BLCK/MFI_STRING)
    write: gr_stacktraceelem-method_name. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**file_name** | /BLCK/MFI_STRING | 
**line_number** | /BLCK/MFI_INT | 
**class_name** | /BLCK/MFI_STRING | 
**method_name** | /BLCK/MFI_STRING | 

* * *
<a name="markdown-header-model-exceptioninfo3"></a> 

# Model: ExceptionInfo3



### Example
```abap
*** model exceptioninfo3 example

* create our variables..
    data gr_exceptioninfo3 type /blck/mfi_exceptioninfo3.
    
* instantiate model and call the setters to set values..
    gr_exceptioninfo3-message = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_exceptioninfo3-stack = l_stack. " (type /BLCK/MFI_STACKTRACEELEM_TT)
    
* pass to example API method
    gcl_exampleapi->update_exceptioninfo3(
      exporting
        i_exceptioninfo3 = gr_exceptioninfo3 ).
    		
    clear gr_exceptioninfo3.
    
* fetch new instance from example API method
    gcl_exampleapi->get_exceptioninfo3(
      exporting
        i_id = 1
      importing 
        e_200 = gr_exceptioninfo3 ).
    		
    write: gr_exceptioninfo3-message. " (type /BLCK/MFI_STRING)
    write: gr_exceptioninfo3-stack. " (type /BLCK/MFI_STACKTRACEELEM_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**message** | /BLCK/MFI_STRING | The raw error message.
**stack** | /BLCK/MFI_STACKTRACEELEM_TT (**[array of StackTraceElement](#markdown-header-model-stacktraceelem)**) | M-Files Web Service server-side stack trace.

* * *
<a name="markdown-header-model-exceptioninfo2"></a> 

# Model: ExceptionInfo2



### Example
```abap
*** model exceptioninfo2 example

* create our variables..
    data gr_exceptioninfo2 type /blck/mfi_exceptioninfo2.
    
* instantiate model and call the setters to set values..
    gr_exceptioninfo2-message = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_exceptioninfo2-inner_exception = l_inner_exception. " (type /BLCK/MFI_EXCEPTIONINFO3)

    gr_exceptioninfo2-stack = l_stack. " (type /BLCK/MFI_STACKTRACEELEM_TT)
    
* pass to example API method
    gcl_exampleapi->update_exceptioninfo2(
      exporting
        i_exceptioninfo2 = gr_exceptioninfo2 ).
    		
    clear gr_exceptioninfo2.
    
* fetch new instance from example API method
    gcl_exampleapi->get_exceptioninfo2(
      exporting
        i_id = 1
      importing 
        e_200 = gr_exceptioninfo2 ).
    		
    write: gr_exceptioninfo2-message. " (type /BLCK/MFI_STRING)
    write: gr_exceptioninfo2-inner_exception. " (type /BLCK/MFI_EXCEPTIONINFO3)
    write: gr_exceptioninfo2-stack. " (type /BLCK/MFI_STACKTRACEELEM_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**message** | /BLCK/MFI_STRING | The raw error message.
**inner_exception** | /BLCK/MFI_EXCEPTIONINFO3 (**[ExceptionInfo3](#markdown-header-model-exceptioninfo3)**) | 
**stack** | /BLCK/MFI_STACKTRACEELEM_TT (**[array of StackTraceElement](#markdown-header-model-stacktraceelem)**) | M-Files Web Service server-side stack trace.

* * *
<a name="markdown-header-model-exception_info"></a> 

# Model: ExceptionInfo



### Example
```abap
*** model exception_info example

* create our variables..
    data gr_exception_info type /blck/mfi_exception_info.
    
* instantiate model and call the setters to set values..
    gr_exception_info-message = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_exception_info-inner_exception = l_inner_exception. " (type /BLCK/MFI_EXCEPTIONINFO2)

    gr_exception_info-stack = l_stack. " (type /BLCK/MFI_STACKTRACEELEM_TT)
    
* pass to example API method
    gcl_exampleapi->update_exception_info(
      exporting
        i_exception_info = gr_exception_info ).
    		
    clear gr_exception_info.
    
* fetch new instance from example API method
    gcl_exampleapi->get_exception_info(
      exporting
        i_id = 1
      importing 
        e_200 = gr_exception_info ).
    		
    write: gr_exception_info-message. " (type /BLCK/MFI_STRING)
    write: gr_exception_info-inner_exception. " (type /BLCK/MFI_EXCEPTIONINFO2)
    write: gr_exception_info-stack. " (type /BLCK/MFI_STACKTRACEELEM_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**message** | /BLCK/MFI_STRING | The raw error message.
**inner_exception** | /BLCK/MFI_EXCEPTIONINFO2 (**[ExceptionInfo2](#markdown-header-model-exceptioninfo2)**) | 
**stack** | /BLCK/MFI_STACKTRACEELEM_TT (**[array of StackTraceElement](#markdown-header-model-stacktraceelem)**) | M-Files Web Service server-side stack trace.

* * *
<a name="markdown-header-enum-mfobjectversio"></a> 

# Enum: MFObjectVersionFlag



### Example
```abap
*** model mfobjectversio example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFObjectVersionFlag.html
*** 0: None 1: Completed 2: HasRelatedObjects

* create our variables..
    data gv_mfobjectversio type /blck/mfi_mfobjectversio.
    
* set the enum value we want
    gv_mfobjectversio = /blck/mfi_cl_model=>mfobjectversio-none.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfobjectversio_state(
      exporting
        i_mfobjectversio = gv_mfobjectversio ).
    		
    clear gv_mfobjectversio.
    
* fetch result from example API method
    gcl_exampleapi->get_mfobjectversio_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mfobjectversio ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mfobjectversio.
    when /blck/mfi_cl_model=>mfobjectversio-none.
*     do something specific to none case..
    when /blck/mfi_cl_model=>mfobjectversio-completed.
*     do something specific to completed case..
    when /blck/mfi_cl_model=>mfobjectversio-has_related_objects.
*     do something specific to has_related_objects case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**none** | 0 | /blck/mfi_cl_model=>mfobjectversio-none.
**completed** | 1 | /blck/mfi_cl_model=>mfobjectversio-completed.
**has_related_objects** | 2 | /blck/mfi_cl_model=>mfobjectversio-has_related_objects.

* * *
<a name="markdown-header-model-object_file"></a> 

# Model: ObjectFile



### Example
```abap
*** model object_file example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjectFile.html

* create our variables..
    data gr_object_file type /blck/mfi_object_file.
    
* instantiate model and call the setters to set values..
    gr_object_file-change_time_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_file-extension = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_file-id = 42. " (type /BLCK/MFI_INT)

    gr_object_file-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_file-version = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_object_file(
      exporting
        i_object_file = gr_object_file ).
    		
    clear gr_object_file.
    
* fetch new instance from example API method
    gcl_exampleapi->get_object_file(
      exporting
        i_id = 1
      importing 
        e_200 = gr_object_file ).
    		
    write: gr_object_file-change_time_utc. " (type /BLCK/MFI_STRING)
    write: gr_object_file-extension. " (type /BLCK/MFI_STRING)
    write: gr_object_file-id. " (type /BLCK/MFI_INT)
    write: gr_object_file-name. " (type /BLCK/MFI_STRING)
    write: gr_object_file-version. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**change_time_utc** | /BLCK/MFI_STRING | 
**extension** | /BLCK/MFI_STRING | 
**id** | /BLCK/MFI_INT | 
**name** | /BLCK/MFI_STRING | 
**version** | /BLCK/MFI_INT | 

* * *
<a name="markdown-header-model-object_version"></a> 

# Model: ObjectVersion



### Example
```abap
*** model object_version example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjectVersion.html

* create our variables..
    data gr_object_version type /blck/mfi_object_version.
    
* instantiate model and call the setters to set values..
    gr_object_version-accessed_by_me_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_version-checked_out_at_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_version-checked_out_to = 42. " (type /BLCK/MFI_INT)

    gr_object_version-checked_out_to_user_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_version-class = 42. " (type /BLCK/MFI_INT)

    gr_object_version-created_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_version-deleted = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-display_id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_version-files = l_files. " (type /BLCK/MFI_OBJECT_FILE_TT)

    gr_object_version-has_assignments = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-hasrelationshipsfromthis = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-has_relationships_to_this = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-is_stub = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-last_modified_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_version-object_checked_out = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-objectcheckedouttothisuser = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-object_version_flags = l_object_version_flags. " (type /BLCK/MFI_MFOBJECTVERSIO)

    gr_object_version-obj_ver = l_obj_ver. " (type /BLCK/MFI_OBJ_VER)

    gr_object_version-single_file = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-thisversionlatesttothisuse = 'X'. " (type /BLCK/MFI_BOOL)

    gr_object_version-title = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_version-visible_after_operation = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_object_version(
      exporting
        i_object_version = gr_object_version ).
    		
    clear gr_object_version.
    
* fetch new instance from example API method
    gcl_exampleapi->get_object_version(
      exporting
        i_id = 1
      importing 
        e_200 = gr_object_version ).
    		
    write: gr_object_version-accessed_by_me_utc. " (type /BLCK/MFI_STRING)
    write: gr_object_version-checked_out_at_utc. " (type /BLCK/MFI_STRING)
    write: gr_object_version-checked_out_to. " (type /BLCK/MFI_INT)
    write: gr_object_version-checked_out_to_user_name. " (type /BLCK/MFI_STRING)
    write: gr_object_version-class. " (type /BLCK/MFI_INT)
    write: gr_object_version-created_utc. " (type /BLCK/MFI_STRING)
    write: gr_object_version-deleted. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-display_id. " (type /BLCK/MFI_STRING)
    write: gr_object_version-files. " (type /BLCK/MFI_OBJECT_FILE_TT)
    write: gr_object_version-has_assignments. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-hasrelationshipsfromthis. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-has_relationships_to_this. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-is_stub. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-last_modified_utc. " (type /BLCK/MFI_STRING)
    write: gr_object_version-object_checked_out. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-objectcheckedouttothisuser. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-object_version_flags. " (type /BLCK/MFI_MFOBJECTVERSIO)
    write: gr_object_version-obj_ver. " (type /BLCK/MFI_OBJ_VER)
    write: gr_object_version-single_file. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-thisversionlatesttothisuse. " (type /BLCK/MFI_BOOL)
    write: gr_object_version-title. " (type /BLCK/MFI_STRING)
    write: gr_object_version-visible_after_operation. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**accessed_by_me_utc** | /BLCK/MFI_STRING | 
**checked_out_at_utc** | /BLCK/MFI_STRING | 
**checked_out_to** | /BLCK/MFI_INT | 
**checked_out_to_user_name** | /BLCK/MFI_STRING | 
**class** | /BLCK/MFI_INT | 
**created_utc** | /BLCK/MFI_STRING | 
**deleted** | /BLCK/MFI_BOOL | 
**display_id** | /BLCK/MFI_STRING | 
**files** | /BLCK/MFI_OBJECT_FILE_TT (**[array of ObjectFile](#markdown-header-model-object_file)**) | 
**has_assignments** | /BLCK/MFI_BOOL | 
**hasrelationshipsfromthis** | /BLCK/MFI_BOOL | 
**has_relationships_to_this** | /BLCK/MFI_BOOL | 
**is_stub** | /BLCK/MFI_BOOL | 
**last_modified_utc** | /BLCK/MFI_STRING | 
**object_checked_out** | /BLCK/MFI_BOOL | 
**objectcheckedouttothisuser** | /BLCK/MFI_BOOL | 
**object_version_flags** | /BLCK/MFI_MFOBJECTVERSIO (**[MFObjectVersionFlag](#markdown-header-enum-mfobjectversio)**) | 
**obj_ver** | /BLCK/MFI_OBJ_VER (**[ObjVer](#markdown-header-model-obj_ver)**) | 
**single_file** | /BLCK/MFI_BOOL | 
**thisversionlatesttothisuse** | /BLCK/MFI_BOOL | 
**title** | /BLCK/MFI_STRING | 
**visible_after_operation** | /BLCK/MFI_BOOL | 

* * *
<a name="markdown-header-model-extendedobjec2"></a> 

# Model: ExtendedObjectClass



### Example
```abap
*** model extendedobjec2 example

* create our variables..
    data gr_extendedobjec2 type /blck/mfi_extendedobjec2.
    
* instantiate model and call the setters to set values..
    gr_extendedobjec2-id = 42. " (type /BLCK/MFI_INT)

    gr_extendedobjec2-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobjec2-name_property_def = 42. " (type /BLCK/MFI_INT)

    gr_extendedobjec2-workflow = 42. " (type /BLCK/MFI_INT)

    gr_extendedobjec2-associated_property_defs = l_associated_property_defs. " (type /BLCK/MFI_ASSOCIATEDPROP_TT)

    gr_extendedobjec2-templates = l_templates. " (type /BLCK/MFI_OBJECT_VERSION_TT)
    
* pass to example API method
    gcl_exampleapi->update_extendedobjec2(
      exporting
        i_extendedobjec2 = gr_extendedobjec2 ).
    		
    clear gr_extendedobjec2.
    
* fetch new instance from example API method
    gcl_exampleapi->get_extendedobjec2(
      exporting
        i_id = 1
      importing 
        e_200 = gr_extendedobjec2 ).
    		
    write: gr_extendedobjec2-id. " (type /BLCK/MFI_INT)
    write: gr_extendedobjec2-name. " (type /BLCK/MFI_STRING)
    write: gr_extendedobjec2-name_property_def. " (type /BLCK/MFI_INT)
    write: gr_extendedobjec2-workflow. " (type /BLCK/MFI_INT)
    write: gr_extendedobjec2-associated_property_defs. " (type /BLCK/MFI_ASSOCIATEDPROP_TT)
    write: gr_extendedobjec2-templates. " (type /BLCK/MFI_OBJECT_VERSION_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/MFI_INT | 
**name** | /BLCK/MFI_STRING | 
**name_property_def** | /BLCK/MFI_INT | 
**workflow** | /BLCK/MFI_INT | 
**associated_property_defs** | /BLCK/MFI_ASSOCIATEDPROP_TT (**[array of AssociatedPropertyDef](#markdown-header-model-associatedprop)**) | Property definitions associated with this class.
**templates** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | Templates available for use with this class.

* * *
<a name="markdown-header-model-extendedobject"></a> 

# Model: ExtendedObjectVersion



### Example
```abap
*** model extendedobject example

* create our variables..
    data gr_extendedobject type /blck/mfi_extendedobject.
    
* instantiate model and call the setters to set values..
    gr_extendedobject-accessed_by_me_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobject-checked_out_at_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobject-checked_out_to = 42. " (type /BLCK/MFI_INT)

    gr_extendedobject-checked_out_to_user_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobject-class = 42. " (type /BLCK/MFI_INT)

    gr_extendedobject-created_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobject-deleted = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-display_id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobject-files = l_files. " (type /BLCK/MFI_OBJECT_FILE_TT)

    gr_extendedobject-has_assignments = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-hasrelationshipsfromthis = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-has_relationships_to_this = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-is_stub = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-last_modified_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobject-object_checked_out = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-objectcheckedouttothisuser = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-object_version_flags = l_object_version_flags. " (type /BLCK/MFI_MFOBJECTVERSIO)

    gr_extendedobject-obj_ver = l_obj_ver. " (type /BLCK/MFI_OBJ_VER)

    gr_extendedobject-single_file = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-thisversionlatesttothisuse = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-title = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_extendedobject-visible_after_operation = 'X'. " (type /BLCK/MFI_BOOL)

    gr_extendedobject-properties = l_properties. " (type /BLCK/MFI_PROPERTY_VALUE_TT)
    
* pass to example API method
    gcl_exampleapi->update_extendedobject(
      exporting
        i_extendedobject = gr_extendedobject ).
    		
    clear gr_extendedobject.
    
* fetch new instance from example API method
    gcl_exampleapi->get_extendedobject(
      exporting
        i_id = 1
      importing 
        e_200 = gr_extendedobject ).
    		
    write: gr_extendedobject-accessed_by_me_utc. " (type /BLCK/MFI_STRING)
    write: gr_extendedobject-checked_out_at_utc. " (type /BLCK/MFI_STRING)
    write: gr_extendedobject-checked_out_to. " (type /BLCK/MFI_INT)
    write: gr_extendedobject-checked_out_to_user_name. " (type /BLCK/MFI_STRING)
    write: gr_extendedobject-class. " (type /BLCK/MFI_INT)
    write: gr_extendedobject-created_utc. " (type /BLCK/MFI_STRING)
    write: gr_extendedobject-deleted. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-display_id. " (type /BLCK/MFI_STRING)
    write: gr_extendedobject-files. " (type /BLCK/MFI_OBJECT_FILE_TT)
    write: gr_extendedobject-has_assignments. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-hasrelationshipsfromthis. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-has_relationships_to_this. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-is_stub. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-last_modified_utc. " (type /BLCK/MFI_STRING)
    write: gr_extendedobject-object_checked_out. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-objectcheckedouttothisuser. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-object_version_flags. " (type /BLCK/MFI_MFOBJECTVERSIO)
    write: gr_extendedobject-obj_ver. " (type /BLCK/MFI_OBJ_VER)
    write: gr_extendedobject-single_file. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-thisversionlatesttothisuse. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-title. " (type /BLCK/MFI_STRING)
    write: gr_extendedobject-visible_after_operation. " (type /BLCK/MFI_BOOL)
    write: gr_extendedobject-properties. " (type /BLCK/MFI_PROPERTY_VALUE_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**accessed_by_me_utc** | /BLCK/MFI_STRING | 
**checked_out_at_utc** | /BLCK/MFI_STRING | 
**checked_out_to** | /BLCK/MFI_INT | 
**checked_out_to_user_name** | /BLCK/MFI_STRING | 
**class** | /BLCK/MFI_INT | 
**created_utc** | /BLCK/MFI_STRING | 
**deleted** | /BLCK/MFI_BOOL | 
**display_id** | /BLCK/MFI_STRING | 
**files** | /BLCK/MFI_OBJECT_FILE_TT (**[array of ObjectFile](#markdown-header-model-object_file)**) | 
**has_assignments** | /BLCK/MFI_BOOL | 
**hasrelationshipsfromthis** | /BLCK/MFI_BOOL | 
**has_relationships_to_this** | /BLCK/MFI_BOOL | 
**is_stub** | /BLCK/MFI_BOOL | 
**last_modified_utc** | /BLCK/MFI_STRING | 
**object_checked_out** | /BLCK/MFI_BOOL | 
**objectcheckedouttothisuser** | /BLCK/MFI_BOOL | 
**object_version_flags** | /BLCK/MFI_MFOBJECTVERSIO (**[MFObjectVersionFlag](#markdown-header-enum-mfobjectversio)**) | 
**obj_ver** | /BLCK/MFI_OBJ_VER (**[ObjVer](#markdown-header-model-obj_ver)**) | 
**single_file** | /BLCK/MFI_BOOL | 
**thisversionlatesttothisuse** | /BLCK/MFI_BOOL | 
**title** | /BLCK/MFI_STRING | 
**visible_after_operation** | /BLCK/MFI_BOOL | 
**properties** | /BLCK/MFI_PROPERTY_VALUE_TT (**[array of PropertyValue](#markdown-header-model-property_value)**) | Object properties

* * *
<a name="markdown-header-enum-mffolderconten"></a> 

# Enum: MFFolderContentItemType



### Example
```abap
*** model mffolderconten example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFFolderContentItemType.html
*** 0:   Unknown   1:  ViewFolder  2:  PropertyFolder  3:  TraditionalFolder  4:
*** ObjectVersion 5: ExternalViewFolder

* create our variables..
    data gv_mffolderconten type /blck/mfi_mffolderconten.
    
* set the enum value we want
    gv_mffolderconten = /blck/mfi_cl_model=>mffolderconten-unknown.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mffolderconten_state(
      exporting
        i_mffolderconten = gv_mffolderconten ).
    		
    clear gv_mffolderconten.
    
* fetch result from example API method
    gcl_exampleapi->get_mffolderconten_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mffolderconten ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mffolderconten.
    when /blck/mfi_cl_model=>mffolderconten-unknown.
*     do something specific to unknown case..
    when /blck/mfi_cl_model=>mffolderconten-view_folder.
*     do something specific to view_folder case..
    when /blck/mfi_cl_model=>mffolderconten-property_folder.
*     do something specific to property_folder case..
    when /blck/mfi_cl_model=>mffolderconten-traditional_folder.
*     do something specific to traditional_folder case..
    when /blck/mfi_cl_model=>mffolderconten-object_version.
*     do something specific to object_version case..
    when /blck/mfi_cl_model=>mffolderconten-external_view_folder.
*     do something specific to external_view_folder case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**unknown** | 0 | /blck/mfi_cl_model=>mffolderconten-unknown.
**view_folder** | 1 | /blck/mfi_cl_model=>mffolderconten-view_folder.
**property_folder** | 2 | /blck/mfi_cl_model=>mffolderconten-property_folder.
**traditional_folder** | 3 | /blck/mfi_cl_model=>mffolderconten-traditional_folder.
**object_version** | 4 | /blck/mfi_cl_model=>mffolderconten-object_version.
**external_view_folder** | 5 | /blck/mfi_cl_model=>mffolderconten-external_view_folder.

* * *
<a name="markdown-header-model-view_location"></a> 

# Model: ViewLocation



### Example
```abap
*** model view_location example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ViewLocation.html

* create our variables..
    data gr_view_location type /blck/mfi_view_location.
    
* instantiate model and call the setters to set values..
    gr_view_location-overlapped_folder = l_overlapped_folder. " (type /BLCK/MFI_TYPED_VALUE)

    gr_view_location-overlapping = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_view_location(
      exporting
        i_view_location = gr_view_location ).
    		
    clear gr_view_location.
    
* fetch new instance from example API method
    gcl_exampleapi->get_view_location(
      exporting
        i_id = 1
      importing 
        e_200 = gr_view_location ).
    		
    write: gr_view_location-overlapped_folder. " (type /BLCK/MFI_TYPED_VALUE)
    write: gr_view_location-overlapping. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**overlapped_folder** | /BLCK/MFI_TYPED_VALUE (**[TypedValue](#markdown-header-model-typed_value)**) | 
**overlapping** | /BLCK/MFI_BOOL | 

* * *
<a name="markdown-header-model-view"></a> 

# Model: View



### Example
```abap
*** model view example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~View.html

* create our variables..
    data gr_view type /blck/mfi_view.
    
* instantiate model and call the setters to set values..
    gr_view-common = 'X'. " (type /BLCK/MFI_BOOL)

    gr_view-id = 42. " (type /BLCK/MFI_INT)

    gr_view-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_view-parent = 42. " (type /BLCK/MFI_INT)

    gr_view-view_location = l_view_location. " (type /BLCK/MFI_VIEW_LOCATION)
    
* pass to example API method
    gcl_exampleapi->update_view(
      exporting
        i_view = gr_view ).
    		
    clear gr_view.
    
* fetch new instance from example API method
    gcl_exampleapi->get_view(
      exporting
        i_id = 1
      importing 
        e_200 = gr_view ).
    		
    write: gr_view-common. " (type /BLCK/MFI_BOOL)
    write: gr_view-id. " (type /BLCK/MFI_INT)
    write: gr_view-name. " (type /BLCK/MFI_STRING)
    write: gr_view-parent. " (type /BLCK/MFI_INT)
    write: gr_view-view_location. " (type /BLCK/MFI_VIEW_LOCATION)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**common** | /BLCK/MFI_BOOL | 
**id** | /BLCK/MFI_INT | 
**name** | /BLCK/MFI_STRING | 
**parent** | /BLCK/MFI_INT | 
**view_location** | /BLCK/MFI_VIEW_LOCATION (**[ViewLocation](#markdown-header-model-view_location)**) | 

* * *
<a name="markdown-header-model-foldercontent2"></a> 

# Model: FolderContentItem



### Example
```abap
*** model foldercontent2 example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~FolderContentItem.html

* create our variables..
    data gr_foldercontent2 type /blck/mfi_foldercontent2.
    
* instantiate model and call the setters to set values..
    gr_foldercontent2-folder_content_item_type = l_folder_content_item_type. " (type /BLCK/MFI_MFFOLDERCONTEN)

    gr_foldercontent2-object_version = l_object_version. " (type /BLCK/MFI_OBJECT_VERSION)

    gr_foldercontent2-property_folder = l_property_folder. " (type /BLCK/MFI_TYPED_VALUE)

    gr_foldercontent2-traditional_folder = l_traditional_folder. " (type /BLCK/MFI_LOOKUP)

    gr_foldercontent2-view = l_view. " (type /BLCK/MFI_VIEW)
    
* pass to example API method
    gcl_exampleapi->update_foldercontent2(
      exporting
        i_foldercontent2 = gr_foldercontent2 ).
    		
    clear gr_foldercontent2.
    
* fetch new instance from example API method
    gcl_exampleapi->get_foldercontent2(
      exporting
        i_id = 1
      importing 
        e_200 = gr_foldercontent2 ).
    		
    write: gr_foldercontent2-folder_content_item_type. " (type /BLCK/MFI_MFFOLDERCONTEN)
    write: gr_foldercontent2-object_version. " (type /BLCK/MFI_OBJECT_VERSION)
    write: gr_foldercontent2-property_folder. " (type /BLCK/MFI_TYPED_VALUE)
    write: gr_foldercontent2-traditional_folder. " (type /BLCK/MFI_LOOKUP)
    write: gr_foldercontent2-view. " (type /BLCK/MFI_VIEW)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**folder_content_item_type** | /BLCK/MFI_MFFOLDERCONTEN (**[MFFolderContentItemType](#markdown-header-enum-mffolderconten)**) | 
**object_version** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-object_version)**) | 
**property_folder** | /BLCK/MFI_TYPED_VALUE (**[TypedValue](#markdown-header-model-typed_value)**) | 
**traditional_folder** | /BLCK/MFI_LOOKUP (**[Lookup](#markdown-header-model-lookup)**) | 
**view** | /BLCK/MFI_VIEW (**[View](#markdown-header-model-view)**) | 

* * *
<a name="markdown-header-model-foldercontenti"></a> 

# Model: FolderContentItems



### Example
```abap
*** model foldercontenti example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~FolderContentItems.html

* create our variables..
    data gr_foldercontenti type /blck/mfi_foldercontenti.
    
* instantiate model and call the setters to set values..
    gr_foldercontenti-path = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_foldercontenti-more_results = 'X'. " (type /BLCK/MFI_BOOL)

    gr_foldercontenti-items = l_items. " (type /BLCK/MFI_FOLDERCONTENT2_TT)
    
* pass to example API method
    gcl_exampleapi->update_foldercontenti(
      exporting
        i_foldercontenti = gr_foldercontenti ).
    		
    clear gr_foldercontenti.
    
* fetch new instance from example API method
    gcl_exampleapi->get_foldercontenti(
      exporting
        i_id = 1
      importing 
        e_200 = gr_foldercontenti ).
    		
    write: gr_foldercontenti-path. " (type /BLCK/MFI_STRING)
    write: gr_foldercontenti-more_results. " (type /BLCK/MFI_BOOL)
    write: gr_foldercontenti-items. " (type /BLCK/MFI_FOLDERCONTENT2_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**path** | /BLCK/MFI_STRING | The path to the current folder.
**more_results** | /BLCK/MFI_BOOL | Specifies whether there are more results in the folder.
**items** | /BLCK/MFI_FOLDERCONTENT2_TT (**[array of FolderContentItem](#markdown-header-model-foldercontent2)**) | The actual folder contents.

* * *
<a name="markdown-header-enum-mf_auth_type"></a> 

# Enum: MFAuthType



### Example
```abap
*** model mf_auth_type example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFAuthType.html
*** 0:    Unknown    1:    LoggedOnWindowsUser    2:    SpecificWindowsUser   3:
*** SpecificMFilesUser

* create our variables..
    data gv_mf_auth_type type /blck/mfi_mf_auth_type.
    
* set the enum value we want
    gv_mf_auth_type = /blck/mfi_cl_model=>mf_auth_type-unknown.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mf_auth_type_state(
      exporting
        i_mf_auth_type = gv_mf_auth_type ).
    		
    clear gv_mf_auth_type.
    
* fetch result from example API method
    gcl_exampleapi->get_mf_auth_type_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mf_auth_type ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mf_auth_type.
    when /blck/mfi_cl_model=>mf_auth_type-unknown.
*     do something specific to unknown case..
    when /blck/mfi_cl_model=>mf_auth_type-logged_on_windows_user.
*     do something specific to logged_on_windows_user case..
    when /blck/mfi_cl_model=>mf_auth_type-specific_windows_user.
*     do something specific to specific_windows_user case..
    when /blck/mfi_cl_model=>mf_auth_type-specific_m_files_user.
*     do something specific to specific_m_files_user case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**unknown** | 0 | /blck/mfi_cl_model=>mf_auth_type-unknown.
**logged_on_windows_user** | 1 | /blck/mfi_cl_model=>mf_auth_type-logged_on_windows_user.
**specific_windows_user** | 2 | /blck/mfi_cl_model=>mf_auth_type-specific_windows_user.
**specific_m_files_user** | 3 | /blck/mfi_cl_model=>mf_auth_type-specific_m_files_user.

* * *
<a name="markdown-header-enum-mfacl_mode"></a> 

# Enum: MFACLMode



### Example
```abap
*** model mfacl_mode example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFACLMode.html
*** 0: Simple 1: AutomaticPermissionsWithComponents

* create our variables..
    data gv_mfacl_mode type /blck/mfi_mfacl_mode.
    
* set the enum value we want
    gv_mfacl_mode = /blck/mfi_cl_model=>mfacl_mode-simple.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfacl_mode_state(
      exporting
        i_mfacl_mode = gv_mfacl_mode ).
    		
    clear gv_mfacl_mode.
    
* fetch result from example API method
    gcl_exampleapi->get_mfacl_mode_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mfacl_mode ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mfacl_mode.
    when /blck/mfi_cl_model=>mfacl_mode-simple.
*     do something specific to simple case..
    when /blck/mfi_cl_model=>mfacl_mode-automaticpermissionswithc.
*     do something specific to automaticpermissionswithc case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**simple** | 0 | /blck/mfi_cl_model=>mfacl_mode-simple.
**automaticpermissionswithc** | 1 | /blck/mfi_cl_model=>mfacl_mode-automaticpermissionswithc.

* * *
<a name="markdown-header-enum-mfautomaticval"></a> 

# Enum: MFAutomaticValueType



### Example
```abap
*** model mfautomaticval example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFAutomaticValueType.html
*** 0:   None   1:   CalculatedWithPlaceholders   2:  CalculatedWithVBScript  3:
*** AutoNumberSimple 4: WithVBScript

* create our variables..
    data gv_mfautomaticval type /blck/mfi_mfautomaticval.
    
* set the enum value we want
    gv_mfautomaticval = /blck/mfi_cl_model=>mfautomaticval-none.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfautomaticval_state(
      exporting
        i_mfautomaticval = gv_mfautomaticval ).
    		
    clear gv_mfautomaticval.
    
* fetch result from example API method
    gcl_exampleapi->get_mfautomaticval_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mfautomaticval ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mfautomaticval.
    when /blck/mfi_cl_model=>mfautomaticval-none.
*     do something specific to none case..
    when /blck/mfi_cl_model=>mfautomaticval-calculatedwithplaceholder.
*     do something specific to calculatedwithplaceholder case..
    when /blck/mfi_cl_model=>mfautomaticval-calculated_with_vb_script.
*     do something specific to calculated_with_vb_script case..
    when /blck/mfi_cl_model=>mfautomaticval-auto_number_simple.
*     do something specific to auto_number_simple case..
    when /blck/mfi_cl_model=>mfautomaticval-with_vb_script.
*     do something specific to with_vb_script case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**none** | 0 | /blck/mfi_cl_model=>mfautomaticval-none.
**calculatedwithplaceholder** | 1 | /blck/mfi_cl_model=>mfautomaticval-calculatedwithplaceholder.
**calculated_with_vb_script** | 2 | /blck/mfi_cl_model=>mfautomaticval-calculated_with_vb_script.
**auto_number_simple** | 3 | /blck/mfi_cl_model=>mfautomaticval-auto_number_simple.
**with_vb_script** | 4 | /blck/mfi_cl_model=>mfautomaticval-with_vb_script.

* * *
<a name="markdown-header-enum-mfcheckoutstat"></a> 

# Enum: MFCheckOutStatus



### Example
```abap
*** model mfcheckoutstat example
*** value  &#x3D;&#x3D;  CheckedOut will not evaluate to true if the object is checked out
*** to the current user. If it doesn’t matter whom the object is checked out to,
*** use value !&#x3D; CheckedIn instead. 0: CheckedIn 1: CheckedOut 2: CheckedOutToMe

* create our variables..
    data gv_mfcheckoutstat type /blck/mfi_mfcheckoutstat.
    
* set the enum value we want
    gv_mfcheckoutstat = /blck/mfi_cl_model=>mfcheckoutstat-checked_in.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfcheckoutstat_state(
      exporting
        i_mfcheckoutstat = gv_mfcheckoutstat ).
    		
    clear gv_mfcheckoutstat.
    
* fetch result from example API method
    gcl_exampleapi->get_mfcheckoutstat_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mfcheckoutstat ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mfcheckoutstat.
    when /blck/mfi_cl_model=>mfcheckoutstat-checked_in.
*     do something specific to checked_in case..
    when /blck/mfi_cl_model=>mfcheckoutstat-checked_out.
*     do something specific to checked_out case..
    when /blck/mfi_cl_model=>mfcheckoutstat-checked_out_to_me.
*     do something specific to checked_out_to_me case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**checked_in** | 0 | /blck/mfi_cl_model=>mfcheckoutstat-checked_in.
**checked_out** | 1 | /blck/mfi_cl_model=>mfcheckoutstat-checked_out.
**checked_out_to_me** | 2 | /blck/mfi_cl_model=>mfcheckoutstat-checked_out_to_me.

* * *
<a name="markdown-header-enum-mfextensionaut"></a> 

# Enum: MFExtensionAuthenticationSpecialUserType



### Example
```abap
*** model mfextensionaut example
*** 0: None 1: Common 2: Indexer 3: Permissions

* create our variables..
    data gv_mfextensionaut type /blck/mfi_mfextensionaut.
    
* set the enum value we want
    gv_mfextensionaut = /blck/mfi_cl_model=>mfextensionaut-none.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfextensionaut_state(
      exporting
        i_mfextensionaut = gv_mfextensionaut ).
    		
    clear gv_mfextensionaut.
    
* fetch result from example API method
    gcl_exampleapi->get_mfextensionaut_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mfextensionaut ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mfextensionaut.
    when /blck/mfi_cl_model=>mfextensionaut-none.
*     do something specific to none case..
    when /blck/mfi_cl_model=>mfextensionaut-common.
*     do something specific to common case..
    when /blck/mfi_cl_model=>mfextensionaut-indexer.
*     do something specific to indexer case..
    when /blck/mfi_cl_model=>mfextensionaut-permissions.
*     do something specific to permissions case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**none** | 0 | /blck/mfi_cl_model=>mfextensionaut-none.
**common** | 1 | /blck/mfi_cl_model=>mfextensionaut-common.
**indexer** | 2 | /blck/mfi_cl_model=>mfextensionaut-indexer.
**permissions** | 3 | /blck/mfi_cl_model=>mfextensionaut-permissions.

* * *
<a name="markdown-header-enum-mfrefreshstatu"></a> 

# Enum: MFRefreshStatus



### Example
```abap
*** model mfrefreshstatu example
*** 0: None 1: Quick 2: Full

* create our variables..
    data gv_mfrefreshstatu type /blck/mfi_mfrefreshstatu.
    
* set the enum value we want
    gv_mfrefreshstatu = /blck/mfi_cl_model=>mfrefreshstatu-none.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfrefreshstatu_state(
      exporting
        i_mfrefreshstatu = gv_mfrefreshstatu ).
    		
    clear gv_mfrefreshstatu.
    
* fetch result from example API method
    gcl_exampleapi->get_mfrefreshstatu_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_mfrefreshstatu ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_mfrefreshstatu.
    when /blck/mfi_cl_model=>mfrefreshstatu-none.
*     do something specific to none case..
    when /blck/mfi_cl_model=>mfrefreshstatu-quick.
*     do something specific to quick case..
    when /blck/mfi_cl_model=>mfrefreshstatu-full.
*     do something specific to full case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**none** | 0 | /blck/mfi_cl_model=>mfrefreshstatu-none.
**quick** | 1 | /blck/mfi_cl_model=>mfrefreshstatu-quick.
**full** | 2 | /blck/mfi_cl_model=>mfrefreshstatu-full.

* * *
<a name="markdown-header-model-obj_id"></a> 

# Model: ObjID



### Example
```abap
*** model obj_id example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjID.html

* create our variables..
    data gr_obj_id type /blck/mfi_obj_id.
    
* instantiate model and call the setters to set values..
    gr_obj_id-id = 42. " (type /BLCK/MFI_INT)

    gr_obj_id-type = 42. " (type /BLCK/MFI_INT)

    gr_obj_id-external_repository_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_obj_id-externalrepositoryobjectid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_obj_id(
      exporting
        i_obj_id = gr_obj_id ).
    		
    clear gr_obj_id.
    
* fetch new instance from example API method
    gcl_exampleapi->get_obj_id(
      exporting
        i_id = 1
      importing 
        e_200 = gr_obj_id ).
    		
    write: gr_obj_id-id. " (type /BLCK/MFI_INT)
    write: gr_obj_id-type. " (type /BLCK/MFI_INT)
    write: gr_obj_id-external_repository_name. " (type /BLCK/MFI_STRING)
    write: gr_obj_id-externalrepositoryobjectid. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/MFI_INT | 
**type** | /BLCK/MFI_INT | 
**external_repository_name** | /BLCK/MFI_STRING | (for external objects only)
**externalrepositoryobjectid** | /BLCK/MFI_STRING | (for external objects only)

* * *
<a name="markdown-header-model-obj_type"></a> 

# Model: ObjType



### Example
```abap
*** model obj_type example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjType.html

* create our variables..
    data gr_obj_type type /blck/mfi_obj_type.
    
* instantiate model and call the setters to set values..
    gr_obj_type-allow_adding = 'X'. " (type /BLCK/MFI_BOOL)

    gr_obj_type-can_have_files = 'X'. " (type /BLCK/MFI_BOOL)

    gr_obj_type-default_property_def = 42. " (type /BLCK/MFI_INT)

    gr_obj_type-external = 'X'. " (type /BLCK/MFI_BOOL)

    gr_obj_type-id = 42. " (type /BLCK/MFI_INT)

    gr_obj_type-name_plural = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_obj_type-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_obj_type-owner_property_def = 42. " (type /BLCK/MFI_INT)

    gr_obj_type-readonlypropertiesduringin = l_readonlypropertiesduringin. " (type /BLCK/MFI_INT_TT)

    gr_obj_type-readonlypropertiesduringup = l_readonlypropertiesduringup. " (type /BLCK/MFI_INT_TT)

    gr_obj_type-real_object_type = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_obj_type(
      exporting
        i_obj_type = gr_obj_type ).
    		
    clear gr_obj_type.
    
* fetch new instance from example API method
    gcl_exampleapi->get_obj_type(
      exporting
        i_id = 1
      importing 
        e_200 = gr_obj_type ).
    		
    write: gr_obj_type-allow_adding. " (type /BLCK/MFI_BOOL)
    write: gr_obj_type-can_have_files. " (type /BLCK/MFI_BOOL)
    write: gr_obj_type-default_property_def. " (type /BLCK/MFI_INT)
    write: gr_obj_type-external. " (type /BLCK/MFI_BOOL)
    write: gr_obj_type-id. " (type /BLCK/MFI_INT)
    write: gr_obj_type-name_plural. " (type /BLCK/MFI_STRING)
    write: gr_obj_type-name. " (type /BLCK/MFI_STRING)
    write: gr_obj_type-owner_property_def. " (type /BLCK/MFI_INT)
    write: gr_obj_type-readonlypropertiesduringin. " (type /BLCK/MFI_INT_TT)
    write: gr_obj_type-readonlypropertiesduringup. " (type /BLCK/MFI_INT_TT)
    write: gr_obj_type-real_object_type. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**allow_adding** | /BLCK/MFI_BOOL | 
**can_have_files** | /BLCK/MFI_BOOL | 
**default_property_def** | /BLCK/MFI_INT | 
**external** | /BLCK/MFI_BOOL | 
**id** | /BLCK/MFI_INT | 
**name_plural** | /BLCK/MFI_STRING | 
**name** | /BLCK/MFI_STRING | 
**owner_property_def** | /BLCK/MFI_INT | 
**readonlypropertiesduringin** | /BLCK/MFI_INT_TT | 
**readonlypropertiesduringup** | /BLCK/MFI_INT_TT | 
**real_object_type** | /BLCK/MFI_BOOL | 

* * *
<a name="markdown-header-model-object_class"></a> 

# Model: ObjectClass



### Example
```abap
*** model object_class example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjectClass.html

* create our variables..
    data gr_object_class type /blck/mfi_object_class.
    
* instantiate model and call the setters to set values..
    gr_object_class-id = 42. " (type /BLCK/MFI_INT)

    gr_object_class-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_object_class-name_property_def = 42. " (type /BLCK/MFI_INT)

    gr_object_class-workflow = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_object_class(
      exporting
        i_object_class = gr_object_class ).
    		
    clear gr_object_class.
    
* fetch new instance from example API method
    gcl_exampleapi->get_object_class(
      exporting
        i_id = 1
      importing 
        e_200 = gr_object_class ).
    		
    write: gr_object_class-id. " (type /BLCK/MFI_INT)
    write: gr_object_class-name. " (type /BLCK/MFI_STRING)
    write: gr_object_class-name_property_def. " (type /BLCK/MFI_INT)
    write: gr_object_class-workflow. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/MFI_INT | 
**name** | /BLCK/MFI_STRING | 
**name_property_def** | /BLCK/MFI_INT | 
**workflow** | /BLCK/MFI_INT | 

* * *
<a name="markdown-header-model-upload_info"></a> 

# Model: UploadInfo



### Example
```abap
*** model upload_info example
*** Contains the information on a temporary upload.

* create our variables..
    data gr_upload_info type /blck/mfi_upload_info.
    
* instantiate model and call the setters to set values..
    gr_upload_info-upload_id = 42. " (type /BLCK/MFI_INT)

    gr_upload_info-title = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_upload_info-extension = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_upload_info-size = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_upload_info(
      exporting
        i_upload_info = gr_upload_info ).
    		
    clear gr_upload_info.
    
* fetch new instance from example API method
    gcl_exampleapi->get_upload_info(
      exporting
        i_id = 1
      importing 
        e_200 = gr_upload_info ).
    		
    write: gr_upload_info-upload_id. " (type /BLCK/MFI_INT)
    write: gr_upload_info-title. " (type /BLCK/MFI_STRING)
    write: gr_upload_info-extension. " (type /BLCK/MFI_STRING)
    write: gr_upload_info-size. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**upload_id** | /BLCK/MFI_INT | Temporary upload ID given by the server.
**title** | /BLCK/MFI_STRING | File name without extension.
**extension** | /BLCK/MFI_STRING | File extension.
**size** | /BLCK/MFI_INT | File size.

* * *
<a name="markdown-header-model-objectcreation"></a> 

# Model: ObjectCreationInfo



### Example
```abap
*** model objectcreation example
*** Specifies the information required when creating a new object.

* create our variables..
    data gr_objectcreation type /blck/mfi_objectcreation.
    
* instantiate model and call the setters to set values..
    gr_objectcreation-property_values = l_property_values. " (type /BLCK/MFI_PROPERTY_VALUE_TT)

    gr_objectcreation-files = l_files. " (type /BLCK/MFI_UPLOAD_INFO_TT)
    
* pass to example API method
    gcl_exampleapi->update_objectcreation(
      exporting
        i_objectcreation = gr_objectcreation ).
    		
    clear gr_objectcreation.
    
* fetch new instance from example API method
    gcl_exampleapi->get_objectcreation(
      exporting
        i_id = 1
      importing 
        e_200 = gr_objectcreation ).
    		
    write: gr_objectcreation-property_values. " (type /BLCK/MFI_PROPERTY_VALUE_TT)
    write: gr_objectcreation-files. " (type /BLCK/MFI_UPLOAD_INFO_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**property_values** | /BLCK/MFI_PROPERTY_VALUE_TT (**[array of PropertyValue](#markdown-header-model-property_value)**) | Properties for the new object.
**files** | /BLCK/MFI_UPLOAD_INFO_TT (**[array of UploadInfo](#markdown-header-model-upload_info)**) | References previously uploaded files.

* * *
<a name="markdown-header-model-objectversionu"></a> 

# Model: ObjectVersionUpdateInformation



### Example
```abap
*** model objectversionu example

* create our variables..
    data gr_objectversionu type /blck/mfi_objectversionu.
    
* instantiate model and call the setters to set values..
    gr_objectversionu-properties = l_properties. " (type /BLCK/MFI_PROPERTY_VALUE_TT)

    gr_objectversionu-accessed_by_me_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectversionu-checked_out_at_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectversionu-checked_out_to = 42. " (type /BLCK/MFI_INT)

    gr_objectversionu-checked_out_to_user_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectversionu-class = 42. " (type /BLCK/MFI_INT)

    gr_objectversionu-created_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectversionu-deleted = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-display_id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectversionu-files = l_files. " (type /BLCK/MFI_OBJECT_FILE_TT)

    gr_objectversionu-has_assignments = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-hasrelationshipsfromthis = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-has_relationships_to_this = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-is_stub = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-last_modified_utc = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectversionu-object_checked_out = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-objectcheckedouttothisuser = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-object_version_flags = l_object_version_flags. " (type /BLCK/MFI_MFOBJECTVERSIO)

    gr_objectversionu-obj_ver = l_obj_ver. " (type /BLCK/MFI_OBJ_VER)

    gr_objectversionu-single_file = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-thisversionlatesttothisuse = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-title = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectversionu-visible_after_operation = 'X'. " (type /BLCK/MFI_BOOL)

    gr_objectversionu-allow_name_change = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_objectversionu(
      exporting
        i_objectversionu = gr_objectversionu ).
    		
    clear gr_objectversionu.
    
* fetch new instance from example API method
    gcl_exampleapi->get_objectversionu(
      exporting
        i_id = 1
      importing 
        e_200 = gr_objectversionu ).
    		
    write: gr_objectversionu-properties. " (type /BLCK/MFI_PROPERTY_VALUE_TT)
    write: gr_objectversionu-accessed_by_me_utc. " (type /BLCK/MFI_STRING)
    write: gr_objectversionu-checked_out_at_utc. " (type /BLCK/MFI_STRING)
    write: gr_objectversionu-checked_out_to. " (type /BLCK/MFI_INT)
    write: gr_objectversionu-checked_out_to_user_name. " (type /BLCK/MFI_STRING)
    write: gr_objectversionu-class. " (type /BLCK/MFI_INT)
    write: gr_objectversionu-created_utc. " (type /BLCK/MFI_STRING)
    write: gr_objectversionu-deleted. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-display_id. " (type /BLCK/MFI_STRING)
    write: gr_objectversionu-files. " (type /BLCK/MFI_OBJECT_FILE_TT)
    write: gr_objectversionu-has_assignments. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-hasrelationshipsfromthis. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-has_relationships_to_this. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-is_stub. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-last_modified_utc. " (type /BLCK/MFI_STRING)
    write: gr_objectversionu-object_checked_out. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-objectcheckedouttothisuser. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-object_version_flags. " (type /BLCK/MFI_MFOBJECTVERSIO)
    write: gr_objectversionu-obj_ver. " (type /BLCK/MFI_OBJ_VER)
    write: gr_objectversionu-single_file. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-thisversionlatesttothisuse. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-title. " (type /BLCK/MFI_STRING)
    write: gr_objectversionu-visible_after_operation. " (type /BLCK/MFI_BOOL)
    write: gr_objectversionu-allow_name_change. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**properties** | /BLCK/MFI_PROPERTY_VALUE_TT (**[array of PropertyValue](#markdown-header-model-property_value)**) | Object properties
**accessed_by_me_utc** | /BLCK/MFI_STRING | 
**checked_out_at_utc** | /BLCK/MFI_STRING | 
**checked_out_to** | /BLCK/MFI_INT | 
**checked_out_to_user_name** | /BLCK/MFI_STRING | 
**class** | /BLCK/MFI_INT | 
**created_utc** | /BLCK/MFI_STRING | 
**deleted** | /BLCK/MFI_BOOL | 
**display_id** | /BLCK/MFI_STRING | 
**files** | /BLCK/MFI_OBJECT_FILE_TT (**[array of ObjectFile](#markdown-header-model-object_file)**) | 
**has_assignments** | /BLCK/MFI_BOOL | 
**hasrelationshipsfromthis** | /BLCK/MFI_BOOL | 
**has_relationships_to_this** | /BLCK/MFI_BOOL | 
**is_stub** | /BLCK/MFI_BOOL | 
**last_modified_utc** | /BLCK/MFI_STRING | 
**object_checked_out** | /BLCK/MFI_BOOL | 
**objectcheckedouttothisuser** | /BLCK/MFI_BOOL | 
**object_version_flags** | /BLCK/MFI_MFOBJECTVERSIO (**[MFObjectVersionFlag](#markdown-header-enum-mfobjectversio)**) | 
**obj_ver** | /BLCK/MFI_OBJ_VER (**[ObjVer](#markdown-header-model-obj_ver)**) | 
**single_file** | /BLCK/MFI_BOOL | 
**thisversionlatesttothisuse** | /BLCK/MFI_BOOL | 
**title** | /BLCK/MFI_STRING | 
**visible_after_operation** | /BLCK/MFI_BOOL | 
**allow_name_change** | /BLCK/MFI_BOOL | 

* * *
<a name="markdown-header-model-objectsupdatei"></a> 

# Model: ObjectsUpdateInfo



### Example
```abap
*** model objectsupdatei example
*** To    be    used    when    setting    properties   on   multiple   objects.
*** https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/setmultipleobjproperties/

* create our variables..
    data gr_objectsupdatei type /blck/mfi_objectsupdatei.
    
* instantiate model and call the setters to set values..
    gr_objectsupdatei-multiple_object_info = l_multiple_object_info. " (type /BLCK/MFI_OBJECTVERSIONU)
    
* pass to example API method
    gcl_exampleapi->update_objectsupdatei(
      exporting
        i_objectsupdatei = gr_objectsupdatei ).
    		
    clear gr_objectsupdatei.
    
* fetch new instance from example API method
    gcl_exampleapi->get_objectsupdatei(
      exporting
        i_id = 1
      importing 
        e_200 = gr_objectsupdatei ).
    		
    write: gr_objectsupdatei-multiple_object_info. " (type /BLCK/MFI_OBJECTVERSIONU)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**multiple_object_info** | /BLCK/MFI_OBJECTVERSIONU (**[ObjectVersionUpdateInformation](#markdown-header-model-objectversionu)**) | 

* * *
<a name="markdown-header-model-objectworkflow"></a> 

# Model: ObjectWorkflowState



### Example
```abap
*** model objectworkflow example

* create our variables..
    data gr_objectworkflow type /blck/mfi_objectworkflow.
    
* instantiate model and call the setters to set values..
    gr_objectworkflow-state = l_state. " (type /BLCK/MFI_PROPERTY_VALUE)

    gr_objectworkflow-state_id = 42. " (type /BLCK/MFI_INT)

    gr_objectworkflow-state_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectworkflow-workflow = l_workflow. " (type /BLCK/MFI_PROPERTY_VALUE)

    gr_objectworkflow-workflow_id = 42. " (type /BLCK/MFI_INT)

    gr_objectworkflow-workflow_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_objectworkflow-version_comment = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_objectworkflow(
      exporting
        i_objectworkflow = gr_objectworkflow ).
    		
    clear gr_objectworkflow.
    
* fetch new instance from example API method
    gcl_exampleapi->get_objectworkflow(
      exporting
        i_id = 1
      importing 
        e_200 = gr_objectworkflow ).
    		
    write: gr_objectworkflow-state. " (type /BLCK/MFI_PROPERTY_VALUE)
    write: gr_objectworkflow-state_id. " (type /BLCK/MFI_INT)
    write: gr_objectworkflow-state_name. " (type /BLCK/MFI_STRING)
    write: gr_objectworkflow-workflow. " (type /BLCK/MFI_PROPERTY_VALUE)
    write: gr_objectworkflow-workflow_id. " (type /BLCK/MFI_INT)
    write: gr_objectworkflow-workflow_name. " (type /BLCK/MFI_STRING)
    write: gr_objectworkflow-version_comment. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**state** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-property_value)**) | 
**state_id** | /BLCK/MFI_INT | The workflow state ID.
**state_name** | /BLCK/MFI_STRING | The workflow state name.
**workflow** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-property_value)**) | 
**workflow_id** | /BLCK/MFI_INT | The workflow ID.
**workflow_name** | /BLCK/MFI_STRING | The workflow name.
**version_comment** | /BLCK/MFI_STRING | Version comment defined on the workflow transition.

* * *
<a name="markdown-header-model-passwordchange"></a> 

# Model: PasswordChange



### Example
```abap
*** model passwordchange example
*** Information required for changing password.

* create our variables..
    data gr_passwordchange type /blck/mfi_passwordchange.
    
* instantiate model and call the setters to set values..
    gr_passwordchange-old_password = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_passwordchange-new_password = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_passwordchange(
      exporting
        i_passwordchange = gr_passwordchange ).
    		
    clear gr_passwordchange.
    
* fetch new instance from example API method
    gcl_exampleapi->get_passwordchange(
      exporting
        i_id = 1
      importing 
        e_200 = gr_passwordchange ).
    		
    write: gr_passwordchange-old_password. " (type /BLCK/MFI_STRING)
    write: gr_passwordchange-new_password. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**old_password** | /BLCK/MFI_STRING | The current password.
**new_password** | /BLCK/MFI_STRING | The new password.

* * *
<a name="markdown-header-model-plugininfoconf"></a> 

# Model: PluginInfoConfiguration



### Example
```abap
*** model plugininfoconf example
*** The configuration for authentication plugin.

* create our variables..
    data gr_plugininfoconf type /blck/mfi_plugininfoconf.
    
* instantiate model and call the setters to set values..
    gr_plugininfoconf-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_plugininfoconf-is_default = 'X'. " (type /BLCK/MFI_BOOL)

    gr_plugininfoconf-assembly_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_plugininfoconf-bridge_class_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_plugininfoconf-is_scope_independent = 'X'. " (type /BLCK/MFI_BOOL)

    gr_plugininfoconf-protocol = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_plugininfoconf-configuration = l_configuration. " (type /BLCK/MFI_STRING_MT)

    gr_plugininfoconf-configuration_source = l_configuration_source. " (type /BLCK/MFI_STRING_MT)
    
* pass to example API method
    gcl_exampleapi->update_plugininfoconf(
      exporting
        i_plugininfoconf = gr_plugininfoconf ).
    		
    clear gr_plugininfoconf.
    
* fetch new instance from example API method
    gcl_exampleapi->get_plugininfoconf(
      exporting
        i_id = 1
      importing 
        e_200 = gr_plugininfoconf ).
    		
    write: gr_plugininfoconf-name. " (type /BLCK/MFI_STRING)
    write: gr_plugininfoconf-is_default. " (type /BLCK/MFI_BOOL)
    write: gr_plugininfoconf-assembly_name. " (type /BLCK/MFI_STRING)
    write: gr_plugininfoconf-bridge_class_name. " (type /BLCK/MFI_STRING)
    write: gr_plugininfoconf-is_scope_independent. " (type /BLCK/MFI_BOOL)
    write: gr_plugininfoconf-protocol. " (type /BLCK/MFI_STRING)
    write: gr_plugininfoconf-configuration. " (type /BLCK/MFI_STRING_MT)
    write: gr_plugininfoconf-configuration_source. " (type /BLCK/MFI_STRING_MT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**name** | /BLCK/MFI_STRING | The name of the plugin configuration.
**is_default** | /BLCK/MFI_BOOL | Specifies if this is the default plugin configuration.
**assembly_name** | /BLCK/MFI_STRING | Assembly name.
**bridge_class_name** | /BLCK/MFI_STRING | Bridge class name.
**is_scope_independent** | /BLCK/MFI_BOOL | Specifies if this plugin configuration is independent of scope.
**protocol** | /BLCK/MFI_STRING | The used protocol for the plug-in, e.g. SAMLv2.0.
**configuration** | /BLCK/MFI_STRING_MT | The name of the plugin configuration.
**configuration_source** | /BLCK/MFI_STRING_MT | The name of the plugin configuration.

* * *
<a name="markdown-header-model-primitivetypei"></a> 

# Model: PrimitiveTypeInt



### Example
```abap
*** model primitivetypei example
*** https://developer.m-files.com/APIs/REST-API/Reference/structs/primitivetypet/

* create our variables..
    data gr_primitivetypei type /blck/mfi_primitivetypei.
    
* instantiate model and call the setters to set values..
    gr_primitivetypei-value = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_primitivetypei(
      exporting
        i_primitivetypei = gr_primitivetypei ).
    		
    clear gr_primitivetypei.
    
* fetch new instance from example API method
    gcl_exampleapi->get_primitivetypei(
      exporting
        i_id = 1
      importing 
        e_200 = gr_primitivetypei ).
    		
    write: gr_primitivetypei-value. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**value** | /BLCK/MFI_INT | Primitive value.

* * *
<a name="markdown-header-model-property_def"></a> 

# Model: PropertyDef



### Example
```abap
*** model property_def example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~PropertyDef.html

* create our variables..
    data gr_property_def type /blck/mfi_property_def.
    
* instantiate model and call the setters to set values..
    gr_property_def-all_object_types = 'X'. " (type /BLCK/MFI_BOOL)

    gr_property_def-automatic_value = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_property_def-automatic_value_type = l_automatic_value_type. " (type /BLCK/MFI_MFAUTOMATICVAL)

    gr_property_def-based_on_value_list = 'X'. " (type /BLCK/MFI_BOOL)

    gr_property_def-data_type = l_data_type. " (type /BLCK/MFI_MF_DATA_TYPE)

    gr_property_def-id = 42. " (type /BLCK/MFI_INT)

    gr_property_def-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_property_def-object_type = 42. " (type /BLCK/MFI_INT)

    gr_property_def-value_list = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_property_def(
      exporting
        i_property_def = gr_property_def ).
    		
    clear gr_property_def.
    
* fetch new instance from example API method
    gcl_exampleapi->get_property_def(
      exporting
        i_id = 1
      importing 
        e_200 = gr_property_def ).
    		
    write: gr_property_def-all_object_types. " (type /BLCK/MFI_BOOL)
    write: gr_property_def-automatic_value. " (type /BLCK/MFI_STRING)
    write: gr_property_def-automatic_value_type. " (type /BLCK/MFI_MFAUTOMATICVAL)
    write: gr_property_def-based_on_value_list. " (type /BLCK/MFI_BOOL)
    write: gr_property_def-data_type. " (type /BLCK/MFI_MF_DATA_TYPE)
    write: gr_property_def-id. " (type /BLCK/MFI_INT)
    write: gr_property_def-name. " (type /BLCK/MFI_STRING)
    write: gr_property_def-object_type. " (type /BLCK/MFI_INT)
    write: gr_property_def-value_list. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**all_object_types** | /BLCK/MFI_BOOL | 
**automatic_value** | /BLCK/MFI_STRING | 
**automatic_value_type** | /BLCK/MFI_MFAUTOMATICVAL (**[MFAutomaticValueType](#markdown-header-enum-mfautomaticval)**) | 
**based_on_value_list** | /BLCK/MFI_BOOL | 
**data_type** | /BLCK/MFI_MF_DATA_TYPE (**[MFDataType](#markdown-header-enum-mf_data_type)**) | 
**id** | /BLCK/MFI_INT | 
**name** | /BLCK/MFI_STRING | 
**object_type** | /BLCK/MFI_INT | 
**value_list** | /BLCK/MFI_INT | 

* * *
<a name="markdown-header-model-propertyvalues"></a> 

# Model: PropertyValueSuggestion



### Example
```abap
*** model propertyvalues example

* create our variables..
    data gr_propertyvalues type /blck/mfi_propertyvalues.
    
* instantiate model and call the setters to set values..
    gr_propertyvalues-display_value = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_propertyvalues-is_fact = 'X'. " (type /BLCK/MFI_BOOL)

    gr_propertyvalues-is_new_value = 'X'. " (type /BLCK/MFI_BOOL)

    gr_propertyvalues-property_def = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_propertyvalues-quality = 42. " (type /BLCK/MFI_INT)

    gr_propertyvalues-typed_value = l_typed_value. " (type /BLCK/MFI_TYPED_VALUE)
    
* pass to example API method
    gcl_exampleapi->update_propertyvalues(
      exporting
        i_propertyvalues = gr_propertyvalues ).
    		
    clear gr_propertyvalues.
    
* fetch new instance from example API method
    gcl_exampleapi->get_propertyvalues(
      exporting
        i_id = 1
      importing 
        e_200 = gr_propertyvalues ).
    		
    write: gr_propertyvalues-display_value. " (type /BLCK/MFI_STRING)
    write: gr_propertyvalues-is_fact. " (type /BLCK/MFI_BOOL)
    write: gr_propertyvalues-is_new_value. " (type /BLCK/MFI_BOOL)
    write: gr_propertyvalues-property_def. " (type /BLCK/MFI_STRING)
    write: gr_propertyvalues-quality. " (type /BLCK/MFI_INT)
    write: gr_propertyvalues-typed_value. " (type /BLCK/MFI_TYPED_VALUE)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**display_value** | /BLCK/MFI_STRING | 
**is_fact** | /BLCK/MFI_BOOL | 
**is_new_value** | /BLCK/MFI_BOOL | 
**property_def** | /BLCK/MFI_STRING | 
**quality** | /BLCK/MFI_INT | 
**typed_value** | /BLCK/MFI_TYPED_VALUE (**[TypedValue](#markdown-header-model-typed_value)**) | 

* * *
<a name="markdown-header-model-public_key"></a> 

# Model: PublicKey



### Example
```abap
*** model public_key example
*** Server public key information.

* create our variables..
    data gr_public_key type /blck/mfi_public_key.
    
* instantiate model and call the setters to set values..
    gr_public_key-exponent = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_public_key-modulus = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_public_key(
      exporting
        i_public_key = gr_public_key ).
    		
    clear gr_public_key.
    
* fetch new instance from example API method
    gcl_exampleapi->get_public_key(
      exporting
        i_id = 1
      importing 
        e_200 = gr_public_key ).
    		
    write: gr_public_key-exponent. " (type /BLCK/MFI_STRING)
    write: gr_public_key-modulus. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**exponent** | /BLCK/MFI_STRING | Base64URL encoded exponent.
**modulus** | /BLCK/MFI_STRING | Base64URL encoded modulus.

* * *
<a name="markdown-header-model-repositoryaut2"></a> 

# Model: RepositoryAuthenticationStatus



### Example
```abap
*** model repositoryaut2 example
*** Structure defining one external repository authentication status.

* create our variables..
    data gr_repositoryaut2 type /blck/mfi_repositoryaut2.
    
* instantiate model and call the setters to set values..
    gr_repositoryaut2-account_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryaut2-extensionauthenticationspe = l_extensionauthenticationspe. " (type /BLCK/MFI_MFEXTENSIONAUT)

    gr_repositoryaut2-target_id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryaut2-user_id = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_repositoryaut2(
      exporting
        i_repositoryaut2 = gr_repositoryaut2 ).
    		
    clear gr_repositoryaut2.
    
* fetch new instance from example API method
    gcl_exampleapi->get_repositoryaut2(
      exporting
        i_id = 1
      importing 
        e_200 = gr_repositoryaut2 ).
    		
    write: gr_repositoryaut2-account_name. " (type /BLCK/MFI_STRING)
    write: gr_repositoryaut2-extensionauthenticationspe. " (type /BLCK/MFI_MFEXTENSIONAUT)
    write: gr_repositoryaut2-target_id. " (type /BLCK/MFI_STRING)
    write: gr_repositoryaut2-user_id. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**account_name** | /BLCK/MFI_STRING | Account name used for authentication.
**extensionauthenticationspe** | /BLCK/MFI_MFEXTENSIONAUT (**[MFExtensionAuthenticationSpecialUserType](#markdown-header-enum-mfextensionaut)**) | 
**target_id** | /BLCK/MFI_STRING | ID of the target repository.
**user_id** | /BLCK/MFI_INT | ID of the authenticated M-Files user.

* * *
<a name="markdown-header-model-repositoryaut3"></a> 

# Model: RepositoryAuthentication



### Example
```abap
*** model repositoryaut3 example
*** Structure    defining    authentication   data   for   external   repository
*** authentication.   ConfigurationName   is   typically   retrieved   from  the
*** PluginInfoConfiguration.Name         information         returned         in
*** RepositoryAuthenticationTarget.   This   must  be  provided  even  if  basic
*** authentication                            is                           being
*** used.https://developer.m-files.com/APIs/REST-API/Reference/structs/repositoryauthenticationtarget/

* create our variables..
    data gr_repositoryaut3 type /blck/mfi_repositoryaut3.
    
* instantiate model and call the setters to set values..
    gr_repositoryaut3-configuration_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryaut3-username = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryaut3-password = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryaut3-authentication_token = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryaut3-refresh_token = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_repositoryaut3(
      exporting
        i_repositoryaut3 = gr_repositoryaut3 ).
    		
    clear gr_repositoryaut3.
    
* fetch new instance from example API method
    gcl_exampleapi->get_repositoryaut3(
      exporting
        i_id = 1
      importing 
        e_200 = gr_repositoryaut3 ).
    		
    write: gr_repositoryaut3-configuration_name. " (type /BLCK/MFI_STRING)
    write: gr_repositoryaut3-username. " (type /BLCK/MFI_STRING)
    write: gr_repositoryaut3-password. " (type /BLCK/MFI_STRING)
    write: gr_repositoryaut3-authentication_token. " (type /BLCK/MFI_STRING)
    write: gr_repositoryaut3-refresh_token. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**configuration_name** | /BLCK/MFI_STRING | Name of the authentication configuration.
**username** | /BLCK/MFI_STRING | Username used for basic authentication.
**password** | /BLCK/MFI_STRING | Password used for basic authentication.
**authentication_token** | /BLCK/MFI_STRING | The authentication token for plugin authentication. Must be null if using basic username/password authentication
**refresh_token** | /BLCK/MFI_STRING | The refresh token for plugin authentication.

* * *
<a name="markdown-header-model-repositoryauth"></a> 

# Model: RepositoryAuthenticationTarget



### Example
```abap
*** model repositoryauth example

* create our variables..
    data gr_repositoryauth type /blck/mfi_repositoryauth.
    
* instantiate model and call the setters to set values..
    gr_repositoryauth-display_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryauth-icon_id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryauth-id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryauth-plugin_info_configurations = l_plugin_info_configurations. " (type /BLCK/MFI_PLUGININFOCONF)

    gr_repositoryauth-requiresuserspecificauthen = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_repositoryauth-repositoryauthenticationst = l_repositoryauthenticationst. " (type /BLCK/MFI_REPOSITORYAUT2)
    
* pass to example API method
    gcl_exampleapi->update_repositoryauth(
      exporting
        i_repositoryauth = gr_repositoryauth ).
    		
    clear gr_repositoryauth.
    
* fetch new instance from example API method
    gcl_exampleapi->get_repositoryauth(
      exporting
        i_id = 1
      importing 
        e_200 = gr_repositoryauth ).
    		
    write: gr_repositoryauth-display_name. " (type /BLCK/MFI_STRING)
    write: gr_repositoryauth-icon_id. " (type /BLCK/MFI_STRING)
    write: gr_repositoryauth-id. " (type /BLCK/MFI_STRING)
    write: gr_repositoryauth-plugin_info_configurations. " (type /BLCK/MFI_PLUGININFOCONF)
    write: gr_repositoryauth-requiresuserspecificauthen. " (type /BLCK/MFI_STRING)
    write: gr_repositoryauth-repositoryauthenticationst. " (type /BLCK/MFI_REPOSITORYAUT2)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**display_name** | /BLCK/MFI_STRING | Display name of the target repository.
**icon_id** | /BLCK/MFI_STRING | Icon id of the target repository.
**id** | /BLCK/MFI_STRING | ID of the target repository.
**plugin_info_configurations** | /BLCK/MFI_PLUGININFOCONF (**[PluginInfoConfiguration](#markdown-header-model-plugininfoconf)**) | 
**requiresuserspecificauthen** | /BLCK/MFI_STRING | Flag indicating if user specific authentication is required.
**repositoryauthenticationst** | /BLCK/MFI_REPOSITORYAUT2 (**[RepositoryAuthenticationStatus](#markdown-header-model-repositoryaut2)**) | 

* * *
<a name="markdown-header-model-resultsobjectv"></a> 

# Model: ResultsObjectVersion



### Example
```abap
*** model resultsobjectv example
*** Results of a query which might leave only a partial set of items..

* create our variables..
    data gr_resultsobjectv type /blck/mfi_resultsobjectv.
    
* instantiate model and call the setters to set values..
    gr_resultsobjectv-items = l_items. " (type /BLCK/MFI_OBJECT_VERSION_TT)

    gr_resultsobjectv-more_results = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_resultsobjectv(
      exporting
        i_resultsobjectv = gr_resultsobjectv ).
    		
    clear gr_resultsobjectv.
    
* fetch new instance from example API method
    gcl_exampleapi->get_resultsobjectv(
      exporting
        i_id = 1
      importing 
        e_200 = gr_resultsobjectv ).
    		
    write: gr_resultsobjectv-items. " (type /BLCK/MFI_OBJECT_VERSION_TT)
    write: gr_resultsobjectv-more_results. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**items** | /BLCK/MFI_OBJECT_VERSION_TT (**[array of ObjectVersion](#markdown-header-model-object_version)**) | Contains results of a query
**more_results** | /BLCK/MFI_BOOL | True if there were more results which were left out.

* * *
<a name="markdown-header-model-valuelistitem"></a> 

# Model: ValueListItem



### Example
```abap
*** model valuelistitem example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ValueListItem.html

* create our variables..
    data gr_valuelistitem type /blck/mfi_valuelistitem.
    
* instantiate model and call the setters to set values..
    gr_valuelistitem-display_id = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_valuelistitem-has_owner = 'X'. " (type /BLCK/MFI_BOOL)

    gr_valuelistitem-has_parent = 'X'. " (type /BLCK/MFI_BOOL)

    gr_valuelistitem-id = 42. " (type /BLCK/MFI_INT)

    gr_valuelistitem-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_valuelistitem-owner_id = 42. " (type /BLCK/MFI_INT)

    gr_valuelistitem-parent_id = 42. " (type /BLCK/MFI_INT)

    gr_valuelistitem-value_list_id = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_valuelistitem(
      exporting
        i_valuelistitem = gr_valuelistitem ).
    		
    clear gr_valuelistitem.
    
* fetch new instance from example API method
    gcl_exampleapi->get_valuelistitem(
      exporting
        i_id = 1
      importing 
        e_200 = gr_valuelistitem ).
    		
    write: gr_valuelistitem-display_id. " (type /BLCK/MFI_STRING)
    write: gr_valuelistitem-has_owner. " (type /BLCK/MFI_BOOL)
    write: gr_valuelistitem-has_parent. " (type /BLCK/MFI_BOOL)
    write: gr_valuelistitem-id. " (type /BLCK/MFI_INT)
    write: gr_valuelistitem-name. " (type /BLCK/MFI_STRING)
    write: gr_valuelistitem-owner_id. " (type /BLCK/MFI_INT)
    write: gr_valuelistitem-parent_id. " (type /BLCK/MFI_INT)
    write: gr_valuelistitem-value_list_id. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**display_id** | /BLCK/MFI_STRING | 
**has_owner** | /BLCK/MFI_BOOL | 
**has_parent** | /BLCK/MFI_BOOL | 
**id** | /BLCK/MFI_INT | 
**name** | /BLCK/MFI_STRING | 
**owner_id** | /BLCK/MFI_INT | 
**parent_id** | /BLCK/MFI_INT | 
**value_list_id** | /BLCK/MFI_INT | 

* * *
<a name="markdown-header-model-resultsvalueli"></a> 

# Model: ResultsValueListItem



### Example
```abap
*** model resultsvalueli example
*** Results of a query which might leave only a partial set of items..

* create our variables..
    data gr_resultsvalueli type /blck/mfi_resultsvalueli.
    
* instantiate model and call the setters to set values..
    gr_resultsvalueli-items = l_items. " (type /BLCK/MFI_VALUELISTITEM_TT)

    gr_resultsvalueli-more_results = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_resultsvalueli(
      exporting
        i_resultsvalueli = gr_resultsvalueli ).
    		
    clear gr_resultsvalueli.
    
* fetch new instance from example API method
    gcl_exampleapi->get_resultsvalueli(
      exporting
        i_id = 1
      importing 
        e_200 = gr_resultsvalueli ).
    		
    write: gr_resultsvalueli-items. " (type /BLCK/MFI_VALUELISTITEM_TT)
    write: gr_resultsvalueli-more_results. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**items** | /BLCK/MFI_VALUELISTITEM_TT (**[array of ValueListItem](#markdown-header-model-valuelistitem)**) | Contains results of a query
**more_results** | /BLCK/MFI_BOOL | True if there were more results which were left out.

* * *
<a name="markdown-header-model-session_info"></a> 

# Model: SessionInfo



### Example
```abap
*** model session_info example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~SessionInfo.html

* create our variables..
    data gr_session_info type /blck/mfi_session_info.
    
* instantiate model and call the setters to set values..
    gr_session_info-account_name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_session_info-acl_mode = l_acl_mode. " (type /BLCK/MFI_MFACL_MODE)

    gr_session_info-authentication_type = l_authentication_type. " (type /BLCK/MFI_MF_AUTH_TYPE)

    gr_session_info-can_force_undo_checkout = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-canmanagecommonuisettings = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-can_manage_common_views = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-canmanagetraditionalfolder = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-can_materialize_views = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-can_see_all_objects = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-can_see_deleted_objects = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-internal_user = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-licenseallowsmodifications = 'X'. " (type /BLCK/MFI_BOOL)

    gr_session_info-user_id = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_session_info(
      exporting
        i_session_info = gr_session_info ).
    		
    clear gr_session_info.
    
* fetch new instance from example API method
    gcl_exampleapi->get_session_info(
      exporting
        i_id = 1
      importing 
        e_200 = gr_session_info ).
    		
    write: gr_session_info-account_name. " (type /BLCK/MFI_STRING)
    write: gr_session_info-acl_mode. " (type /BLCK/MFI_MFACL_MODE)
    write: gr_session_info-authentication_type. " (type /BLCK/MFI_MF_AUTH_TYPE)
    write: gr_session_info-can_force_undo_checkout. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-canmanagecommonuisettings. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-can_manage_common_views. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-canmanagetraditionalfolder. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-can_materialize_views. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-can_see_all_objects. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-can_see_deleted_objects. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-internal_user. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-licenseallowsmodifications. " (type /BLCK/MFI_BOOL)
    write: gr_session_info-user_id. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**account_name** | /BLCK/MFI_STRING | 
**acl_mode** | /BLCK/MFI_MFACL_MODE (**[MFACLMode](#markdown-header-enum-mfacl_mode)**) | 
**authentication_type** | /BLCK/MFI_MF_AUTH_TYPE (**[MFAuthType](#markdown-header-enum-mf_auth_type)**) | 
**can_force_undo_checkout** | /BLCK/MFI_BOOL | 
**canmanagecommonuisettings** | /BLCK/MFI_BOOL | 
**can_manage_common_views** | /BLCK/MFI_BOOL | 
**canmanagetraditionalfolder** | /BLCK/MFI_BOOL | 
**can_materialize_views** | /BLCK/MFI_BOOL | 
**can_see_all_objects** | /BLCK/MFI_BOOL | 
**can_see_deleted_objects** | /BLCK/MFI_BOOL | 
**internal_user** | /BLCK/MFI_BOOL | 
**licenseallowsmodifications** | /BLCK/MFI_BOOL | 
**user_id** | /BLCK/MFI_INT | 

* * *
<a name="markdown-header-model-statusresponse"></a> 

# Model: StatusResponse



### Example
```abap
*** model statusresponse example
*** Response for status requests.

* create our variables..
    data gr_statusresponse type /blck/mfi_statusresponse.
    
* instantiate model and call the setters to set values..
    gr_statusresponse-successful = 'X'. " (type /BLCK/MFI_BOOL)

    gr_statusresponse-message = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_statusresponse(
      exporting
        i_statusresponse = gr_statusresponse ).
    		
    clear gr_statusresponse.
    
* fetch new instance from example API method
    gcl_exampleapi->get_statusresponse(
      exporting
        i_id = 1
      importing 
        e_200 = gr_statusresponse ).
    		
    write: gr_statusresponse-successful. " (type /BLCK/MFI_BOOL)
    write: gr_statusresponse-message. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**successful** | /BLCK/MFI_BOOL | The result of the status request.
**message** | /BLCK/MFI_STRING | Display message for the status.

* * *
<a name="markdown-header-model-vault"></a> 

# Model: Vault



### Example
```abap
*** model vault example
*** Vault information.

* create our variables..
    data gr_vault type /blck/mfi_vault.
    
* instantiate model and call the setters to set values..
    gr_vault-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_vault-guid = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_vault-authentication = 'ipsum lorem'. " (type /BLCK/MFI_STRING)
    
* pass to example API method
    gcl_exampleapi->update_vault(
      exporting
        i_vault = gr_vault ).
    		
    clear gr_vault.
    
* fetch new instance from example API method
    gcl_exampleapi->get_vault(
      exporting
        i_id = 1
      importing 
        e_200 = gr_vault ).
    		
    write: gr_vault-name. " (type /BLCK/MFI_STRING)
    write: gr_vault-guid. " (type /BLCK/MFI_STRING)
    write: gr_vault-authentication. " (type /BLCK/MFI_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**name** | /BLCK/MFI_STRING | Vault name.
**guid** | /BLCK/MFI_STRING | Vault GUID.
**authentication** | /BLCK/MFI_STRING | Vault-specific authentication token.

* * *
<a name="markdown-header-model-versioncomment"></a> 

# Model: VersionComment



### Example
```abap
*** model versioncomment example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~VersionComment.html

* create our variables..
    data gr_versioncomment type /blck/mfi_versioncomment.
    
* instantiate model and call the setters to set values..
    gr_versioncomment-last_modified_by = l_last_modified_by. " (type /BLCK/MFI_PROPERTY_VALUE)

    gr_versioncomment-obj_ver = l_obj_ver. " (type /BLCK/MFI_OBJ_VER)

    gr_versioncomment-status_changed = l_status_changed. " (type /BLCK/MFI_PROPERTY_VALUE)

    gr_versioncomment-comment = l_comment. " (type /BLCK/MFI_PROPERTY_VALUE)
    
* pass to example API method
    gcl_exampleapi->update_versioncomment(
      exporting
        i_versioncomment = gr_versioncomment ).
    		
    clear gr_versioncomment.
    
* fetch new instance from example API method
    gcl_exampleapi->get_versioncomment(
      exporting
        i_id = 1
      importing 
        e_200 = gr_versioncomment ).
    		
    write: gr_versioncomment-last_modified_by. " (type /BLCK/MFI_PROPERTY_VALUE)
    write: gr_versioncomment-obj_ver. " (type /BLCK/MFI_OBJ_VER)
    write: gr_versioncomment-status_changed. " (type /BLCK/MFI_PROPERTY_VALUE)
    write: gr_versioncomment-comment. " (type /BLCK/MFI_PROPERTY_VALUE)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**last_modified_by** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-property_value)**) | 
**obj_ver** | /BLCK/MFI_OBJ_VER (**[ObjVer](#markdown-header-model-obj_ver)**) | 
**status_changed** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-property_value)**) | 
**comment** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-property_value)**) | 

* * *
<a name="markdown-header-model-webserviceerro"></a> 

# Model: WebServiceError



### Example
```abap
*** model webserviceerro example
*** M-Files Web Service error object.

* create our variables..
    data gr_webserviceerro type /blck/mfi_webserviceerro.
    
* instantiate model and call the setters to set values..
    gr_webserviceerro-status = 42. " (type /BLCK/MFI_INT)

    gr_webserviceerro-url = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_webserviceerro-method = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_webserviceerro-exception = l_exception. " (type /BLCK/MFI_EXCEPTION_INFO)
    
* pass to example API method
    gcl_exampleapi->update_webserviceerro(
      exporting
        i_webserviceerro = gr_webserviceerro ).
    		
    clear gr_webserviceerro.
    
* fetch new instance from example API method
    gcl_exampleapi->get_webserviceerro(
      exporting
        i_id = 1
      importing 
        e_200 = gr_webserviceerro ).
    		
    write: gr_webserviceerro-status. " (type /BLCK/MFI_INT)
    write: gr_webserviceerro-url. " (type /BLCK/MFI_STRING)
    write: gr_webserviceerro-method. " (type /BLCK/MFI_STRING)
    write: gr_webserviceerro-exception. " (type /BLCK/MFI_EXCEPTION_INFO)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**status** | /BLCK/MFI_INT | HTTP Status code
**url** | /BLCK/MFI_STRING | The request URL which caused this error.
**method** | /BLCK/MFI_STRING | The request method.
**exception** | /BLCK/MFI_EXCEPTION_INFO (**[ExceptionInfo](#markdown-header-model-exception_info)**) | 

* * *
<a name="markdown-header-model-workflow"></a> 

# Model: Workflow



### Example
```abap
*** model workflow example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~Workflow.html

* create our variables..
    data gr_workflow type /blck/mfi_workflow.
    
* instantiate model and call the setters to set values..
    gr_workflow-id = 42. " (type /BLCK/MFI_INT)

    gr_workflow-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_workflow-object_class = 42. " (type /BLCK/MFI_INT)
    
* pass to example API method
    gcl_exampleapi->update_workflow(
      exporting
        i_workflow = gr_workflow ).
    		
    clear gr_workflow.
    
* fetch new instance from example API method
    gcl_exampleapi->get_workflow(
      exporting
        i_id = 1
      importing 
        e_200 = gr_workflow ).
    		
    write: gr_workflow-id. " (type /BLCK/MFI_INT)
    write: gr_workflow-name. " (type /BLCK/MFI_STRING)
    write: gr_workflow-object_class. " (type /BLCK/MFI_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | /BLCK/MFI_INT | 
**name** | /BLCK/MFI_STRING | 
**object_class** | /BLCK/MFI_INT | 

* * *
<a name="markdown-header-model-workflow_state"></a> 

# Model: WorkflowState



### Example
```abap
*** model workflow_state example
*** Workflow                          state                         information.
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~State.html

* create our variables..
    data gr_workflow_state type /blck/mfi_workflow_state.
    
* instantiate model and call the setters to set values..
    gr_workflow_state-name = 'ipsum lorem'. " (type /BLCK/MFI_STRING)

    gr_workflow_state-id = 42. " (type /BLCK/MFI_INT)

    gr_workflow_state-selectable = 'X'. " (type /BLCK/MFI_BOOL)
    
* pass to example API method
    gcl_exampleapi->update_workflow_state(
      exporting
        i_workflow_state = gr_workflow_state ).
    		
    clear gr_workflow_state.
    
* fetch new instance from example API method
    gcl_exampleapi->get_workflow_state(
      exporting
        i_id = 1
      importing 
        e_200 = gr_workflow_state ).
    		
    write: gr_workflow_state-name. " (type /BLCK/MFI_STRING)
    write: gr_workflow_state-id. " (type /BLCK/MFI_INT)
    write: gr_workflow_state-selectable. " (type /BLCK/MFI_BOOL)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**name** | /BLCK/MFI_STRING | Workflow state name.
**id** | /BLCK/MFI_INT | Workflow state ID.
**selectable** | /BLCK/MFI_BOOL | Defines whether this state is selectable for the current object.

