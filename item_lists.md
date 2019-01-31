# Gravy Menu Import API

## Introduction

The Gravy backend stores **Schemas** that map Client **Item List** structures to Gravy's internal item
storage system.

Once a **Schema** is configured for a Client, then the Client can consume this API with the JSON structure
from their own system.

As an example, if a Client's **Item List** structure looks as follows:
    
    # Example item_list structure
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

The Gravy Menu Import API would consume this item_list and convert it into Gravy's storage system using the **Schema** associated with the client.

The response returns an exact instance of the **Item List** that is either 
passed into the request or stored in the Gravy Database, with customized dynamic prices
injected in.

## POST /item_lists

### Request

    POST /item_lists

#### Required Body Parameters:

| Parameter | Type | Description |
|:---|:---|---|
| `client_id` | String | ID relating to the client organization |
| `items_list` | Object | A JSON ItemList |
| `vendor.name` | String | The Name of the Vendor |
| `vendor_id` | String | The vendor selling the items in question |

#### Structure

    {
        client_id: [string:token - required]
        item_list: {
            ...
        }
        vendor: {
            name: [string - required]
        }
        vendor_id: [string - required] 
    }
 
#### Example
    
    {
        "client_id": "23fj3p4p0jeswcps04fw3pf0jw3p",
        "item_list": {
            "items": [
                {
                    "item_id": "ask73h1222d",
                    "value": 9.89,
                    "quantity": 1
                },
                {
                    "item_id": "62521gbjask73hd",
                    "value": 19.29,
                    "quantity": 2
                },
            ],
        },
        "vendor": {
            "name": "Joe's Burger Joint"
        },
        "vendor_id": "325dgyhu2jid2",
    }
    
### Response

A successful response will have a code of 204 NO CONTENT and an empty response body