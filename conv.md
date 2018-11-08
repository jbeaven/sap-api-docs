# API: ControlApi

All URIs are relative to *http://localhost:3015/v1*

## operation: **jobs_job_id_delete**
Delete a job

Deletes a job. In case the job is in status processing, it is aborted before removing the data. 


### Example
```abap
*** method ControlApi->jobs_job_id_delete example
*** Delete a job

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_ControlApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_delete via HTTP DELETE
*** i_job_id: Id of a previously created job
    /blck/cnv_cl_ControlApi=>jobs_job_id_delete(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_start_post**
Start processing.

Start processing of a job. If processing is already triggered nothing is done. Job status can be polled via `/jobs/{jobId}/status` route. 


### Example
```abap
*** method ControlApi->jobs_job_id_start_post example
*** Start processing.

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_ControlApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_start_post via HTTP POST
*** i_job_id: Id of a previously created job
    /blck/cnv_cl_ControlApi=>jobs_job_id_start_post(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_status_get**
Get job status information

Get a object with job status and output information 


### Example
```abap
*** method ControlApi->jobs_job_id_status_get example
*** Get job status information

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/CNV_JOB_STATUS
    data gr_http200 type /BLCK/CNV_JOB_STATUS.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_ControlApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_status_get via HTTP GET
*** i_job_id: Id of a previously created job
    /blck/cnv_cl_ControlApi=>jobs_job_id_status_get(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/CNV_JOB_STATUS)
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/CNV_JOB_STATUS (**[JobStatus](#markdown-header-model-)**) | OK, job status information returned
 401 | **e_401** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 404 | **e_404** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_jobid_process_post**
Conversion fast lane

Easy way to convert with a single REST call: - Creates a single input file with default vaules in previously created (empty) job - Uploads the request body as content - Starts processing and wait for output result. - Returns output result as response. If more than one output result was created, the first output result with file id 0 (zero) is returned. - Auto deletes job after sending response successfully 


### Example
```abap
*** method ControlApi->jobs_jobid_process_post example
*** Conversion fast lane

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_jobid:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_jobid type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_jobid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_ControlApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_jobid_process_post via HTTP POST
*** i_jobid: Id of a previously created job
    /blck/cnv_cl_ControlApi=>jobs_jobid_process_post(
      exporting
        i_jobid = gvs_jobid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_jobid** | /BLCK/CNV_STRING | Id of a previously created job 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octed-stream, application/json


# API: JobsApi

All URIs are relative to *http://localhost:3015/v1*

## operation: **jobs_job_id_get**
Get full job information

Get a object with full job status, input and output information. 


### Example
```abap
*** method JobsApi->jobs_job_id_get example
*** Get full job information

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/CNV_JOB_DATA
    data gr_http200 type /BLCK/CNV_JOB_DATA.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_get via HTTP GET
*** i_job_id: Id of a previously created job
    /blck/cnv_cl_JobsApi=>jobs_job_id_get(
      exporting
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/CNV_JOB_DATA)
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/CNV_JOB_DATA (**[JobData](#markdown-header-model-)**) | OK, job status information returned
 401 | **e_401** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 404 | **e_404** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Not found
 500 | **e_500** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


## operation: **jobs_job_id_input_post**
Append a new input file to a job.

Appends a new input file to the input file list of a job.


### Example
```abap
*** method JobsApi->jobs_job_id_input_post example
*** Append a new input file to a job.

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/CNV_INPUT_FILE
    data gm_body type /BLCK/CNV_INPUT_FILE.

*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP200 we expect type /BLCK/CNV_STRING
    data gr_http200 type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-mime_type = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_job_id_input_post via HTTP POST
*** i_body: File ticket for preprocessing. 
*** i_job_id: Id of a previously created job
    /blck/cnv_cl_JobsApi=>jobs_job_id_input_post(
      exporting
        i_body = gm_body
        i_job_id = gvs_job_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/CNV_STRING)
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/CNV_INPUT_FILE (**[input_file](#markdown-header-model-input_file)**) | File ticket for preprocessing.  
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/CNV_STRING | OK, entry created. Returns fileId as index of created file in input file list, starting with zero.
 401 | **e_401** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 409 | **e_409** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobs_jobid_process_post**
Conversion fast lane

Easy way to convert with a single REST call: - Creates a single input file with default vaules in previously created (empty) job - Uploads the request body as content - Starts processing and wait for output result. - Returns output result as response. If more than one output result was created, the first output result with file id 0 (zero) is returned. - Auto deletes job after sending response successfully 


### Example
```abap
*** method JobsApi->jobs_jobid_process_post example
*** Conversion fast lane

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_jobid:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_jobid type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_jobid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_jobid_process_post via HTTP POST
*** i_jobid: Id of a previously created job
    /blck/cnv_cl_JobsApi=>jobs_jobid_process_post(
      exporting
        i_jobid = gvs_jobid
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_jobid** | /BLCK/CNV_STRING | Id of a previously created job 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octed-stream, application/json


## operation: **jobs_post**
Create a new job.


### Example
```abap
*** method JobsApi->jobs_post example
*** Create a new job.

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/CNV_JOB_TICKET
    data gm_body type /BLCK/CNV_JOB_TICKET.
*   when the the result of the call is HTTP200 we expect type /BLCK/CNV_STRING
    data gr_http200 type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobs_post via HTTP POST
*** i_body: Job ticket for preprocessing. 
    /blck/cnv_cl_JobsApi=>jobs_post(
      exporting
        i_body = gm_body
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_200 = gr_http200
        e_401 = gr_http401
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       do something with gr_http200 (type /BLCK/CNV_STRING)
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | /BLCK/CNV_JOB_TICKET (**[job_ticket](#markdown-header-model-job_ticket)**) | Job ticket for preprocessing.  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_200** | /BLCK/CNV_STRING | OK, entry created. Returns a job id.
 401 | **e_401** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unauthorized (Auth token invalid)
 409 | **e_409** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_500** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Application Error
 0 | **e_0** | /BLCK/CNV_ERROR (**[Error](#markdown-header-model-)**) | Unexpected error

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


## operation: **jobsjobidinputfileidcontentpos**
Upload input file binary input content.

Upload input file binary input content.


### Example
```abap
*** method JobsApi->jobsjobidinputfileidcontentpos example
*** Upload input file binary input content.

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.

*   for parameter i_file_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_file_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.
*   gvs_file_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobsjobidinputfileidcontentpos via HTTP POST
*** i_job_id: Id of a previously created job
*** i_file_id: Id (index) of a previously created input file
    /blck/cnv_cl_JobsApi=>jobsjobidinputfileidcontentpos(
      exporting
        i_job_id = gvs_job_id
        i_file_id = gvs_file_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_409 = gr_http409
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 
 **i_file_id** | /BLCK/CNV_STRING | Id (index) of a previously created input file 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octed-stream, application/json


## operation: **jobsjobidoutputfileidcontentge**
Get processing result content.

Get processing result binary content. 


### Example
```abap
*** method JobsApi->jobsjobidoutputfileidcontentge example
*** Get processing result content.

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.

*   for parameter i_file_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_file_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.
*   gvs_file_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_JobsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobsjobidoutputfileidcontentge via HTTP GET
*** i_job_id: Id of a previously created job
*** i_file_id: Id (index) of the file in the output file list
    /blck/cnv_cl_JobsApi=>jobsjobidoutputfileidcontentge(
      exporting
        i_job_id = gvs_job_id
        i_file_id = gvs_file_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 
 **i_file_id** | /BLCK/CNV_STRING | Id (index) of the file in the output file list 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octed-stream, application/json


# API: ResultsApi

All URIs are relative to *http://localhost:3015/v1*

## operation: **jobsjobidoutputfileidcontentge**
Get processing result content.

Get processing result binary content. 


### Example
```abap
*** method ResultsApi->jobsjobidoutputfileidcontentge example
*** Get processing result content.

  constants:
    gcc_basepath type string value 'http://localhost:3015/v1'.
    
  data:  
    gcl_auth type ref to /blck/api_cl_auth,
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.

*   for parameter i_file_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_file_id type /BLCK/CNV_STRING.
*   when the the result of the call is HTTP401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the the result of the call is HTTP0 we expect type /BLCK/CNV_ERROR
    data gr_http0 type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.
*   gvs_file_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/api_cl_auth and assign to 
*   gcl_auth if bespoke auth is needed
*   gcl_auth = lcl_my_auth.
    
*** update the configuration if needed, a default basepath is set from the spec
    /blck/cnv_cl_ResultsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method jobsjobidoutputfileidcontentge via HTTP GET
*** i_job_id: Id of a previously created job
*** i_file_id: Id (index) of the file in the output file list
    /blck/cnv_cl_ResultsApi=>jobsjobidoutputfileidcontentge(
      exporting
        i_job_id = gvs_job_id
        i_file_id = gvs_file_id
      importing
        e_code = gvi_code
        e_message = gvs_msg
        e_401 = gr_http401
        e_404 = gr_http404
        e_500 = gr_http500
        e_0 = gr_http0 ).

*** do something with the result if applicable..
    case gvi_code.
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when 0.
*       do something with gr_http0 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | /BLCK/CNV_STRING | Id of a previously created job 
 **i_file_id** | /BLCK/CNV_STRING | Id (index) of the file in the output file list 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octed-stream, application/json


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
<a name="markdown-header-model-file_id"></a> 

# Model: file_id



### Example
```abap
*** model file_id example
*** Id (index) of file in file list

* create our variables..
    data gcl_file_id type ref to /blck/mdl_cl_file_id.
    
* instantiate model and call the setters to set values..
    gcl_file_id = /blck/mdl_cl_file_id=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_file_id(
    	exporting
    		i_file_id = gcl_file_id ).
    		
    clear gcl_file_id.
    
* fetch new instance from example API method
    gcl_file_id = gcl_exampleapi->get_file_id(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-model-input_file"></a> 

# Model: input_file



### Example
```abap
*** model input_file example
*** Description of a single file

* create our variables..
    data gcl_input_file type ref to /blck/mdl_cl_input_file.
    
* instantiate model and call the setters to set values..
    gcl_input_file = /blck/mdl_cl_input_file=>create( ).
    gcl_input_file->set_mime_type( 'ipsum lorem' ). " (type string)
    gcl_input_file->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_input_file(
    	exporting
    		i_input_file = gcl_input_file ).
    		
    clear gcl_input_file.
    
* fetch new instance from example API method
    gcl_input_file = gcl_exampleapi->get_input_file(
    	exporting
    		i_id = 1 ).
    		
    l_mime_type = gcl_input_file->get_mime_type( ). " (type string)
    l_metadata = gcl_input_file->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**mime_type** | string | Mime type of the file. | [optional] [default to null]
**metadata** | string | File specific parameter, will be merged with job metadata at runtime. | [optional] [default to null]

* * *
<a name="markdown-header-model-job_id"></a> 

# Model: job_id



### Example
```abap
*** model job_id example
*** Id of created preprocessing job for later use.

* create our variables..
    data gcl_job_id type ref to /blck/mdl_cl_job_id.
    
* instantiate model and call the setters to set values..
    gcl_job_id = /blck/mdl_cl_job_id=>create( ).
    
* pass to example API method
    gcl_exampleapi->update_job_id(
    	exporting
    		i_job_id = gcl_job_id ).
    		
    clear gcl_job_id.
    
* fetch new instance from example API method
    gcl_job_id = gcl_exampleapi->get_job_id(
    	exporting
    		i_id = 1 ).
    		

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------

* * *
<a name="markdown-header-enum-jobstatusenum"></a> 

# Enum: jobstatusenum



### Example
```abap
*** model jobstatusenum example
*** Definition of allowed status names

* create our variables..
    data gcl_jobstatusenum type ref to /blck/mdl_cl_jobstatusenum.
    
* instantiate model relevant to the enum value we want
    gcl_jobstatusenum = /blck/mdl_cl_jobstatusenum=>enum_open( ).
    
* pass the enum to the example API via method
    gcl_exampleapi->set_jobstatusenum_state(
    	exporting
    		i_jobstatusenum = gcl_jobstatusenum ).
    		
    clear gcl_jobstatusenum.
    
* fetch result from example API method
    gcl_jobstatusenum = gcl_exampleapi->get_jobstatusenum_state(
    	exporting
    		i_id = 1 ).
    	
* we have two ways to handle the result, either "if" with individual cases..
  if gcl_jobstatusenum->is_open( ) eq 'X'.
*   do something specific to open case..
  endif.
  
* .. or use a case clause to handle all scenarios:
  case gcl_jobstatusenum->get_value( ).
    when /blck/mdl_cl_jobstatusenum=>mce_open.
*     do something specific to open case..
    when /blck/mdl_cl_jobstatusenum=>mce_waiting.
*     do something specific to waiting case..
    when /blck/mdl_cl_jobstatusenum=>mce_processing.
*     do something specific to processing case..
    when /blck/mdl_cl_jobstatusenum=>mce_completed.
*     do something specific to completed case..
    when /blck/mdl_cl_jobstatusenum=>mce_error.
*     do something specific to error case..
  endcase.


```

## Enum Values

Name | Value | Instantiation
------------ | ------------- | -------------
**open** | open | /blck/mdl_cl_jobstatusenum=>enum_open( ).
**waiting** | waiting | /blck/mdl_cl_jobstatusenum=>enum_waiting( ).
**processing** | processing | /blck/mdl_cl_jobstatusenum=>enum_processing( ).
**completed** | completed | /blck/mdl_cl_jobstatusenum=>enum_completed( ).
**error** | error | /blck/mdl_cl_jobstatusenum=>enum_error( ).

* * *
<a name="markdown-header-model-job_ticket"></a> 

# Model: job_ticket



### Example
```abap
*** model job_ticket example
*** A  JSON object containing the name of the rule to execute for a job and it&#x27;s
*** paramters.

* create our variables..
    data gcl_job_ticket type ref to /blck/mdl_cl_job_ticket.
    
* instantiate model and call the setters to set values..
    gcl_job_ticket = /blck/mdl_cl_job_ticket=>create( ).
    gcl_job_ticket->set_name( 'ipsum lorem' ). " (type string)
    gcl_job_ticket->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_job_ticket(
    	exporting
    		i_job_ticket = gcl_job_ticket ).
    		
    clear gcl_job_ticket.
    
* fetch new instance from example API method
    gcl_job_ticket = gcl_exampleapi->get_job_ticket(
    	exporting
    		i_id = 1 ).
    		
    l_name = gcl_job_ticket->get_name( ). " (type string)
    l_metadata = gcl_job_ticket->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | string | Name of preprocessing rule to use | [optional] [default to null]
**metadata** | string | Rule specific parameter. | [optional] [default to null]

* * *
<a name="markdown-header-model-output_file"></a> 

# Model: output_file



### Example
```abap
*** model output_file example
*** All available data for a single output file

* create our variables..
    data gcl_output_file type ref to /blck/mdl_cl_output_file.
    
* instantiate model and call the setters to set values..
    gcl_output_file = /blck/mdl_cl_output_file=>create( ).
    gcl_output_file->set_mime_type( 'ipsum lorem' ). " (type string)
    gcl_output_file->set_metadata( 'ipsum lorem' ). " (type string)
    
* pass to example API method
    gcl_exampleapi->update_output_file(
    	exporting
    		i_output_file = gcl_output_file ).
    		
    clear gcl_output_file.
    
* fetch new instance from example API method
    gcl_output_file = gcl_exampleapi->get_output_file(
    	exporting
    		i_id = 1 ).
    		
    l_mime_type = gcl_output_file->get_mime_type( ). " (type string)
    l_metadata = gcl_output_file->get_metadata( ). " (type string)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**mime_type** | string | Mime type of the file. | [optional] [default to null]
**metadata** | string | Output file specific parameter. Result of merged job metadata, input file metadata and rule target metadata.  | [optional] [default to null]

* * *
<a name="markdown-header-model-job_data"></a> 

# Model: job_data



### Example
```abap
*** model job_data example
*** All available data for a single job

* create our variables..
    data gcl_job_data type ref to /blck/mdl_cl_job_data.
    
* instantiate model and call the setters to set values..
    gcl_job_data = /blck/mdl_cl_job_data=>create( ).
    gcl_job_data->set_job_id( l_job_id ). " (type /BLCK/CNV_job_id)
    gcl_job_data->set_job_status( l_job_status ). " (type /BLCK/CNV_jobstatusenum)
    gcl_job_data->set_creation_date( 42 ). " (type i)
    gcl_job_data->set_job_ticket( l_job_ticket ). " (type /BLCK/CNV_job_ticket)
    gcl_job_data->set_input( l_input ). " (type /BLCK/CNV_input_file_tt)
    gcl_job_data->set_output( l_output ). " (type /BLCK/CNV_output_file_tt)
    
* pass to example API method
    gcl_exampleapi->update_job_data(
    	exporting
    		i_job_data = gcl_job_data ).
    		
    clear gcl_job_data.
    
* fetch new instance from example API method
    gcl_job_data = gcl_exampleapi->get_job_data(
    	exporting
    		i_id = 1 ).
    		
    l_job_id = gcl_job_data->get_job_id( ). " (type /BLCK/CNV_job_id)
    l_job_status = gcl_job_data->get_job_status( ). " (type /BLCK/CNV_jobstatusenum)
    l_creation_date = gcl_job_data->get_creation_date( ). " (type i)
    l_job_ticket = gcl_job_data->get_job_ticket( ). " (type /BLCK/CNV_job_ticket)
    l_input = gcl_job_data->get_input( ). " (type /BLCK/CNV_input_file_tt)
    l_output = gcl_job_data->get_output( ). " (type /BLCK/CNV_output_file_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**job_id** | /BLCK/CNV_job_id (**[job_id](#markdown-header-model-job_id)**) |  | [optional] [default to null]
**job_status** | /BLCK/CNV_jobstatusenum (**[jobstatusenum](#markdown-header-enum-jobstatusenum)**) |  | [optional] [default to null]
**creation_date** | i | Time stamp of creation date | [optional] [default to null]
**job_ticket** | /BLCK/CNV_job_ticket (**[job_ticket](#markdown-header-model-job_ticket)**) |  | [optional] [default to null]
**input** | /BLCK/CNV_input_file_tt (**[array of input_file](#markdown-header-model-input_file)**) | input file list | [optional] [default to null]
**output** | /BLCK/CNV_output_file_tt (**[array of output_file](#markdown-header-model-output_file)**) | generated output file list | [optional] [default to null]

* * *
<a name="markdown-header-model-job_status"></a> 

# Model: job_status



### Example
```abap
*** model job_status example
*** Entry for job list

* create our variables..
    data gcl_job_status type ref to /blck/mdl_cl_job_status.
    
* instantiate model and call the setters to set values..
    gcl_job_status = /blck/mdl_cl_job_status=>create( ).
    gcl_job_status->set_job_id( l_job_id ). " (type /BLCK/CNV_job_id)
    gcl_job_status->set_job_status( l_job_status ). " (type /BLCK/CNV_jobstatusenum)
    gcl_job_status->set_output( l_output ). " (type /BLCK/CNV_output_file_tt)
    
* pass to example API method
    gcl_exampleapi->update_job_status(
    	exporting
    		i_job_status = gcl_job_status ).
    		
    clear gcl_job_status.
    
* fetch new instance from example API method
    gcl_job_status = gcl_exampleapi->get_job_status(
    	exporting
    		i_id = 1 ).
    		
    l_job_id = gcl_job_status->get_job_id( ). " (type /BLCK/CNV_job_id)
    l_job_status = gcl_job_status->get_job_status( ). " (type /BLCK/CNV_jobstatusenum)
    l_output = gcl_job_status->get_output( ). " (type /BLCK/CNV_output_file_tt)

```

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**job_id** | /BLCK/CNV_job_id (**[job_id](#markdown-header-model-job_id)**) |  | [optional] [default to null]
**job_status** | /BLCK/CNV_jobstatusenum (**[jobstatusenum](#markdown-header-enum-jobstatusenum)**) |  | [optional] [default to null]
**output** | /BLCK/CNV_output_file_tt (**[array of output_file](#markdown-header-model-output_file)**) | generated output file list | [optional] [default to null]

