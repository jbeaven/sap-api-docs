# API: GroupsApi
## &nbsp; &nbsp; [Operation: groups_get](#markdown-header-op-GroupsApi-groups_get)
## &nbsp; &nbsp; [Operation: groupsattendeesbygroupkeyget](#markdown-header-op-GroupsApi-groupsattendeesbygroupkeyget)
## &nbsp; &nbsp; [Operation: groupshistoricalmeetingsbygrou](#markdown-header-op-GroupsApi-groupshistoricalmeetingsbygrou)
## &nbsp; &nbsp; [Operation: groupsorganizersbygroupkeyget](#markdown-header-op-GroupsApi-groupsorganizersbygroupkeyget)
## &nbsp; &nbsp; [Operation: groupsorganizersbygroupkeypost](#markdown-header-op-GroupsApi-groupsorganizersbygroupkeypost)
## &nbsp; &nbsp; [Operation: groupsupcomingmeetingsbygroupk](#markdown-header-op-GroupsApi-groupsupcomingmeetingsbygroupk)
# API: MeetingsApi
## &nbsp; &nbsp; [Operation: historical_meetings_get](#markdown-header-op-MeetingsApi-historical_meetings_get)
## &nbsp; &nbsp; [Operation: meetings_by_meeting_id_delete](#markdown-header-op-MeetingsApi-meetings_by_meeting_id_delete)
## &nbsp; &nbsp; [Operation: meetings_by_meeting_id_get](#markdown-header-op-MeetingsApi-meetings_by_meeting_id_get)
## &nbsp; &nbsp; [Operation: meetings_by_meeting_id_put](#markdown-header-op-MeetingsApi-meetings_by_meeting_id_put)
## &nbsp; &nbsp; [Operation: meetings_post](#markdown-header-op-MeetingsApi-meetings_post)
## &nbsp; &nbsp; [Operation: meetingsattendeesbymeetinginst](#markdown-header-op-MeetingsApi-meetingsattendeesbymeetinginst)
## &nbsp; &nbsp; [Operation: meetingsstartbymeetingidget](#markdown-header-op-MeetingsApi-meetingsstartbymeetingidget)
## &nbsp; &nbsp; [Operation: upcoming_meetings_get](#markdown-header-op-MeetingsApi-upcoming_meetings_get)
# API: OrganizersApi
## &nbsp; &nbsp; [Operation: organizers_delete](#markdown-header-op-OrganizersApi-organizers_delete)
## &nbsp; &nbsp; [Operation: organizers_get](#markdown-header-op-OrganizersApi-organizers_get)
## &nbsp; &nbsp; [Operation: organizers_post](#markdown-header-op-OrganizersApi-organizers_post)
## &nbsp; &nbsp; [Operation: organizersattendeesbyorganizer](#markdown-header-op-OrganizersApi-organizersattendeesbyorganizer)
## &nbsp; &nbsp; [Operation: organizersbyorganizerkeydelete](#markdown-header-op-OrganizersApi-organizersbyorganizerkeydelete)
## &nbsp; &nbsp; [Operation: organizersbyorganizerkeyget](#markdown-header-op-OrganizersApi-organizersbyorganizerkeyget)
## &nbsp; &nbsp; [Operation: organizersbyorganizerkeyput](#markdown-header-op-OrganizersApi-organizersbyorganizerkeyput)
## &nbsp; &nbsp; [Operation: organizershistoricalmeetingsby](#markdown-header-op-OrganizersApi-organizershistoricalmeetingsby)
# Models and Enumerations
## &nbsp; &nbsp; [Model: MeetingRequest](#markdown-header-model-meetingrequest) (type `/blck/g2m_meetingrequest`)
## &nbsp; &nbsp; [Model: OrganizerInGrouprequest](#markdown-header-model-organizeringro) (type `/blck/g2m_organizeringro`)
## &nbsp; &nbsp; [Model: OrganizerRequest](#markdown-header-model-organizerreque) (type `/blck/g2m_organizerreque`)

# API: GroupsApi

All URIs are relative to *https://api.getgo.com/G2M/rest*

<a name="markdown-header-op-GroupsApi-groups_get"></a>

## operation: **groups_get**
Groups

List all groups for an account. This API call is only available to users with the admin role.


### Example
```abap
*** method GroupsApi->groups_get example
*** Groups

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_GroupsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method groups_get via HTTP GET
    /blck/g2m_cl_GroupsApi=>groups_get(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-GroupsApi-groupsattendeesbygroupkeyget"></a>

## operation: **groupsattendeesbygroupkeyget**
Attendees by group

Returns all attendees for all meetings within specified date range held by organizers within the specified group. This API call is only available to users with the admin role. This API call can be used only for groups with maximum 50 organizers.


### Example
```abap
*** method GroupsApi->groupsattendeesbygroupkeyget example
*** Attendees by group

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_start_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_start_date type /BLCK/G2M_STRING.
*   for parameter i_end_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_end_date type /BLCK/G2M_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_groupkey:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_groupkey type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_start_date = 'ipsum lorem'.
*   gvs_end_date = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_groupkey = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_GroupsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method groupsattendeesbygroupkeyget via HTTP GET
    /blck/g2m_cl_GroupsApi=>groupsattendeesbygroupkeyget(
      exporting
        i_start_date = gvs_start_date
        i_end_date = gvs_end_date
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_groupkey = gvs_groupkey
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
 **i_start_date** | `/BLCK/G2M_STRING` |  
 **i_end_date** | `/BLCK/G2M_STRING` |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_groupkey** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-GroupsApi-groupshistoricalmeetingsbygrou"></a>

## operation: **groupshistoricalmeetingsbygrou**
Historical meetings by group

Get historical meetings for the specified group that started within the specified date/time range. This API call is only available to users with the admin role. This API call is restricted to groups with a maximum of 50 organizers. Remark: Meetings which are still ongoing at the time of the request are NOT contained in the result array.


### Example
```abap
*** method GroupsApi->groupshistoricalmeetingsbygrou example
*** Historical meetings by group

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_start_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_start_date type /BLCK/G2M_STRING.
*   for parameter i_end_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_end_date type /BLCK/G2M_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_groupkey:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_groupkey type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_start_date = 'ipsum lorem'.
*   gvs_end_date = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_groupkey = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_GroupsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method groupshistoricalmeetingsbygrou via HTTP GET
    /blck/g2m_cl_GroupsApi=>groupshistoricalmeetingsbygrou(
      exporting
        i_start_date = gvs_start_date
        i_end_date = gvs_end_date
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_groupkey = gvs_groupkey
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
 **i_start_date** | `/BLCK/G2M_STRING` |  
 **i_end_date** | `/BLCK/G2M_STRING` |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_groupkey** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-GroupsApi-groupsorganizersbygroupkeyget"></a>

## operation: **groupsorganizersbygroupkeyget**
Organizers by group

Returns all the organizers within a specific group. This API call is only available to users with the admin role.


### Example
```abap
*** method GroupsApi->groupsorganizersbygroupkeyget example
*** Organizers by group

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_groupkey:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_groupkey type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_groupkey = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_GroupsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method groupsorganizersbygroupkeyget via HTTP GET
    /blck/g2m_cl_GroupsApi=>groupsorganizersbygroupkeyget(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_groupkey = gvs_groupkey
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_groupkey** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-GroupsApi-groupsorganizersbygroupkeypost"></a>

## operation: **groupsorganizersbygroupkeypost**
Organizer in group

<p>Creates a new organizer and sends an email to the email address defined in request. This API call is only available to users with the admin role. You may also pass 'G2W' or 'G2T' or 'OPENVOICE' as productType variables, creating organizers for those products. A G2W or G2T organizer will also have access to G2M.</p>  <table border=1>            <tr> <th> field </th> <th> value </th> <th> description </th> </tr>  <tr> <td> \"organizerEmail\" </td> <td> \"valid.org@email.com\" </td> <td> String with valid email syntax </td> </tr>  <tr> <td> \"firstName\" </td> <td> \"First\" </td> <td> String - max 25 characters </td> </tr>  <tr> <td> \"lastName\" </td> <td> \"Last\" </td> <td> String - max 25 characters </td> </tr>  <tr> <td> \"productType\" </td> <td> \"G2M\" </td> <td> Must be: G2M, G2W, G2T, OV </td> </tr>  </table>


### Example
```abap
*** method GroupsApi->groupsorganizersbygroupkeypost example
*** Organizer in group

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/G2M_ORGANIZERINGRO
    data gm_body type /BLCK/G2M_ORGANIZERINGRO.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_group_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_group_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gm_body-organizer_email = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-first_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-last_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-product_type = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_group_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_GroupsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method groupsorganizersbygroupkeypost via HTTP POST
    /blck/g2m_cl_GroupsApi=>groupsorganizersbygroupkeypost(
      exporting
        i_body = gm_body
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_group_key = gvs_group_key
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
 **i_body** | `/BLCK/G2M_ORGANIZERINGRO` (**[OrganizerInGrouprequest](#markdown-header-model-organizeringro)**) |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_group_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: Not defined


<a name="markdown-header-op-GroupsApi-groupsupcomingmeetingsbygroupk"></a>

## operation: **groupsupcomingmeetingsbygroupk**
Upcoming meetings by group

Get upcoming meetings for a specified group. This API call is only available to users with the admin role. This API call can be used only for groups with maximum 50 organizers.


### Example
```abap
*** method GroupsApi->groupsupcomingmeetingsbygroupk example
*** Upcoming meetings by group

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_group_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_group_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_group_key = 'ipsum lorem'.


    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_GroupsApi=>config(
      exporting
        i_basepath = gcc_basepath ).
        
*** call the API method groupsupcomingmeetingsbygroupk via HTTP GET
    /blck/g2m_cl_GroupsApi=>groupsupcomingmeetingsbygroupk(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_group_key = gvs_group_key
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_group_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined



# API: MeetingsApi

All URIs are relative to *https://api.getgo.com/G2M/rest*

<a name="markdown-header-op-MeetingsApi-historical_meetings_get"></a>

## operation: **historical_meetings_get**
Historical meetings

Get historical meetings for the currently authenticated organizer that started within the specified date/time range. Remark: Meetings which are still ongoing at the time of the request are NOT contained in the result array.


### Example
```abap
*** method MeetingsApi->historical_meetings_get example
*** Historical meetings

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_start_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_start_date type /BLCK/G2M_STRING.
*   for parameter i_end_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_end_date type /BLCK/G2M_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_start_date = 'ipsum lorem'.
*   gvs_end_date = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method historical_meetings_get via HTTP GET
    /blck/g2m_cl_MeetingsApi=>historical_meetings_get(
      exporting
        i_start_date = gvs_start_date
        i_end_date = gvs_end_date
        i_content_type = gvs_content_type
        i_accept = gvs_accept
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
 **i_start_date** | `/BLCK/G2M_STRING` |  
 **i_end_date** | `/BLCK/G2M_STRING` |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-MeetingsApi-meetings_by_meeting_id_delete"></a>

## operation: **meetings_by_meeting_id_delete**
Meeting

Deletes the meeting identified by the meetingId.


### Example
```abap
*** method MeetingsApi->meetings_by_meeting_id_delete example
*** Meeting

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_meeting_id:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_meeting_id type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_meeting_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method meetings_by_meeting_id_delete via HTTP DELETE
    /blck/g2m_cl_MeetingsApi=>meetings_by_meeting_id_delete(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_meeting_id = gvs_meeting_id
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_meeting_id** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-MeetingsApi-meetings_by_meeting_id_get"></a>

## operation: **meetings_by_meeting_id_get**
Meeting

Returns the meeting details for the specified meeting.


### Example
```abap
*** method MeetingsApi->meetings_by_meeting_id_get example
*** Meeting

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_meeting_id:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_meeting_id type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_meeting_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method meetings_by_meeting_id_get via HTTP GET
    /blck/g2m_cl_MeetingsApi=>meetings_by_meeting_id_get(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_meeting_id = gvs_meeting_id
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_meeting_id** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-MeetingsApi-meetings_by_meeting_id_put"></a>

## operation: **meetings_by_meeting_id_put**
Meeting

<p>Updates an existing meeting specified by meetingId.</p>    <table border=1>            <tr> <th> field </th> <th> value </th> <th> description </th> </tr>  <tr> <td> \"subject\" </td> <td> \"subject\" </td> <td> String - max 100 char. </td> </tr>  <tr> <td> \"starttime\" </td> <td> \"2019-05-10T12:00:00Z\" </td> <td> {YYYY}-{MM}-{DD}T{HH}:{MM}:{SS}Z format, UTC only </td> </tr>  <tr> <td> \"endtime\" </td> <td> \"2019-05-10T13:00:00Z\" </td> <td> {YYYY}-{MM}-{DD}T{HH}:{MM}:{SS}Z format, UTC only </td> </tr>  <tr> <td> \"passwordRequired\" </td> <td> FALSE </td> <td> Boolean: true, false </td> </tr>  <tr> <td> \"conferencecallinfo\" </td> <td> \"hybrid\" </td> <td> Must be one of: Hybrid, PTSN, Free, Private, VoIP. </td> </tr>  <tr> <td> \"timezonekey\" </td> <td> <leave blank> </td> <td> All times default to UTC </td> </tr>  <tr> <td> \"meetingtype\" </td> <td> \"scheduled\" </td> <td> Must be one of: scheduled, recurring, immediate </td> </tr>  </table>


### Example
```abap
*** method MeetingsApi->meetings_by_meeting_id_put example
*** Meeting

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/G2M_MEETINGREQUEST
    data gm_body type /BLCK/G2M_MEETINGREQUEST.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_meeting_id:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_meeting_id type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gm_body-subject = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-starttime = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-endtime = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-passwordrequired = 'X'. " (type /BLCK/G2M_BOOL)
*   gm_body-conferencecallinfo = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-timezonekey = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-meetingtype = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_meeting_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method meetings_by_meeting_id_put via HTTP PUT
    /blck/g2m_cl_MeetingsApi=>meetings_by_meeting_id_put(
      exporting
        i_body = gm_body
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_meeting_id = gvs_meeting_id
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
 **i_body** | `/BLCK/G2M_MEETINGREQUEST` (**[MeetingRequest](#markdown-header-model-meetingrequest)**) |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_meeting_id** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: Not defined


<a name="markdown-header-op-MeetingsApi-meetings_post"></a>

## operation: **meetings_post**
Meeting

<p>Create a new meeting based on the parameters specified.</p>    <table border=1>            <tr> <th> field </th> <th> value </th> <th> description </th> </tr>  <tr> <td> \"subject\" </td> <td> \"subject\" </td> <td> String - max 100 char. </td> </tr>  <tr> <td> \"starttime\" </td> <td> \"2019-05-10T12:00:00Z\" </td> <td> {YYYY}-{MM}-{DD}T{HH}:{MM}:{SS}Z format, UTC only </td> </tr>  <tr> <td> \"endtime\" </td> <td> \"2019-05-10T13:00:00Z\" </td> <td> {YYYY}-{MM}-{DD}T{HH}:{MM}:{SS}Z format, UTC only </td> </tr>  <tr> <td> \"passwordRequired\" </td> <td> FALSE </td> <td> Boolean: true, false </td> </tr>  <tr> <td> \"conferencecallinfo\" </td> <td> \"hybrid\" </td> <td> Must be one of: Hybrid, PTSN, Free, Private, VoIP. </td> </tr>  <tr> <td> \"timezonekey\" </td> <td> <leave blank> </td> <td> All times default to UTC </td> </tr>  <tr> <td> \"meetingtype\" </td> <td> \"scheduled\" </td> <td> Must be one of: scheduled, recurring, immediate </td> </tr>  </table>


### Example
```abap
*** method MeetingsApi->meetings_post example
*** Meeting

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/G2M_MEETINGREQUEST
    data gm_body type /BLCK/G2M_MEETINGREQUEST.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gm_body-subject = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-starttime = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-endtime = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-passwordrequired = 'X'. " (type /BLCK/G2M_BOOL)
*   gm_body-conferencecallinfo = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-timezonekey = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-meetingtype = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method meetings_post via HTTP POST
    /blck/g2m_cl_MeetingsApi=>meetings_post(
      exporting
        i_body = gm_body
        i_content_type = gvs_content_type
        i_accept = gvs_accept
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
 **i_body** | `/BLCK/G2M_MEETINGREQUEST` (**[MeetingRequest](#markdown-header-model-meetingrequest)**) |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: Not defined


<a name="markdown-header-op-MeetingsApi-meetingsattendeesbymeetinginst"></a>

## operation: **meetingsattendeesbymeetinginst**
Attendees by meeting

List all attendees for specified meetingId of historical meeting. The historical meetings can be fetched using 'Get historical meetings', 'Get historical meetings by organizer', and 'Get historical meetings by group'. For users with the admin role this call returns attendees for any meeting. For any other user the call will return attendees for meetings on which the user is a valid organizer.


### Example
```abap
*** method MeetingsApi->meetingsattendeesbymeetinginst example
*** Attendees by meeting

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_meeting_instance_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_meeting_instance_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_meeting_instance_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method meetingsattendeesbymeetinginst via HTTP GET
    /blck/g2m_cl_MeetingsApi=>meetingsattendeesbymeetinginst(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_meeting_instance_key = gvs_meeting_instance_key
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_meeting_instance_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-MeetingsApi-meetingsstartbymeetingidget"></a>

## operation: **meetingsstartbymeetingidget**
Meeting link

Returns a host URL that can be used to start a meeting. When this URL is opened in a web browser, the GoToMeeting client will be downloaded and launched and the meeting will start. The end user is not required to login to a client.


### Example
```abap
*** method MeetingsApi->meetingsstartbymeetingidget example
*** Meeting link

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_meeting_id:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_meeting_id type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_meeting_id = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method meetingsstartbymeetingidget via HTTP GET
    /blck/g2m_cl_MeetingsApi=>meetingsstartbymeetingidget(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_meeting_id = gvs_meeting_id
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_meeting_id** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-MeetingsApi-upcoming_meetings_get"></a>

## operation: **upcoming_meetings_get**
Upcoming meetings

Gets upcoming meetings for the current authenticated organizer.


### Example
```abap
*** method MeetingsApi->upcoming_meetings_get example
*** Upcoming meetings

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_MeetingsApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method upcoming_meetings_get via HTTP GET
    /blck/g2m_cl_MeetingsApi=>upcoming_meetings_get(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined



# API: OrganizersApi

All URIs are relative to *https://api.getgo.com/G2M/rest*

<a name="markdown-header-op-OrganizersApi-organizers_delete"></a>

## operation: **organizers_delete**
Organizer by email

Deletes the individual organizer specified by the email address. This API call is only available to users with the admin role.


### Example
```abap
*** method OrganizersApi->organizers_delete example
*** Organizer by email

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_email:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_email type /BLCK/G2M_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_email = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizers_delete via HTTP DELETE
    /blck/g2m_cl_OrganizersApi=>organizers_delete(
      exporting
        i_email = gvs_email
        i_content_type = gvs_content_type
        i_accept = gvs_accept
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
 **i_email** | `/BLCK/G2M_STRING` |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-OrganizersApi-organizers_get"></a>

## operation: **organizers_get**
Organizer by email

Gets the individual organizer specified by the organizer's email address. If an email address is not specified, all organizers are returned. This API call is only available to users with the admin role.


### Example
```abap
*** method OrganizersApi->organizers_get example
*** Organizer by email

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_email:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_email type /BLCK/G2M_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_email = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizers_get via HTTP GET
    /blck/g2m_cl_OrganizersApi=>organizers_get(
      exporting
        i_email = gvs_email
        i_content_type = gvs_content_type
        i_accept = gvs_accept
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
 **i_email** | `/BLCK/G2M_STRING` |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-OrganizersApi-organizers_post"></a>

## operation: **organizers_post**
Organizer

<p>Creates a new organizer and sends an email to the email address defined in the request. This API call is only available to users with the admin role. You may also pass 'G2W' or 'G2T' or 'OPENVOICE' as productType, to create organizers for those products. A G2W or G2T organizer will also have access to G2M.</p>    <table border=1>            <tr> <th> field </th> <th> value </th> <th> description </th> </tr>  <tr> <td> \"firstName\" </td> <td> \"First\" </td> <td> String - max 25 characters </td> </tr>  <tr> <td> \"lastName\" </td> <td> \"Last\" </td> <td> String - max 25 characters </td> </tr>  <tr> <td> \"organizerEmail\" </td> <td> \"valid.org@email.com\" </td> <td> String with valid email syntax </td> </tr>  <tr> <td> \"productType\" </td> <td> \"G2M\" </td> <td> Must be: G2M, G2W, G2T, OV </td> </tr>  </table>


### Example
```abap
*** method OrganizersApi->organizers_post example
*** Organizer

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_body:
*   a reference to model type /BLCK/G2M_ORGANIZERREQUE
    data gm_body type /BLCK/G2M_ORGANIZERREQUE.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gm_body-first_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-last_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-organizer_email = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gm_body-product_type = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizers_post via HTTP POST
    /blck/g2m_cl_OrganizersApi=>organizers_post(
      exporting
        i_body = gm_body
        i_content_type = gvs_content_type
        i_accept = gvs_accept
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
 **i_body** | `/BLCK/G2M_ORGANIZERREQUE` (**[OrganizerRequest](#markdown-header-model-organizerreque)**) |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: Not defined


<a name="markdown-header-op-OrganizersApi-organizersattendeesbyorganizer"></a>

## operation: **organizersattendeesbyorganizer**
Attendees by organizer

Lists all attendees for all meetings within a specified date range for a specified organizer. This API call is only available to users with the admin role.


### Example
```abap
*** method OrganizersApi->organizersattendeesbyorganizer example
*** Attendees by organizer

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_starttime:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_starttime type /BLCK/G2M_STRING.
*   for parameter i_end_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_end_date type /BLCK/G2M_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_organizer_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_organizer_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_starttime = 'ipsum lorem'.
*   gvs_end_date = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_organizer_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizersattendeesbyorganizer via HTTP GET
    /blck/g2m_cl_OrganizersApi=>organizersattendeesbyorganizer(
      exporting
        i_starttime = gvs_starttime
        i_end_date = gvs_end_date
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_organizer_key = gvs_organizer_key
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
 **i_starttime** | `/BLCK/G2M_STRING` |  
 **i_end_date** | `/BLCK/G2M_STRING` |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_organizer_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-OrganizersApi-organizersbyorganizerkeydelete"></a>

## operation: **organizersbyorganizerkeydelete**
Organizer

Deletes the individual organizer specified by the organizer key. This API call is only available to users with the admin role.


### Example
```abap
*** method OrganizersApi->organizersbyorganizerkeydelete example
*** Organizer

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_organizer_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_organizer_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_organizer_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizersbyorganizerkeydelete via HTTP DELETE
    /blck/g2m_cl_OrganizersApi=>organizersbyorganizerkeydelete(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_organizer_key = gvs_organizer_key
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_organizer_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-OrganizersApi-organizersbyorganizerkeyget"></a>

## operation: **organizersbyorganizerkeyget**
Organizer

Gets the individual organizer specified by the organizer's email address. If an email address is not specified, all organizers are returned. This API call is only available to users with the admin role.


### Example
```abap
*** method OrganizersApi->organizersbyorganizerkeyget example
*** Organizer

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_organizer_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_organizer_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_organizer_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizersbyorganizerkeyget via HTTP GET
    /blck/g2m_cl_OrganizersApi=>organizersbyorganizerkeyget(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_organizer_key = gvs_organizer_key
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_organizer_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-OrganizersApi-organizersbyorganizerkeyput"></a>

## operation: **organizersbyorganizerkeyput**
Organizer

<p>Updates the products of the specified organizer. To add a product (G2M, G2W, G2T, OPENVOICE) for the organizer, the call must be sent once for each product you want to add. To remove all products for the organizer, set status to 'suspended'. The call is limited to users with the admin role.</p>  <table border=1>            <tr> <th> field </th> <th> value </th> <th> description </th> </tr>  <tr> <td> \"firstName\" </td> <td> \"First\" </td> <td> String - max 25 characters </td> </tr>  <tr> <td> \"lastName\" </td> <td> \"Last\" </td> <td> String - max 25 characters </td> </tr>  <tr> <td> \"organizerEmail\" </td> <td> \"valid.org@email.com\" </td> <td> String with valid email syntax </td> </tr>  <tr> <td> \"productType\" </td> <td> \"G2M\" </td> <td> Must be: G2M, G2W, G2T, OV </td> </tr>  <tr> <td> \"status\" </td> <td> \"suspended\" </td> <td> Must be: blank or suspended </td> </tr>  </table>


### Example
```abap
*** method OrganizersApi->organizersbyorganizerkeyput example
*** Organizer

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_organizer_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_organizer_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_organizer_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizersbyorganizerkeyput via HTTP PUT
    /blck/g2m_cl_OrganizersApi=>organizersbyorganizerkeyput(
      exporting
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_organizer_key = gvs_organizer_key
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
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_organizer_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


<a name="markdown-header-op-OrganizersApi-organizershistoricalmeetingsby"></a>

## operation: **organizershistoricalmeetingsby**
Historical meetings by organizer

Get historical meetings for the specified organizer that started within the specified date/time range. Meetings which are still ongoing at the time of the request are not included in the result.


### Example
```abap
*** method OrganizersApi->organizershistoricalmeetingsby example
*** Historical meetings by organizer

  constants:
    gcc_basepath type string value 'https://api.getgo.com/G2M/rest'.
    
  data:  
    gcl_auth type ref to z_api_cl_auth, " descended from /blck/g2m_cl_auth
    gvi_code type /blck/g2m_int,
    gvs_msg  type /blck/g2m_string.
    
*** create variables for input and output as needed
*   for parameter i_start_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_start_date type /BLCK/G2M_STRING.
*   for parameter i_end_date:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_end_date type /BLCK/G2M_STRING.
*   for parameter i_content_type:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_content_type type /BLCK/G2M_STRING.
*   for parameter i_accept:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_accept type /BLCK/G2M_STRING.
*   for parameter i_organizer_key:
*   a simple ABAP primitive of type /BLCK/G2M_STRING
    data gvs_organizer_key type /BLCK/G2M_STRING.
        
*** set data according to requirements of the API call
*   gvs_start_date = 'ipsum lorem'.
*   gvs_end_date = 'ipsum lorem'.
*   gvs_content_type = 'ipsum lorem'.
*   gvs_accept = 'ipsum lorem'.
*   gvs_organizer_key = 'ipsum lorem'.


*** optional: instantiate descendant of /blck/g2m_cl_auth 
*** (gcl_auth) if bespoke auth is needed
*    create object gcl_auth exporting ...
    
*** update the configuration if needed, a default basepath is already set from the spec
*** so the parameter i_basepath is only needed if the url should be different to that specified
    /blck/g2m_cl_OrganizersApi=>config(
      exporting
        i_basepath = gcc_basepath
        i_auth = gcl_auth ).
        
*** call the API method organizershistoricalmeetingsby via HTTP GET
    /blck/g2m_cl_OrganizersApi=>organizershistoricalmeetingsby(
      exporting
        i_start_date = gvs_start_date
        i_end_date = gvs_end_date
        i_content_type = gvs_content_type
        i_accept = gvs_accept
        i_organizer_key = gvs_organizer_key
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
 **i_start_date** | `/BLCK/G2M_STRING` |  
 **i_end_date** | `/BLCK/G2M_STRING` |  
 **i_content_type** | `/BLCK/G2M_STRING` |  
 **i_accept** | `/BLCK/G2M_STRING` |  
 **i_organizer_key** | `/BLCK/G2M_STRING` |  

### Return types


### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


* * *
<a name="markdown-header-model-meetingrequest"></a> 

# Model: MeetingRequest



### Example
```abap
*** model meetingrequest example

* create our variables..
    data gr_meetingrequest type /blck/g2m_meetingrequest.
    
* fill model with data as appropriate..
    gr_meetingrequest-subject = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_meetingrequest-starttime = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_meetingrequest-endtime = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_meetingrequest-passwordrequired = 'X'. " (type /BLCK/G2M_BOOL)
    gr_meetingrequest-conferencecallinfo = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_meetingrequest-timezonekey = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_meetingrequest-meetingtype = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_meetingrequest(
      exporting
        i_meetingrequest = gr_meetingrequest ).
    		
    clear gr_meetingrequest.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_meetingrequest(
      exporting
        i_id = 1
      importing 
        e_200 = gr_meetingrequest ).
    		
    write: gr_meetingrequest-subject. " (type /BLCK/G2M_STRING)
    write: gr_meetingrequest-starttime. " (type /BLCK/G2M_STRING)
    write: gr_meetingrequest-endtime. " (type /BLCK/G2M_STRING)
    write: gr_meetingrequest-passwordrequired. " (type /BLCK/G2M_BOOL)
    write: gr_meetingrequest-conferencecallinfo. " (type /BLCK/G2M_STRING)
    write: gr_meetingrequest-timezonekey. " (type /BLCK/G2M_STRING)
    write: gr_meetingrequest-meetingtype. " (type /BLCK/G2M_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**subject** | `/BLCK/G2M_STRING` | 
**starttime** | `/BLCK/G2M_STRING` | 
**endtime** | `/BLCK/G2M_STRING` | 
**passwordrequired** | `/BLCK/G2M_BOOL` | 
**conferencecallinfo** | `/BLCK/G2M_STRING` | 
**timezonekey** | `/BLCK/G2M_STRING` | 
**meetingtype** | `/BLCK/G2M_STRING` | 

* * *
<a name="markdown-header-model-organizeringro"></a> 

# Model: OrganizerInGrouprequest



### Example
```abap
*** model organizeringro example

* create our variables..
    data gr_organizeringro type /blck/g2m_organizeringro.
    
* fill model with data as appropriate..
    gr_organizeringro-organizer_email = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_organizeringro-first_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_organizeringro-last_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_organizeringro-product_type = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_organizeringro(
      exporting
        i_organizeringro = gr_organizeringro ).
    		
    clear gr_organizeringro.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_organizeringro(
      exporting
        i_id = 1
      importing 
        e_200 = gr_organizeringro ).
    		
    write: gr_organizeringro-organizer_email. " (type /BLCK/G2M_STRING)
    write: gr_organizeringro-first_name. " (type /BLCK/G2M_STRING)
    write: gr_organizeringro-last_name. " (type /BLCK/G2M_STRING)
    write: gr_organizeringro-product_type. " (type /BLCK/G2M_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**organizer_email** | `/BLCK/G2M_STRING` | 
**first_name** | `/BLCK/G2M_STRING` | 
**last_name** | `/BLCK/G2M_STRING` | 
**product_type** | `/BLCK/G2M_STRING` | 

* * *
<a name="markdown-header-model-organizerreque"></a> 

# Model: OrganizerRequest



### Example
```abap
*** model organizerreque example

* create our variables..
    data gr_organizerreque type /blck/g2m_organizerreque.
    
* fill model with data as appropriate..
    gr_organizerreque-first_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_organizerreque-last_name = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_organizerreque-organizer_email = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    gr_organizerreque-product_type = 'ipsum lorem'. " (type /BLCK/G2M_STRING)
    
* pass to example API method
    /blck/cl_example_api=>update_organizerreque(
      exporting
        i_organizerreque = gr_organizerreque ).
    		
    clear gr_organizerreque.
    
* fetch model data from example API method
    /blck/cl_example_api=>get_organizerreque(
      exporting
        i_id = 1
      importing 
        e_200 = gr_organizerreque ).
    		
    write: gr_organizerreque-first_name. " (type /BLCK/G2M_STRING)
    write: gr_organizerreque-last_name. " (type /BLCK/G2M_STRING)
    write: gr_organizerreque-organizer_email. " (type /BLCK/G2M_STRING)
    write: gr_organizerreque-product_type. " (type /BLCK/G2M_STRING)

```

## Properties

Name | Type | Description
------------ | ------------- | -------------
**first_name** | `/BLCK/G2M_STRING` | 
**last_name** | `/BLCK/G2M_STRING` | 
**organizer_email** | `/BLCK/G2M_STRING` | 
**product_type** | `/BLCK/G2M_STRING` | 

