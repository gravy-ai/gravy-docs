# Gravy Pricing API

## Introduction

The Gravy Pricing API exists to apply dynamic pricing rules in real time to consumers.
The Gravy backend stores **Schemas** that map Client **Item Lists** to Gravy's internal item
storage system.

The API then responds with item lists that are identical the Client's **Item List** data structure 
in order to reduce the complexity of an integration.

As an example, if a Client's **Item List** structure looks as follows:
    
    # Example item_list request
    {
        "items": [
            {
                "InternalID": "163412",
                "name": "Popular Item",
                "price": 9.55 
            },
            {...}
        ], 
    } 

The Gravy Pricing API would respond with items in the exact same format
with the dynamic prices injected in place of the initial price.

    # Example item_list response
    {
        "items": [
            {
                "InternalID": "163412",
                "name": "Popular Item",
                "price": 9.96 
            },
            {...}
        ], 
    }

The response returns an exact instance of the **Item List** that is either 
passed into the request or stored in the Gravy Database, with customized dynamic prices
injected in.


## GET vendors/_{vendor_id}_/item-list

If a vendor has an item list stored in Gravy, use this method to get 
the dynamically priced item list.

### Request

    GET /api/v1/vendors/[vendor_id]/item-list
    
#### Required Query Parameters:

| Parameter | Description |
| --- | --- |
| `vendor_id` | ID of the requested item list's vendor |

#### Optional Query Parameters:

| Parameter | Description |
| --- | --- |
| `user_id` | the ID of a specific user. This will be used to provide custom logic for returning/specific users. |

### Response

    {
	    meta: { 
	        test_id: [string:token]
        }
	    data: [string, JSON of item_list]
    }

| Parameter | Description |
| --- | --- |
| `meta` | Container for response metadata |
| `meta.test_id` | A UUID hex that is unique to each response the API generates. It is to be returned with the subsequent data events so we can tie those events to a specific session |
| `data` | A stringified JSON blob of the consumer's item list, where the prices have been adjusted based on the any tests running on that client |

#### Example Response:
    
    {
	    meta: {
		    "test_id": "23fj3p4p0jeswcps04fw3pf0jw3p",
	    },
	    data: {...}
    }
    
## POST vendors/_{vendor_id}_/item-list

If a vendor **does not** have an item list stored in Gravy, use this method and
pass in the item_list as a parameter to get the dynamically priced item list.

### Request

    POST /api/v1/vendors/[vendor_id]/item-list
    
#### Required Query Parameters:

| Parameter | Description |
| --- | --- |
| `vendor_id` | ID of the requested item list's vendor |

#### Required Body Parameters:

| Parameter | Description |
| --- |--- |
| `item_list` | A JSON ItemList. This will be used instead of the stored item list for the vendor, and pricing changes will be injected into this object instead |

#### Optional Body Parameters:

| Parameter | Description |
| --- | --- |
| `user_id` | the ID of a specific user. This will be used to provide custom logic for returning/specific users. |

### Response

    {
	    meta: { 
	        test_id: [string:token]
        }
	    data: [string, JSON of item_list]
    }

| Parameter | Description |
| --- | --- |
| `meta` | Container for response metadata |
| `meta.test_id` | A UUID hex that is unique to each response the API generates. It is to be returned with the subsequent data events so we can tie those events to a specific session |
| `data` | A stringified JSON blob of the consumer's item list, where the prices have been adjusted based on the any tests running on that client |

#### Example Response:
    
    {
	    meta: {
		    "test_id": "23fj3p4p0jeswcps04fw3pf0jw3p",
	    },
	    data: {...}
    }
