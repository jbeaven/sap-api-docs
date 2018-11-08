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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJ_ID (**[obj_id](#markdown-header-model-obj_id)**) |  [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_UPLOAD_INFO
    data gr_http200 type /BLCK/MFI_UPLOAD_INFO.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_UPLOAD_INFO)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_UPLOAD_INFO (**[UploadInfo](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJECTCREATION (**[objectcreation](#markdown-header-model-objectcreation)**) |  
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT_TT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJ_ID_TTT (**[array of obj_id](#markdown-header-model-)**) | Holds file upload ids and property values for fetching automatic metadata. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT_TT (**[array](#markdown-header-model-)**) | successful operation

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
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_force** | /BLCK/MFI_BOOL | If true, DELETE will perform an undo checkout even if the object isn’t checked out to the current user on this computer. [optional]
 **i_all_versions** | /BLCK/MFI_BOOL | If true, DELETE will destroy the whole object. Unlike normal DELETE, this will not require the object to be checked out. [optional]

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTYVALUES_TT
    data gr_http200 type /BLCK/MFI_PROPERTYVALUES_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTYVALUES_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_AUTOMATICMETAD (**[automaticmetad](#markdown-header-model-automaticmetad)**) | Holds file upload ids and property values for fetching automatic metadata. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_PROPERTYVALUES_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_MFCHECKOUTSTAT
    data gr_http200 type /BLCK/MFI_MFCHECKOUTSTAT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_MFCHECKOUTSTAT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_MFCHECKOUTSTAT (**[MFCheckOutStatus](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VERSIONCOMMENT_TT
    data gr_http200 type /BLCK/MFI_VERSIONCOMMENT_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VERSIONCOMMENT_TT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_VERSIONCOMMENT_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_BOOL
    data gr_http200 type /BLCK/MFI_BOOL.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BOOL)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_BOOL | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_BINARY | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_FILE
    data gr_http200 type /BLCK/MFI_OBJECT_FILE.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_FILE)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_FILE (**[ObjectFile](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
*   when the the result of the call is HTTP404 we expect type /BLCK/MFI_BINARY
    data gr_http404 type /BLCK/MFI_BINARY.
        
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
        e_200 = gr_http200
        e_404 = gr_http404 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when 404.
*       do something with gr_http404 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_BINARY | successful operation
 404 | **e_404** | /BLCK/MFI_BINARY | If a preview cannot be generated the service responds with a 404.

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_STRING | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_FILE_TT
    data gr_http200 type /BLCK/MFI_OBJECT_FILE_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_FILE_TT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_FILE_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_object_ids** | /BLCK/MFI_STRING | The object versions are specified, seperated with semicolons, e.g. 0/5/6;0/112/latest;136/2/3 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_STRING | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_BINARY | successful operation
 404 | value not returned |  | If a preview cannot be generated the service responds with a 404.

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSOBJECTV
    data gr_http200 type /BLCK/MFI_RESULTSOBJECTV.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSOBJECTV)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_RESULTSOBJECTV (**[ResultsObjectVersion](#markdown-header-model-)**) | Retrieves objects. The amount of returned objects is limited by the server, by default to 500 items.

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSOBJECTV
    data gr_http200 type /BLCK/MFI_RESULTSOBJECTV.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSOBJECTV)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_RESULTSOBJECTV (**[ResultsObjectVersion](#markdown-header-model-)**) | Retrieves objects of the given type. The amount of returned objects is limited by the server.

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_VALUE_TT
    data gr_http200 type /BLCK/MFI_PROPERTY_VALUE_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_VALUE_TT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_PROPERTY_VALUE_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_VALUE
    data gr_http200 type /BLCK/MFI_PROPERTY_VALUE.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_VALUE)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_PROPERTY_VALUE (**[PropertyValue](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_INT | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECTWORKFLOW
    data gr_http200 type /BLCK/MFI_OBJECTWORKFLOW.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECTWORKFLOW)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECTWORKFLOW (**[ObjectWorkflowState](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_INT | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array](#markdown-header-model-)**) | successful operation

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
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_file** | /BLCK/MFI_INT |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP204 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http204 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_204 = gr_http204 ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       do something with gr_http204 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
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
 204 | **e_204** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT_TT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJECTSUPDATEI (**[objectsupdatei](#markdown-header-model-objectsupdatei)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION (**[ObjectVersion](#markdown-header-model-)**) | successful operation
 401 | value not returned |  | If the object has an automatic title PUT will result in 401.

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_PROPERTY_VALUE_TTT (**[array of property_value](#markdown-header-model-)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_PROPERTY_VALUE (**[property_value](#markdown-header-model-property_value)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJECTWORKFLOW (**[objectworkflow](#markdown-header-model-objectworkflow)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation
 401 | value not returned |  | If the object has an automatic workflow state PUT will result in 401.

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_PROPERTY_VALUE_TTT (**[array of property_value](#markdown-header-model-)**) |  
 **i_type** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  
 **i_version** | /BLCK/MFI_STRING |  [default "latest"]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJECT
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJECT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJECT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_OBJ_ID (**[obj_id](#markdown-header-model-obj_id)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJECT (**[ExtendedObjectVersion](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_VERSION_TT
    data gr_http200 type /BLCK/MFI_OBJECT_VERSION_TT.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_VERSION_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJECT_VERSION_TT (**[array](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_REPOSITORYAUTH_TT
    data gr_http200 type /BLCK/MFI_REPOSITORYAUTH_TT.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_REPOSITORYAUTH_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_REPOSITORYAUTH_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_REPOSITORYAUT2
    data gr_http200 type /BLCK/MFI_REPOSITORYAUT2.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_REPOSITORYAUT2)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_REPOSITORYAUT3 (**[repositoryaut3](#markdown-header-model-repositoryaut3)**) |  
 **i_targetid** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_REPOSITORYAUT2 (**[RepositoryAuthenticationStatus](#markdown-header-model-)**) | successful operation

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
 **i_targetid** | /BLCK/MFI_INT |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_AUTHENTICATION (**[authentication](#markdown-header-model-authentication)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_STRING | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_PUBLIC_KEY
    data gr_http200 type /BLCK/MFI_PUBLIC_KEY.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PUBLIC_KEY)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_PUBLIC_KEY (**[PublicKey](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_STATUSRESPONSE
    data gr_http200 type /BLCK/MFI_STATUSRESPONSE.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STATUSRESPONSE)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_STATUSRESPONSE (**[StatusResponse](#markdown-header-model-)**) | successful operation
 503 | value not returned |  | the M-Files server is unavailable

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_REPOSITORYAUTH_TT
    data gr_http200 type /BLCK/MFI_REPOSITORYAUTH_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_REPOSITORYAUTH_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_online** | /BLCK/MFI_BOOL | If true, return only online vaults. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_REPOSITORYAUTH_TT (**[array](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_STRING | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_SESSION_INFO
    data gr_http200 type /BLCK/MFI_SESSION_INFO.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_SESSION_INFO)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_SESSION_INFO (**[SessionInfo](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_PRIMITIVETYPEI
    data gr_http200 type /BLCK/MFI_PRIMITIVETYPEI.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PRIMITIVETYPEI)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_PRIMITIVETYPEI (**[PrimitiveTypeInt](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VAULT
    data gr_http200 type /BLCK/MFI_VAULT.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VAULT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_VAULT (**[Vault](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VAULT_TT
    data gr_http200 type /BLCK/MFI_VAULT_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VAULT_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_AUTHENTICATION (**[authentication](#markdown-header-model-authentication)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_VAULT_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VAULT
    data gr_http200 type /BLCK/MFI_VAULT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_VAULT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/MFI_VAULT (**[vault](#markdown-header-model-vault)**) |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_VAULT (**[Vault](#markdown-header-model-)**) | successful operation
 409 | value not returned |  | there are multiple vaults with the same name

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
    data gr_http200 type /BLCK/MFI_VALUELISTITEM.
        
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
        e_200 = gr_http200 ).

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
 **i_body** | /BLCK/MFI_VALUELISTITEM (**[valuelistitem](#markdown-header-model-valuelistitem)**) |  
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_BINARY | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_guid** | /BLCK/MFI_STRING |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_INT | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_EXTENDEDOBJEC2
    data gr_http200 type /BLCK/MFI_EXTENDEDOBJEC2.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_EXTENDEDOBJEC2)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_EXTENDEDOBJEC2 (**[ExtendedObjectClass](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
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
        
*** call the API method get_item via HTTP GET
    /blck/mfi_cl_VaultApi=>get_item(
      exporting
        i_id = gvi_id
        i_objectid = gvi_objectid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

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
 200 | **e_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_STRING
    data gr_http200 type /BLCK/MFI_STRING.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_STRING)
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
 200 | **e_200** | /BLCK/MFI_STRING | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSVALUELI
    data gr_http200 type /BLCK/MFI_RESULTSVALUELI.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSVALUELI)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_RESULTSVALUELI (**[ResultsValueListItem](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_CLASS_TT
    data gr_http200 type /BLCK/MFI_OBJECT_CLASS_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_CLASS_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_objtype** | /BLCK/MFI_INT | Object type ID. Filters the returned classes by object type. Only classes belonging to the object type are returned. [optional]

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJECT_CLASS_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE
    data gr_http200 type /BLCK/MFI_OBJ_TYPE.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJ_TYPE (**[ObjType](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJECT_CLASS_TT
    data gr_http200 type /BLCK/MFI_OBJECT_CLASS_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJECT_CLASS_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJECT_CLASS_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_BINARY
    data gr_http200 type /BLCK/MFI_BINARY.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_BINARY)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_type** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_BINARY | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE_TT
    data gr_http200 type /BLCK/MFI_OBJ_TYPE_TT.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJ_TYPE_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE
    data gr_http200 type /BLCK/MFI_OBJ_TYPE.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJ_TYPE (**[ObjType](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_OBJ_TYPE_TT
    data gr_http200 type /BLCK/MFI_OBJ_TYPE_TT.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_OBJ_TYPE_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_OBJ_TYPE_TT (**[array](#markdown-header-model-)**) | successful operation

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
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_DEF_TT
    data gr_http200 type /BLCK/MFI_PROPERTY_DEF_TT.
        


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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_DEF_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_PROPERTY_DEF_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_PROPERTY_DEF
    data gr_http200 type /BLCK/MFI_PROPERTY_DEF.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_PROPERTY_DEF)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_PROPERTY_DEF (**[PropertyDef](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW
    data gr_http200 type /BLCK/MFI_WORKFLOW.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_WORKFLOW (**[Workflow](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_STATE
    data gr_http200 type /BLCK/MFI_WORKFLOW_STATE.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_STATE)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_WORKFLOW_STATE (**[WorkflowState](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_STATE_TT
    data gr_http200 type /BLCK/MFI_WORKFLOW_STATE_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_STATE_TT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_WORKFLOW_STATE_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_STATE_TT
    data gr_http200 type /BLCK/MFI_WORKFLOW_STATE_TT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_STATE_TT)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_WORKFLOW_STATE_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   for parameter i_id:
*   a simple ABAP primitive of type /BLCK/MFI_INT
    data gvi_id type /BLCK/MFI_INT.
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_WORKFLOW_TT
    data gr_http200 type /BLCK/MFI_WORKFLOW_TT.
        
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
        
*** call the API method get_workflows via HTTP GET
    /blck/mfi_cl_VaultApi=>get_workflows(
      exporting
        i_id = gvi_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_WORKFLOW_TT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_id** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_WORKFLOW_TT (**[array](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
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
        e_200 = gr_http200 ).

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
 200 | **e_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_VALUELISTITEM
    data gr_http200 type /BLCK/MFI_VALUELISTITEM.
        
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
        e_200 = gr_http200 ).

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
 **i_body** | /BLCK/MFI_STRING |  
 **i_id** | /BLCK/MFI_INT |  
 **i_objectid** | /BLCK/MFI_INT |  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_VALUELISTITEM (**[ValueListItem](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_MFREFRESHSTATU
    data gr_http200 type /BLCK/MFI_MFREFRESHSTATU.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_MFREFRESHSTATU)
      when others.
* handle the general case..
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
 200 | **e_200** | /BLCK/MFI_MFREFRESHSTATU (**[MFRefreshStatus](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_FOLDERCONTENTI
    data gr_http200 type /BLCK/MFI_FOLDERCONTENTI.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_FOLDERCONTENTI)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/MFI_STRING | Any number of path segments separated with &#x27;/&#x27;. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_FOLDERCONTENTI (**[FolderContentItems](#markdown-header-model-)**) | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_INT
    data gr_http200 type /BLCK/MFI_INT.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_INT)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/MFI_STRING | Any number of path segments separated with &#x27;/&#x27;. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_INT | successful operation

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
*   when the the result of the call is HTTP200 we expect type /BLCK/MFI_RESULTSOBJECTV
    data gr_http200 type /BLCK/MFI_RESULTSOBJECTV.
        
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
        e_200 = gr_http200 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/MFI_RESULTSOBJECTV)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_path** | /BLCK/MFI_STRING | Any number of path segments separated with &#x27;/&#x27;. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/MFI_RESULTSOBJECTV (**[ResultsObjectVersion](#markdown-header-model-)**) | successful operation

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-associatedprop"></a> 

# Model: associatedprop



### Example
```abap
*** model associatedprop example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~AssociatedPropertyDef.html

* create our variables..
    data gcl_associatedprop type ref to /blck/mdl_cl_associatedprop.
    
* instantiate model and call the setters to set values..
    gcl_associatedprop = /blck/mdl_cl_associatedprop=>create( ).
    gcl_associatedprop->set_property_def( 42 ). " (type i)
    gcl_associatedprop->set_required( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_associatedprop(
    	exporting
    		i_associatedprop = gcl_associatedprop ).
    		
    clear gcl_associatedprop.
    
* fetch new instance from example API method
    gcl_associatedprop = gcl_exampleapi->get_associatedprop(
    	exporting
    		i_id = 1 ).
    		
    l_property_def = gcl_associatedprop->get_property_def( ). " (type i)
    l_required = gcl_associatedprop->get_required( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**property_def** | i |  | [optional] [default to null]
**required** | flag |  | [optional] [default to null]

* * *
<a name="markdown-header-model-authentication"></a> 

# Model: authentication



### Example
```abap
*** model authentication example
*** Structures the details used for authentication with the M-Files Web Service.

* create our variables..
    data gcl_authentication type ref to /blck/mdl_cl_authentication.
    
* instantiate model and call the setters to set values..
    gcl_authentication = /blck/mdl_cl_authentication=>create( ).
    gcl_authentication->set_username( 'ipsum lorem' ). " (type string)
    gcl_authentication->set_password( 'ipsum lorem' ). " (type string)
    gcl_authentication->set_domain( 'ipsum lorem' ). " (type string)
    gcl_authentication->set_windows_user( 'X' ). " (type flag)
    gcl_authentication->set_computer_name( 'ipsum lorem' ). " (type string)
    gcl_authentication->set_vault_guid( 'ipsum lorem' ). " (type string)
    gcl_authentication->set_expiration( 'ipsum lorem' ). " (type string)
    gcl_authentication->set_read_only( 'X' ). " (type flag)
    gcl_authentication->set_url( 'ipsum lorem' ). " (type string)
    gcl_authentication->set_method( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_authentication(
    	exporting
    		i_authentication = gcl_authentication ).
    		
    clear gcl_authentication.
    
* fetch new instance from example API method
    gcl_authentication = gcl_exampleapi->get_authentication(
    	exporting
    		i_id = 1 ).
    		
    l_username = gcl_authentication->get_username( ). " (type string)
    l_password = gcl_authentication->get_password( ). " (type string)
    l_domain = gcl_authentication->get_domain( ). " (type string)
    l_windows_user = gcl_authentication->get_windows_user( ). " (type flag)
    l_computer_name = gcl_authentication->get_computer_name( ). " (type string)
    l_vault_guid = gcl_authentication->get_vault_guid( ). " (type string)
    l_expiration = gcl_authentication->get_expiration( ). " (type string)
    l_read_only = gcl_authentication->get_read_only( ). " (type flag)
    l_url = gcl_authentication->get_url( ). " (type string)
    l_method = gcl_authentication->get_method( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**username** | string |  | [optional] [default to null]
**password** | string |  | [optional] [default to null]
**domain** | string |  | [optional] [default to null]
**windows_user** | flag |  | [optional] [default to null]
**computer_name** | string |  | [optional] [default to null]
**vault_guid** | string |  | [optional] [default to null]
**expiration** | string |  | [optional] [default to null]
**read_only** | flag |  | [optional] [default to null]
**url** | string |  | [optional] [default to null]
**method** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-obj_ver"></a> 

# Model: obj_ver



### Example
```abap
*** model obj_ver example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjVer.html

* create our variables..
    data gcl_obj_ver type ref to /blck/mdl_cl_obj_ver.
    
* instantiate model and call the setters to set values..
    gcl_obj_ver = /blck/mdl_cl_obj_ver=>create( ).
    gcl_obj_ver->set_id( 42 ). " (type i)
    gcl_obj_ver->set_type( 42 ). " (type i)
    gcl_obj_ver->set_version( 42 ). " (type i)
    gcl_obj_ver->set_external_repository_name( 'ipsum lorem' ). " (type string)
    gcl_obj_ver->set_externalrepositoryobjectid( 'ipsum lorem' ). " (type string)
    gcl_obj_ver->set_externalrepositoryobjectve( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_obj_ver(
    	exporting
    		i_obj_ver = gcl_obj_ver ).
    		
    clear gcl_obj_ver.
    
* fetch new instance from example API method
    gcl_obj_ver = gcl_exampleapi->get_obj_ver(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_obj_ver->get_id( ). " (type i)
    l_type = gcl_obj_ver->get_type( ). " (type i)
    l_version = gcl_obj_ver->get_version( ). " (type i)
    l_external_repository_name = gcl_obj_ver->get_external_repository_name( ). " (type string)
    l_externalrepositoryobjectid = gcl_obj_ver->get_externalrepositoryobjectid( ). " (type string)
    l_externalrepositoryobjectve = gcl_obj_ver->get_externalrepositoryobjectve( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**type** | i |  | [optional] [default to null]
**version** | i |  | [optional] [default to null]
**external_repository_name** | string | (for external objects only) | [optional] [default to null]
**externalrepositoryobjectid** | string | (for external objects only) | [optional] [default to null]
**externalrepositoryobjectve** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-lookup"></a> 

# Model: lookup



### Example
```abap
*** model lookup example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~Lookup.html

* create our variables..
    data gcl_lookup type ref to /blck/mdl_cl_lookup.
    
* instantiate model and call the setters to set values..
    gcl_lookup = /blck/mdl_cl_lookup=>create( ).
    gcl_lookup->set_deleted( 'X' ). " (type flag)
    gcl_lookup->set_display_value( 'ipsum lorem' ). " (type string)
    gcl_lookup->set_hidden( 'X' ). " (type flag)
    gcl_lookup->set_item( 42 ). " (type i)
    gcl_lookup->set_version( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_lookup(
    	exporting
    		i_lookup = gcl_lookup ).
    		
    clear gcl_lookup.
    
* fetch new instance from example API method
    gcl_lookup = gcl_exampleapi->get_lookup(
    	exporting
    		i_id = 1 ).
    		
    l_deleted = gcl_lookup->get_deleted( ). " (type flag)
    l_display_value = gcl_lookup->get_display_value( ). " (type string)
    l_hidden = gcl_lookup->get_hidden( ). " (type flag)
    l_item = gcl_lookup->get_item( ). " (type i)
    l_version = gcl_lookup->get_version( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**deleted** | flag |  | [optional] [default to null]
**display_value** | string |  | [optional] [default to null]
**hidden** | flag |  | [optional] [default to null]
**item** | i |  | [optional] [default to null]
**version** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-enum-mf_data_type"></a> 

# Enum: mf_data_type



### Example
```abap
*** model mf_data_type example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFDataType.html
*** 0: Uninitialized 1: Text 2: Integer 3: Floating 5: Date 6: Time 7: Timestamp
*** 8:  Boolean  9:  Lookup 10: MultiSelectLookup 11: Integer64 12: FILETIME 13:
*** MultiLineText 14: ACL

* create our variables..
    data gcl_mf_data_type type ref to /blck/mdl_cl_mf_data_type.
    
* instantiate model relevant to the enum value we want
    gcl_mf_data_type = /blck/mdl_cl_mf_data_type=>enum_uninitialized( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mf_data_type_state(
    	exporting
    		i_mf_data_type = gcl_mf_data_type ).
    		
    clear gcl_mf_data_type.
    
* fetch result from example API method
    gcl_mf_data_type = gcl_exampleapi->get_mf_data_type_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mf_data_type->is_uninitialized( ) eq 'X'.
*   do something specific to uninitialized case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mf_data_type->get_value( ).
    when /blck/mdl_cl_mf_data_type=>mce_uninitialized.
*     do something specific to uninitialized case..
    when /blck/mdl_cl_mf_data_type=>mce_text.
*     do something specific to text case..
    when /blck/mdl_cl_mf_data_type=>mce_integer.
*     do something specific to integer case..
    when /blck/mdl_cl_mf_data_type=>mce_floating.
*     do something specific to floating case..
    when /blck/mdl_cl_mf_data_type=>mce_date.
*     do something specific to date case..
    when /blck/mdl_cl_mf_data_type=>mce_time.
*     do something specific to time case..
    when /blck/mdl_cl_mf_data_type=>mce_timestamp.
*     do something specific to timestamp case..
    when /blck/mdl_cl_mf_data_type=>mce_boolean.
*     do something specific to boolean case..
    when /blck/mdl_cl_mf_data_type=>mce_lookup.
*     do something specific to lookup case..
    when /blck/mdl_cl_mf_data_type=>mce_multi_select_lookup.
*     do something specific to multi_select_lookup case..
    when /blck/mdl_cl_mf_data_type=>mce_integer64.
*     do something specific to integer64 case..
    when /blck/mdl_cl_mf_data_type=>mce_filetime.
*     do something specific to filetime case..
    when /blck/mdl_cl_mf_data_type=>mce_multi_line_text.
*     do something specific to multi_line_text case..
    when /blck/mdl_cl_mf_data_type=>mce_acl.
*     do something specific to acl case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**uninitialized** | 0 | /blck/mdl_cl_mf_data_type=>enum_uninitialized( ).
**text** | 1 | /blck/mdl_cl_mf_data_type=>enum_text( ).
**integer** | 2 | /blck/mdl_cl_mf_data_type=>enum_integer( ).
**floating** | 3 | /blck/mdl_cl_mf_data_type=>enum_floating( ).
**date** | 5 | /blck/mdl_cl_mf_data_type=>enum_date( ).
**time** | 6 | /blck/mdl_cl_mf_data_type=>enum_time( ).
**timestamp** | 7 | /blck/mdl_cl_mf_data_type=>enum_timestamp( ).
**boolean** | 8 | /blck/mdl_cl_mf_data_type=>enum_boolean( ).
**lookup** | 9 | /blck/mdl_cl_mf_data_type=>enum_lookup( ).
**multi_select_lookup** | 10 | /blck/mdl_cl_mf_data_type=>enum_multi_select_lookup( ).
**integer64** | 11 | /blck/mdl_cl_mf_data_type=>enum_integer64( ).
**filetime** | 12 | /blck/mdl_cl_mf_data_type=>enum_filetime( ).
**multi_line_text** | 13 | /blck/mdl_cl_mf_data_type=>enum_multi_line_text( ).
**acl** | 14 | /blck/mdl_cl_mf_data_type=>enum_acl( ).

* * *
<a name="markdown-header-model-typed_value"></a> 

# Model: typed_value



### Example
```abap
*** model typed_value example
*** A  &#x27;typed  value&#x27;  represents  a value, such as text, number, date or lookup
*** item.                                                                       
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~TypedValue.html

* create our variables..
    data gcl_typed_value type ref to /blck/mdl_cl_typed_value.
    
* instantiate model and call the setters to set values..
    gcl_typed_value = /blck/mdl_cl_typed_value=>create( ).
    gcl_typed_value->set_data_type( l_data_type ). " (type /BLCK/MFI_mf_data_type)
    gcl_typed_value->set_has_value( 'X' ). " (type flag)
    gcl_typed_value->set_value( 'ipsum lorem' ). " (type string)
    gcl_typed_value->set_lookup( l_lookup ). " (type /BLCK/MFI_lookup)
    gcl_typed_value->set_lookups( l_lookups ). " (type /BLCK/MFI_lookup_tt)
    gcl_typed_value->set_display_value( 'ipsum lorem' ). " (type string)
    gcl_typed_value->set_sorting_key( 'ipsum lorem' ). " (type string)
    gcl_typed_value->set_serialized_value( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_typed_value(
    	exporting
    		i_typed_value = gcl_typed_value ).
    		
    clear gcl_typed_value.
    
* fetch new instance from example API method
    gcl_typed_value = gcl_exampleapi->get_typed_value(
    	exporting
    		i_id = 1 ).
    		
    l_data_type = gcl_typed_value->get_data_type( ). " (type /BLCK/MFI_mf_data_type)
    l_has_value = gcl_typed_value->get_has_value( ). " (type flag)
    l_value = gcl_typed_value->get_value( ). " (type string)
    l_lookup = gcl_typed_value->get_lookup( ). " (type /BLCK/MFI_lookup)
    l_lookups = gcl_typed_value->get_lookups( ). " (type /BLCK/MFI_lookup_tt)
    l_display_value = gcl_typed_value->get_display_value( ). " (type string)
    l_sorting_key = gcl_typed_value->get_sorting_key( ). " (type string)
    l_serialized_value = gcl_typed_value->get_serialized_value( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**data_type** | /BLCK/MFI_mf_data_type (**[mf_data_type](#markdown-header-enum-mf_data_type)**) |  | [optional] [default to null]
**has_value** | flag | Specifies whether the typed value contains a real value. | [optional] [default to null]
**value** | string | Specifies the string, number or boolean value when the DataType is not a lookup type. | [optional] [default to null]
**lookup** | /BLCK/MFI_lookup (**[lookup](#markdown-header-model-lookup)**) |  | [optional] [default to null]
**lookups** | /BLCK/MFI_lookup_tt (**[array of lookup](#markdown-header-model-lookup)**) | Specifies the collection of Lookups when the DataType is MultiSelectLookup. | [optional] [default to null]
**display_value** | string | Provides the value formatted for display. | [optional] [default to null]
**sorting_key** | string | Provides a key that can be used to sort TypedValues | [optional] [default to null]
**serialized_value** | string | Provides the typed value in a serialized format suitable to be used in URIs. | [optional] [default to null]

* * *
<a name="markdown-header-model-property_value"></a> 

# Model: property_value



### Example
```abap
*** model property_value example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~PropertyValue.html

* create our variables..
    data gcl_property_value type ref to /blck/mdl_cl_property_value.
    
* instantiate model and call the setters to set values..
    gcl_property_value = /blck/mdl_cl_property_value=>create( ).
    gcl_property_value->set_property_def( 42 ). " (type i)
    gcl_property_value->set_typed_value( l_typed_value ). " (type /BLCK/MFI_typed_value)
    
* pass to example API method
    gcl_exampleapi->update_property_value(
    	exporting
    		i_property_value = gcl_property_value ).
    		
    clear gcl_property_value.
    
* fetch new instance from example API method
    gcl_property_value = gcl_exampleapi->get_property_value(
    	exporting
    		i_id = 1 ).
    		
    l_property_def = gcl_property_value->get_property_def( ). " (type i)
    l_typed_value = gcl_property_value->get_typed_value( ). " (type /BLCK/MFI_typed_value)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**property_def** | i |  | [optional] [default to null]
**typed_value** | /BLCK/MFI_typed_value (**[typed_value](#markdown-header-model-typed_value)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-automaticmetad"></a> 

# Model: automaticmetad



### Example
```abap
*** model automaticmetad example
*** Holds  file  upload ids and property values for fetching automatic metadata.
*** This struct is used when automatic metadata is fetched from server.

* create our variables..
    data gcl_automaticmetad type ref to /blck/mdl_cl_automaticmetad.
    
* instantiate model and call the setters to set values..
    gcl_automaticmetad = /blck/mdl_cl_automaticmetad=>create( ).
    gcl_automaticmetad->set_upload_ids( l_upload_ids ). " (type /blck/api_i_tt)
    gcl_automaticmetad->set_property_values( l_property_values ). " (type /BLCK/MFI_property_value_tt)
    gcl_automaticmetad->set_obj_ver( l_obj_ver ). " (type /BLCK/MFI_obj_ver)
    gcl_automaticmetad->set_object_type( 42 ). " (type i)
    gcl_automaticmetad->set_metadata_provider_ids( l_metadata_provider_ids ). " (type /blck/api_string_tt)
    gcl_automaticmetad->set_custom_data( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_automaticmetad(
    	exporting
    		i_automaticmetad = gcl_automaticmetad ).
    		
    clear gcl_automaticmetad.
    
* fetch new instance from example API method
    gcl_automaticmetad = gcl_exampleapi->get_automaticmetad(
    	exporting
    		i_id = 1 ).
    		
    l_upload_ids = gcl_automaticmetad->get_upload_ids( ). " (type /blck/api_i_tt)
    l_property_values = gcl_automaticmetad->get_property_values( ). " (type /BLCK/MFI_property_value_tt)
    l_obj_ver = gcl_automaticmetad->get_obj_ver( ). " (type /BLCK/MFI_obj_ver)
    l_object_type = gcl_automaticmetad->get_object_type( ). " (type i)
    l_metadata_provider_ids = gcl_automaticmetad->get_metadata_provider_ids( ). " (type /blck/api_string_tt)
    l_custom_data = gcl_automaticmetad->get_custom_data( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**upload_ids** | /blck/api_i_tt | List of temporary file upload ids. | [optional] [default to null]
**property_values** | /BLCK/MFI_property_value_tt (**[array of property_value](#markdown-header-model-property_value)**) | Array of object’s current property values. | [optional] [default to null]
**obj_ver** | /BLCK/MFI_obj_ver (**[obj_ver](#markdown-header-model-obj_ver)**) |  | [optional] [default to null]
**object_type** | i | The object type of the new object. | [optional] [default to null]
**metadata_provider_ids** | /blck/api_string_tt | List of metadata provider ids. | [optional] [default to null]
**custom_data** | string | Custom data provided to the providers. | [optional] [default to null]

* * *
<a name="markdown-header-model-class_group"></a> 

# Model: class_group



### Example
```abap
*** model class_group example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ClassGroup.html

* create our variables..
    data gcl_class_group type ref to /blck/mdl_cl_class_group.
    
* instantiate model and call the setters to set values..
    gcl_class_group = /blck/mdl_cl_class_group=>create( ).
    gcl_class_group->set_name( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_class_group(
    	exporting
    		i_class_group = gcl_class_group ).
    		
    clear gcl_class_group.
    
* fetch new instance from example API method
    gcl_class_group = gcl_exampleapi->get_class_group(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_class_group->get_name( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-stacktraceelem"></a> 

# Model: stacktraceelem



### Example
```abap
*** model stacktraceelem example
*** M-Files Web Service error stack trace element.

* create our variables..
    data gcl_stacktraceelem type ref to /blck/mdl_cl_stacktraceelem.
    
* instantiate model and call the setters to set values..
    gcl_stacktraceelem = /blck/mdl_cl_stacktraceelem=>create( ).
    gcl_stacktraceelem->set_file_name( 'ipsum lorem' ). " (type string)
    gcl_stacktraceelem->set_line_number( 42 ). " (type i)
    gcl_stacktraceelem->set_class_name( 'ipsum lorem' ). " (type string)
    gcl_stacktraceelem->set_method_name( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_stacktraceelem(
    	exporting
    		i_stacktraceelem = gcl_stacktraceelem ).
    		
    clear gcl_stacktraceelem.
    
* fetch new instance from example API method
    gcl_stacktraceelem = gcl_exampleapi->get_stacktraceelem(
    	exporting
    		i_id = 1 ).
    		
    l_file_name = gcl_stacktraceelem->get_file_name( ). " (type string)
    l_line_number = gcl_stacktraceelem->get_line_number( ). " (type i)
    l_class_name = gcl_stacktraceelem->get_class_name( ). " (type string)
    l_method_name = gcl_stacktraceelem->get_method_name( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**file_name** | string |  | [optional] [default to null]
**line_number** | i |  | [optional] [default to null]
**class_name** | string |  | [optional] [default to null]
**method_name** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-exceptioninfo3"></a> 

# Model: exceptioninfo3



### Example
```abap
*** model exceptioninfo3 example

* create our variables..
    data gcl_exceptioninfo3 type ref to /blck/mdl_cl_exceptioninfo3.
    
* instantiate model and call the setters to set values..
    gcl_exceptioninfo3 = /blck/mdl_cl_exceptioninfo3=>create( ).
    gcl_exceptioninfo3->set_message( 'ipsum lorem' ). " (type string)
    gcl_exceptioninfo3->set_stack( l_stack ). " (type /BLCK/MFI_stacktraceelem_tt)
    
* pass to example API method
    gcl_exampleapi->update_exceptioninfo3(
    	exporting
    		i_exceptioninfo3 = gcl_exceptioninfo3 ).
    		
    clear gcl_exceptioninfo3.
    
* fetch new instance from example API method
    gcl_exceptioninfo3 = gcl_exampleapi->get_exceptioninfo3(
    	exporting
    		i_id = 1 ).
    		
    l_message = gcl_exceptioninfo3->get_message( ). " (type string)
    l_stack = gcl_exceptioninfo3->get_stack( ). " (type /BLCK/MFI_stacktraceelem_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**message** | string | The raw error message. | [optional] [default to null]
**stack** | /BLCK/MFI_stacktraceelem_tt (**[array of stacktraceelem](#markdown-header-model-stacktraceelem)**) | M-Files Web Service server-side stack trace. | [optional] [default to null]

* * *
<a name="markdown-header-model-exceptioninfo2"></a> 

# Model: exceptioninfo2



### Example
```abap
*** model exceptioninfo2 example

* create our variables..
    data gcl_exceptioninfo2 type ref to /blck/mdl_cl_exceptioninfo2.
    
* instantiate model and call the setters to set values..
    gcl_exceptioninfo2 = /blck/mdl_cl_exceptioninfo2=>create( ).
    gcl_exceptioninfo2->set_message( 'ipsum lorem' ). " (type string)
    gcl_exceptioninfo2->set_inner_exception( l_inner_exception ). " (type /BLCK/MFI_exceptioninfo3)
    gcl_exceptioninfo2->set_stack( l_stack ). " (type /BLCK/MFI_stacktraceelem_tt)
    
* pass to example API method
    gcl_exampleapi->update_exceptioninfo2(
    	exporting
    		i_exceptioninfo2 = gcl_exceptioninfo2 ).
    		
    clear gcl_exceptioninfo2.
    
* fetch new instance from example API method
    gcl_exceptioninfo2 = gcl_exampleapi->get_exceptioninfo2(
    	exporting
    		i_id = 1 ).
    		
    l_message = gcl_exceptioninfo2->get_message( ). " (type string)
    l_inner_exception = gcl_exceptioninfo2->get_inner_exception( ). " (type /BLCK/MFI_exceptioninfo3)
    l_stack = gcl_exceptioninfo2->get_stack( ). " (type /BLCK/MFI_stacktraceelem_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**message** | string | The raw error message. | [optional] [default to null]
**inner_exception** | /BLCK/MFI_exceptioninfo3 (**[exceptioninfo3](#markdown-header-model-exceptioninfo3)**) |  | [optional] [default to null]
**stack** | /BLCK/MFI_stacktraceelem_tt (**[array of stacktraceelem](#markdown-header-model-stacktraceelem)**) | M-Files Web Service server-side stack trace. | [optional] [default to null]

* * *
<a name="markdown-header-model-exception_info"></a> 

# Model: exception_info



### Example
```abap
*** model exception_info example

* create our variables..
    data gcl_exception_info type ref to /blck/mdl_cl_exception_info.
    
* instantiate model and call the setters to set values..
    gcl_exception_info = /blck/mdl_cl_exception_info=>create( ).
    gcl_exception_info->set_message( 'ipsum lorem' ). " (type string)
    gcl_exception_info->set_inner_exception( l_inner_exception ). " (type /BLCK/MFI_exceptioninfo2)
    gcl_exception_info->set_stack( l_stack ). " (type /BLCK/MFI_stacktraceelem_tt)
    
* pass to example API method
    gcl_exampleapi->update_exception_info(
    	exporting
    		i_exception_info = gcl_exception_info ).
    		
    clear gcl_exception_info.
    
* fetch new instance from example API method
    gcl_exception_info = gcl_exampleapi->get_exception_info(
    	exporting
    		i_id = 1 ).
    		
    l_message = gcl_exception_info->get_message( ). " (type string)
    l_inner_exception = gcl_exception_info->get_inner_exception( ). " (type /BLCK/MFI_exceptioninfo2)
    l_stack = gcl_exception_info->get_stack( ). " (type /BLCK/MFI_stacktraceelem_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**message** | string | The raw error message. | [optional] [default to null]
**inner_exception** | /BLCK/MFI_exceptioninfo2 (**[exceptioninfo2](#markdown-header-model-exceptioninfo2)**) |  | [optional] [default to null]
**stack** | /BLCK/MFI_stacktraceelem_tt (**[array of stacktraceelem](#markdown-header-model-stacktraceelem)**) | M-Files Web Service server-side stack trace. | [optional] [default to null]

* * *
<a name="markdown-header-enum-mfobjectversio"></a> 

# Enum: mfobjectversio



### Example
```abap
*** model mfobjectversio example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFObjectVersionFlag.html
*** 0: None 1: Completed 2: HasRelatedObjects

* create our variables..
    data gcl_mfobjectversio type ref to /blck/mdl_cl_mfobjectversio.
    
* instantiate model relevant to the enum value we want
    gcl_mfobjectversio = /blck/mdl_cl_mfobjectversio=>enum_none( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfobjectversio_state(
    	exporting
    		i_mfobjectversio = gcl_mfobjectversio ).
    		
    clear gcl_mfobjectversio.
    
* fetch result from example API method
    gcl_mfobjectversio = gcl_exampleapi->get_mfobjectversio_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mfobjectversio->is_none( ) eq 'X'.
*   do something specific to none case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mfobjectversio->get_value( ).
    when /blck/mdl_cl_mfobjectversio=>mce_none.
*     do something specific to none case..
    when /blck/mdl_cl_mfobjectversio=>mce_completed.
*     do something specific to completed case..
    when /blck/mdl_cl_mfobjectversio=>mce_has_related_objects.
*     do something specific to has_related_objects case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**none** | 0 | /blck/mdl_cl_mfobjectversio=>enum_none( ).
**completed** | 1 | /blck/mdl_cl_mfobjectversio=>enum_completed( ).
**has_related_objects** | 2 | /blck/mdl_cl_mfobjectversio=>enum_has_related_objects( ).

* * *
<a name="markdown-header-model-object_file"></a> 

# Model: object_file



### Example
```abap
*** model object_file example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjectFile.html

* create our variables..
    data gcl_object_file type ref to /blck/mdl_cl_object_file.
    
* instantiate model and call the setters to set values..
    gcl_object_file = /blck/mdl_cl_object_file=>create( ).
    gcl_object_file->set_change_time_utc( 'ipsum lorem' ). " (type string)
    gcl_object_file->set_extension( 'ipsum lorem' ). " (type string)
    gcl_object_file->set_id( 42 ). " (type i)
    gcl_object_file->set_name( 'ipsum lorem' ). " (type string)
    gcl_object_file->set_version( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_object_file(
    	exporting
    		i_object_file = gcl_object_file ).
    		
    clear gcl_object_file.
    
* fetch new instance from example API method
    gcl_object_file = gcl_exampleapi->get_object_file(
    	exporting
    		i_id = 1 ).
    		
    l_change_time_utc = gcl_object_file->get_change_time_utc( ). " (type string)
    l_extension = gcl_object_file->get_extension( ). " (type string)
    l_id = gcl_object_file->get_id( ). " (type i)
    l_name = gcl_object_file->get_name( ). " (type string)
    l_version = gcl_object_file->get_version( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**change_time_utc** | string |  | [optional] [default to null]
**extension** | string |  | [optional] [default to null]
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**version** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-model-object_version"></a> 

# Model: object_version



### Example
```abap
*** model object_version example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjectVersion.html

* create our variables..
    data gcl_object_version type ref to /blck/mdl_cl_object_version.
    
* instantiate model and call the setters to set values..
    gcl_object_version = /blck/mdl_cl_object_version=>create( ).
    gcl_object_version->set_accessed_by_me_utc( 'ipsum lorem' ). " (type string)
    gcl_object_version->set_checked_out_at_utc( 'ipsum lorem' ). " (type string)
    gcl_object_version->set_checked_out_to( 42 ). " (type i)
    gcl_object_version->set_checked_out_to_user_name( 'ipsum lorem' ). " (type string)
    gcl_object_version->set_class( 42 ). " (type i)
    gcl_object_version->set_created_utc( 'ipsum lorem' ). " (type string)
    gcl_object_version->set_deleted( 'X' ). " (type flag)
    gcl_object_version->set_display_id( 'ipsum lorem' ). " (type string)
    gcl_object_version->set_files( l_files ). " (type /BLCK/MFI_object_file_tt)
    gcl_object_version->set_has_assignments( 'X' ). " (type flag)
    gcl_object_version->set_hasrelationshipsfromthis( 'X' ). " (type flag)
    gcl_object_version->set_has_relationships_to_this( 'X' ). " (type flag)
    gcl_object_version->set_is_stub( 'X' ). " (type flag)
    gcl_object_version->set_last_modified_utc( 'ipsum lorem' ). " (type string)
    gcl_object_version->set_object_checked_out( 'X' ). " (type flag)
    gcl_object_version->set_objectcheckedouttothisuser( 'X' ). " (type flag)
    gcl_object_version->set_object_version_flags( l_object_version_flags ). " (type /BLCK/MFI_mfobjectversio)
    gcl_object_version->set_obj_ver( l_obj_ver ). " (type /BLCK/MFI_obj_ver)
    gcl_object_version->set_single_file( 'X' ). " (type flag)
    gcl_object_version->set_thisversionlatesttothisuse( 'X' ). " (type flag)
    gcl_object_version->set_title( 'ipsum lorem' ). " (type string)
    gcl_object_version->set_visible_after_operation( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_object_version(
    	exporting
    		i_object_version = gcl_object_version ).
    		
    clear gcl_object_version.
    
* fetch new instance from example API method
    gcl_object_version = gcl_exampleapi->get_object_version(
    	exporting
    		i_id = 1 ).
    		
    l_accessed_by_me_utc = gcl_object_version->get_accessed_by_me_utc( ). " (type string)
    l_checked_out_at_utc = gcl_object_version->get_checked_out_at_utc( ). " (type string)
    l_checked_out_to = gcl_object_version->get_checked_out_to( ). " (type i)
    l_checked_out_to_user_name = gcl_object_version->get_checked_out_to_user_name( ). " (type string)
    l_class = gcl_object_version->get_class( ). " (type i)
    l_created_utc = gcl_object_version->get_created_utc( ). " (type string)
    l_deleted = gcl_object_version->get_deleted( ). " (type flag)
    l_display_id = gcl_object_version->get_display_id( ). " (type string)
    l_files = gcl_object_version->get_files( ). " (type /BLCK/MFI_object_file_tt)
    l_has_assignments = gcl_object_version->get_has_assignments( ). " (type flag)
    l_hasrelationshipsfromthis = gcl_object_version->get_hasrelationshipsfromthis( ). " (type flag)
    l_has_relationships_to_this = gcl_object_version->get_has_relationships_to_this( ). " (type flag)
    l_is_stub = gcl_object_version->get_is_stub( ). " (type flag)
    l_last_modified_utc = gcl_object_version->get_last_modified_utc( ). " (type string)
    l_object_checked_out = gcl_object_version->get_object_checked_out( ). " (type flag)
    l_objectcheckedouttothisuser = gcl_object_version->get_objectcheckedouttothisuser( ). " (type flag)
    l_object_version_flags = gcl_object_version->get_object_version_flags( ). " (type /BLCK/MFI_mfobjectversio)
    l_obj_ver = gcl_object_version->get_obj_ver( ). " (type /BLCK/MFI_obj_ver)
    l_single_file = gcl_object_version->get_single_file( ). " (type flag)
    l_thisversionlatesttothisuse = gcl_object_version->get_thisversionlatesttothisuse( ). " (type flag)
    l_title = gcl_object_version->get_title( ). " (type string)
    l_visible_after_operation = gcl_object_version->get_visible_after_operation( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**accessed_by_me_utc** | string |  | [optional] [default to null]
**checked_out_at_utc** | string |  | [optional] [default to null]
**checked_out_to** | i |  | [optional] [default to null]
**checked_out_to_user_name** | string |  | [optional] [default to null]
**class** | i |  | [optional] [default to null]
**created_utc** | string |  | [optional] [default to null]
**deleted** | flag |  | [optional] [default to null]
**display_id** | string |  | [optional] [default to null]
**files** | /BLCK/MFI_object_file_tt (**[array of object_file](#markdown-header-model-object_file)**) |  | [optional] [default to null]
**has_assignments** | flag |  | [optional] [default to null]
**hasrelationshipsfromthis** | flag |  | [optional] [default to null]
**has_relationships_to_this** | flag |  | [optional] [default to null]
**is_stub** | flag |  | [optional] [default to null]
**last_modified_utc** | string |  | [optional] [default to null]
**object_checked_out** | flag |  | [optional] [default to null]
**objectcheckedouttothisuser** | flag |  | [optional] [default to null]
**object_version_flags** | /BLCK/MFI_mfobjectversio (**[mfobjectversio](#markdown-header-enum-mfobjectversio)**) |  | [optional] [default to null]
**obj_ver** | /BLCK/MFI_obj_ver (**[obj_ver](#markdown-header-model-obj_ver)**) |  | [optional] [default to null]
**single_file** | flag |  | [optional] [default to null]
**thisversionlatesttothisuse** | flag |  | [optional] [default to null]
**title** | string |  | [optional] [default to null]
**visible_after_operation** | flag |  | [optional] [default to null]

* * *
<a name="markdown-header-model-extendedobjec2"></a> 

# Model: extendedobjec2



### Example
```abap
*** model extendedobjec2 example

* create our variables..
    data gcl_extendedobjec2 type ref to /blck/mdl_cl_extendedobjec2.
    
* instantiate model and call the setters to set values..
    gcl_extendedobjec2 = /blck/mdl_cl_extendedobjec2=>create( ).
    gcl_extendedobjec2->set_id( 42 ). " (type i)
    gcl_extendedobjec2->set_name( 'ipsum lorem' ). " (type string)
    gcl_extendedobjec2->set_name_property_def( 42 ). " (type i)
    gcl_extendedobjec2->set_workflow( 42 ). " (type i)
    gcl_extendedobjec2->set_associated_property_defs( l_associated_property_defs ). " (type /BLCK/MFI_associatedprop_tt)
    gcl_extendedobjec2->set_templates( l_templates ). " (type /BLCK/MFI_object_version_tt)
    
* pass to example API method
    gcl_exampleapi->update_extendedobjec2(
    	exporting
    		i_extendedobjec2 = gcl_extendedobjec2 ).
    		
    clear gcl_extendedobjec2.
    
* fetch new instance from example API method
    gcl_extendedobjec2 = gcl_exampleapi->get_extendedobjec2(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_extendedobjec2->get_id( ). " (type i)
    l_name = gcl_extendedobjec2->get_name( ). " (type string)
    l_name_property_def = gcl_extendedobjec2->get_name_property_def( ). " (type i)
    l_workflow = gcl_extendedobjec2->get_workflow( ). " (type i)
    l_associated_property_defs = gcl_extendedobjec2->get_associated_property_defs( ). " (type /BLCK/MFI_associatedprop_tt)
    l_templates = gcl_extendedobjec2->get_templates( ). " (type /BLCK/MFI_object_version_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**name_property_def** | i |  | [optional] [default to null]
**workflow** | i |  | [optional] [default to null]
**associated_property_defs** | /BLCK/MFI_associatedprop_tt (**[array of associatedprop](#markdown-header-model-associatedprop)**) | Property definitions associated with this class. | [optional] [default to null]
**templates** | /BLCK/MFI_object_version_tt (**[array of object_version](#markdown-header-model-object_version)**) | Templates available for use with this class. | [optional] [default to null]

* * *
<a name="markdown-header-model-extendedobject"></a> 

# Model: extendedobject



### Example
```abap
*** model extendedobject example

* create our variables..
    data gcl_extendedobject type ref to /blck/mdl_cl_extendedobject.
    
* instantiate model and call the setters to set values..
    gcl_extendedobject = /blck/mdl_cl_extendedobject=>create( ).
    gcl_extendedobject->set_accessed_by_me_utc( 'ipsum lorem' ). " (type string)
    gcl_extendedobject->set_checked_out_at_utc( 'ipsum lorem' ). " (type string)
    gcl_extendedobject->set_checked_out_to( 42 ). " (type i)
    gcl_extendedobject->set_checked_out_to_user_name( 'ipsum lorem' ). " (type string)
    gcl_extendedobject->set_class( 42 ). " (type i)
    gcl_extendedobject->set_created_utc( 'ipsum lorem' ). " (type string)
    gcl_extendedobject->set_deleted( 'X' ). " (type flag)
    gcl_extendedobject->set_display_id( 'ipsum lorem' ). " (type string)
    gcl_extendedobject->set_files( l_files ). " (type /BLCK/MFI_object_file_tt)
    gcl_extendedobject->set_has_assignments( 'X' ). " (type flag)
    gcl_extendedobject->set_hasrelationshipsfromthis( 'X' ). " (type flag)
    gcl_extendedobject->set_has_relationships_to_this( 'X' ). " (type flag)
    gcl_extendedobject->set_is_stub( 'X' ). " (type flag)
    gcl_extendedobject->set_last_modified_utc( 'ipsum lorem' ). " (type string)
    gcl_extendedobject->set_object_checked_out( 'X' ). " (type flag)
    gcl_extendedobject->set_objectcheckedouttothisuser( 'X' ). " (type flag)
    gcl_extendedobject->set_object_version_flags( l_object_version_flags ). " (type /BLCK/MFI_mfobjectversio)
    gcl_extendedobject->set_obj_ver( l_obj_ver ). " (type /BLCK/MFI_obj_ver)
    gcl_extendedobject->set_single_file( 'X' ). " (type flag)
    gcl_extendedobject->set_thisversionlatesttothisuse( 'X' ). " (type flag)
    gcl_extendedobject->set_title( 'ipsum lorem' ). " (type string)
    gcl_extendedobject->set_visible_after_operation( 'X' ). " (type flag)
    gcl_extendedobject->set_properties( l_properties ). " (type /BLCK/MFI_property_value_tt)
    
* pass to example API method
    gcl_exampleapi->update_extendedobject(
    	exporting
    		i_extendedobject = gcl_extendedobject ).
    		
    clear gcl_extendedobject.
    
* fetch new instance from example API method
    gcl_extendedobject = gcl_exampleapi->get_extendedobject(
    	exporting
    		i_id = 1 ).
    		
    l_accessed_by_me_utc = gcl_extendedobject->get_accessed_by_me_utc( ). " (type string)
    l_checked_out_at_utc = gcl_extendedobject->get_checked_out_at_utc( ). " (type string)
    l_checked_out_to = gcl_extendedobject->get_checked_out_to( ). " (type i)
    l_checked_out_to_user_name = gcl_extendedobject->get_checked_out_to_user_name( ). " (type string)
    l_class = gcl_extendedobject->get_class( ). " (type i)
    l_created_utc = gcl_extendedobject->get_created_utc( ). " (type string)
    l_deleted = gcl_extendedobject->get_deleted( ). " (type flag)
    l_display_id = gcl_extendedobject->get_display_id( ). " (type string)
    l_files = gcl_extendedobject->get_files( ). " (type /BLCK/MFI_object_file_tt)
    l_has_assignments = gcl_extendedobject->get_has_assignments( ). " (type flag)
    l_hasrelationshipsfromthis = gcl_extendedobject->get_hasrelationshipsfromthis( ). " (type flag)
    l_has_relationships_to_this = gcl_extendedobject->get_has_relationships_to_this( ). " (type flag)
    l_is_stub = gcl_extendedobject->get_is_stub( ). " (type flag)
    l_last_modified_utc = gcl_extendedobject->get_last_modified_utc( ). " (type string)
    l_object_checked_out = gcl_extendedobject->get_object_checked_out( ). " (type flag)
    l_objectcheckedouttothisuser = gcl_extendedobject->get_objectcheckedouttothisuser( ). " (type flag)
    l_object_version_flags = gcl_extendedobject->get_object_version_flags( ). " (type /BLCK/MFI_mfobjectversio)
    l_obj_ver = gcl_extendedobject->get_obj_ver( ). " (type /BLCK/MFI_obj_ver)
    l_single_file = gcl_extendedobject->get_single_file( ). " (type flag)
    l_thisversionlatesttothisuse = gcl_extendedobject->get_thisversionlatesttothisuse( ). " (type flag)
    l_title = gcl_extendedobject->get_title( ). " (type string)
    l_visible_after_operation = gcl_extendedobject->get_visible_after_operation( ). " (type flag)
    l_properties = gcl_extendedobject->get_properties( ). " (type /BLCK/MFI_property_value_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**accessed_by_me_utc** | string |  | [optional] [default to null]
**checked_out_at_utc** | string |  | [optional] [default to null]
**checked_out_to** | i |  | [optional] [default to null]
**checked_out_to_user_name** | string |  | [optional] [default to null]
**class** | i |  | [optional] [default to null]
**created_utc** | string |  | [optional] [default to null]
**deleted** | flag |  | [optional] [default to null]
**display_id** | string |  | [optional] [default to null]
**files** | /BLCK/MFI_object_file_tt (**[array of object_file](#markdown-header-model-object_file)**) |  | [optional] [default to null]
**has_assignments** | flag |  | [optional] [default to null]
**hasrelationshipsfromthis** | flag |  | [optional] [default to null]
**has_relationships_to_this** | flag |  | [optional] [default to null]
**is_stub** | flag |  | [optional] [default to null]
**last_modified_utc** | string |  | [optional] [default to null]
**object_checked_out** | flag |  | [optional] [default to null]
**objectcheckedouttothisuser** | flag |  | [optional] [default to null]
**object_version_flags** | /BLCK/MFI_mfobjectversio (**[mfobjectversio](#markdown-header-enum-mfobjectversio)**) |  | [optional] [default to null]
**obj_ver** | /BLCK/MFI_obj_ver (**[obj_ver](#markdown-header-model-obj_ver)**) |  | [optional] [default to null]
**single_file** | flag |  | [optional] [default to null]
**thisversionlatesttothisuse** | flag |  | [optional] [default to null]
**title** | string |  | [optional] [default to null]
**visible_after_operation** | flag |  | [optional] [default to null]
**properties** | /BLCK/MFI_property_value_tt (**[array of property_value](#markdown-header-model-property_value)**) | Object properties | [optional] [default to null]

* * *
<a name="markdown-header-enum-mffolderconten"></a> 

# Enum: mffolderconten



### Example
```abap
*** model mffolderconten example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFFolderContentItemType.html
*** 0:   Unknown   1:  ViewFolder  2:  PropertyFolder  3:  TraditionalFolder  4:
*** ObjectVersion 5: ExternalViewFolder

* create our variables..
    data gcl_mffolderconten type ref to /blck/mdl_cl_mffolderconten.
    
* instantiate model relevant to the enum value we want
    gcl_mffolderconten = /blck/mdl_cl_mffolderconten=>enum_unknown( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mffolderconten_state(
    	exporting
    		i_mffolderconten = gcl_mffolderconten ).
    		
    clear gcl_mffolderconten.
    
* fetch result from example API method
    gcl_mffolderconten = gcl_exampleapi->get_mffolderconten_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mffolderconten->is_unknown( ) eq 'X'.
*   do something specific to unknown case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mffolderconten->get_value( ).
    when /blck/mdl_cl_mffolderconten=>mce_unknown.
*     do something specific to unknown case..
    when /blck/mdl_cl_mffolderconten=>mce_view_folder.
*     do something specific to view_folder case..
    when /blck/mdl_cl_mffolderconten=>mce_property_folder.
*     do something specific to property_folder case..
    when /blck/mdl_cl_mffolderconten=>mce_traditional_folder.
*     do something specific to traditional_folder case..
    when /blck/mdl_cl_mffolderconten=>mce_object_version.
*     do something specific to object_version case..
    when /blck/mdl_cl_mffolderconten=>mce_external_view_folder.
*     do something specific to external_view_folder case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**unknown** | 0 | /blck/mdl_cl_mffolderconten=>enum_unknown( ).
**view_folder** | 1 | /blck/mdl_cl_mffolderconten=>enum_view_folder( ).
**property_folder** | 2 | /blck/mdl_cl_mffolderconten=>enum_property_folder( ).
**traditional_folder** | 3 | /blck/mdl_cl_mffolderconten=>enum_traditional_folder( ).
**object_version** | 4 | /blck/mdl_cl_mffolderconten=>enum_object_version( ).
**external_view_folder** | 5 | /blck/mdl_cl_mffolderconten=>enum_external_view_folder( ).

* * *
<a name="markdown-header-model-view_location"></a> 

# Model: view_location



### Example
```abap
*** model view_location example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ViewLocation.html

* create our variables..
    data gcl_view_location type ref to /blck/mdl_cl_view_location.
    
* instantiate model and call the setters to set values..
    gcl_view_location = /blck/mdl_cl_view_location=>create( ).
    gcl_view_location->set_overlapped_folder( l_overlapped_folder ). " (type /BLCK/MFI_typed_value)
    gcl_view_location->set_overlapping( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_view_location(
    	exporting
    		i_view_location = gcl_view_location ).
    		
    clear gcl_view_location.
    
* fetch new instance from example API method
    gcl_view_location = gcl_exampleapi->get_view_location(
    	exporting
    		i_id = 1 ).
    		
    l_overlapped_folder = gcl_view_location->get_overlapped_folder( ). " (type /BLCK/MFI_typed_value)
    l_overlapping = gcl_view_location->get_overlapping( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**overlapped_folder** | /BLCK/MFI_typed_value (**[typed_value](#markdown-header-model-typed_value)**) |  | [optional] [default to null]
**overlapping** | flag |  | [optional] [default to null]

* * *
<a name="markdown-header-model-view"></a> 

# Model: view



### Example
```abap
*** model view example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~View.html

* create our variables..
    data gcl_view type ref to /blck/mdl_cl_view.
    
* instantiate model and call the setters to set values..
    gcl_view = /blck/mdl_cl_view=>create( ).
    gcl_view->set_common( 'X' ). " (type flag)
    gcl_view->set_id( 42 ). " (type i)
    gcl_view->set_name( 'ipsum lorem' ). " (type string)
    gcl_view->set_parent( 42 ). " (type i)
    gcl_view->set_view_location( l_view_location ). " (type /BLCK/MFI_view_location)
    
* pass to example API method
    gcl_exampleapi->update_view(
    	exporting
    		i_view = gcl_view ).
    		
    clear gcl_view.
    
* fetch new instance from example API method
    gcl_view = gcl_exampleapi->get_view(
    	exporting
    		i_id = 1 ).
    		
    l_common = gcl_view->get_common( ). " (type flag)
    l_id = gcl_view->get_id( ). " (type i)
    l_name = gcl_view->get_name( ). " (type string)
    l_parent = gcl_view->get_parent( ). " (type i)
    l_view_location = gcl_view->get_view_location( ). " (type /BLCK/MFI_view_location)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**common** | flag |  | [optional] [default to null]
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**parent** | i |  | [optional] [default to null]
**view_location** | /BLCK/MFI_view_location (**[view_location](#markdown-header-model-view_location)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-foldercontent2"></a> 

# Model: foldercontent2



### Example
```abap
*** model foldercontent2 example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~FolderContentItem.html

* create our variables..
    data gcl_foldercontent2 type ref to /blck/mdl_cl_foldercontent2.
    
* instantiate model and call the setters to set values..
    gcl_foldercontent2 = /blck/mdl_cl_foldercontent2=>create( ).
    gcl_foldercontent2->set_folder_content_item_type( l_folder_content_item_type ). " (type /BLCK/MFI_mffolderconten)
    gcl_foldercontent2->set_object_version( l_object_version ). " (type /BLCK/MFI_object_version)
    gcl_foldercontent2->set_property_folder( l_property_folder ). " (type /BLCK/MFI_typed_value)
    gcl_foldercontent2->set_traditional_folder( l_traditional_folder ). " (type /BLCK/MFI_lookup)
    gcl_foldercontent2->set_view( l_view ). " (type /BLCK/MFI_view)
    
* pass to example API method
    gcl_exampleapi->update_foldercontent2(
    	exporting
    		i_foldercontent2 = gcl_foldercontent2 ).
    		
    clear gcl_foldercontent2.
    
* fetch new instance from example API method
    gcl_foldercontent2 = gcl_exampleapi->get_foldercontent2(
    	exporting
    		i_id = 1 ).
    		
    l_folder_content_item_type = gcl_foldercontent2->get_folder_content_item_type( ). " (type /BLCK/MFI_mffolderconten)
    l_object_version = gcl_foldercontent2->get_object_version( ). " (type /BLCK/MFI_object_version)
    l_property_folder = gcl_foldercontent2->get_property_folder( ). " (type /BLCK/MFI_typed_value)
    l_traditional_folder = gcl_foldercontent2->get_traditional_folder( ). " (type /BLCK/MFI_lookup)
    l_view = gcl_foldercontent2->get_view( ). " (type /BLCK/MFI_view)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**folder_content_item_type** | /BLCK/MFI_mffolderconten (**[mffolderconten](#markdown-header-enum-mffolderconten)**) |  | [optional] [default to null]
**object_version** | /BLCK/MFI_object_version (**[object_version](#markdown-header-model-object_version)**) |  | [optional] [default to null]
**property_folder** | /BLCK/MFI_typed_value (**[typed_value](#markdown-header-model-typed_value)**) |  | [optional] [default to null]
**traditional_folder** | /BLCK/MFI_lookup (**[lookup](#markdown-header-model-lookup)**) |  | [optional] [default to null]
**view** | /BLCK/MFI_view (**[view](#markdown-header-model-view)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-foldercontenti"></a> 

# Model: foldercontenti



### Example
```abap
*** model foldercontenti example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~FolderContentItems.html

* create our variables..
    data gcl_foldercontenti type ref to /blck/mdl_cl_foldercontenti.
    
* instantiate model and call the setters to set values..
    gcl_foldercontenti = /blck/mdl_cl_foldercontenti=>create( ).
    gcl_foldercontenti->set_path( 'ipsum lorem' ). " (type string)
    gcl_foldercontenti->set_more_results( 'X' ). " (type flag)
    gcl_foldercontenti->set_items( l_items ). " (type /BLCK/MFI_foldercontent2_tt)
    
* pass to example API method
    gcl_exampleapi->update_foldercontenti(
    	exporting
    		i_foldercontenti = gcl_foldercontenti ).
    		
    clear gcl_foldercontenti.
    
* fetch new instance from example API method
    gcl_foldercontenti = gcl_exampleapi->get_foldercontenti(
    	exporting
    		i_id = 1 ).
    		
    l_path = gcl_foldercontenti->get_path( ). " (type string)
    l_more_results = gcl_foldercontenti->get_more_results( ). " (type flag)
    l_items = gcl_foldercontenti->get_items( ). " (type /BLCK/MFI_foldercontent2_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**path** | string | The path to the current folder. | [optional] [default to null]
**more_results** | flag | Specifies whether there are more results in the folder. | [optional] [default to null]
**items** | /BLCK/MFI_foldercontent2_tt (**[array of foldercontent2](#markdown-header-model-foldercontent2)**) | The actual folder contents. | [optional] [default to null]

* * *
<a name="markdown-header-enum-mf_auth_type"></a> 

# Enum: mf_auth_type



### Example
```abap
*** model mf_auth_type example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFAuthType.html
*** 0:    Unknown    1:    LoggedOnWindowsUser    2:    SpecificWindowsUser   3:
*** SpecificMFilesUser

* create our variables..
    data gcl_mf_auth_type type ref to /blck/mdl_cl_mf_auth_type.
    
* instantiate model relevant to the enum value we want
    gcl_mf_auth_type = /blck/mdl_cl_mf_auth_type=>enum_unknown( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mf_auth_type_state(
    	exporting
    		i_mf_auth_type = gcl_mf_auth_type ).
    		
    clear gcl_mf_auth_type.
    
* fetch result from example API method
    gcl_mf_auth_type = gcl_exampleapi->get_mf_auth_type_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mf_auth_type->is_unknown( ) eq 'X'.
*   do something specific to unknown case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mf_auth_type->get_value( ).
    when /blck/mdl_cl_mf_auth_type=>mce_unknown.
*     do something specific to unknown case..
    when /blck/mdl_cl_mf_auth_type=>mce_logged_on_windows_user.
*     do something specific to logged_on_windows_user case..
    when /blck/mdl_cl_mf_auth_type=>mce_specific_windows_user.
*     do something specific to specific_windows_user case..
    when /blck/mdl_cl_mf_auth_type=>mce_specific_m_files_user.
*     do something specific to specific_m_files_user case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**unknown** | 0 | /blck/mdl_cl_mf_auth_type=>enum_unknown( ).
**logged_on_windows_user** | 1 | /blck/mdl_cl_mf_auth_type=>enum_logged_on_windows_user( ).
**specific_windows_user** | 2 | /blck/mdl_cl_mf_auth_type=>enum_specific_windows_user( ).
**specific_m_files_user** | 3 | /blck/mdl_cl_mf_auth_type=>enum_specific_m_files_user( ).

* * *
<a name="markdown-header-enum-mfacl_mode"></a> 

# Enum: mfacl_mode



### Example
```abap
*** model mfacl_mode example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFACLMode.html
*** 0: Simple 1: AutomaticPermissionsWithComponents

* create our variables..
    data gcl_mfacl_mode type ref to /blck/mdl_cl_mfacl_mode.
    
* instantiate model relevant to the enum value we want
    gcl_mfacl_mode = /blck/mdl_cl_mfacl_mode=>enum_simple( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfacl_mode_state(
    	exporting
    		i_mfacl_mode = gcl_mfacl_mode ).
    		
    clear gcl_mfacl_mode.
    
* fetch result from example API method
    gcl_mfacl_mode = gcl_exampleapi->get_mfacl_mode_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mfacl_mode->is_simple( ) eq 'X'.
*   do something specific to simple case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mfacl_mode->get_value( ).
    when /blck/mdl_cl_mfacl_mode=>mce_simple.
*     do something specific to simple case..
    when /blck/mdl_cl_mfacl_mode=>mce_automaticpermissionswithc.
*     do something specific to automaticpermissionswithc case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**simple** | 0 | /blck/mdl_cl_mfacl_mode=>enum_simple( ).
**automaticpermissionswithc** | 1 | /blck/mdl_cl_mfacl_mode=>enum_automaticpermissionswithc( ).

* * *
<a name="markdown-header-enum-mfautomaticval"></a> 

# Enum: mfautomaticval



### Example
```abap
*** model mfautomaticval example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~MFAutomaticValueType.html
*** 0:   None   1:   CalculatedWithPlaceholders   2:  CalculatedWithVBScript  3:
*** AutoNumberSimple 4: WithVBScript

* create our variables..
    data gcl_mfautomaticval type ref to /blck/mdl_cl_mfautomaticval.
    
* instantiate model relevant to the enum value we want
    gcl_mfautomaticval = /blck/mdl_cl_mfautomaticval=>enum_none( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfautomaticval_state(
    	exporting
    		i_mfautomaticval = gcl_mfautomaticval ).
    		
    clear gcl_mfautomaticval.
    
* fetch result from example API method
    gcl_mfautomaticval = gcl_exampleapi->get_mfautomaticval_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mfautomaticval->is_none( ) eq 'X'.
*   do something specific to none case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mfautomaticval->get_value( ).
    when /blck/mdl_cl_mfautomaticval=>mce_none.
*     do something specific to none case..
    when /blck/mdl_cl_mfautomaticval=>mce_calculatedwithplaceholder.
*     do something specific to calculatedwithplaceholder case..
    when /blck/mdl_cl_mfautomaticval=>mce_calculated_with_vb_script.
*     do something specific to calculated_with_vb_script case..
    when /blck/mdl_cl_mfautomaticval=>mce_auto_number_simple.
*     do something specific to auto_number_simple case..
    when /blck/mdl_cl_mfautomaticval=>mce_with_vb_script.
*     do something specific to with_vb_script case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**none** | 0 | /blck/mdl_cl_mfautomaticval=>enum_none( ).
**calculatedwithplaceholder** | 1 | /blck/mdl_cl_mfautomaticval=>enum_calculatedwithplaceholder( ).
**calculated_with_vb_script** | 2 | /blck/mdl_cl_mfautomaticval=>enum_calculated_with_vb_script( ).
**auto_number_simple** | 3 | /blck/mdl_cl_mfautomaticval=>enum_auto_number_simple( ).
**with_vb_script** | 4 | /blck/mdl_cl_mfautomaticval=>enum_with_vb_script( ).

* * *
<a name="markdown-header-enum-mfcheckoutstat"></a> 

# Enum: mfcheckoutstat



### Example
```abap
*** model mfcheckoutstat example
*** value  &#x3D;&#x3D;  CheckedOut will not evaluate to true if the object is checked out
*** to the current user. If it doesn’t matter whom the object is checked out to,
*** use value !&#x3D; CheckedIn instead. 0: CheckedIn 1: CheckedOut 2: CheckedOutToMe

* create our variables..
    data gcl_mfcheckoutstat type ref to /blck/mdl_cl_mfcheckoutstat.
    
* instantiate model relevant to the enum value we want
    gcl_mfcheckoutstat = /blck/mdl_cl_mfcheckoutstat=>enum_checked_in( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfcheckoutstat_state(
    	exporting
    		i_mfcheckoutstat = gcl_mfcheckoutstat ).
    		
    clear gcl_mfcheckoutstat.
    
* fetch result from example API method
    gcl_mfcheckoutstat = gcl_exampleapi->get_mfcheckoutstat_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mfcheckoutstat->is_checked_in( ) eq 'X'.
*   do something specific to checked_in case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mfcheckoutstat->get_value( ).
    when /blck/mdl_cl_mfcheckoutstat=>mce_checked_in.
*     do something specific to checked_in case..
    when /blck/mdl_cl_mfcheckoutstat=>mce_checked_out.
*     do something specific to checked_out case..
    when /blck/mdl_cl_mfcheckoutstat=>mce_checked_out_to_me.
*     do something specific to checked_out_to_me case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**checked_in** | 0 | /blck/mdl_cl_mfcheckoutstat=>enum_checked_in( ).
**checked_out** | 1 | /blck/mdl_cl_mfcheckoutstat=>enum_checked_out( ).
**checked_out_to_me** | 2 | /blck/mdl_cl_mfcheckoutstat=>enum_checked_out_to_me( ).

* * *
<a name="markdown-header-enum-mfextensionaut"></a> 

# Enum: mfextensionaut



### Example
```abap
*** model mfextensionaut example
*** 0: None 1: Common 2: Indexer 3: Permissions

* create our variables..
    data gcl_mfextensionaut type ref to /blck/mdl_cl_mfextensionaut.
    
* instantiate model relevant to the enum value we want
    gcl_mfextensionaut = /blck/mdl_cl_mfextensionaut=>enum_none( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfextensionaut_state(
    	exporting
    		i_mfextensionaut = gcl_mfextensionaut ).
    		
    clear gcl_mfextensionaut.
    
* fetch result from example API method
    gcl_mfextensionaut = gcl_exampleapi->get_mfextensionaut_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mfextensionaut->is_none( ) eq 'X'.
*   do something specific to none case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mfextensionaut->get_value( ).
    when /blck/mdl_cl_mfextensionaut=>mce_none.
*     do something specific to none case..
    when /blck/mdl_cl_mfextensionaut=>mce_common.
*     do something specific to common case..
    when /blck/mdl_cl_mfextensionaut=>mce_indexer.
*     do something specific to indexer case..
    when /blck/mdl_cl_mfextensionaut=>mce_permissions.
*     do something specific to permissions case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**none** | 0 | /blck/mdl_cl_mfextensionaut=>enum_none( ).
**common** | 1 | /blck/mdl_cl_mfextensionaut=>enum_common( ).
**indexer** | 2 | /blck/mdl_cl_mfextensionaut=>enum_indexer( ).
**permissions** | 3 | /blck/mdl_cl_mfextensionaut=>enum_permissions( ).

* * *
<a name="markdown-header-enum-mfrefreshstatu"></a> 

# Enum: mfrefreshstatu



### Example
```abap
*** model mfrefreshstatu example
*** 0: None 1: Quick 2: Full

* create our variables..
    data gcl_mfrefreshstatu type ref to /blck/mdl_cl_mfrefreshstatu.
    
* instantiate model relevant to the enum value we want
    gcl_mfrefreshstatu = /blck/mdl_cl_mfrefreshstatu=>enum_none( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_mfrefreshstatu_state(
    	exporting
    		i_mfrefreshstatu = gcl_mfrefreshstatu ).
    		
    clear gcl_mfrefreshstatu.
    
* fetch result from example API method
    gcl_mfrefreshstatu = gcl_exampleapi->get_mfrefreshstatu_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_mfrefreshstatu->is_none( ) eq 'X'.
*   do something specific to none case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_mfrefreshstatu->get_value( ).
    when /blck/mdl_cl_mfrefreshstatu=>mce_none.
*     do something specific to none case..
    when /blck/mdl_cl_mfrefreshstatu=>mce_quick.
*     do something specific to quick case..
    when /blck/mdl_cl_mfrefreshstatu=>mce_full.
*     do something specific to full case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**none** | 0 | /blck/mdl_cl_mfrefreshstatu=>enum_none( ).
**quick** | 1 | /blck/mdl_cl_mfrefreshstatu=>enum_quick( ).
**full** | 2 | /blck/mdl_cl_mfrefreshstatu=>enum_full( ).

* * *
<a name="markdown-header-model-obj_id"></a> 

# Model: obj_id



### Example
```abap
*** model obj_id example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjID.html

* create our variables..
    data gcl_obj_id type ref to /blck/mdl_cl_obj_id.
    
* instantiate model and call the setters to set values..
    gcl_obj_id = /blck/mdl_cl_obj_id=>create( ).
    gcl_obj_id->set_id( 42 ). " (type i)
    gcl_obj_id->set_type( 42 ). " (type i)
    gcl_obj_id->set_external_repository_name( 'ipsum lorem' ). " (type string)
    gcl_obj_id->set_externalrepositoryobjectid( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_obj_id(
    	exporting
    		i_obj_id = gcl_obj_id ).
    		
    clear gcl_obj_id.
    
* fetch new instance from example API method
    gcl_obj_id = gcl_exampleapi->get_obj_id(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_obj_id->get_id( ). " (type i)
    l_type = gcl_obj_id->get_type( ). " (type i)
    l_external_repository_name = gcl_obj_id->get_external_repository_name( ). " (type string)
    l_externalrepositoryobjectid = gcl_obj_id->get_externalrepositoryobjectid( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**type** | i |  | [optional] [default to null]
**external_repository_name** | string | (for external objects only) | [optional] [default to null]
**externalrepositoryobjectid** | string | (for external objects only) | [optional] [default to null]

* * *
<a name="markdown-header-model-obj_type"></a> 

# Model: obj_type



### Example
```abap
*** model obj_type example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjType.html

* create our variables..
    data gcl_obj_type type ref to /blck/mdl_cl_obj_type.
    
* instantiate model and call the setters to set values..
    gcl_obj_type = /blck/mdl_cl_obj_type=>create( ).
    gcl_obj_type->set_allow_adding( 'X' ). " (type flag)
    gcl_obj_type->set_can_have_files( 'X' ). " (type flag)
    gcl_obj_type->set_default_property_def( 42 ). " (type i)
    gcl_obj_type->set_external( 'X' ). " (type flag)
    gcl_obj_type->set_id( 42 ). " (type i)
    gcl_obj_type->set_name_plural( 'ipsum lorem' ). " (type string)
    gcl_obj_type->set_name( 'ipsum lorem' ). " (type string)
    gcl_obj_type->set_owner_property_def( 42 ). " (type i)
    gcl_obj_type->set_readonlypropertiesduringin( l_readonlypropertiesduringin ). " (type /blck/api_i_tt)
    gcl_obj_type->set_readonlypropertiesduringup( l_readonlypropertiesduringup ). " (type /blck/api_i_tt)
    gcl_obj_type->set_real_object_type( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_obj_type(
    	exporting
    		i_obj_type = gcl_obj_type ).
    		
    clear gcl_obj_type.
    
* fetch new instance from example API method
    gcl_obj_type = gcl_exampleapi->get_obj_type(
    	exporting
    		i_id = 1 ).
    		
    l_allow_adding = gcl_obj_type->get_allow_adding( ). " (type flag)
    l_can_have_files = gcl_obj_type->get_can_have_files( ). " (type flag)
    l_default_property_def = gcl_obj_type->get_default_property_def( ). " (type i)
    l_external = gcl_obj_type->get_external( ). " (type flag)
    l_id = gcl_obj_type->get_id( ). " (type i)
    l_name_plural = gcl_obj_type->get_name_plural( ). " (type string)
    l_name = gcl_obj_type->get_name( ). " (type string)
    l_owner_property_def = gcl_obj_type->get_owner_property_def( ). " (type i)
    l_readonlypropertiesduringin = gcl_obj_type->get_readonlypropertiesduringin( ). " (type /blck/api_i_tt)
    l_readonlypropertiesduringup = gcl_obj_type->get_readonlypropertiesduringup( ). " (type /blck/api_i_tt)
    l_real_object_type = gcl_obj_type->get_real_object_type( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**allow_adding** | flag |  | [optional] [default to null]
**can_have_files** | flag |  | [optional] [default to null]
**default_property_def** | i |  | [optional] [default to null]
**external** | flag |  | [optional] [default to null]
**id** | i |  | [optional] [default to null]
**name_plural** | string |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**owner_property_def** | i |  | [optional] [default to null]
**readonlypropertiesduringin** | /blck/api_i_tt |  | [optional] [default to null]
**readonlypropertiesduringup** | /blck/api_i_tt |  | [optional] [default to null]
**real_object_type** | flag |  | [optional] [default to null]

* * *
<a name="markdown-header-model-object_class"></a> 

# Model: object_class



### Example
```abap
*** model object_class example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ObjectClass.html

* create our variables..
    data gcl_object_class type ref to /blck/mdl_cl_object_class.
    
* instantiate model and call the setters to set values..
    gcl_object_class = /blck/mdl_cl_object_class=>create( ).
    gcl_object_class->set_id( 42 ). " (type i)
    gcl_object_class->set_name( 'ipsum lorem' ). " (type string)
    gcl_object_class->set_name_property_def( 42 ). " (type i)
    gcl_object_class->set_workflow( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_object_class(
    	exporting
    		i_object_class = gcl_object_class ).
    		
    clear gcl_object_class.
    
* fetch new instance from example API method
    gcl_object_class = gcl_exampleapi->get_object_class(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_object_class->get_id( ). " (type i)
    l_name = gcl_object_class->get_name( ). " (type string)
    l_name_property_def = gcl_object_class->get_name_property_def( ). " (type i)
    l_workflow = gcl_object_class->get_workflow( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**name_property_def** | i |  | [optional] [default to null]
**workflow** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-model-upload_info"></a> 

# Model: upload_info



### Example
```abap
*** model upload_info example
*** Contains the information on a temporary upload.

* create our variables..
    data gcl_upload_info type ref to /blck/mdl_cl_upload_info.
    
* instantiate model and call the setters to set values..
    gcl_upload_info = /blck/mdl_cl_upload_info=>create( ).
    gcl_upload_info->set_upload_id( 42 ). " (type i)
    gcl_upload_info->set_title( 'ipsum lorem' ). " (type string)
    gcl_upload_info->set_extension( 'ipsum lorem' ). " (type string)
    gcl_upload_info->set_size( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_upload_info(
    	exporting
    		i_upload_info = gcl_upload_info ).
    		
    clear gcl_upload_info.
    
* fetch new instance from example API method
    gcl_upload_info = gcl_exampleapi->get_upload_info(
    	exporting
    		i_id = 1 ).
    		
    l_upload_id = gcl_upload_info->get_upload_id( ). " (type i)
    l_title = gcl_upload_info->get_title( ). " (type string)
    l_extension = gcl_upload_info->get_extension( ). " (type string)
    l_size = gcl_upload_info->get_size( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**upload_id** | i | Temporary upload ID given by the server. | [optional] [default to null]
**title** | string | File name without extension. | [optional] [default to null]
**extension** | string | File extension. | [optional] [default to null]
**size** | i | File size. | [optional] [default to null]

* * *
<a name="markdown-header-model-objectcreation"></a> 

# Model: objectcreation



### Example
```abap
*** model objectcreation example
*** Specifies the information required when creating a new object.

* create our variables..
    data gcl_objectcreation type ref to /blck/mdl_cl_objectcreation.
    
* instantiate model and call the setters to set values..
    gcl_objectcreation = /blck/mdl_cl_objectcreation=>create( ).
    gcl_objectcreation->set_property_values( l_property_values ). " (type /BLCK/MFI_property_value_tt)
    gcl_objectcreation->set_files( l_files ). " (type /BLCK/MFI_upload_info_tt)
    
* pass to example API method
    gcl_exampleapi->update_objectcreation(
    	exporting
    		i_objectcreation = gcl_objectcreation ).
    		
    clear gcl_objectcreation.
    
* fetch new instance from example API method
    gcl_objectcreation = gcl_exampleapi->get_objectcreation(
    	exporting
    		i_id = 1 ).
    		
    l_property_values = gcl_objectcreation->get_property_values( ). " (type /BLCK/MFI_property_value_tt)
    l_files = gcl_objectcreation->get_files( ). " (type /BLCK/MFI_upload_info_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**property_values** | /BLCK/MFI_property_value_tt (**[array of property_value](#markdown-header-model-property_value)**) | Properties for the new object. | [optional] [default to null]
**files** | /BLCK/MFI_upload_info_tt (**[array of upload_info](#markdown-header-model-upload_info)**) | References previously uploaded files. | [optional] [default to null]

* * *
<a name="markdown-header-model-objectversionu"></a> 

# Model: objectversionu



### Example
```abap
*** model objectversionu example

* create our variables..
    data gcl_objectversionu type ref to /blck/mdl_cl_objectversionu.
    
* instantiate model and call the setters to set values..
    gcl_objectversionu = /blck/mdl_cl_objectversionu=>create( ).
    gcl_objectversionu->set_properties( l_properties ). " (type /BLCK/MFI_property_value_tt)
    gcl_objectversionu->set_accessed_by_me_utc( 'ipsum lorem' ). " (type string)
    gcl_objectversionu->set_checked_out_at_utc( 'ipsum lorem' ). " (type string)
    gcl_objectversionu->set_checked_out_to( 42 ). " (type i)
    gcl_objectversionu->set_checked_out_to_user_name( 'ipsum lorem' ). " (type string)
    gcl_objectversionu->set_class( 42 ). " (type i)
    gcl_objectversionu->set_created_utc( 'ipsum lorem' ). " (type string)
    gcl_objectversionu->set_deleted( 'X' ). " (type flag)
    gcl_objectversionu->set_display_id( 'ipsum lorem' ). " (type string)
    gcl_objectversionu->set_files( l_files ). " (type /BLCK/MFI_object_file_tt)
    gcl_objectversionu->set_has_assignments( 'X' ). " (type flag)
    gcl_objectversionu->set_hasrelationshipsfromthis( 'X' ). " (type flag)
    gcl_objectversionu->set_has_relationships_to_this( 'X' ). " (type flag)
    gcl_objectversionu->set_is_stub( 'X' ). " (type flag)
    gcl_objectversionu->set_last_modified_utc( 'ipsum lorem' ). " (type string)
    gcl_objectversionu->set_object_checked_out( 'X' ). " (type flag)
    gcl_objectversionu->set_objectcheckedouttothisuser( 'X' ). " (type flag)
    gcl_objectversionu->set_object_version_flags( l_object_version_flags ). " (type /BLCK/MFI_mfobjectversio)
    gcl_objectversionu->set_obj_ver( l_obj_ver ). " (type /BLCK/MFI_obj_ver)
    gcl_objectversionu->set_single_file( 'X' ). " (type flag)
    gcl_objectversionu->set_thisversionlatesttothisuse( 'X' ). " (type flag)
    gcl_objectversionu->set_title( 'ipsum lorem' ). " (type string)
    gcl_objectversionu->set_visible_after_operation( 'X' ). " (type flag)
    gcl_objectversionu->set_allow_name_change( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_objectversionu(
    	exporting
    		i_objectversionu = gcl_objectversionu ).
    		
    clear gcl_objectversionu.
    
* fetch new instance from example API method
    gcl_objectversionu = gcl_exampleapi->get_objectversionu(
    	exporting
    		i_id = 1 ).
    		
    l_properties = gcl_objectversionu->get_properties( ). " (type /BLCK/MFI_property_value_tt)
    l_accessed_by_me_utc = gcl_objectversionu->get_accessed_by_me_utc( ). " (type string)
    l_checked_out_at_utc = gcl_objectversionu->get_checked_out_at_utc( ). " (type string)
    l_checked_out_to = gcl_objectversionu->get_checked_out_to( ). " (type i)
    l_checked_out_to_user_name = gcl_objectversionu->get_checked_out_to_user_name( ). " (type string)
    l_class = gcl_objectversionu->get_class( ). " (type i)
    l_created_utc = gcl_objectversionu->get_created_utc( ). " (type string)
    l_deleted = gcl_objectversionu->get_deleted( ). " (type flag)
    l_display_id = gcl_objectversionu->get_display_id( ). " (type string)
    l_files = gcl_objectversionu->get_files( ). " (type /BLCK/MFI_object_file_tt)
    l_has_assignments = gcl_objectversionu->get_has_assignments( ). " (type flag)
    l_hasrelationshipsfromthis = gcl_objectversionu->get_hasrelationshipsfromthis( ). " (type flag)
    l_has_relationships_to_this = gcl_objectversionu->get_has_relationships_to_this( ). " (type flag)
    l_is_stub = gcl_objectversionu->get_is_stub( ). " (type flag)
    l_last_modified_utc = gcl_objectversionu->get_last_modified_utc( ). " (type string)
    l_object_checked_out = gcl_objectversionu->get_object_checked_out( ). " (type flag)
    l_objectcheckedouttothisuser = gcl_objectversionu->get_objectcheckedouttothisuser( ). " (type flag)
    l_object_version_flags = gcl_objectversionu->get_object_version_flags( ). " (type /BLCK/MFI_mfobjectversio)
    l_obj_ver = gcl_objectversionu->get_obj_ver( ). " (type /BLCK/MFI_obj_ver)
    l_single_file = gcl_objectversionu->get_single_file( ). " (type flag)
    l_thisversionlatesttothisuse = gcl_objectversionu->get_thisversionlatesttothisuse( ). " (type flag)
    l_title = gcl_objectversionu->get_title( ). " (type string)
    l_visible_after_operation = gcl_objectversionu->get_visible_after_operation( ). " (type flag)
    l_allow_name_change = gcl_objectversionu->get_allow_name_change( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**properties** | /BLCK/MFI_property_value_tt (**[array of property_value](#markdown-header-model-property_value)**) | Object properties | [optional] [default to null]
**accessed_by_me_utc** | string |  | [optional] [default to null]
**checked_out_at_utc** | string |  | [optional] [default to null]
**checked_out_to** | i |  | [optional] [default to null]
**checked_out_to_user_name** | string |  | [optional] [default to null]
**class** | i |  | [optional] [default to null]
**created_utc** | string |  | [optional] [default to null]
**deleted** | flag |  | [optional] [default to null]
**display_id** | string |  | [optional] [default to null]
**files** | /BLCK/MFI_object_file_tt (**[array of object_file](#markdown-header-model-object_file)**) |  | [optional] [default to null]
**has_assignments** | flag |  | [optional] [default to null]
**hasrelationshipsfromthis** | flag |  | [optional] [default to null]
**has_relationships_to_this** | flag |  | [optional] [default to null]
**is_stub** | flag |  | [optional] [default to null]
**last_modified_utc** | string |  | [optional] [default to null]
**object_checked_out** | flag |  | [optional] [default to null]
**objectcheckedouttothisuser** | flag |  | [optional] [default to null]
**object_version_flags** | /BLCK/MFI_mfobjectversio (**[mfobjectversio](#markdown-header-enum-mfobjectversio)**) |  | [optional] [default to null]
**obj_ver** | /BLCK/MFI_obj_ver (**[obj_ver](#markdown-header-model-obj_ver)**) |  | [optional] [default to null]
**single_file** | flag |  | [optional] [default to null]
**thisversionlatesttothisuse** | flag |  | [optional] [default to null]
**title** | string |  | [optional] [default to null]
**visible_after_operation** | flag |  | [optional] [default to null]
**allow_name_change** | flag |  | [optional] [default to null]

* * *
<a name="markdown-header-model-objectsupdatei"></a> 

# Model: objectsupdatei



### Example
```abap
*** model objectsupdatei example
*** To    be    used    when    setting    properties   on   multiple   objects.
*** https://developer.m-files.com/APIs/REST-API/Reference/resources/objects/setmultipleobjproperties/

* create our variables..
    data gcl_objectsupdatei type ref to /blck/mdl_cl_objectsupdatei.
    
* instantiate model and call the setters to set values..
    gcl_objectsupdatei = /blck/mdl_cl_objectsupdatei=>create( ).
    gcl_objectsupdatei->set_multiple_object_info( l_multiple_object_info ). " (type /BLCK/MFI_objectversionu)
    
* pass to example API method
    gcl_exampleapi->update_objectsupdatei(
    	exporting
    		i_objectsupdatei = gcl_objectsupdatei ).
    		
    clear gcl_objectsupdatei.
    
* fetch new instance from example API method
    gcl_objectsupdatei = gcl_exampleapi->get_objectsupdatei(
    	exporting
    		i_id = 1 ).
    		
    l_multiple_object_info = gcl_objectsupdatei->get_multiple_object_info( ). " (type /BLCK/MFI_objectversionu)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**multiple_object_info** | /BLCK/MFI_objectversionu (**[objectversionu](#markdown-header-model-objectversionu)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-objectworkflow"></a> 

# Model: objectworkflow



### Example
```abap
*** model objectworkflow example

* create our variables..
    data gcl_objectworkflow type ref to /blck/mdl_cl_objectworkflow.
    
* instantiate model and call the setters to set values..
    gcl_objectworkflow = /blck/mdl_cl_objectworkflow=>create( ).
    gcl_objectworkflow->set_state( l_state ). " (type /BLCK/MFI_property_value)
    gcl_objectworkflow->set_state_id( 42 ). " (type i)
    gcl_objectworkflow->set_state_name( 'ipsum lorem' ). " (type string)
    gcl_objectworkflow->set_workflow( l_workflow ). " (type /BLCK/MFI_property_value)
    gcl_objectworkflow->set_workflow_id( 42 ). " (type i)
    gcl_objectworkflow->set_workflow_name( 'ipsum lorem' ). " (type string)
    gcl_objectworkflow->set_version_comment( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_objectworkflow(
    	exporting
    		i_objectworkflow = gcl_objectworkflow ).
    		
    clear gcl_objectworkflow.
    
* fetch new instance from example API method
    gcl_objectworkflow = gcl_exampleapi->get_objectworkflow(
    	exporting
    		i_id = 1 ).
    		
    l_state = gcl_objectworkflow->get_state( ). " (type /BLCK/MFI_property_value)
    l_state_id = gcl_objectworkflow->get_state_id( ). " (type i)
    l_state_name = gcl_objectworkflow->get_state_name( ). " (type string)
    l_workflow = gcl_objectworkflow->get_workflow( ). " (type /BLCK/MFI_property_value)
    l_workflow_id = gcl_objectworkflow->get_workflow_id( ). " (type i)
    l_workflow_name = gcl_objectworkflow->get_workflow_name( ). " (type string)
    l_version_comment = gcl_objectworkflow->get_version_comment( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**state** | /BLCK/MFI_property_value (**[property_value](#markdown-header-model-property_value)**) |  | [optional] [default to null]
**state_id** | i | The workflow state ID. | [optional] [default to null]
**state_name** | string | The workflow state name. | [optional] [default to null]
**workflow** | /BLCK/MFI_property_value (**[property_value](#markdown-header-model-property_value)**) |  | [optional] [default to null]
**workflow_id** | i | The workflow ID. | [optional] [default to null]
**workflow_name** | string | The workflow name. | [optional] [default to null]
**version_comment** | string | Version comment defined on the workflow transition. | [optional] [default to null]

* * *
<a name="markdown-header-model-passwordchange"></a> 

# Model: passwordchange



### Example
```abap
*** model passwordchange example
*** Information required for changing password.

* create our variables..
    data gcl_passwordchange type ref to /blck/mdl_cl_passwordchange.
    
* instantiate model and call the setters to set values..
    gcl_passwordchange = /blck/mdl_cl_passwordchange=>create( ).
    gcl_passwordchange->set_old_password( 'ipsum lorem' ). " (type string)
    gcl_passwordchange->set_new_password( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_passwordchange(
    	exporting
    		i_passwordchange = gcl_passwordchange ).
    		
    clear gcl_passwordchange.
    
* fetch new instance from example API method
    gcl_passwordchange = gcl_exampleapi->get_passwordchange(
    	exporting
    		i_id = 1 ).
    		
    l_old_password = gcl_passwordchange->get_old_password( ). " (type string)
    l_new_password = gcl_passwordchange->get_new_password( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**old_password** | string | The current password. | [optional] [default to null]
**new_password** | string | The new password. | [optional] [default to null]

* * *
<a name="markdown-header-model-plugininfoconf"></a> 

# Model: plugininfoconf



### Example
```abap
*** model plugininfoconf example
*** The configuration for authentication plugin.

* create our variables..
    data gcl_plugininfoconf type ref to /blck/mdl_cl_plugininfoconf.
    
* instantiate model and call the setters to set values..
    gcl_plugininfoconf = /blck/mdl_cl_plugininfoconf=>create( ).
    gcl_plugininfoconf->set_name( 'ipsum lorem' ). " (type string)
    gcl_plugininfoconf->set_is_default( 'X' ). " (type flag)
    gcl_plugininfoconf->set_assembly_name( 'ipsum lorem' ). " (type string)
    gcl_plugininfoconf->set_bridge_class_name( 'ipsum lorem' ). " (type string)
    gcl_plugininfoconf->set_is_scope_independent( 'X' ). " (type flag)
    gcl_plugininfoconf->set_protocol( 'ipsum lorem' ). " (type string)
    gcl_plugininfoconf->set_configuration( l_configuration ). " (type /blck/api_string_mt)
    gcl_plugininfoconf->set_configuration_source( l_configuration_source ). " (type /blck/api_string_mt)
    
* pass to example API method
    gcl_exampleapi->update_plugininfoconf(
    	exporting
    		i_plugininfoconf = gcl_plugininfoconf ).
    		
    clear gcl_plugininfoconf.
    
* fetch new instance from example API method
    gcl_plugininfoconf = gcl_exampleapi->get_plugininfoconf(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_plugininfoconf->get_name( ). " (type string)
    l_is_default = gcl_plugininfoconf->get_is_default( ). " (type flag)
    l_assembly_name = gcl_plugininfoconf->get_assembly_name( ). " (type string)
    l_bridge_class_name = gcl_plugininfoconf->get_bridge_class_name( ). " (type string)
    l_is_scope_independent = gcl_plugininfoconf->get_is_scope_independent( ). " (type flag)
    l_protocol = gcl_plugininfoconf->get_protocol( ). " (type string)
    l_configuration = gcl_plugininfoconf->get_configuration( ). " (type /blck/api_string_mt)
    l_configuration_source = gcl_plugininfoconf->get_configuration_source( ). " (type /blck/api_string_mt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string | The name of the plugin configuration. | [optional] [default to null]
**is_default** | flag | Specifies if this is the default plugin configuration. | [optional] [default to null]
**assembly_name** | string | Assembly name. | [optional] [default to null]
**bridge_class_name** | string | Bridge class name. | [optional] [default to null]
**is_scope_independent** | flag | Specifies if this plugin configuration is independent of scope. | [optional] [default to null]
**protocol** | string | The used protocol for the plug-in, e.g. SAMLv2.0. | [optional] [default to null]
**configuration** | /blck/api_string_mt | The name of the plugin configuration. | [optional] [default to null]
**configuration_source** | /blck/api_string_mt | The name of the plugin configuration. | [optional] [default to null]

* * *
<a name="markdown-header-model-primitivetypei"></a> 

# Model: primitivetypei



### Example
```abap
*** model primitivetypei example
*** https://developer.m-files.com/APIs/REST-API/Reference/structs/primitivetypet/

* create our variables..
    data gcl_primitivetypei type ref to /blck/mdl_cl_primitivetypei.
    
* instantiate model and call the setters to set values..
    gcl_primitivetypei = /blck/mdl_cl_primitivetypei=>create( ).
    gcl_primitivetypei->set_value( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_primitivetypei(
    	exporting
    		i_primitivetypei = gcl_primitivetypei ).
    		
    clear gcl_primitivetypei.
    
* fetch new instance from example API method
    gcl_primitivetypei = gcl_exampleapi->get_primitivetypei(
    	exporting
    		i_id = 1 ).
    		
    l_value = gcl_primitivetypei->get_value( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**value** | i | Primitive value. | [optional] [default to null]

* * *
<a name="markdown-header-model-property_def"></a> 

# Model: property_def



### Example
```abap
*** model property_def example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~PropertyDef.html

* create our variables..
    data gcl_property_def type ref to /blck/mdl_cl_property_def.
    
* instantiate model and call the setters to set values..
    gcl_property_def = /blck/mdl_cl_property_def=>create( ).
    gcl_property_def->set_all_object_types( 'X' ). " (type flag)
    gcl_property_def->set_automatic_value( 'ipsum lorem' ). " (type string)
    gcl_property_def->set_automatic_value_type( l_automatic_value_type ). " (type /BLCK/MFI_mfautomaticval)
    gcl_property_def->set_based_on_value_list( 'X' ). " (type flag)
    gcl_property_def->set_data_type( l_data_type ). " (type /BLCK/MFI_mf_data_type)
    gcl_property_def->set_id( 42 ). " (type i)
    gcl_property_def->set_name( 'ipsum lorem' ). " (type string)
    gcl_property_def->set_object_type( 42 ). " (type i)
    gcl_property_def->set_value_list( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_property_def(
    	exporting
    		i_property_def = gcl_property_def ).
    		
    clear gcl_property_def.
    
* fetch new instance from example API method
    gcl_property_def = gcl_exampleapi->get_property_def(
    	exporting
    		i_id = 1 ).
    		
    l_all_object_types = gcl_property_def->get_all_object_types( ). " (type flag)
    l_automatic_value = gcl_property_def->get_automatic_value( ). " (type string)
    l_automatic_value_type = gcl_property_def->get_automatic_value_type( ). " (type /BLCK/MFI_mfautomaticval)
    l_based_on_value_list = gcl_property_def->get_based_on_value_list( ). " (type flag)
    l_data_type = gcl_property_def->get_data_type( ). " (type /BLCK/MFI_mf_data_type)
    l_id = gcl_property_def->get_id( ). " (type i)
    l_name = gcl_property_def->get_name( ). " (type string)
    l_object_type = gcl_property_def->get_object_type( ). " (type i)
    l_value_list = gcl_property_def->get_value_list( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**all_object_types** | flag |  | [optional] [default to null]
**automatic_value** | string |  | [optional] [default to null]
**automatic_value_type** | /BLCK/MFI_mfautomaticval (**[mfautomaticval](#markdown-header-enum-mfautomaticval)**) |  | [optional] [default to null]
**based_on_value_list** | flag |  | [optional] [default to null]
**data_type** | /BLCK/MFI_mf_data_type (**[mf_data_type](#markdown-header-enum-mf_data_type)**) |  | [optional] [default to null]
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**object_type** | i |  | [optional] [default to null]
**value_list** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-model-propertyvalues"></a> 

# Model: propertyvalues



### Example
```abap
*** model propertyvalues example

* create our variables..
    data gcl_propertyvalues type ref to /blck/mdl_cl_propertyvalues.
    
* instantiate model and call the setters to set values..
    gcl_propertyvalues = /blck/mdl_cl_propertyvalues=>create( ).
    gcl_propertyvalues->set_display_value( 'ipsum lorem' ). " (type string)
    gcl_propertyvalues->set_is_fact( 'X' ). " (type flag)
    gcl_propertyvalues->set_is_new_value( 'X' ). " (type flag)
    gcl_propertyvalues->set_property_def( 'ipsum lorem' ). " (type string)
    gcl_propertyvalues->set_quality( 42 ). " (type i)
    gcl_propertyvalues->set_typed_value( l_typed_value ). " (type /BLCK/MFI_typed_value)
    
* pass to example API method
    gcl_exampleapi->update_propertyvalues(
    	exporting
    		i_propertyvalues = gcl_propertyvalues ).
    		
    clear gcl_propertyvalues.
    
* fetch new instance from example API method
    gcl_propertyvalues = gcl_exampleapi->get_propertyvalues(
    	exporting
    		i_id = 1 ).
    		
    l_display_value = gcl_propertyvalues->get_display_value( ). " (type string)
    l_is_fact = gcl_propertyvalues->get_is_fact( ). " (type flag)
    l_is_new_value = gcl_propertyvalues->get_is_new_value( ). " (type flag)
    l_property_def = gcl_propertyvalues->get_property_def( ). " (type string)
    l_quality = gcl_propertyvalues->get_quality( ). " (type i)
    l_typed_value = gcl_propertyvalues->get_typed_value( ). " (type /BLCK/MFI_typed_value)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**display_value** | string |  | [optional] [default to null]
**is_fact** | flag |  | [optional] [default to null]
**is_new_value** | flag |  | [optional] [default to null]
**property_def** | string |  | [optional] [default to null]
**quality** | i |  | [optional] [default to null]
**typed_value** | /BLCK/MFI_typed_value (**[typed_value](#markdown-header-model-typed_value)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-public_key"></a> 

# Model: public_key



### Example
```abap
*** model public_key example
*** Server public key information.

* create our variables..
    data gcl_public_key type ref to /blck/mdl_cl_public_key.
    
* instantiate model and call the setters to set values..
    gcl_public_key = /blck/mdl_cl_public_key=>create( ).
    gcl_public_key->set_exponent( 'ipsum lorem' ). " (type string)
    gcl_public_key->set_modulus( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_public_key(
    	exporting
    		i_public_key = gcl_public_key ).
    		
    clear gcl_public_key.
    
* fetch new instance from example API method
    gcl_public_key = gcl_exampleapi->get_public_key(
    	exporting
    		i_id = 1 ).
    		
    l_exponent = gcl_public_key->get_exponent( ). " (type string)
    l_modulus = gcl_public_key->get_modulus( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**exponent** | string | Base64URL encoded exponent. | [optional] [default to null]
**modulus** | string | Base64URL encoded modulus. | [optional] [default to null]

* * *
<a name="markdown-header-model-repositoryaut2"></a> 

# Model: repositoryaut2



### Example
```abap
*** model repositoryaut2 example
*** Structure defining one external repository authentication status.

* create our variables..
    data gcl_repositoryaut2 type ref to /blck/mdl_cl_repositoryaut2.
    
* instantiate model and call the setters to set values..
    gcl_repositoryaut2 = /blck/mdl_cl_repositoryaut2=>create( ).
    gcl_repositoryaut2->set_account_name( 'ipsum lorem' ). " (type string)
    gcl_repositoryaut2->set_extensionauthenticationspe( l_extensionauthenticationspe ). " (type /BLCK/MFI_mfextensionaut)
    gcl_repositoryaut2->set_target_id( 'ipsum lorem' ). " (type string)
    gcl_repositoryaut2->set_user_id( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_repositoryaut2(
    	exporting
    		i_repositoryaut2 = gcl_repositoryaut2 ).
    		
    clear gcl_repositoryaut2.
    
* fetch new instance from example API method
    gcl_repositoryaut2 = gcl_exampleapi->get_repositoryaut2(
    	exporting
    		i_id = 1 ).
    		
    l_account_name = gcl_repositoryaut2->get_account_name( ). " (type string)
    l_extensionauthenticationspe = gcl_repositoryaut2->get_extensionauthenticationspe( ). " (type /BLCK/MFI_mfextensionaut)
    l_target_id = gcl_repositoryaut2->get_target_id( ). " (type string)
    l_user_id = gcl_repositoryaut2->get_user_id( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**account_name** | string | Account name used for authentication. | [optional] [default to null]
**extensionauthenticationspe** | /BLCK/MFI_mfextensionaut (**[mfextensionaut](#markdown-header-enum-mfextensionaut)**) |  | [optional] [default to null]
**target_id** | string | ID of the target repository. | [optional] [default to null]
**user_id** | i | ID of the authenticated M-Files user. | [optional] [default to null]

* * *
<a name="markdown-header-model-repositoryaut3"></a> 

# Model: repositoryaut3



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
    data gcl_repositoryaut3 type ref to /blck/mdl_cl_repositoryaut3.
    
* instantiate model and call the setters to set values..
    gcl_repositoryaut3 = /blck/mdl_cl_repositoryaut3=>create( ).
    gcl_repositoryaut3->set_configuration_name( 'ipsum lorem' ). " (type string)
    gcl_repositoryaut3->set_username( 'ipsum lorem' ). " (type string)
    gcl_repositoryaut3->set_password( 'ipsum lorem' ). " (type string)
    gcl_repositoryaut3->set_authentication_token( 'ipsum lorem' ). " (type string)
    gcl_repositoryaut3->set_refresh_token( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_repositoryaut3(
    	exporting
    		i_repositoryaut3 = gcl_repositoryaut3 ).
    		
    clear gcl_repositoryaut3.
    
* fetch new instance from example API method
    gcl_repositoryaut3 = gcl_exampleapi->get_repositoryaut3(
    	exporting
    		i_id = 1 ).
    		
    l_configuration_name = gcl_repositoryaut3->get_configuration_name( ). " (type string)
    l_username = gcl_repositoryaut3->get_username( ). " (type string)
    l_password = gcl_repositoryaut3->get_password( ). " (type string)
    l_authentication_token = gcl_repositoryaut3->get_authentication_token( ). " (type string)
    l_refresh_token = gcl_repositoryaut3->get_refresh_token( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**configuration_name** | string | Name of the authentication configuration. | [optional] [default to null]
**username** | string | Username used for basic authentication. | [optional] [default to null]
**password** | string | Password used for basic authentication. | [optional] [default to null]
**authentication_token** | string | The authentication token for plugin authentication. Must be null if using basic username/password authentication | [optional] [default to null]
**refresh_token** | string | The refresh token for plugin authentication. | [optional] [default to null]

* * *
<a name="markdown-header-model-repositoryauth"></a> 

# Model: repositoryauth



### Example
```abap
*** model repositoryauth example

* create our variables..
    data gcl_repositoryauth type ref to /blck/mdl_cl_repositoryauth.
    
* instantiate model and call the setters to set values..
    gcl_repositoryauth = /blck/mdl_cl_repositoryauth=>create( ).
    gcl_repositoryauth->set_display_name( 'ipsum lorem' ). " (type string)
    gcl_repositoryauth->set_icon_id( 'ipsum lorem' ). " (type string)
    gcl_repositoryauth->set_id( 'ipsum lorem' ). " (type string)
    gcl_repositoryauth->set_plugin_info_configurations( l_plugin_info_configurations ). " (type /BLCK/MFI_plugininfoconf)
    gcl_repositoryauth->set_requiresuserspecificauthen( 'ipsum lorem' ). " (type string)
    gcl_repositoryauth->set_repositoryauthenticationst( l_repositoryauthenticationst ). " (type /BLCK/MFI_repositoryaut2)
    
* pass to example API method
    gcl_exampleapi->update_repositoryauth(
    	exporting
    		i_repositoryauth = gcl_repositoryauth ).
    		
    clear gcl_repositoryauth.
    
* fetch new instance from example API method
    gcl_repositoryauth = gcl_exampleapi->get_repositoryauth(
    	exporting
    		i_id = 1 ).
    		
    l_display_name = gcl_repositoryauth->get_display_name( ). " (type string)
    l_icon_id = gcl_repositoryauth->get_icon_id( ). " (type string)
    l_id = gcl_repositoryauth->get_id( ). " (type string)
    l_plugin_info_configurations = gcl_repositoryauth->get_plugin_info_configurations( ). " (type /BLCK/MFI_plugininfoconf)
    l_requiresuserspecificauthen = gcl_repositoryauth->get_requiresuserspecificauthen( ). " (type string)
    l_repositoryauthenticationst = gcl_repositoryauth->get_repositoryauthenticationst( ). " (type /BLCK/MFI_repositoryaut2)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**display_name** | string | Display name of the target repository. | [optional] [default to null]
**icon_id** | string | Icon id of the target repository. | [optional] [default to null]
**id** | string | ID of the target repository. | [optional] [default to null]
**plugin_info_configurations** | /BLCK/MFI_plugininfoconf (**[plugininfoconf](#markdown-header-model-plugininfoconf)**) |  | [optional] [default to null]
**requiresuserspecificauthen** | string | Flag indicating if user specific authentication is required. | [optional] [default to null]
**repositoryauthenticationst** | /BLCK/MFI_repositoryaut2 (**[repositoryaut2](#markdown-header-model-repositoryaut2)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-resultsobjectv"></a> 

# Model: resultsobjectv



### Example
```abap
*** model resultsobjectv example
*** Results of a query which might leave only a partial set of items..

* create our variables..
    data gcl_resultsobjectv type ref to /blck/mdl_cl_resultsobjectv.
    
* instantiate model and call the setters to set values..
    gcl_resultsobjectv = /blck/mdl_cl_resultsobjectv=>create( ).
    gcl_resultsobjectv->set_items( l_items ). " (type /BLCK/MFI_object_version_tt)
    gcl_resultsobjectv->set_more_results( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_resultsobjectv(
    	exporting
    		i_resultsobjectv = gcl_resultsobjectv ).
    		
    clear gcl_resultsobjectv.
    
* fetch new instance from example API method
    gcl_resultsobjectv = gcl_exampleapi->get_resultsobjectv(
    	exporting
    		i_id = 1 ).
    		
    l_items = gcl_resultsobjectv->get_items( ). " (type /BLCK/MFI_object_version_tt)
    l_more_results = gcl_resultsobjectv->get_more_results( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**items** | /BLCK/MFI_object_version_tt (**[array of object_version](#markdown-header-model-object_version)**) | Contains results of a query | [optional] [default to null]
**more_results** | flag | True if there were more results which were left out. | [optional] [default to null]

* * *
<a name="markdown-header-model-valuelistitem"></a> 

# Model: valuelistitem



### Example
```abap
*** model valuelistitem example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~ValueListItem.html

* create our variables..
    data gcl_valuelistitem type ref to /blck/mdl_cl_valuelistitem.
    
* instantiate model and call the setters to set values..
    gcl_valuelistitem = /blck/mdl_cl_valuelistitem=>create( ).
    gcl_valuelistitem->set_display_id( 'ipsum lorem' ). " (type string)
    gcl_valuelistitem->set_has_owner( 'X' ). " (type flag)
    gcl_valuelistitem->set_has_parent( 'X' ). " (type flag)
    gcl_valuelistitem->set_id( 42 ). " (type i)
    gcl_valuelistitem->set_name( 'ipsum lorem' ). " (type string)
    gcl_valuelistitem->set_owner_id( 42 ). " (type i)
    gcl_valuelistitem->set_parent_id( 42 ). " (type i)
    gcl_valuelistitem->set_value_list_id( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_valuelistitem(
    	exporting
    		i_valuelistitem = gcl_valuelistitem ).
    		
    clear gcl_valuelistitem.
    
* fetch new instance from example API method
    gcl_valuelistitem = gcl_exampleapi->get_valuelistitem(
    	exporting
    		i_id = 1 ).
    		
    l_display_id = gcl_valuelistitem->get_display_id( ). " (type string)
    l_has_owner = gcl_valuelistitem->get_has_owner( ). " (type flag)
    l_has_parent = gcl_valuelistitem->get_has_parent( ). " (type flag)
    l_id = gcl_valuelistitem->get_id( ). " (type i)
    l_name = gcl_valuelistitem->get_name( ). " (type string)
    l_owner_id = gcl_valuelistitem->get_owner_id( ). " (type i)
    l_parent_id = gcl_valuelistitem->get_parent_id( ). " (type i)
    l_value_list_id = gcl_valuelistitem->get_value_list_id( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**display_id** | string |  | [optional] [default to null]
**has_owner** | flag |  | [optional] [default to null]
**has_parent** | flag |  | [optional] [default to null]
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**owner_id** | i |  | [optional] [default to null]
**parent_id** | i |  | [optional] [default to null]
**value_list_id** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-model-resultsvalueli"></a> 

# Model: resultsvalueli



### Example
```abap
*** model resultsvalueli example
*** Results of a query which might leave only a partial set of items..

* create our variables..
    data gcl_resultsvalueli type ref to /blck/mdl_cl_resultsvalueli.
    
* instantiate model and call the setters to set values..
    gcl_resultsvalueli = /blck/mdl_cl_resultsvalueli=>create( ).
    gcl_resultsvalueli->set_items( l_items ). " (type /BLCK/MFI_valuelistitem_tt)
    gcl_resultsvalueli->set_more_results( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_resultsvalueli(
    	exporting
    		i_resultsvalueli = gcl_resultsvalueli ).
    		
    clear gcl_resultsvalueli.
    
* fetch new instance from example API method
    gcl_resultsvalueli = gcl_exampleapi->get_resultsvalueli(
    	exporting
    		i_id = 1 ).
    		
    l_items = gcl_resultsvalueli->get_items( ). " (type /BLCK/MFI_valuelistitem_tt)
    l_more_results = gcl_resultsvalueli->get_more_results( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**items** | /BLCK/MFI_valuelistitem_tt (**[array of valuelistitem](#markdown-header-model-valuelistitem)**) | Contains results of a query | [optional] [default to null]
**more_results** | flag | True if there were more results which were left out. | [optional] [default to null]

* * *
<a name="markdown-header-model-session_info"></a> 

# Model: session_info



### Example
```abap
*** model session_info example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~SessionInfo.html

* create our variables..
    data gcl_session_info type ref to /blck/mdl_cl_session_info.
    
* instantiate model and call the setters to set values..
    gcl_session_info = /blck/mdl_cl_session_info=>create( ).
    gcl_session_info->set_account_name( 'ipsum lorem' ). " (type string)
    gcl_session_info->set_acl_mode( l_acl_mode ). " (type /BLCK/MFI_mfacl_mode)
    gcl_session_info->set_authentication_type( l_authentication_type ). " (type /BLCK/MFI_mf_auth_type)
    gcl_session_info->set_can_force_undo_checkout( 'X' ). " (type flag)
    gcl_session_info->set_canmanagecommonuisettings( 'X' ). " (type flag)
    gcl_session_info->set_can_manage_common_views( 'X' ). " (type flag)
    gcl_session_info->set_canmanagetraditionalfolder( 'X' ). " (type flag)
    gcl_session_info->set_can_materialize_views( 'X' ). " (type flag)
    gcl_session_info->set_can_see_all_objects( 'X' ). " (type flag)
    gcl_session_info->set_can_see_deleted_objects( 'X' ). " (type flag)
    gcl_session_info->set_internal_user( 'X' ). " (type flag)
    gcl_session_info->set_licenseallowsmodifications( 'X' ). " (type flag)
    gcl_session_info->set_user_id( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_session_info(
    	exporting
    		i_session_info = gcl_session_info ).
    		
    clear gcl_session_info.
    
* fetch new instance from example API method
    gcl_session_info = gcl_exampleapi->get_session_info(
    	exporting
    		i_id = 1 ).
    		
    l_account_name = gcl_session_info->get_account_name( ). " (type string)
    l_acl_mode = gcl_session_info->get_acl_mode( ). " (type /BLCK/MFI_mfacl_mode)
    l_authentication_type = gcl_session_info->get_authentication_type( ). " (type /BLCK/MFI_mf_auth_type)
    l_can_force_undo_checkout = gcl_session_info->get_can_force_undo_checkout( ). " (type flag)
    l_canmanagecommonuisettings = gcl_session_info->get_canmanagecommonuisettings( ). " (type flag)
    l_can_manage_common_views = gcl_session_info->get_can_manage_common_views( ). " (type flag)
    l_canmanagetraditionalfolder = gcl_session_info->get_canmanagetraditionalfolder( ). " (type flag)
    l_can_materialize_views = gcl_session_info->get_can_materialize_views( ). " (type flag)
    l_can_see_all_objects = gcl_session_info->get_can_see_all_objects( ). " (type flag)
    l_can_see_deleted_objects = gcl_session_info->get_can_see_deleted_objects( ). " (type flag)
    l_internal_user = gcl_session_info->get_internal_user( ). " (type flag)
    l_licenseallowsmodifications = gcl_session_info->get_licenseallowsmodifications( ). " (type flag)
    l_user_id = gcl_session_info->get_user_id( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**account_name** | string |  | [optional] [default to null]
**acl_mode** | /BLCK/MFI_mfacl_mode (**[mfacl_mode](#markdown-header-enum-mfacl_mode)**) |  | [optional] [default to null]
**authentication_type** | /BLCK/MFI_mf_auth_type (**[mf_auth_type](#markdown-header-enum-mf_auth_type)**) |  | [optional] [default to null]
**can_force_undo_checkout** | flag |  | [optional] [default to null]
**canmanagecommonuisettings** | flag |  | [optional] [default to null]
**can_manage_common_views** | flag |  | [optional] [default to null]
**canmanagetraditionalfolder** | flag |  | [optional] [default to null]
**can_materialize_views** | flag |  | [optional] [default to null]
**can_see_all_objects** | flag |  | [optional] [default to null]
**can_see_deleted_objects** | flag |  | [optional] [default to null]
**internal_user** | flag |  | [optional] [default to null]
**licenseallowsmodifications** | flag |  | [optional] [default to null]
**user_id** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-model-statusresponse"></a> 

# Model: statusresponse



### Example
```abap
*** model statusresponse example
*** Response for status requests.

* create our variables..
    data gcl_statusresponse type ref to /blck/mdl_cl_statusresponse.
    
* instantiate model and call the setters to set values..
    gcl_statusresponse = /blck/mdl_cl_statusresponse=>create( ).
    gcl_statusresponse->set_successful( 'X' ). " (type flag)
    gcl_statusresponse->set_message( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_statusresponse(
    	exporting
    		i_statusresponse = gcl_statusresponse ).
    		
    clear gcl_statusresponse.
    
* fetch new instance from example API method
    gcl_statusresponse = gcl_exampleapi->get_statusresponse(
    	exporting
    		i_id = 1 ).
    		
    l_successful = gcl_statusresponse->get_successful( ). " (type flag)
    l_message = gcl_statusresponse->get_message( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**successful** | flag | The result of the status request. | [optional] [default to null]
**message** | string | Display message for the status. | [optional] [default to null]

* * *
<a name="markdown-header-model-vault"></a> 

# Model: vault



### Example
```abap
*** model vault example
*** Vault information.

* create our variables..
    data gcl_vault type ref to /blck/mdl_cl_vault.
    
* instantiate model and call the setters to set values..
    gcl_vault = /blck/mdl_cl_vault=>create( ).
    gcl_vault->set_name( 'ipsum lorem' ). " (type string)
    gcl_vault->set_guid( 'ipsum lorem' ). " (type string)
    gcl_vault->set_authentication( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_vault(
    	exporting
    		i_vault = gcl_vault ).
    		
    clear gcl_vault.
    
* fetch new instance from example API method
    gcl_vault = gcl_exampleapi->get_vault(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_vault->get_name( ). " (type string)
    l_guid = gcl_vault->get_guid( ). " (type string)
    l_authentication = gcl_vault->get_authentication( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string | Vault name. | [optional] [default to null]
**guid** | string | Vault GUID. | [optional] [default to null]
**authentication** | string | Vault-specific authentication token. | [optional] [default to null]

* * *
<a name="markdown-header-model-versioncomment"></a> 

# Model: versioncomment



### Example
```abap
*** model versioncomment example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~VersionComment.html

* create our variables..
    data gcl_versioncomment type ref to /blck/mdl_cl_versioncomment.
    
* instantiate model and call the setters to set values..
    gcl_versioncomment = /blck/mdl_cl_versioncomment=>create( ).
    gcl_versioncomment->set_last_modified_by( l_last_modified_by ). " (type /BLCK/MFI_property_value)
    gcl_versioncomment->set_obj_ver( l_obj_ver ). " (type /BLCK/MFI_obj_ver)
    gcl_versioncomment->set_status_changed( l_status_changed ). " (type /BLCK/MFI_property_value)
    gcl_versioncomment->set_comment( l_comment ). " (type /BLCK/MFI_property_value)
    
* pass to example API method
    gcl_exampleapi->update_versioncomment(
    	exporting
    		i_versioncomment = gcl_versioncomment ).
    		
    clear gcl_versioncomment.
    
* fetch new instance from example API method
    gcl_versioncomment = gcl_exampleapi->get_versioncomment(
    	exporting
    		i_id = 1 ).
    		
    l_last_modified_by = gcl_versioncomment->get_last_modified_by( ). " (type /BLCK/MFI_property_value)
    l_obj_ver = gcl_versioncomment->get_obj_ver( ). " (type /BLCK/MFI_obj_ver)
    l_status_changed = gcl_versioncomment->get_status_changed( ). " (type /BLCK/MFI_property_value)
    l_comment = gcl_versioncomment->get_comment( ). " (type /BLCK/MFI_property_value)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**last_modified_by** | /BLCK/MFI_property_value (**[property_value](#markdown-header-model-property_value)**) |  | [optional] [default to null]
**obj_ver** | /BLCK/MFI_obj_ver (**[obj_ver](#markdown-header-model-obj_ver)**) |  | [optional] [default to null]
**status_changed** | /BLCK/MFI_property_value (**[property_value](#markdown-header-model-property_value)**) |  | [optional] [default to null]
**comment** | /BLCK/MFI_property_value (**[property_value](#markdown-header-model-property_value)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-webserviceerro"></a> 

# Model: webserviceerro



### Example
```abap
*** model webserviceerro example
*** M-Files Web Service error object.

* create our variables..
    data gcl_webserviceerro type ref to /blck/mdl_cl_webserviceerro.
    
* instantiate model and call the setters to set values..
    gcl_webserviceerro = /blck/mdl_cl_webserviceerro=>create( ).
    gcl_webserviceerro->set_status( 42 ). " (type i)
    gcl_webserviceerro->set_url( 'ipsum lorem' ). " (type string)
    gcl_webserviceerro->set_method( 'ipsum lorem' ). " (type string)
    gcl_webserviceerro->set_exception( l_exception ). " (type /BLCK/MFI_exception_info)
    
* pass to example API method
    gcl_exampleapi->update_webserviceerro(
    	exporting
    		i_webserviceerro = gcl_webserviceerro ).
    		
    clear gcl_webserviceerro.
    
* fetch new instance from example API method
    gcl_webserviceerro = gcl_exampleapi->get_webserviceerro(
    	exporting
    		i_id = 1 ).
    		
    l_status = gcl_webserviceerro->get_status( ). " (type i)
    l_url = gcl_webserviceerro->get_url( ). " (type string)
    l_method = gcl_webserviceerro->get_method( ). " (type string)
    l_exception = gcl_webserviceerro->get_exception( ). " (type /BLCK/MFI_exception_info)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**status** | i | HTTP Status code | [optional] [default to null]
**url** | string | The request URL which caused this error. | [optional] [default to null]
**method** | string | The request method. | [optional] [default to null]
**exception** | /BLCK/MFI_exception_info (**[exception_info](#markdown-header-model-exception_info)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-workflow"></a> 

# Model: workflow



### Example
```abap
*** model workflow example
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~Workflow.html

* create our variables..
    data gcl_workflow type ref to /blck/mdl_cl_workflow.
    
* instantiate model and call the setters to set values..
    gcl_workflow = /blck/mdl_cl_workflow=>create( ).
    gcl_workflow->set_id( 42 ). " (type i)
    gcl_workflow->set_name( 'ipsum lorem' ). " (type string)
    gcl_workflow->set_object_class( 42 ). " (type i)
    
* pass to example API method
    gcl_exampleapi->update_workflow(
    	exporting
    		i_workflow = gcl_workflow ).
    		
    clear gcl_workflow.
    
* fetch new instance from example API method
    gcl_workflow = gcl_exampleapi->get_workflow(
    	exporting
    		i_id = 1 ).
    		
    l_id = gcl_workflow->get_id( ). " (type i)
    l_name = gcl_workflow->get_name( ). " (type string)
    l_object_class = gcl_workflow->get_object_class( ). " (type i)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**id** | i |  | [optional] [default to null]
**name** | string |  | [optional] [default to null]
**object_class** | i |  | [optional] [default to null]

* * *
<a name="markdown-header-model-workflow_state"></a> 

# Model: workflow_state



### Example
```abap
*** model workflow_state example
*** Workflow                          state                         information.
*** https://www.m-files.com/api/documentation/latest/index.html#MFilesAPI~State.html

* create our variables..
    data gcl_workflow_state type ref to /blck/mdl_cl_workflow_state.
    
* instantiate model and call the setters to set values..
    gcl_workflow_state = /blck/mdl_cl_workflow_state=>create( ).
    gcl_workflow_state->set_name( 'ipsum lorem' ). " (type string)
    gcl_workflow_state->set_id( 42 ). " (type i)
    gcl_workflow_state->set_selectable( 'X' ). " (type flag)
    
* pass to example API method
    gcl_exampleapi->update_workflow_state(
    	exporting
    		i_workflow_state = gcl_workflow_state ).
    		
    clear gcl_workflow_state.
    
* fetch new instance from example API method
    gcl_workflow_state = gcl_exampleapi->get_workflow_state(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_workflow_state->get_name( ). " (type string)
    l_id = gcl_workflow_state->get_id( ). " (type i)
    l_selectable = gcl_workflow_state->get_selectable( ). " (type flag)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string | Workflow state name. | [optional] [default to null]
**id** | i | Workflow state ID. | [optional] [default to null]
**selectable** | flag | Defines whether this state is selectable for the current object. | [optional] [default to null]

