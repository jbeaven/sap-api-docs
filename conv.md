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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 201.
*       handle code 201, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 201.
*       handle code 201, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/CNV_JOB_STATUS
    data gr_http200 type /BLCK/CNV_JOB_STATUS.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/CNV_JOB_STATUS` (**[JobStatus](#markdown-header-model-job_status)**) | OK, job status information returned
 401 | **e_code_401** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 404 | **e_code_404** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Not found
 500 | **e_code_500** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_jobid:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_jobid type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_jobid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_jobid** | `/BLCK/CNV_STRING` | Id of a previously created job 

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/CNV_JOB_DATA
    data gr_http200 type /BLCK/CNV_JOB_DATA.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/CNV_JOB_DATA` (**[JobData](#markdown-header-model-job_data)**) | OK, job status information returned
 401 | **e_code_401** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 404 | **e_code_404** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Not found
 500 | **e_code_500** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/CNV_INPUT_FILE
    data gm_body type /BLCK/CNV_INPUT_FILE.
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/CNV_STRING
    data gr_http200 type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-mime_type = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
*   gvs_job_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | `/BLCK/CNV_INPUT_FILE` (**[InputFile](#markdown-header-model-input_file)**) | File ticket for preprocessing.  
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/CNV_STRING` | OK, entry created. Returns fileId as index of created file in input file list, starting with zero.
 401 | **e_code_401** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 409 | **e_code_409** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_code_500** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_jobid:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_jobid type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_jobid = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_jobid** | `/BLCK/CNV_STRING` | Id of a previously created job 

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/CNV_JOB_TICKET
    data gm_body type /BLCK/CNV_JOB_TICKET.
*   when the result of the call is HTTP Code: 200 we expect type /BLCK/CNV_STRING
    data gr_http200 type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gm_body-name = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
*   gm_body-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_200 = gr_http200
        e_code_401 = gr_http401
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

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
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_body** | `/BLCK/CNV_JOB_TICKET` (**[JobTicket](#markdown-header-model-job_ticket)**) | Job ticket for preprocessing.  

### Return types

HTTP Code | Name | Type | Description  
------------- | ------------- | ------------- | ------------- 
 200 | **e_code_200** | `/BLCK/CNV_STRING` | OK, entry created. Returns a job id.
 401 | **e_code_401** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unauthorized (Auth token invalid)
 409 | **e_code_409** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Conflict, ressource could not be created. See error message for details. 
 500 | **e_code_500** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Application Error
 other | **e_code_other** | `/BLCK/CNV_ERROR` (**[Error](#markdown-header-model-error)**) | Unexpected error

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   for parameter i_file_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_file_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 409 we expect type /BLCK/CNV_ERROR
    data gr_http409 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.
*   gvs_file_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_409 = gr_http409
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 201.
*       handle code 201, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 409.
*       do something with gr_http409 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 
 **i_file_id** | `/BLCK/CNV_STRING` | Id (index) of a previously created input file 

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   for parameter i_file_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_file_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.
*   gvs_file_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 
 **i_file_id** | `/BLCK/CNV_STRING` | Id (index) of the file in the output file list 

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
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/cnv_cl_auth
    gvi_code type /blck/cnv_int,
    gvs_msg  type /blck/cnv_string.
    
*** create variables for input and output as needed
*   for parameter i_job_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_job_id type /BLCK/CNV_STRING.
*   for parameter i_file_id:
*   a simple ABAP primitive of type /BLCK/CNV_STRING
    data gvs_file_id type /BLCK/CNV_STRING.
*   when the result of the call is HTTP Code: 401 we expect type /BLCK/CNV_ERROR
    data gr_http401 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 404 we expect type /BLCK/CNV_ERROR
    data gr_http404 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: 500 we expect type /BLCK/CNV_ERROR
    data gr_http500 type /BLCK/CNV_ERROR.
*   when the result of the call is HTTP Code: other we expect type /BLCK/CNV_ERROR
    data gr_httpother type /BLCK/CNV_ERROR.
        
*** set data according to requirements of the API call
*   gvs_job_id = 'ipsum lorem'.
*   gvs_file_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/cnv_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
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
        e_code_401 = gr_http401
        e_code_404 = gr_http404
        e_code_500 = gr_http500
        e_code_other = gr_httpother ).

*** do something with the result if applicable..
    case gvi_code.
      when 200.
*       handle code 200, e_message => gvs_msg
      when 401.
*       do something with gr_http401 (type /BLCK/CNV_ERROR)
      when 404.
*       do something with gr_http404 (type /BLCK/CNV_ERROR)
      when 500.
*       do something with gr_http500 (type /BLCK/CNV_ERROR)
      when others.
* handle the general case..
*       do something with gr_httpother (type /BLCK/CNV_ERROR)
    endcase.

```

### Parameters
Name | Type | Description  
------------- | ------------- | ------------- 
 **i_job_id** | `/BLCK/CNV_STRING` | Id of a previously created job 
 **i_file_id** | `/BLCK/CNV_STRING` | Id (index) of the file in the output file list 

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/octed-stream, application/json


* * *
<a name="markdown-header-model-error"></a> 

# Model: Error



### Example
```abap
*** model error example

* create our variables..
    data gr_error type /blck/cnv_error.
    
* fill model with data as appropriate..
    gr_error-code = 42. " (type /BLCK/CNV_INT)
    gr_error-message = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    gr_error-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_error(
      exporting
        i_error = gr_error ).
    		
    clear gr_error.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_error(
      exporting
        i_id = 1
      importing 
        e_200 = gr_error ).
    		
    write: gr_error-code. " (type /BLCK/CNV_INT)
    write: gr_error-message. " (type /BLCK/CNV_STRING)
    write: gr_error-metadata. " (type /BLCK/CNV_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**code** | `/BLCK/CNV_INT` | 
**message** | `/BLCK/CNV_STRING` | 
**metadata** | `/BLCK/CNV_STRING` | 

* * *
<a name="markdown-header-model-file_id"></a> 

# Model: FileId



### Example
```abap
*** model file_id example
*** Id (index) of file in file list

* create our variables..
    data gr_file_id type /blck/cnv_file_id.
    
* fill model with data as appropriate..
    
* pass to example API method
    /blck/cl_example_api=>update_file_id(
      exporting
        i_file_id = gr_file_id ).
    		
    clear gr_file_id.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_file_id(
      exporting
        i_id = 1
      importing 
        e_200 = gr_file_id ).
    		

```

## Properties

Name | Type | Description
------------ | ------------- | -------------

* * *
<a name="markdown-header-model-input_file"></a> 

# Model: InputFile



### Example
```abap
*** model input_file example
*** Description of a single file

* create our variables..
    data gr_input_file type /blck/cnv_input_file.
    
* fill model with data as appropriate..
    gr_input_file-mime_type = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    gr_input_file-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_input_file(
      exporting
        i_input_file = gr_input_file ).
    		
    clear gr_input_file.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_input_file(
      exporting
        i_id = 1
      importing 
        e_200 = gr_input_file ).
    		
    write: gr_input_file-mime_type. " (type /BLCK/CNV_STRING)
    write: gr_input_file-metadata. " (type /BLCK/CNV_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**mime_type** | `/BLCK/CNV_STRING` | Mime type of the file.
**metadata** | `/BLCK/CNV_STRING` | File specific parameter, will be merged with job metadata at runtime.

* * *
<a name="markdown-header-model-job_id"></a> 

# Model: JobId



### Example
```abap
*** model job_id example
*** Id of created preprocessing job for later use.

* create our variables..
    data gr_job_id type /blck/cnv_job_id.
    
* fill model with data as appropriate..
    
* pass to example API method
    /blck/cl_example_api=>update_job_id(
      exporting
        i_job_id = gr_job_id ).
    		
    clear gr_job_id.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_job_id(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_id ).
    		

```

## Properties

Name | Type | Description
------------ | ------------- | -------------

* * *
<a name="markdown-header-enum-jobstatusenum"></a> 

# Enum: JobStatusEnum



### Example
```abap
*** model jobstatusenum example
*** Definition of allowed status names

* create our variables..
    data gv_jobstatusenum type /blck/cnv_jobstatusenum.
    
* set the enum value we want
    gv_jobstatusenum = /blck/cnv_const=>me_jobstatusenum-open.
    
* pass the enum value to the example API via method
    /blck/cl_example_api=>set_jobstatusenum_state(
      exporting
        i_jobstatusenum = gv_jobstatusenum ).
    		
    clear gv_jobstatusenum.
    
* fetch result from example API method
    /blck/cl_example_api=>get_jobstatusenum_state(
      exporting
        i_id = 1
      importing
        e_200 = gv_jobstatusenum ).
    	
* we can handle the result with either "if" with individual cases
* or use a case clause to handle all scenarios:
  case gv_jobstatusenum.
    when /blck/cnv_const=>me_jobstatusenum-open.
*     do something specific to open case..
    when /blck/cnv_const=>me_jobstatusenum-waiting.
*     do something specific to waiting case..
    when /blck/cnv_const=>me_jobstatusenum-processing.
*     do something specific to processing case..
    when /blck/cnv_const=>me_jobstatusenum-completed.
*     do something specific to completed case..
    when /blck/cnv_const=>me_jobstatusenum-error.
*     do something specific to error case..
  endcase.


```

## Enum Values

Name | Value | Constant
------------ | ------------- | -------------
**open** | open | `/blck/cnv_const=>me_jobstatusenum-open`
**waiting** | waiting | `/blck/cnv_const=>me_jobstatusenum-waiting`
**processing** | processing | `/blck/cnv_const=>me_jobstatusenum-processing`
**completed** | completed | `/blck/cnv_const=>me_jobstatusenum-completed`
**error** | error | `/blck/cnv_const=>me_jobstatusenum-error`

* * *
<a name="markdown-header-model-job_ticket"></a> 

# Model: JobTicket



### Example
```abap
*** model job_ticket example
*** A  JSON object containing the name of the rule to execute for a job and it&#x27;s
*** paramters.

* create our variables..
    data gr_job_ticket type /blck/cnv_job_ticket.
    
* fill model with data as appropriate..
    gr_job_ticket-name = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    gr_job_ticket-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_job_ticket(
      exporting
        i_job_ticket = gr_job_ticket ).
    		
    clear gr_job_ticket.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_job_ticket(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_ticket ).
    		
    write: gr_job_ticket-name. " (type /BLCK/CNV_STRING)
    write: gr_job_ticket-metadata. " (type /BLCK/CNV_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**name** | `/BLCK/CNV_STRING` | Name of preprocessing rule to use
**metadata** | `/BLCK/CNV_STRING` | Rule specific parameter.

* * *
<a name="markdown-header-model-output_file"></a> 

# Model: OutputFile



### Example
```abap
*** model output_file example
*** All available data for a single output file

* create our variables..
    data gr_output_file type /blck/cnv_output_file.
    
* fill model with data as appropriate..
    gr_output_file-mime_type = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    gr_output_file-metadata = 'ipsum lorem'. " (type /BLCK/CNV_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_output_file(
      exporting
        i_output_file = gr_output_file ).
    		
    clear gr_output_file.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_output_file(
      exporting
        i_id = 1
      importing 
        e_200 = gr_output_file ).
    		
    write: gr_output_file-mime_type. " (type /BLCK/CNV_STRING)
    write: gr_output_file-metadata. " (type /BLCK/CNV_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**mime_type** | `/BLCK/CNV_STRING` | Mime type of the file.
**metadata** | `/BLCK/CNV_STRING` | Output file specific parameter. Result of merged job metadata, input file metadata and rule target metadata. 

* * *
<a name="markdown-header-model-job_data"></a> 

# Model: JobData



### Example
```abap
*** model job_data example
*** All available data for a single job

* create our variables..
    data gr_job_data type /blck/cnv_job_data.
    
* fill model with data as appropriate..
    gr_job_data-job_id = l_job_id. " (type /BLCK/CNV_JOB_ID)
    gr_job_data-job_status = /blck/cnv_const=>me_jobstatusenum-open. " (enum /BLCK/CNV_JOBSTATUSENUM)
    gr_job_data-creation_date = 42. " (type /BLCK/CNV_INT)
    gr_job_data-job_ticket = l_job_ticket. " (type /BLCK/CNV_JOB_TICKET)
    gr_job_data-input = l_input. " (type /BLCK/CNV_INPUT_FILE_TT)
    gr_job_data-output = l_output. " (type /BLCK/CNV_OUTPUT_FILE_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_job_data(
      exporting
        i_job_data = gr_job_data ).
    		
    clear gr_job_data.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_job_data(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_data ).
    		
    write: gr_job_data-job_id. " (type /BLCK/CNV_JOB_ID)
    write: gr_job_data-job_status. " (type /BLCK/CNV_JOBSTATUSENUM)
    write: gr_job_data-creation_date. " (type /BLCK/CNV_INT)
    write: gr_job_data-job_ticket. " (type /BLCK/CNV_JOB_TICKET)
    write: gr_job_data-input. " (type /BLCK/CNV_INPUT_FILE_TT)
    write: gr_job_data-output. " (type /BLCK/CNV_OUTPUT_FILE_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**job_id** | `/BLCK/CNV_JOB_ID` (**[JobId](#markdown-header-model-job_id)**) | 
**job_status** | `/BLCK/CNV_JOBSTATUSENUM` (**[JobStatusEnum](#markdown-header-enum-jobstatusenum)**) | 
**creation_date** | `/BLCK/CNV_INT` | Time stamp of creation date
**job_ticket** | `/BLCK/CNV_JOB_TICKET` (**[JobTicket](#markdown-header-model-job_ticket)**) | 
**input** | `/BLCK/CNV_INPUT_FILE_TT` (**[array of InputFile](#markdown-header-model-input_file)**) | input file list
**output** | `/BLCK/CNV_OUTPUT_FILE_TT` (**[array of OutputFile](#markdown-header-model-output_file)**) | generated output file list

* * *
<a name="markdown-header-model-job_status"></a> 

# Model: JobStatus



### Example
```abap
*** model job_status example
*** Entry for job list

* create our variables..
    data gr_job_status type /blck/cnv_job_status.
    
* fill model with data as appropriate..
    gr_job_status-job_id = l_job_id. " (type /BLCK/CNV_JOB_ID)
    gr_job_status-job_status = /blck/cnv_const=>me_jobstatusenum-open. " (enum /BLCK/CNV_JOBSTATUSENUM)
    gr_job_status-output = l_output. " (type /BLCK/CNV_OUTPUT_FILE_TT)
    
* pass to example API method
    /blck/cl_example_api=>update_job_status(
      exporting
        i_job_status = gr_job_status ).
    		
    clear gr_job_status.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_job_status(
      exporting
        i_id = 1
      importing 
        e_200 = gr_job_status ).
    		
    write: gr_job_status-job_id. " (type /BLCK/CNV_JOB_ID)
    write: gr_job_status-job_status. " (type /BLCK/CNV_JOBSTATUSENUM)
    write: gr_job_status-output. " (type /BLCK/CNV_OUTPUT_FILE_TT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**job_id** | `/BLCK/CNV_JOB_ID` (**[JobId](#markdown-header-model-job_id)**) | 
**job_status** | `/BLCK/CNV_JOBSTATUSENUM` (**[JobStatusEnum](#markdown-header-enum-jobstatusenum)**) | 
**output** | `/BLCK/CNV_OUTPUT_FILE_TT` (**[array of OutputFile](#markdown-header-model-output_file)**) | generated output file list

