# IRRC Mobile API Documentation

### NOTE : ALL THE REQUESTS ARE POST REQUESTS (HTTP POST)

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
     - [Get Specific Item](#to-get-specific-request-item-api)
     - [Reject Specific Item](#to-reject-specific-request-item-api)
     - [Request Product List](#to-get-request-product-list-api)
     - [Cancel Specific Item](#to-cancel-specific-request-item-api)
     - [Item Availability](#to-get-request-item-availablilty-api)
     - [Collection Point List](#to-get-collection-point-details-api)
     - [Fulfillment Mode List](#to-get-request-fulfillment-mode-list-api)
     - [Request Tag List](#to-get-request-tags-api)
     - [Request Status List](#to-get-request-status-api)
     - [Request Beneficiary](#to-update-request-beneficiary-api)
     - [Update Item Data](#to-update-request-item-data-api)
- [Contact Person API](#contact-person-api)
     - [List of Person Title](#to-get-contact-person-title-api)
     - [List of Countries](#to-get-person-country-api)
     - [List of Languages](#to-get-person-languages-api)
     - [List of Person Tags](#to-get-person-tag-data-api)
     - [Update Contact Person](#to-update-contact-person-data-api)
     - [Encrypted API](#encrypted-api-requests)
          - [Beneficiary Details](#to-get-contact-person-title-api)
          - [Donor Details](#to-get-contact-person-title-api)
- [Donation Module API](#donation-api)
     - [List Of donation](#to-get-list-of-donations-api)
     - [Get donation details](#to-get-specific-donation-item-details-api)
     - [Get donation item pictures](#to-get-donation-item-pictures-api)
     - [Update Donation item pictures](#to-update-donation-item-pictures-api)
     - [List Of donation products](#to-get-donation-product-list-api)
     - [Donation Tag List](#to-get-donation-tag-list-api)
     - [Donation Status List](#to-get-donation-status-list-api)
     - [Donation Condition List](#to-get-donation-condition-list-api)
     - [Donation Logistic Mode List](#to-get-donation-logistic-mode-api)
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
      "base64 of 16 bit IV Key generated during encryption"
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
        "base64 of 16 bit IV Key generated during encryption"
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
      "base64 of 16 bit IV Key generated during encryption"
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
        "base64 of 16 bit IV Key generated during encryption"
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
|state_key|Array|Array of Status keys for filteration of data|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "state_key": ["review", "reject"],
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
            "total_pages": 3,
            "total_count": 28,
            "max_records_for_page": 10,
            "current_page": 2,
            "count": 10,
            "requests_list": [
                {
                    "request_id": 81,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040042-02",
                    "submission_date": "17/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 8,
                    "category_name": "Safety Clothes",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 82,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040043-01",
                    "submission_date": "17/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 5,
                    "category_name": "Laptops",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 83,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040043-02",
                    "submission_date": "17/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 12,
                    "category_name": "Mobile Phone",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 86,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040048-01",
                    "submission_date": "19/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 5,
                    "category_name": "Laptops",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 87,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040048-02",
                    "submission_date": "19/04/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "category_id": 7,
                    "category_name": "Mens Clothing",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 88,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040048-02",
                    "submission_date": "19/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 12,
                    "category_name": "Mobile Phone",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 93,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040046-01",
                    "submission_date": "23/04/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "category_id": -1,
                    "category_name": "",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 98,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040053-01",
                    "submission_date": "29/04/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "category_id": 12,
                    "category_name": "Mobile Phone",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 100,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040054-01",
                    "submission_date": "29/04/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "category_id": 4,
                    "category_name": "Events",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 102,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24050004-01",
                    "submission_date": "02/05/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 10,
                    "category_name": "Household",
                    "state_key": "review",
                    "state": "Review"
                }
            ]
        },
        "error": {}
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
|state_key|Array|Array of Status keys for filteration of data|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "state_key": ["review", "reject"],
    "page": 2,
    "limit": 5
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
            "total_pages": 6,
            "total_count": 26,
            "max_records_for_page": 5,
            "current_page": 2,
            "count": 5,
            "requests_list": [
                {
                    "request_id": 21,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040004-01",
                    "submission_date": "03/04/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "category_id": 7,
                    "category_name": "Mens Clothing",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 63,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040034-01",
                    "submission_date": "16/04/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "category_id": -1,
                    "category_name": "",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 80,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040042-02",
                    "submission_date": "17/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 12,
                    "category_name": "Mobile Phone",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 79,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040042-02",
                    "submission_date": "17/04/2024",
                    "responsible_id": -1,
                    "responsible_name": "",
                    "category_id": 7,
                    "category_name": "Mens Clothing",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 78,
                    "contact_id": -1,
                    "contact_name": "",
                    "contact_phone": "",
                    "contact_mobile": "",
                    "contact_email": "",
                    "request_ref": "RQ24040042-02",
                    "submission_date": "17/04/2024",
                    "responsible_id": 10,
                    "responsible_name": "Tiara Tan",
                    "category_id": 5,
                    "category_name": "Laptops",
                    "state_key": "review",
                    "state": "Review"
                }
            ]
        },
        "error": {}
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
|state_key|Array|Array of Status keys for filteration of data|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "state_key": ["review", "reject"],
    "page": 1,
    "limit": 5
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
            "total_pages": 1,
            "total_count": 2,
            "max_records_for_page": 5,
            "current_page": 1,
            "count": 2,
            "requests_list": [
                {
                    "request_id": 117,
                    "contact_id": 159,
                    "contact_name": "Mr webform donation tester 1",
                    "contact_phone": "",
                    "contact_mobile": "91866079",
                    "contact_email": "marco.applivon@test.com",
                    "request_ref": "RQ24050017",
                    "submission_date": "07/05/2024",
                    "responsible_id": 6,
                    "responsible_name": "Jessie Lim",
                    "category_id": 18,
                    "category_name": "Inspirre Store Booking (4 May 10am - 2pm)",
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "request_id": 118,
                    "contact_id": 160,
                    "contact_name": "Mr webform donation tester 1",
                    "contact_phone": "",
                    "contact_mobile": "91866079",
                    "contact_email": "marco.applivon@test.com",
                    "request_ref": "RQ24050018",
                    "submission_date": "07/05/2024",
                    "responsible_id": 6,
                    "responsible_name": "Jessie Lim",
                    "category_id": 18,
                    "category_name": "Inspirre Store Booking (4 May 10am - 2pm)",
                    "state_key": "review",
                    "state": "Review"
                }
            ]
        },
        "error": {}
    }
}
```

### Remarks


### TO GET SPECIFIC REQUEST ITEM API

To Get Specific Request Item

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
irrc/get_specific_request_items_details
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
|request_id|Integer|Request unique id for request details |


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
            "requests_details": {
                "request_id": 93,
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
                "request_ref": "RQ24040046-01",
                "submission_date": "23/04/2024",
                "responsible_id": -1,
                "responsible_name": "",
                "is_eligible": true,
                "reviewers_remarks": "",
                "beneficiary_remarks": "",
                "category_id": -1,
                "category_name": "",
                "request_qty": 1,
                "processed_qty": 1,
                "is_available": false,
                "is_allocated": false,
                "is_ready_to_process": false,
                "item_to_allocate_id": -1,
                "item_to_allocate_name": "",
                "fulfillment_mode_key": "collection_point",
                "fulfillment_mode": "Collection Point",
                "state_key": "review",
                "state": "Review",
                "collection_point_id": 2,
                "collection_point_name": "Tampines Grande",
                "collection_point_details": "Open during office hours only:\nMon - Fri : 9am - 5pm",
                "collection_appt": "",
                "eligibility_conditions": "",
                "eligibility_criteria_line": []
            }
        },
        "error": {}
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


### TO GET REQUEST TAGS API

Get Request tag list.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_requests_tags_list
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
            "tags_list": [
                {
                    "id": 1,
                    "name": "New"
                },
                {
                    "id": 2,
                    "name": "Used"
                },
                {
                    "id": 3,
                    "name": "Refurbished"
                }
            ]
        }
    }
}
```

### Remarks



### TO GET REQUEST STATUS API

Get Request status list.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_request_status_list
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
            "status_list": [
                {
                    "state_key": "new",
                    "state": "New"
                },
                {
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "state_key": "reject",
                    "state": "Reject"
                },
                {
                    "state_key": "in_queue",
                    "state": "In Queue"
                },
                {
                    "state_key": "ready_to_process",
                    "state": "Ready to Process"
                },
                {
                    "state_key": "processing",
                    "state": "Processing"
                },
                {
                    "state_key": "fulfilled",
                    "state": "Fulfilled"
                },
                {
                    "state_key": "cancel",
                    "state": "Cancelled"
                }
            ]
        }
    }
}
```

### Remarks


### TO GET REQUEST FULFILLMENT MODE LIST API

Get Fulfillment mode list.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_requests_fulfillment_mode
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
            "fulfillment_mode_list": [
                {
                    "fulfillment_mode_key": "collection_point",
                    "fulfillment_mode": "Collection Point"
                },
                {
                    "fulfillment_mode_key": "warehouse_collection",
                    "fulfillment_mode": "Warehouse Collection"
                },
                {
                    "fulfillment_mode_key": "deliver_to_beneficiary",
                    "fulfillment_mode": "Deliver to Beneficiary"
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
|collection_appt|DATETIME|Collection Date for item (UTC Datetime in String)|
|collection_point_id|Integer|Collection point unique id for Collection identification|
|request_id|Integer|Request unique id for Item eligibility|
|eligibility_criteria_line|Array|Array of Eligilibility condition question, response & remarks|



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
        "collection_point_id": 2,
        "eligibility_criteria_line": [
            {
                "eligibility_criteria_line_id": 2,
                "question": "Question 1",
                "response": "Response 1",
                "remarks": "Remark 1"
            },
            {
                "eligibility_criteria_line_id": 4,
                "question": "Question 2",
                "response": "Response 2",
                "remarks": "Remark 2"
            }
        ]
    }
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


### TO GET PERSON TAG DATA API

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
      "base64 of 16 bit IV Key generated during encryption"
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
        "base64 of 16 bit IV Key generated during encryption"
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
      "base64 of 16 bit IV Key generated during encryption"
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
        "base64 of 16 bit IV Key generated during encryption"
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
|state_key|Array|Array of State keys to filter the data accordingly|
|page|Integer|Page number for data paging|
|limit|Integer|Page Data limit for data paging|

### Example

##### Request

```
{
  "params": {
    "keyword_search": "",
    "state_key": ["review", "accept"],
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
            "total_pages": 5,
            "total_count": 9,
            "max_records_for_page": 2,
            "current_page": 2,
            "count": 2,
            "donations_list": [
                {
                    "donation_id": 3,
                    "contact_id": 8,
                    "contact_name": "ABC Pte Ltd",
                    "contact_phone": "",
                    "contact_mobile": "77776666",
                    "contact_email": "",
                    "donations_ref": "DI24050008-01",
                    "submission_date": "07/05/2024",
                    "responsible_id": 26,
                    "responsible_name": "John Doe",
                    "category_id": 7,
                    "category_name": "Mens Clothing",
                    "state_key": "accept",
                    "state": "Accepted"
                },
                {
                    "donation_id": 4,
                    "contact_id": 8,
                    "contact_name": "ABC Pte Ltd",
                    "contact_phone": "",
                    "contact_mobile": "77776666",
                    "contact_email": "",
                    "donations_ref": "DI24050008-02",
                    "submission_date": "13/05/2024",
                    "responsible_id": 6,
                    "responsible_name": "Jessie Lim",
                    "category_id": 5,
                    "category_name": "Laptops",
                    "state_key": "review",
                    "state": "Review"
                }
            ]
        },
        "error": {}
    }
}
```
### Remarks

### TO GET SPECIFIC DONATION ITEM DETAILS API

To get Specific Donation Item details

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_specific_donation_items_details
```

### Request headers

| Name | Value |
|:-----|:------|
|Content-Type|application/json|
|TOKEN|aqsw3sakskwj32kj3k2j33j2j3k23kj2k3j|

### Request body

| Parameter | Type | Description |
|:----------|:-----|:------------|
|donation_id|Integer|Donation unique id for donation details |




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
            "donations_details": {
                "donation_id": 1,
                "contact_id": 154,
                "contact_name": "Donor Mr Ali",
                "contact_phone": "",
                "contact_mobile": "99774455",
                "contact_email": "mrali@donor.com",
                "contact_street": "",
                "contact_street2": "",
                "contact_city": "",
                "contact_state_id": "",
                "contact_zip": "",
                "contact_country_id": "",
                "donations_ref": "DI24050006-01",
                "submission_date": "06/05/2024",
                "responsible_id": 6,
                "responsible_name": "Jessie Lim",
                "reviewers_remarks": "Excess Stock from warehouse. ",
                "donor_remarks": "Received and checked. No issue.",
                "category_id": 10,
                "category_name": "Household",
                "product_id": 37,
                "product_name": "[HS00002] Umbrella",
                "donation_qty": 4,
                "logistic_mode_key": "irr",
                "logistic_mode": "IRR Collect",
                "state_key": "accept",
                "state": "Accepted",
                "collection_point_id": 2,
                "collection_point_name": "Tampines Grande",
                "collection_appt": ""
            }
        },
        "error": {}
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
|donation_id|Integer|Donation unique id for rejection |
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


### TO GET DONATION LOGISTIC MODE API

Get Donations Logistic Mode values.

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donations_logistic_mode
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
            "logistic_mode_list": [
                {
                    "logistic_mode_key": "drop_off",
                    "logistic_mode": "Drop-Off Center"
                },
                {
                    "logistic_mode_key": "irr",
                    "logistic_mode": "IRR Collect"
                },
                {
                    "logistic_mode_key": "donor",
                    "logistic_mode": "Donor Deliver"
                }
            ]
        }
    }
}
```

### Remarks


### TO GET DONATION TAG LIST API

To Get Donations Tags Values

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donations_tags_list
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
                    "id": 1,
                    "name": "High Value"
                },
                {
                    "id": 2,
                    "name": "New"
                }
            ]
        }
    }
}
```

### Remarks


### TO GET DONATION STATUS LIST API

Get Donations Status Values

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donation_status_list
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
            "status_list": [
                {
                    "state_key": "new",
                    "state": "New"
                },
                {
                    "state_key": "review",
                    "state": "Review"
                },
                {
                    "state_key": "partial_reject",
                    "state": "Partial Rejected"
                },
                {
                    "state_key": "accept",
                    "state": "Accepted"
                },
                {
                    "state_key": "reject",
                    "state": "Rejected"
                },
                {
                    "state_key": "partial_disburse",
                    "state": "Partial Disbursed"
                },
                {
                    "state_key": "fully_disburse",
                    "state": "Fully Disbursed"
                },
                {
                    "state_key": "cancel",
                    "state": "Cancelled"
                }
            ]
        }
    }
}

```

### Remarks


### TO GET DONATION CONDITION LIST API

Get Donations Conditions Values

### Prerequisites
There is no Prerequistes for this API

### HTTP Request

```
/irrc/get_donation_conditions_list
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
            "conditions_list": [
                {
                    "condition_key": "new",
                    "condition": "New"
                },
                {
                    "condition_key": "mint",
                    "condition": "Mint"
                },
                {
                    "condition_key": "good",
                    "condition": "Good"
                },
                {
                    "condition_key": "average",
                    "condition": "average"
                },
                {
                    "condition_key": "poor",
                    "condition": "Poor"
                }
            ]
        }
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
|donation_id|Integer|Donation unique id for cancelletion |
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
|donation_id|Integer|Donation unique id |


### Example

##### Request

```
{
  "params": {
    "donation_id": 6
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
                {
                    "donation_id": 6,
                    "key": 809,
                    "value": "http://188.166.215.73:17004/web/content/809"
                },
                {
                    "donation_id": 6,
                    "key": 808,
                    "value": "http://188.166.215.73:17004/web/content/808"
                }
            ]
        },
        "error": {}
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
|donation_id|Integer|Donation unique id  |
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
|donation_id|Integer|Donation unique id|


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
|collection_appt|DateTime|Collection appointment date based on collection point option (UTC Date time in String)|
|tag_ids|Array| Selection for new or high value |
|donation_id|Integer|Donation unique id |
|value|Integer|Donation amount |
|condition_key|String|Condition key for recieved from get_donation_conditions_list API|


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
        "collection_appt": "17/05/2024 11:35:59",
        "condition_key":"mint"
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
    "data": {},
    "error": {
      "status_code": 400,
      "errors": [
        {
          "reason": "badRequest",
          "message": u"Request Item Record Not found!"
        }
      ]
    }
  }
}

```

### Example

```

{
    "jsonrpc": "2.0",
    "id": null,
    "result": {
        "meta": {
            "status": false,
            "message": ""
        },
        "data": {},
        "error": {
            "status_code": 404,
            "errors": [
                {
                    "reason": "notFound",
                    "message": "Donation Item Record Not found!"
                }
            ]
        }
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
