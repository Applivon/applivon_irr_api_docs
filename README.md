# IRRC Mobile API Documentation

NOTE : ALL THE REQUESTS ARE POST REQUESTS (HTTP POST)

Postman Collection :
```
https://api.postman.com/collections/15976179-ded2f6f7-77ab-4d81-abba-aecdbb04b3cb?access_key=PMAT-01HQAK34VJQRJC3HPCJTFYM8HK
```

- [Authentication API](#authentication-apis)
     - [Auth Encrypted API](#auth-encrypted-api)
       - [Login](#login-api)
       - [Change Password](#change-user-password-api)
     - [Logout](#logout-api)
     - [Get Password Policy](#get-user-password-policy-api)
- [Dashboard](#dashboard-api)
     - [Pending Donation](#get-pending-donation-request--count-api)
     - [Pending Donation based on status](#get-pending-donation-request--count-with-status-filteration-api)
- [Request Module API](#request-module-api)
     - [Tangible Item List](#to-get-list-of-item-tangible-request-api)
     - [List Of Service request](#to-get-list-of-service-request-api)
     - [Reject Specific Item](#to-reject-specific-request-item-api)
     - [Request Product List](#to-get-request-product-list-api)
     - [Cancel Specific Item](#to-cancel-specific-request-item-api)
     - [Item Availability](#to-get-request-item-availablilty-api)
     - [Collection Point List](#to-get-collection-point-details-api)
     - [Request Beneficiary](#to-update-request-beneficiary-api)
     - [Update Item Data](#to-update-request-item-data-api)
- [Contact Person API](#contact-person-api)
     - [List of Person Title](#to-get-contact-person-title-api)
     - [List of Countries](#to-get-person-country-api)
     - [List of Languages](#to-get-person-languages-api)
     - [Update Contact Person](#to-update-contact-person-data-api)
     - [Encrypted API](#encrypted-api-requests)
          - [Beneficiary Details](#to-get-contact-person-title-api)
          - [Donor Details](#to-get-contact-person-title-api)
- [Donation Module API](#donation-api)
     - [List Of donation](#to-get-list-of-donations-api)
     - [Get donation item pictures](#to-get-donation-item-pictures-api)
     - [Update Donation item pictures](#to-update-donation-item-pictures-api)
     - [List Of donation products](#to-get-donation-product-list-api)
     - [Reject Specific donation](#to-reject-specific-donation-api)
     - [Cancel Specific donation](#to--cancel-specific-donation-api)
     - [Update donation item data](#to-update-donation-item-data-api)
- [API Standard Exceptions](#api-error-response)     
- [Data Encryption](#data-encryption)
     - [Encryption](#encryption-of-data)
     - [Decryption](#decryption-of-data)
     
          






## Authentication APIs


### Auth Encrypted API

### LOGIN API
To Login Account and generate token for API validation

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/login
```

### Request headers

|    Name    |       Value     |
|:-----------|:----------------|
|Content-Type|application/json|

### Request body

| Parameter | Type |           Description     |
|:----------|:-----|:--------------------------|
|login|String|Username provided for login|
|password|String|Secret password for login|


### Example

##### Request

```
{
  "params": {
    "login": "user@mail.com",
    "password": "1234"
  }
}
```
##### Encrypted Request

```
{
  "params": {
    "encrypted_data": [
      "YOUR ENCRYTED BASE 64 DATA",
      "16 bit IV Key generated during encryption"
    ]
  }
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": ["YOUR ENCRYTED BASE 64 DATA",
        "16 bit IV Key generated during encryption"
    ]
}

```

##### Decrypted Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Login Successfully!"
        },
        "data": {
            "user_id": 24,
            "token": "8f693a2c9225cccd4306d4343434334e648c715d66c040de38da9fb193d10a1c8cd42c2134fb598e43e0a8ca6e82bf65ed2a48ea0e184ca2595f71cbf892f",
            "name": "Store Manager",
            "contact_id": 137,
            "contact_name": "Store Manager",
            "email": "sample@mail.com",
            "mobile": "",
            "is_internal": true,
            "is_external": false,
            "is_system_admin": false,
            "is_director": false,
            "is_manager": false,
            "is_operations": false,
            "is_store_manager": true,
            "is_volunteer": false,
            "is_lead_volunteer": false
        }
    }
}
```

### Remarks

[The above encryption & decryption of data is implemented using AES encryption technique.](#data-encryption) 

#  CHANGE USER PASSWORD API

To change Logged-in User's Password

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/change_user_password
```

### Request headers

|    Name    |       Value     |
|:-----------|:----------------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type |           Description     |
|:----------|:-----|:--------------------------|
|old_password|String|Existing password|
|new_password|String|New password|


### Example

##### Request

```
{
  "params": {
    "old_password": "admin@1234",
    "new_password": "1234Admin"
  }
}
```

##### Encrypted Request

```
{
  "params": {
    "encrypted_data": [
      "YOUR ENCRYTED BASE 64 DATA",
      "16 bit IV Key generated during encryption"
    ]
  }
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": ["YOUR ENCRYTED BASE 64 DATA",
        "16 bit IV Key generated during encryption"
    ]
}

```


##### Decrypted Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Password Updated Successfully!"
        },
        "data": {}
    }
}
```

### Remarks

[The above encryption & decryption of data is implemented using AES encryption technique.](#data-encryption) 

### LOGOUT API

To Logout Account and clear token.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/logout
```

### Request headers

|    Name    |       Value     |
|:-----------|:----------------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type |           Description     |
|:----------|:-----|:--------------------------|

Pass Empty Json : {}

### Example

##### Request

```
{ 
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Logout Successfully!"
        },
        "data": {}
    }
}
```

### Remarks


###  GET USER PASSWORD POLICY API

To get the Password create/update Condition

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_user_password_policy
```

### Request headers

|    Name    |       Value     |
|:-----------|:----------------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type |           Description     |
|:----------|:-----|:--------------------------|
|min_password_length|Integer|Minimum Password length|
|password_lower_required|Boolean|To set lower case validation for password creation|
|password_upper_required|Boolean|To set upper case validation for password creation|
|password_numeric_required|Boolean|To set numeric value validation for password creation|
|password_special_required|Boolean|To set special character validation for password creation|

OR 

Pass Empty Json : { "params":{}"}


### Example

##### Request

```
{
  "params": {
  }
}
```
OR
```
{
  "params": {
    "min_password_length": 2,
    "password_lower_required": false,
    "password_upper_required": false,
    "password_numeric_required": false,
    "password_special_required": false
  }
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "user_password_policy": [
                {
                    "min_password_length": 2,
                    "password_lower_required": false,
                    "password_upper_required": false,
                    "password_numeric_required": false,
                    "password_special_required": false
                }
            ]
        }
    }
}
```

### Remarks

### Dashboard API

### GET PENDING DONATION REQUEST & COUNT API

To get the count of Pending Requests/Donations.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donation_requests_pending_count
```

### Request parameters

In the request URL, provide the following query parameters with values.

| Parameter | Type | Description |
|:----------|:-----|:------------|


### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|from_date|Date|From date for filteration of data|
|to_date|Date|To date for filteration of data|

Above are the Optional Parameters

### Example

##### Request

```
{
  "params": {
    "from_date": "01/05/2024",
    "to_date": "31/05/2024"
  }
}

```
OR

```
{
  "params": {}
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "from_date": "01/05/2024",
            "to_date": "31/05/2024",
            "pending_donations": 0,
            "pending_requests": 9
        }
    }
}
```

### Remarks

### GET PENDING DONATION REQUEST & COUNT WITH STATUS FILTERATION API

To get the count of Statuswise Requests/Donations.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donation_requests_status_count
```

### Request parameters

In the request URL, provide the following query parameters with values.

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|from_date|Date|From date for filteration of data|
|to_date|Date|To date for filteration of data|

Above are the Optional Parameters

### Example

##### Request

```
{
  "params": {
    "from_date": "01/05/2024",
    "to_date": "31/05/2024"
  }
}

```
OR

```
{
  "params": {}
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "from_date": "01/04/2024",
            "to_date": "31/05/2024",
            "review_donations": 0,
            "accept_donations": 2,
            "review_requests": 22,
            "in_queue_requests": 4,
            "ready_to_process_requests": 13,
            "processing_requests": 9
        }
    }
}
```

### Remarks

### Request Module API
### TO GET REQUEST ITEM LIST API

To get the list of Requests (Service & Tangible) based on Created Date in Asc Order.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_request_items_list
```

### Request parameters

In the request URL, provide the following query parameters with values.

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|keyword_search|String|Search keyword for filteration of data|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "page": 2,
    "limit": 10
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "total_pages": 28,
            "total_count": 83,
            "max_records_for_page": 3,
            "current_page": 2,
            "count": 3,
            "requests_list": [
                {
                    "request_id": 5,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "request_ref": "RQ24030003-01",
                    "submission_date": "18/03/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "is_eligible": false,
                    "reviewers_remarks": "",
                    "beneficiary_remarks": "",
                    "category_id": 7,
                    "category_name": "Mens Clothing",
                    "request_qty": 10,
                    "processed_qty": 0,
                    "is_available": false,
                    "is_allocated": false,
                    "is_ready_to_process": false,
                    "item_to_allocate_id": 13,
                    "item_to_allocate_name": "T-Shirt",
                    "fulfillment_mode_key": "",
                    "fulfillment_mode": "",
                    "collection_point_id": 3,
                    "collection_point_name": "InspIRRe Store",
                    "collection_point_details": "",
                    "collection_appt": "",
                    "eligibility_conditions": "eligibility conditions goes here",
                    "eligibility_criteria_line": [
                        {
                            "eligibility_criteria_line_id": 128,
                            "question": "question 1 goes here",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 129,
                            "question": "question 3",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 130,
                            "question": "question 2",
                            "response": "",
                            "reviewers_remarks": ""
                        }
                    ]
                },
                {
                    "request_id": 6,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "request_ref": "RQ24030004-01",
                    "submission_date": "20/03/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "is_eligible": false,
                    "reviewers_remarks": "",
                    "beneficiary_remarks": "",
                    "category_id": 7,
                    "category_name": "Mens Clothing",
                    "request_qty": 10,
                    "processed_qty": 10,
                    "is_available": true,
                    "is_allocated": false,
                    "is_ready_to_process": false,
                    "item_to_allocate_id": 13,
                    "item_to_allocate_name": "T-Shirt",
                    "fulfillment_mode_key": "collection_point",
                    "fulfillment_mode": "Collection Point",
                    "collection_point_id": 3,
                    "collection_point_name": "InspIRRe Store",
                    "collection_point_details": "",
                    "collection_appt": "21/03/2024 06:00:00",
                    "eligibility_conditions": "eligibility conditions goes here",
                    "eligibility_criteria_line": [
                        {
                            "eligibility_criteria_line_id": 128,
                            "question": "question 1 goes here",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 129,
                            "question": "question 3",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 130,
                            "question": "question 2",
                            "response": "",
                            "reviewers_remarks": ""
                        }
                    ]
                },
                {
                    "request_id": 13,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "request_ref": "RQ24030004-02",
                    "submission_date": "28/03/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "is_eligible": false,
                    "reviewers_remarks": "",
                    "beneficiary_remarks": "",
                    "category_id": -1,
                    "category_name": "",
                    "request_qty": 0,
                    "processed_qty": 0,
                    "is_available": false,
                    "is_allocated": false,
                    "is_ready_to_process": false,
                    "item_to_allocate_id": -1,
                    "item_to_allocate_name": "",
                    "fulfillment_mode_key": "collection_point",
                    "fulfillment_mode": "Collection Point",
                    "collection_point_id": -1,
                    "collection_point_name": "",
                    "collection_point_details": "",
                    "collection_appt": "",
                    "eligibility_conditions": "eligibility conditions goes here",
                    "eligibility_criteria_line": []
                }
            ]
        }
    }
}
```

### Remarks

### TO GET LIST OF ITEM TANGIBLE REQUEST API

To get the list of Tangible Requests based on Created Date in Ascending Order

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_tangible_request_items_list
```

### Request parameters

In the request URL, provide the following query parameters with values.

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|keyword_search|String|Search keyword for filteration of data|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "page": 2,
    "limit": 2
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "total_pages": 21,
            "total_count": 41,
            "max_records_for_page": 2,
            "current_page": 1,
            "count": 2,
            "requests_list": [
                {
                    "request_id": 57,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "request_ref": "RQ24040031-01",
                    "submission_date": "16/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "is_eligible": true,
                    "reviewers_remarks": "",
                    "beneficiary_remarks": "",
                    "category_id": 8,
                    "category_name": "Safety Clothes",
                    "request_qty": 1,
                    "processed_qty": 1,
                    "is_available": true,
                    "is_allocated": false,
                    "is_ready_to_process": true,
                    "item_to_allocate_id": 21,
                    "item_to_allocate_name": "Safety Hat",
                    "fulfillment_mode_key": "collection_point",
                    "fulfillment_mode": "Collection Point",
                    "collection_point_id": 3,
                    "collection_point_name": "InspIRRe Store",
                    "collection_point_details": "",
                    "collection_appt": "",
                    "eligibility_conditions": "eligibility conditions goes here",
                    "eligibility_criteria_line": [
                        {
                            "eligibility_criteria_line_id": 128,
                            "question": "question 1 goes here",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 129,
                            "question": "question 3",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 130,
                            "question": "question 2",
                            "response": "",
                            "reviewers_remarks": ""
                        }
                    ]
                },
                {
                    "request_id": 58,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "request_ref": "RQ24040031-02",
                    "submission_date": "16/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "is_eligible": true,
                    "reviewers_remarks": "",
                    "beneficiary_remarks": "",
                    "category_id": 8,
                    "category_name": "Safety Clothes",
                    "request_qty": 1,
                    "processed_qty": 1,
                    "is_available": true,
                    "is_allocated": false,
                    "is_ready_to_process": true,
                    "item_to_allocate_id": 7,
                    "item_to_allocate_name": "Safety Shoes",
                    "fulfillment_mode_key": "collection_point",
                    "fulfillment_mode": "Collection Point",
                    "collection_point_id": 3,
                    "collection_point_name": "InspIRRe Store",
                    "collection_point_details": "",
                    "collection_appt": "",
                    "eligibility_conditions": "eligibility conditions goes here",
                    "eligibility_criteria_line": []
                }
            ]
        }
    }
}
```

### Remarks


### TO GET LIST OF SERVICE REQUEST API

To get the list of Service Requests based on Created Date in Ascending Order

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_service_request_items_list
```

### Request parameters

In the request URL, provide the following query parameters with values.

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|keyword_search|String|Search keyword for filteration of data|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "page": 2,
    "limit": 2
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "total_pages": 21,
            "total_count": 41,
            "max_records_for_page": 2,
            "current_page": 1,
            "count": 2,
            "requests_list": [
                {
                    "request_id": 57,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "request_ref": "RQ24040031-01",
                    "submission_date": "16/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "is_eligible": true,
                    "reviewers_remarks": "",
                    "beneficiary_remarks": "",
                    "category_id": 8,
                    "category_name": "Safety Clothes",
                    "request_qty": 1,
                    "processed_qty": 1,
                    "is_available": true,
                    "is_allocated": false,
                    "is_ready_to_process": true,
                    "item_to_allocate_id": 21,
                    "item_to_allocate_name": "Safety Hat",
                    "fulfillment_mode_key": "collection_point",
                    "fulfillment_mode": "Collection Point",
                    "collection_point_id": 3,
                    "collection_point_name": "InspIRRe Store",
                    "collection_point_details": "",
                    "collection_appt": "",
                    "eligibility_conditions": "eligibility conditions goes here",
                    "eligibility_criteria_line": [
                        {
                            "eligibility_criteria_line_id": 128,
                            "question": "question 1 goes here",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 129,
                            "question": "question 3",
                            "response": "",
                            "reviewers_remarks": ""
                        },
                        {
                            "eligibility_criteria_line_id": 130,
                            "question": "question 2",
                            "response": "",
                            "reviewers_remarks": ""
                        }
                    ]
                },
                {
                    "request_id": 58,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "request_ref": "RQ24040031-02",
                    "submission_date": "16/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "is_eligible": true,
                    "reviewers_remarks": "",
                    "beneficiary_remarks": "",
                    "category_id": 8,
                    "category_name": "Safety Clothes",
                    "request_qty": 1,
                    "processed_qty": 1,
                    "is_available": true,
                    "is_allocated": false,
                    "is_ready_to_process": true,
                    "item_to_allocate_id": 7,
                    "item_to_allocate_name": "Safety Shoes",
                    "fulfillment_mode_key": "collection_point",
                    "fulfillment_mode": "Collection Point",
                    "collection_point_id": 3,
                    "collection_point_name": "InspIRRe Store",
                    "collection_point_details": "",
                    "collection_appt": "",
                    "eligibility_conditions": "eligibility conditions goes here",
                    "eligibility_criteria_line": []
                }
            ]
        }
    }
}
```

### Remarks


### TO REJECT SPECIFIC REQUEST ITEM API

To Reject Specific Request Item

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/reject_request_items
```

### Request parameters

In the request URL, provide the following query parameters with values.

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|reviewers_remarks|String|Reviewers rejection remark|
|request_id|Integer|Request unique id for rejection |


### Example

##### Request

```
{
  "params": {
    "request_id": 93,
    "reviewers_remarks": "test rejection"
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Request Item Rejected Successfully!"
        },
        "data": {}
    }
}

```

### Remarks


### TO GET REQUEST PRODUCT LIST API

Get Request Item Product Selection List

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_requests_products_list
```

### Request parameters

In the request URL, provide the following query parameters with values.

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|request_id|Integer|Request id to fetch associated product list|


### Example

##### Request

```
{
  "params": {
    "request_id": 93
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "products_list": [
                {
                    "product_id": 5,
                    "product_name": "[1212121] Acer 8GB Ram"
                },
                {
                    "product_id": 17,
                    "product_name": "[LP00001] Laptop 8GB"
                },
                {
                    "product_id": 19,
                    "product_name": "Test Laptop"
                }
            ]
        },
        "error": {}
    }
}
```

### Remarks


### TO CANCEL SPECIFIC REQUEST ITEM API

To Cancel Specific Request Item

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/cancel_request_items
```

### Request parameters

In the request URL, provide the following query parameters with values.

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|cancel_reason|String|Cancellation  remark|
Optional Parameter
|request_id|Integer|Request item unique id for rejection |


### Example

##### Request

```
{
  "params": {
    "request_id": 93,
    "cancel_reason": "test cancellation"
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Request Item Cancelled Successfully!"
        },
        "data": {}
    }
}

```

### Remarks


### TO GET REQUEST ITEM AVAILABLILTY API

To Get Request Item Availability

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_requests_availability_list
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
Optional Parameter
|request_id|Integer|Request item unique id for Item availability |


### Example

##### Request

```
{
  "params": {
    "request_id": 54
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "availability_info": [
                {
                    "location_id": 18,
                    "location_name": "Stock",
                    "product_id": 37,
                    "product_name": "Umbrella",
                    "available_quantity": 1.0
                },
                {
                    "location_id": 18,
                    "location_name": "Stock",
                    "product_id": 37,
                    "product_name": "Umbrella",
                    "available_quantity": 1.0
                },
                {
                    "location_id": 18,
                    "location_name": "Stock",
                    "product_id": 37,
                    "product_name": "Umbrella",
                    "available_quantity": 1.0
                },
                {
                    "location_id": 24,
                    "location_name": "Stock",
                    "product_id": 37,
                    "product_name": "Umbrella",
                    "available_quantity": -1.0
                }
            ]
        }
    }
}

```

### Remarks


### TO GET COLLECTION POINT DETAILS API

Get Collection Point Values.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_collection_point_details
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|


### Example

##### Request

```
{
    "params": {}
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "collection_points_list": [
                {
                    "id": 1,
                    "name": "HQ"
                },
                {
                    "id": 2,
                    "name": "Tampines Grande"
                },
                {
                    "id": 3,
                    "name": "InspIRRe Store"
                }
            ]
        }
    }
}
```

### Remarks


### TO UPDATE REQUEST BENEFICIARY API

To Update Request Beneficiary Data.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/update_requests_beneficiary_data
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description | Type |
|:----------|:-----|:------------|:-----|
|name|String| Name of the beneficiary|
|phone|String| Phone number of the beneficiary|
|mobile|String| Mobile number of the beneficiary|
|email|String| Email of the beneficiary|
|street|String| Street of the beneficiary|
|street2|String| Street Line 2 of the beneficiary|
|city|String| City of the beneficiary|
|zip|String| Zip code of the beneficiary|
|country_id|String| Country unique id of the beneficiary|
|title_id|String| Title unique id of the beneficiary|
|tag_ids|Array|Array fo Tag unique ids|
|nationality_id|String| Name of the beneficiary|
|dob|String| Date of birth of the beneficiary|
|marital_status_key|String| Marital Status of the beneficiary|
|highest_qualification_key|String| Highest qualification of the beneficiary|
|languages_known_line|Array| Array of languages know|
|contact_id|Integer|Contact Person unique id


### Example

##### Request

```
{
  "params": {
    "contact_id": 12,
    "name": "test user",
    "phone": "12345678",
    "mobile": "87654321",
    "email": "admin@example.com",
    "street": "",
    "street2": "",
    "city": "SG",
    "zip": "12345",
    "country_id": 197,
    "title_id": 2,
    "tag_ids": [1, 4],
    "nationality_id": 197,
    "dob": "22/04/2000",
    "marital_status_key": "married",
    "highest_qualification_key": "degree",
    "languages_known_line": [
        {"id": 3, "language_id": 2, "spoken_key": "advance", "written_key": "intermediate"},
        {"language_id": 4, "spoken_key": "basic", "written_key": "basic"}
    ]
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Contact Person Details updated Successfully!"
        },
        "data": {}
    }
}
```

### Remarks



### TO UPDATE REQUEST ITEM DATA API

To Update Request Items Data.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/update_request_items_data
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|item_to_allocate_id|Integer|Item allocatin unique id for Item|
|tag_ids|Array|List of Person tags id used|
|processed_qty|Integer|Processed Quantity|
|fulfillment_mode_key|Integer|Fulfillment Mode key used for item|
|reviewers_remarks|Integer|Reviewers remarks for Item|
|is_eligible|Boolean|Item eligibility|
|collection_appt|DATETIME|Collection Date for item|
|collection_point_id|Integer|Collection point unique id for Collection identification|
|request_id|Integer|Request unique id for Item eligibility|



### Example

##### Request

```
{
    "params": {
        "request_id": 51,
        "item_to_allocate_id": 5,
        "tag_ids": [
            1,
            3
        ],
        "processed_qty": 2,
        "fulfillment_mode_key": "collection_point",
        "reviewers_remarks": "test review remarks",
        "is_eligible": false,
        "collection_appt": "17/05/2024 11:35:59",
        "collection_point_id": 2
    }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Request Item updated Successfully!"
        },
        "data": {}
    }
}
```

### Remarks

### CONTACT PERSON API 

### TO GET PERSON LANGUAGES API

Get Contact Person Language Values.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_contact_person_languages
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|


### Example

##### Request

```
{
    "params": {}
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "languages_list": [
                {
                    "id": 1,
                    "name": "English"
                },
                {
                    "id": 2,
                    "name": "Malay"
                },
                {
                    "id": 3,
                    "name": "Hindi"
                },
                {
                    "id": 4,
                    "name": "Tamil"
                },
                {
                    "id": 5,
                    "name": "Chinese"
                }
            ]
        }
    }
}
```

### Remarks

### TO GET PERSON COUNTRY API

To Get Contact Person Country / Nationality Values.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_contact_person_country_nationality
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|

Body is passed empty as shown below.

### Example

##### Request

```
{
    "params": {}
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "country_list": [
                {
                    "id": 3,
                    "name": "Afghanistan"
                },
                {
                    "id": 6,
                    "name": "Albania"
                }
            ]
        }
    }
}
```

### Remarks



### TO GET CONTACT PERSON TITLE API

To Get Contact Person Title Values.

### Prerequisites
There is no Prerequisites for this API

### HTTP Request

```
/irrc/get_contact_person_title
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|

Body is passed Empty as shown below.


### Example

##### Request

```
{
    "params": {}
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "title_list": [
                {
                    "id": 4,
                    "name": "Doctor"
                },
                {
                    "id": 1,
                    "name": "Madam"
                },
                {
                    "id": 2,
                    "name": "Miss"
                },
                {
                    "id": 3,
                    "name": "Mister"
                },
                {
                    "id": 6,
                    "name": "Mr"
                },
                {
                    "id": 5,
                    "name": "Professor"
                }
            ]
        }
    }
}
```

### Remarks


### TO UPDATE REQUEST ITEM DATA API

To Get Contact Person Tag Values.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_contact_person_tags
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|

Body is passed empty as shown below.


### Example

##### Request

```
{
    "params": {}
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "tags_list": [
                {
                    "id": 2,
                    "name": "Accounts"
                },
                {
                    "id": 1,
                    "name": "Finance"
                },
                {
                    "id": 3,
                    "name": "Sales"
                },
                {
                    "id": 4,
                    "name": "Service Provider"
                }
            ]
        }
    }
}
```

### Remarks


### TO UPDATE CONTACT PERSON DATA API

Update Contact Person Details.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/update_contact_person_data
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter  | Type | Description              |
|:-----------|:-----|:-------------------------|
| contact_id |Integer| Contact Person unique id |


### Example

##### Request

```
{
  "params": {
    "contact_id": 133,
    "name": "test userrrr",
    "phone": "12345678",
    "mobile": "87654321",
    "email": "admin@example.com",
    "street": "",
    "street2": "",
    "city": "SG",
    "zip": "12345",
    "country_id": 197,
    "title_id": 2,
    "tag_ids": [1, 4],
    "nationality_id": 197,
    "dob": "22/04/2000",
    "marital_status_key": "married",
    "highest_qualification_key": "degree",
    "languages_known_line": [
        {"id": 3, "language_id": 2, "spoken_key": "advance", "written_key": "intermediate"},
        {"language_id": 4, "spoken_key": "basic", "written_key": "basic"}
    ]
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Contact Person Details updated Successfully!"
        },
        "data": {}
    }
}
```

### Remarks

### ENCRYPTED API REQUESTS

### TO GET BENEFICIARY DETAILS API

Get Request Beneficiary Details.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_requests_beneficiary_data
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|request_id|String|Request unique id for beneficiary|


### Example

##### Request

```
{
  "params": {
    "request_id": 93
  }
}

```

##### Encrypted Request

```
{
  "params": {
    "encrypted_data": [
      "YOUR ENCRYTED BASE 64 DATA",
      "16 bit IV Key generated during encryption"
    ]
  }
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": ["YOUR ENCRYTED BASE 64 DATA",
        "16 bit IV Key generated during encryption"
    ]
}
```

#### Decrypted Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "beneficiary_info": [
                {
                    "contact_id": 133,
                    "contact_name": "test userrrr",
                    "contact_phone": "12345678",
                    "contact_mobile": "87654321",
                    "contact_email": "admin@example.com",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "SG",
                    "contact_zip": "12345",
                    "contact_country_id": 197,
                    "contact_country_name": "Singapore",
                    "contact_title_id": 2,
                    "contact_title_name": "Miss",
                    "contact_nationality_id": 197,
                    "contact_nationality_name": "Singapore",
                    "tag_ids": [
                        {
                            "id": 1,
                            "name": "Tag 1"
                        },
                        {
                            "id": 4,
                            "name": "Tag 4"
                        }
                    ],
                    "dob": "22/04/2000",
                    "marital_status_key": "married",
                    "marital_status": "Married",
                    "highest_qualification_key": "degree",
                    "highest_qualification": "Degree",
                    "languages_known_line": [
                        {
                            "languages_known_line_id": 9,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 10,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 11,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 12,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 13,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        }
                    ]
                }
            ]
        },
        "error": {}
    }
}
```

### Remarks

[The above encryption & decryption of data is implemented using AES encryption technique.](#data-encryption) 


### TO GET DONATION DETAILS API

Get Donations Donor Details.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donations_donor_data
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|donation_id|String|Donation unique id for beneficiary|


### Example

##### Request

```
{
  "params": {
    "donation_id": 58
  }
}

```

##### Encrypted Request

```
{
  "params": {
    "encrypted_data": [
      "YOUR ENCRYTED BASE 64 DATA",
      "16 bit IV Key generated during encryption"
    ]
  }
}
```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": ["YOUR ENCRYTED BASE 64 DATA",
        "16 bit IV Key generated during encryption"
    ]
}
```

#### Decrypted Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "donation_info": [
                {
                    "contact_id": 133,
                    "contact_name": "test userrrr",
                    "contact_phone": "12345678",
                    "contact_mobile": "87654321",
                    "contact_email": "admin@example.com",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "SG",
                    "contact_zip": "12345",
                    "contact_country_id": 197,
                    "contact_country_name": "Singapore",
                    "contact_title_id": 2,
                    "contact_title_name": "Miss",
                    "contact_nationality_id": 197,
                    "contact_nationality_name": "Singapore",
                    "tag_ids": [
                        {
                            "id": 1,
                            "name": "Tag 1"
                        },
                        {
                            "id": 4,
                            "name": "Tag 4"
                        }
                    ],
                    "dob": "22/04/2000",
                    "marital_status_key": "married",
                    "marital_status": "Married",
                    "highest_qualification_key": "degree",
                    "highest_qualification": "Degree",
                    "languages_known_line": [
                        {
                            "languages_known_line_id": 9,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 10,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 11,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 12,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        },
                        {
                            "languages_known_line_id": 13,
                            "language_id": 4,
                            "language_name": "Tamil",
                            "spoken_key": "basic",
                            "spoken": "Basic",
                            "written_key": "basic",
                            "written": "Basic"
                        }
                    ]
                }
            ]
        },
        "error": {}
    }
}
```
### Remarks

[The above encryption & decryption of data is implemented using AES encryption technique.](#data-encryption) 

# Donation API
### TO GET LIST OF DONATIONS API

To get the list of Donations (Monetary & Service & Tangible) based on Created Date in Asc Order.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donation_items_list
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|keyword_search|String|Search keyword for filteration of data|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "page": 2,
    "limit": 2
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "total_pages": 2,
            "total_count": 3,
            "max_records_for_page": 2,
            "current_page": 2,
            "count": 1,
            "donations_list": [
                {
                    "donation_id": 68,
                    "contact_id": 8,
                    "contact_name": "ABC Pte Ltd",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "contact_street": "",
                    "contact_street2": "",
                    "contact_city": "",
                    "contact_state_id": "",
                    "contact_zip": "",
                    "contact_country_id": "",
                    "donations_ref": "DI24050008-01",
                    "submission_date": "07/05/2024",
                    "responsible_id": 26,
                    "responsible_name": "John Doe",
                    "reviewers_remarks": "",
                    "donor_remarks": "",
                    "category_id": 7,
                    "category_name": "Mens Clothing",
                    "product_id": 13,
                    "product_name": "T-Shirt",
                    "donation_qty": 3,
                    "logistic_mode_key": "drop_off",
                    "logistic_mode": "Drop-Off Center",
                    "collection_point_id": 2,
                    "collection_point_name": "Tampines Grande"
                }
            ]
        }
    }
}
```
### Remarks




### TO REJECT SPECIFIC DONATION API

To Reject Specific Donation Item

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/reject_donation_items
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|donation_id|Integer|Request unique id for rejection |
|reviewers_remarks|String|Reviewers rejection remark|



### Example

##### Request

```
{
  "params": {
    "donation_id": 93,
    "reviewers_remarks": "test donation rejection"
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Donation Item Rejected Successfully!"
        },
        "data": {}
    }
}

```

### Remarks




#### TO  CANCEL SPECIFIC DONATION API

To Cancel Specific Donation Item

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/cancel_donation_items
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|donation_id|Integer|Request unique id for cancel |
|cancel_reason|String|Cancel reason for donation|



### Example

##### Request

```
{
  "params": {
    "donation_id": 93,
    "cancel_reason": "test donation cancel"
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Donation Item Cancelled Successfully"
        },
        "data": {}
    }
}

```

### Remarks


### TO GET DONATION ITEM PICTURES API

To get Donation Item pictures

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donation_item_pictures
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|donation_id|Integer|Request unique id for rejection |


### Example

##### Request

```
{
  "params": {
    "donation_id": 95
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "attachments_list": [
                "http://localhost:8704/web/content/813",
                "http://localhost:8704/web/content/814"
            ]
        }
    }
}

```

### Remarks


#### TO UPDATE DONATION ITEM PICTURES API

To update Donation Item pictures

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/update_donation_item_pictures
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Multi-Part Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|donation_id|Integer|Request unique id for rejection |
|attachment|File|Files to be uploaded |
|attachment_deletes|Array|List of attachment Ids to be deleted |


### Example

##### Request

```
Dart Code

var request = http.MultipartRequest('POST', Uri.parse('irrc/update_donation_item_pictures'));
request.fields.addAll({
  'donation_id': '95',
  'attachment_deletes': '[813, 818]'
});
request.files.add(await http.MultipartFile.fromPath('attachment', '/Users/directory/Downloads/home.png'));

```

##### Response

```
{
  "result": {
    "meta": {
      "status": true,
      "message": "Attachments Uploaded Successfully!"
    },
    "data": {}
  }
}

```

### Remarks



#### TO GET DONATION PRODUCT LIST API

To get Donation product list

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donations_products_list
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|donation_id|Integer|Request unique id for rejection |


### Example

##### Request

```
{
  "params": {
    "donation_id": 1
  }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": ""
        },
        "data": {
            "products_list": [
                {
                    "product_id": 23,
                    "product_name": "[HS00001] Kettle"
                },
                {
                    "product_id": 37,
                    "product_name": "[HS00002] Umbrella"
                }
            ]
        },
        "error": {}
    }
}

```

### Remarks



### TO UPDATE DONATION ITEM DATA API

To Update Donation Items Data.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/update_donation_items_data
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|product_id|Integer|Product unique id for donation|
|donation_qty|Integer|Donation quantity for donation|
|reviewers_remarks|String|Reviewers remarks for donation|
|logistic_mode_key|String|Logistic mode key for donation|
|collection_point_id|Integer|Collection point unique Id for donation|
|tag_ids|Array| Selection for new or high value |
|donation_id|Integer|Donation unique id |
|value|Integer|Donation amount |


### Example

##### Request

```
{
    "params": {
        "donation_id": 23,
        "product_id": 5,
        "tag_ids": [
            1,
            2
        ],
        "donation_qty": 2,
        "value": 0,
        "reviewers_remarks": "test review remarks",
        "logistic_mode_key": "drop_off",
        "collection_point_id": 2
    }
}

```

##### Response

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": true,
            "message": "Donation Item updated Successfully!"
        },
        "data": {}
    }
}

```

### Remarks


# API Error Response

Errors will be tracked & traced down in the Error node in the API Response.

```
{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": false,
            "message": ""
        },
        "data": {}
         error: {}
    }
}

```


# Data Encryption

### Encryption of Data

Package : https://pub.dev/packages/encrypt

```

// Package Imports
import 'package:encrypt/encrypt.dart' as ds;
import "dart:convert";

 // Shared Private Key for Encryption
 final key = ds.Key.fromBase64('YOUR BASE 64 STRING HERE');

 // Random Unqiue Key for Encryption
 final iv = ds.IV.fromSecureRandom(16);

 // Encryption process
 final encrypter = ds.Encrypter(ds.AES(key, mode: ds.AESMode.cbc));
 final encrypted = encrypter.encrypt('YOUR PLAIN TEXT', iv: iv);

 // Encrypted data
 String encryptedData = encrypted.base64;


```
### Decryption of Data

```
 // Shared Private Key for Decryption
 final key = ds.Key.fromBase64('YOUR BASE 64 STRING HERE'');

 // Random Unqiue Key for Decryption
 final iv = ds.IV.fromBase64('KEY PASSED DURING ENCRYPTION');

 // Decryption process
 final encrypter = ds.Encrypter(ds.AES(key, mode: ds.AESMode.cbc));

 // Decrypted data
 String decryptedData = encrypter.decrypt64('YOUR ENCRYPTED DATA', iv: iv);
      

```
