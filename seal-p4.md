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
    
*** create variables for input and output as needed
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P4_JOBSTATUSEVENT
    data gr_http200 type /BLCK/P4_JOBSTATUSEVENT.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        


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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P4_JOBSTATUSEVENT (**[JobStatusEvent](#markdown-header-model-jobstatusevent)**) | OK, job status is returned
 401 | **e_code_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 403 | **e_code_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Forbidden. The user lacks acces rights. 
 500 | **e_code_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P4_JOB_ID
    data gr_http200 type /BLCK/P4_JOB_ID.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        
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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/P4_STRING | job header data of the entry to be created 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P4_JOB_ID (**[JobId](#markdown-header-model-job_id)**) | OK, job ID is returned.
 401 | **e_code_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 403 | **e_code_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Forbidden. The user lacks acces rights to access the service list. 
 409 | **e_code_409** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_code_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

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
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        
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
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
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
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P4_JOB_STATUS
    data gr_http200 type /BLCK/P4_JOB_STATUS.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/P4_ERROR
    data gr_http404 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        
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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_uuid** | /BLCK/P4_STRING | ID of the current job. 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P4_JOB_STATUS (**[JobStatus](#markdown-header-model-job_status)**) | OK, job status is returned
 401 | **e_code_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 403 | **e_code_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Forbidden. The user lacks acces rights to access the service metadata. 
 404 | **e_code_404** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | The requested Service was not found.
 500 | **e_code_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

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
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        
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
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
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
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        
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
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
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
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        
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
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
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
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/P4_ERROR
    data gr_http409 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        
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
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 204.
*       handle code 204, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/P4_ERROR)
      when 403.
*       do something with gr_http403 (type /BLCK/P4_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/P4_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/P4_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
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
    
*** create variables for input and output as needed
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/P4_PRINTER_TT
    data gr_http200 type /BLCK/P4_PRINTER_TT.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/P4_ERROR
    data gr_http401 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 403 we expect type /BLCK/P4_ERROR
    data gr_http403 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/P4_ERROR
    data gr_http500 type /BLCK/P4_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/P4_ERROR
    data gr_httpother type /BLCK/P4_ERROR.
        


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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_403 = gr_http403
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/P4_ERROR)
    endcase.

```

### Parameters
This end-point does not need any parameters.

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | /BLCK/P4_PRINTER_TT (**[array of Printer](#markdown-header-model-printer)**) | OK, array of printer objects is returned
 401 | **e_code_401** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 403 | **e_code_403** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Forbidden. The user lacks acces rights. 
 500 | **e_code_500** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | /BLCK/P4_ERROR (**[Error](#markdown-header-model-error)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


* * *
<a name="markdown-header-model-error"></a> 

# Model: Error



### Example
```abap
*** model error example

* create our variables..
    data gr_error type /blck/p4_error.
    
* fill model with data as appropriate..
    gr_error-code = 42. " (type /BLCK/P4_INT)
    gr_error-message = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    gr_error-metadata = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    
* pass to example API method
    gcl_exampleapi->update_error(
      exporting
        i_error = gr_error ).
    		
    clear gr_error.
    
* fetch new instance from example API method
    gcl_exampleapi->get_error(
      exporting
        i_id = 1
      importing 
        e_200 = gr_error ).
    		
    write: gr_error-code. " (type /BLCK/P4_INT)
    write: gr_error-message. " (type /BLCK/P4_STRING)
    write: gr_error-metadata. " (type /BLCK/P4_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**code** | /BLCK/P4_INT | 
**message** | /BLCK/P4_STRING | 
**metadata** | /BLCK/P4_STRING | 

* * *
<a name="markdown-header-model-job_header"></a> 

# Model: JobHeader



### Example
```abap
*** model job_header example
*** key value entries of a PLOSSYS 4 header

* create our variables..
    data gr_job_header type /blck/p4_job_header.
    
* fill model with data as appropriate..
    
* pass to example API method
    gcl_exampleapi->update_job_header(
      exporting
        i_job_header = gr_job_header ).
    		
    clear gr_job_header.
    
* fetch new instance from example API method
    gcl_exampleapi->get_job_header(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_header ).
    		

```

## Properties

Name | Type | Description
------------ | ------------- | -------------

* * *
<a name="markdown-header-model-job_id"></a> 

# Model: JobId



### Example
```abap
*** model job_id example
*** A JobId represents a PLOSSYS 4 job

* create our variables..
    data gr_job_id type /blck/p4_job_id.
    
* fill model with data as appropriate..
    gr_job_id-uuid = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    
* pass to example API method
    gcl_exampleapi->update_job_id(
      exporting
        i_job_id = gr_job_id ).
    		
    clear gr_job_id.
    
* fetch new instance from example API method
    gcl_exampleapi->get_job_id(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_id ).
    		
    write: gr_job_id-uuid. " (type /BLCK/P4_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**uuid** | /BLCK/P4_STRING | Identifier of the job

* * *
<a name="markdown-header-enum-status_type"></a> 

# Enum: StatusType



### Example
```abap
*** model status_type example
*** Definition of allowed status names

* create our variables..
    data gv_status_type type /blck/p4_status_type.
    
* set the enum value we want
    gv_status_type = /blck/p4_cl_model=>status_type-open.
    
* pass the enum to the example API via method
    gcl_exampleapi->set_status_type_state(
      exporting
        i_status_type = gv_status_type ).
    		
    clear gv_status_type.
    
* fetch result from example API method
    gcl_exampleapi->get_status_type_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_status_type ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_status_type.
    when /blck/p4_cl_model=>status_type-open.
*     do something specific to open case..
    when /blck/p4_cl_model=>status_type-processing.
*     do something specific to processing case..
    when /blck/p4_cl_model=>status_type-completed.
*     do something specific to completed case..
    when /blck/p4_cl_model=>status_type-paused.
*     do something specific to paused case..
    when /blck/p4_cl_model=>status_type-aborted.
*     do something specific to aborted case..
    when /blck/p4_cl_model=>status_type-failed.
*     do something specific to failed case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**open** | open | /blck/p4_cl_model=>status_type-open.
**processing** | processing | /blck/p4_cl_model=>status_type-processing.
**completed** | completed | /blck/p4_cl_model=>status_type-completed.
**paused** | paused | /blck/p4_cl_model=>status_type-paused.
**aborted** | aborted | /blck/p4_cl_model=>status_type-aborted.
**failed** | failed | /blck/p4_cl_model=>status_type-failed.

* * *
<a name="markdown-header-model-job_status"></a> 

# Model: JobStatus



### Example
```abap
*** model job_status example
*** The status of a job

* create our variables..
    data gr_job_status type /blck/p4_job_status.
    
* fill model with data as appropriate..
    gr_job_status-status = l_status. " (type /BLCK/P4_STATUS_TYPE)
    
* pass to example API method
    gcl_exampleapi->update_job_status(
      exporting
        i_job_status = gr_job_status ).
    		
    clear gr_job_status.
    
* fetch new instance from example API method
    gcl_exampleapi->get_job_status(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_status ).
    		
    write: gr_job_status-status. " (type /BLCK/P4_STATUS_TYPE)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**status** | /BLCK/P4_STATUS_TYPE (**[StatusType](#markdown-header-enum-status_type)**) | 

* * *
<a name="markdown-header-model-jobstatusevent"></a> 

# Model: JobStatusEvent



### Example
```abap
*** model jobstatusevent example
*** Status of a PLOSSYS 4 job

* create our variables..
    data gr_jobstatusevent type /blck/p4_jobstatusevent.
    
* fill model with data as appropriate..
    gr_jobstatusevent-type = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    gr_jobstatusevent-scope = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    gr_jobstatusevent-parameters = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    
* pass to example API method
    gcl_exampleapi->update_jobstatusevent(
      exporting
        i_jobstatusevent = gr_jobstatusevent ).
    		
    clear gr_jobstatusevent.
    
* fetch new instance from example API method
    gcl_exampleapi->get_jobstatusevent(
      exporting
        i_id = 1
      importing 
        e_200 = gr_jobstatusevent ).
    		
    write: gr_jobstatusevent-type. " (type /BLCK/P4_STRING)
    write: gr_jobstatusevent-scope. " (type /BLCK/P4_STRING)
    write: gr_jobstatusevent-parameters. " (type /BLCK/P4_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**type** | /BLCK/P4_STRING | name of event, possible values: &#x27;UPDATE_JOB&#x27; 
**scope** | /BLCK/P4_STRING | uuid of PLOSSYS 4 job
**parameters** | /BLCK/P4_STRING | key/value pairs with event specific parameters. E.g. for UPDATE_JOB: &#x27;status: completed&#x27; 

* * *
<a name="markdown-header-model-printer"></a> 

# Model: Printer



### Example
```abap
*** model printer example
*** Printer capabilities

* create our variables..
    data gr_printer type /blck/p4_printer.
    
* fill model with data as appropriate..
    gr_printer-printer = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    gr_printer-display_name = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    gr_printer-comment = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    gr_printer-color = 'X'. " (type /BLCK/P4_BOOL)
    gr_printer-color_default = 'X'. " (type /BLCK/P4_BOOL)
    gr_printer-duplex = 'X'. " (type /BLCK/P4_BOOL)
    gr_printer-duplex_default = 'ipsum lorem'. " (type /BLCK/P4_STRING)
    gr_printer-trays = l_trays. " (type /BLCK/P4_STRING_TT)
    gr_printer-tray_media = l_tray_media. " (type /BLCK/P4_STRING_TT)
    
* pass to example API method
    gcl_exampleapi->update_printer(
      exporting
        i_printer = gr_printer ).
    		
    clear gr_printer.
    
* fetch new instance from example API method
    gcl_exampleapi->get_printer(
      exporting
        i_id = 1
      importing 
        e_200 = gr_printer ).
    		
    write: gr_printer-printer. " (type /BLCK/P4_STRING)
    write: gr_printer-display_name. " (type /BLCK/P4_STRING)
    write: gr_printer-comment. " (type /BLCK/P4_STRING)
    write: gr_printer-color. " (type /BLCK/P4_BOOL)
    write: gr_printer-color_default. " (type /BLCK/P4_BOOL)
    write: gr_printer-duplex. " (type /BLCK/P4_BOOL)
    write: gr_printer-duplex_default. " (type /BLCK/P4_STRING)
    write: gr_printer-trays. " (type /BLCK/P4_STRING_TT)
    write: gr_printer-tray_media. " (type /BLCK/P4_STRING_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**printer** | /BLCK/P4_STRING | Printer name
**display_name** | /BLCK/P4_STRING | Name used for displaying the printer (if empty use Printer instead)
**comment** | /BLCK/P4_STRING | Text describing the printer
**color** | /BLCK/P4_BOOL | True if printer is capable of printing color, otherwise false
**color_default** | /BLCK/P4_BOOL | Default color setting for jobs, sent to this printer
**duplex** | /BLCK/P4_BOOL | True if printer is capable of printin in duplex mode, otherwise false
**duplex_default** | /BLCK/P4_STRING | Default duplex setting for jobs, sent to this printer
**trays** | /BLCK/P4_STRING_TT | Paper format loaded in each of the printer&#x27;s input trays
**tray_media** | /BLCK/P4_STRING_TT | Media type loaded in each of the printer&#x27;s input trays

