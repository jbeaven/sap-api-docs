# API: EventsApi

All URIs are relative to *https://operator-seal.cloudapp.net/v1*

## operation: **event_notifications_get**
Retrieve job status

Opens a websocket connection and returns status changes of all jobs send by Operator as status events. Events are generated only for jobs which status was previously requested via GET /jobs/{uuid} 


### Example
```abap
*** method EventsApi->event_notifications_get example
*** Retrieve job status

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/P4_JOBSTATUSEVENT
    data gr_http200 type /BLCK/P4_JOBSTATUSEVENT.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_EventsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method event_notifications_get via HTTP GET
    /blck/p4_cl_EventsApi=>event_notifications_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P4_JOBSTATUSEVENT)
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P4_JOBSTATUSEVENT (**[JobStatusEvent](#markdown-header-model-)**) | OK, job status is returned
 401 | **e_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights. 
 500 | **e_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: JobsApi

All URIs are relative to *https://operator-seal.cloudapp.net/v1*

## operation: **jobs_post**
Create new job

A POST call to this route will create a new jobs and return it's uuid. 


### Example
```abap
*** method JobsApi->jobs_post example
*** Create new job

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/P4_STRING
    data gvs_body type /BLCK/P4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P4_JOB_ID
    data gr_http200 type /BLCK/P4_JOB_ID.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_post via HTTP POST
*** i_body: job header data of the entry to be created
    /blck/p4_cl_JobsApi=>jobs_post(
      exporting
        i_body = gvs_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P4_JOB_ID)
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P4_STRING | job header data of the entry to be created 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P4_JOB_ID (**[JobId](#markdown-header-model-)**) | OK, job ID is returned.
 401 | **e_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service list. 
 409 | **e_409** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobs_uuid_abort_post**
Abort a job

A POST call to this route will abort a running job. 


### Example
```abap
*** method JobsApi->jobs_uuid_abort_post example
*** Abort a job

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed
*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/P4_STRING
    data gvs_uuid type /BLCK/P4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_uuid_abort_post via HTTP POST
*** i_uuid: ID of the current job.
    /blck/p4_cl_JobsApi=>jobs_uuid_abort_post(
      exporting
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_uuid** | /BLCK/P4_STRING | ID of the current job. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_uuid_get**
Retrieve job status

returns status of given job


### Example
```abap
*** method JobsApi->jobs_uuid_get example
*** Retrieve job status

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed
*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/P4_STRING
    data gvs_uuid type /BLCK/P4_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/P4_JOB_STATUS
    data gr_http200 type /BLCK/P4_JOB_STATUS.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/P4_ERROR
    data gr_http404 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_uuid_get via HTTP GET
*** i_uuid: ID of the current job.
    /blck/p4_cl_JobsApi=>jobs_uuid_get(
      exporting
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P4_JOB_STATUS)
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_uuid** | /BLCK/P4_STRING | ID of the current job. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P4_JOB_STATUS (**[JobStatus](#markdown-header-model-)**) | OK, job status is returned
 401 | **e_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights to access the service metadata. 
 404 | **e_404** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | The requested Service was not found.
 500 | **e_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_uuid_pause_post**
Abort a job

A POST call to this route will pause a running job. 


### Example
```abap
*** method JobsApi->jobs_uuid_pause_post example
*** Abort a job

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed
*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/P4_STRING
    data gvs_uuid type /BLCK/P4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_uuid_pause_post via HTTP POST
*** i_uuid: ID of the current job.
    /blck/p4_cl_JobsApi=>jobs_uuid_pause_post(
      exporting
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_uuid** | /BLCK/P4_STRING | ID of the current job. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_uuid_put**
Add files to the job

A PUT call to this route will add a new file to the job. Data type is given in HTTP `Content-Type` header item. 


### Example
```abap
*** method JobsApi->jobs_uuid_put example
*** Add files to the job

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed
*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/P4_STRING
    data gvs_uuid type /BLCK/P4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_uuid_put via HTTP PUT
*** i_uuid: ID of the current job.
    /blck/p4_cl_JobsApi=>jobs_uuid_put(
      exporting
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_uuid** | /BLCK/P4_STRING | ID of the current job. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_uuid_resume_post**
Resume a job

A POST call to this route will resume a paused job. 


### Example
```abap
*** method JobsApi->jobs_uuid_resume_post example
*** Resume a job

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed
*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/P4_STRING
    data gvs_uuid type /BLCK/P4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_uuid_resume_post via HTTP POST
*** i_uuid: ID of the current job.
    /blck/p4_cl_JobsApi=>jobs_uuid_resume_post(
      exporting
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_uuid** | /BLCK/P4_STRING | ID of the current job. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_uuid_start_post**
Start a job

A POST call to this route will start a previously created job. 


### Example
```abap
*** method JobsApi->jobs_uuid_start_post example
*** Start a job

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed
*   for parameter i_uuid:
*   a simple ABAP primitive of type /BLCK/P4_STRING
    data gvs_uuid type /BLCK/P4_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        
*** set data according to requirements of the API call
*   gvs_uuid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_uuid_start_post via HTTP POST
*** i_uuid: ID of the current job.
    /blck/p4_cl_JobsApi=>jobs_uuid_start_post(
      exporting
        i_uuid = gvs_uuid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_403 = gr_http403
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_uuid** | /BLCK/P4_STRING | ID of the current job. 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


# API: PrintersApi

All URIs are relative to *https://operator-seal.cloudapp.net/v1*

## operation: **printers_get**
Retrieve printer list

Returns list of available printers inluding their capabilities 


### Example
```abap
*** method PrintersApi->printers_get example
*** Retrieve printer list

  constants:
    gcc_basepath type string value 'https://operator-seal.cloudapp.net/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/p4_int,
    gvs_msg  type /blck/p4_string.
    
*** create variables for input and output as needed*   when the the result of the call is HTTP200 we expect type /BLCK/P4_PRINTER_TT
    data gr_http200 type /BLCK/P4_PRINTER_TT.
*   when the the result of the call is HTTP401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/P4_ERROR
    data gr_http0 type /BLCK/P4_ERROR.
        


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/p4_cl_PrintersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method printers_get via HTTP GET
    /blck/p4_cl_PrintersApi=>printers_get(
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_403 = gr_http403
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/P4_PRINTER_TT)
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/P4_PRINTER_TT (**[array](#markdown-header-model-)**) | OK, array of printer objects is returned
 401 | **e_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 403 | **e_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Forbidden. The user lacks acces rights. 
 500 | **e_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


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
    gcl_error->set_metadata( 'ipsum lorem' ). " (type string)
    
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
    l_metadata = gcl_error->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | i |  | [optional] [default to null]
**message** | string |  | [optional] [default to null]
**metadata** | string |  | [optional] [default to null]

* * *
<a name="markdown-header-model-job_header"></a> 

# Model: job_header



### Example
```abap
*** model job_header example
*** key value entries of a PLOSSYS 4 header

* create our variables..
    data gcl_job_header type ref to /blck/mdl_cl_job_header.
    
* instantiate model and call the setters to set values..
    gcl_job_header = /blck/mdl_cl_job_header=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_job_header(
    	exporting
    		i_job_header = gcl_job_header ).
    		
    clear gcl_job_header.
    
* fetch new instance from example API method
    gcl_job_header = gcl_exampleapi->get_job_header(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-model-job_id"></a> 

# Model: job_id



### Example
```abap
*** model job_id example
*** A JobId represents a PLOSSYS 4 job

* create our variables..
    data gcl_job_id type ref to /blck/mdl_cl_job_id.
    
* instantiate model and call the setters to set values..
    gcl_job_id = /blck/mdl_cl_job_id=>create( ).
    gcl_job_id->set_uuid( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_job_id(
    	exporting
    		i_job_id = gcl_job_id ).
    		
    clear gcl_job_id.
    
* fetch new instance from example API method
    gcl_job_id = gcl_exampleapi->get_job_id(
    	exporting
    		i_id = 1 ).
    		
    l_uuid = gcl_job_id->get_uuid( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**uuid** | string | Identifier of the job | [optional] [default to null]

* * *
<a name="markdown-header-enum-status_type"></a> 

# Enum: status_type



### Example
```abap
*** model status_type example
*** Definition of allowed status names

* create our variables..
    data gcl_status_type type ref to /blck/mdl_cl_status_type.
    
* instantiate model relevant to the enum value we want
    gcl_status_type = /blck/mdl_cl_status_type=>enum_open( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_status_type_state(
    	exporting
    		i_status_type = gcl_status_type ).
    		
    clear gcl_status_type.
    
* fetch result from example API method
    gcl_status_type = gcl_exampleapi->get_status_type_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_status_type->is_open( ) eq 'X'.
*   do something specific to open case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_status_type->get_value( ).
    when /blck/mdl_cl_status_type=>mce_open.
*     do something specific to open case..
    when /blck/mdl_cl_status_type=>mce_processing.
*     do something specific to processing case..
    when /blck/mdl_cl_status_type=>mce_completed.
*     do something specific to completed case..
    when /blck/mdl_cl_status_type=>mce_paused.
*     do something specific to paused case..
    when /blck/mdl_cl_status_type=>mce_aborted.
*     do something specific to aborted case..
    when /blck/mdl_cl_status_type=>mce_failed.
*     do something specific to failed case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**open** | open | /blck/mdl_cl_status_type=>enum_open( ).
**processing** | processing | /blck/mdl_cl_status_type=>enum_processing( ).
**completed** | completed | /blck/mdl_cl_status_type=>enum_completed( ).
**paused** | paused | /blck/mdl_cl_status_type=>enum_paused( ).
**aborted** | aborted | /blck/mdl_cl_status_type=>enum_aborted( ).
**failed** | failed | /blck/mdl_cl_status_type=>enum_failed( ).

* * *
<a name="markdown-header-model-job_status"></a> 

# Model: job_status



### Example
```abap
*** model job_status example
*** The status of a job

* create our variables..
    data gcl_job_status type ref to /blck/mdl_cl_job_status.
    
* instantiate model and call the setters to set values..
    gcl_job_status = /blck/mdl_cl_job_status=>create( ).
    gcl_job_status->set_status( l_status ). " (type /BLCK/P4_status_type)
    
* pass to example API method
    gcl_exampleapi->update_job_status(
    	exporting
    		i_job_status = gcl_job_status ).
    		
    clear gcl_job_status.
    
* fetch new instance from example API method
    gcl_job_status = gcl_exampleapi->get_job_status(
    	exporting
    		i_id = 1 ).
    		
    l_status = gcl_job_status->get_status( ). " (type /BLCK/P4_status_type)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**status** | /BLCK/P4_status_type (**[status_type](#markdown-header-enum-status_type)**) |  | [optional] [default to null]

* * *
<a name="markdown-header-model-jobstatusevent"></a> 

# Model: jobstatusevent



### Example
```abap
*** model jobstatusevent example
*** Status of a PLOSSYS 4 job

* create our variables..
    data gcl_jobstatusevent type ref to /blck/mdl_cl_jobstatusevent.
    
* instantiate model and call the setters to set values..
    gcl_jobstatusevent = /blck/mdl_cl_jobstatusevent=>create( ).
    gcl_jobstatusevent->set_type( 'ipsum lorem' ). " (type string)
    gcl_jobstatusevent->set_scope( 'ipsum lorem' ). " (type string)
    gcl_jobstatusevent->set_parameters( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_jobstatusevent(
    	exporting
    		i_jobstatusevent = gcl_jobstatusevent ).
    		
    clear gcl_jobstatusevent.
    
* fetch new instance from example API method
    gcl_jobstatusevent = gcl_exampleapi->get_jobstatusevent(
    	exporting
    		i_id = 1 ).
    		
    l_type = gcl_jobstatusevent->get_type( ). " (type string)
    l_scope = gcl_jobstatusevent->get_scope( ). " (type string)
    l_parameters = gcl_jobstatusevent->get_parameters( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**type** | string | name of event, possible values: &#x27;UPDATE_JOB&#x27;  | [optional] [default to null]
**scope** | string | uuid of PLOSSYS 4 job | [optional] [default to null]
**parameters** | string | key/value pairs with event specific parameters. E.g. for UPDATE_JOB: &#x27;status: completed&#x27;  | [optional] [default to null]

* * *
<a name="markdown-header-model-printer"></a> 

# Model: printer



### Example
```abap
*** model printer example
*** Printer capabilities

* create our variables..
    data gcl_printer type ref to /blck/mdl_cl_printer.
    
* instantiate model and call the setters to set values..
    gcl_printer = /blck/mdl_cl_printer=>create( ).
    gcl_printer->set_printer( 'ipsum lorem' ). " (type string)
    gcl_printer->set_display_name( 'ipsum lorem' ). " (type string)
    gcl_printer->set_comment( 'ipsum lorem' ). " (type string)
    gcl_printer->set_color( 'X' ). " (type flag)
    gcl_printer->set_color_default( 'X' ). " (type flag)
    gcl_printer->set_duplex( 'X' ). " (type flag)
    gcl_printer->set_duplex_default( 'ipsum lorem' ). " (type string)
    gcl_printer->set_trays( l_trays ). " (type /blck/api_string_tt)
    gcl_printer->set_tray_media( l_tray_media ). " (type /blck/api_string_tt)
    
* pass to example API method
    gcl_exampleapi->update_printer(
    	exporting
    		i_printer = gcl_printer ).
    		
    clear gcl_printer.
    
* fetch new instance from example API method
    gcl_printer = gcl_exampleapi->get_printer(
    	exporting
    		i_id = 1 ).
    		
    l_printer = gcl_printer->get_printer( ). " (type string)
    l_display_name = gcl_printer->get_display_name( ). " (type string)
    l_comment = gcl_printer->get_comment( ). " (type string)
    l_color = gcl_printer->get_color( ). " (type flag)
    l_color_default = gcl_printer->get_color_default( ). " (type flag)
    l_duplex = gcl_printer->get_duplex( ). " (type flag)
    l_duplex_default = gcl_printer->get_duplex_default( ). " (type string)
    l_trays = gcl_printer->get_trays( ). " (type /blck/api_string_tt)
    l_tray_media = gcl_printer->get_tray_media( ). " (type /blck/api_string_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**printer** | string | Printer name | [optional] [default to null]
**display_name** | string | Name used for displaying the printer (if empty use Printer instead) | [optional] [default to null]
**comment** | string | Text describing the printer | [optional] [default to null]
**color** | flag | True if printer is capable of printing color, otherwise false | [optional] [default to null]
**color_default** | flag | Default color setting for jobs, sent to this printer | [optional] [default to null]
**duplex** | flag | True if printer is capable of printin in duplex mode, otherwise false | [optional] [default to null]
**duplex_default** | string | Default duplex setting for jobs, sent to this printer | [optional] [default to null]
**trays** | /blck/api_string_tt | Paper format loaded in each of the printer&#x27;s input trays | [optional] [default to null]
**tray_media** | /blck/api_string_tt | Media type loaded in each of the printer&#x27;s input trays | [optional] [default to null]

