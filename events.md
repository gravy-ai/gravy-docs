# Gravy Events API

## POST /events

### Request

    POST /events

#### Required Body Parameters:

| Parameter | Type | Description |
|:---|:---|---|
| `client_id` | String | ID relating to the client organization |
| `event_type` | String | The event type. One of `item_add_to_cart`, `item_purchase`, or `item_view` |
| `items.item_id` | String | ID mapping this item to the item in Gravy |
| `items.value` | Double | The price the user saw for this item |
| `items.quantity` | Integer | The quantity of items in cart (default to 1 if event is an `item_view`) |
| `vendor_id` | String | The vendor selling the items in question |


#### Optional Body Parameters :

| Parameter | Type | Description |
|:---|:---|---|
| `user_id` | String | ID relating to the user on the client |
| `test_id` | String | A UUID hex passed from the Pricing API in the `meta` object. Used to identify a user session. |

#### Structure

    {
        client_id: [string:token - required]
        event_type: [string - required]
        items: [
            {   
                item_id: [string - required]
                value: [double - required]
                quantity: [integer - required]
            }
        ]
        vendor_id: [string - required]
        user_id: [string]
        test_id: [string]
    }
 
#### Example
    
    {
        client_id: '23fj3p4p0jeswcps04fw3pf0jw3p',
        event_type: 'product_view',
        items: [
            {
                item_id: 'ask73h1222d',
                value: 9.89,
                quantity: 1
            },
            {
                item_id: '62521gbjask73hd',
                value: 19.29,
                quantity: 2
            },
        ],
        vendor_id: '325dgyhu2jid2',
        user_id: 'some_user_id',
        test_id: 'some_test_id'
    }
    
### Response

A successful response will have a code of 204 NO CONTENT and an empty response body