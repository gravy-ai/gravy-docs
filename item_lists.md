# Gravy Menu Import API

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