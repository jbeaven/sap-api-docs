# API: DefaultApi
## &nbsp; &nbsp; [Operation: tickets_json_post](#markdown-header-op-DefaultApi-tickets_json_post)
# Models and Enumerations
## &nbsp; &nbsp; [Model: Ticket](#markdown-header-model-ticket) (type `/blck/zd_ticket`)
## &nbsp; &nbsp; [Model: TicketResponse](#markdown-header-model-ticketresponse) (type `/blck/zd_ticketresponse`)

# API: DefaultApi

All URIs are relative to *http://{host}.zendesk.com/api/v2/*

<a name="markdown-header-op-DefaultApi-tickets_json_post"></a>

## operation: **tickets_json_post**
createTicket

Create Ticket


### Example
```abap
*** method DefaultApi->tickets_json_post example
*** createTicket

  constants:
    gcc_basepath type string value 'http://{host}.zendesk.com/api/v2/'.
    
  data:  
    gvi_code type /blck/zd_int,
    gvs_msg  type /blck/zd_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a simple ABAP primitive of type /BLCK/ZD_STRING
    data gvs_body type /BLCK/ZD_STRING.
        
*** set data according to requirements of the API call
*   gvs_body = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/zd_cl_DefaultApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method tickets_json_post via HTTP POST
*** i_body: Ticket
    /blck/zd_cl_DefaultApi=>tickets_json_post(
      exporting
        i_body = gvs_body
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
 **i_body** | `/BLCK/ZD_STRING` | Ticket 

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: Not defined


* * *
<a name="markdown-header-model-ticket"></a> 

# Model: Ticket



### Example
```abap
*** model ticket example

* create our variables..
    data gr_ticket type /blck/zd_ticket.
    
* fill model with data as appropriate..
    gr_ticket-ticket = l_ticket. " (type /BLCK/ZD_STRING_MT)
    
* pass to example API method
    /blck/cl_example_api=>update_ticket(
      exporting
        i_ticket = gr_ticket ).
    		
    clear gr_ticket.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_ticket(
      exporting
        i_id = 1
      importing 
        e_200 = gr_ticket ).
    		
    write: gr_ticket-ticket. " (type /BLCK/ZD_STRING_MT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**ticket** | `/BLCK/ZD_STRING_MT` | 

* * *
<a name="markdown-header-model-ticketresponse"></a> 

# Model: TicketResponse



### Example
```abap
*** model ticketresponse example

* create our variables..
    data gr_ticketresponse type /blck/zd_ticketresponse.
    
* fill model with data as appropriate..
    gr_ticketresponse-id = 42. " (type /BLCK/ZD_INT)
    
* pass to example API method
    /blck/cl_example_api=>update_ticketresponse(
      exporting
        i_ticketresponse = gr_ticketresponse ).
    		
    clear gr_ticketresponse.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_ticketresponse(
      exporting
        i_id = 1
      importing 
        e_200 = gr_ticketresponse ).
    		
    write: gr_ticketresponse-id. " (type /BLCK/ZD_INT)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**id** | `/BLCK/ZD_INT` | 

