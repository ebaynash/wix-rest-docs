SortOrder: 1
# Example Flows

To retrieve an order's fulfillments, pass the `orderId` to the [List Fulfillments For Single Order](/docs/LINK) endpoint:

```sh
curl -X GET 'https://www.wixapis.com/ecom/v1/fulfillments/orders/{orderId}' \
    -H 'Content-Type: application/json' \
    -H 'Authorization: <AUTH>'
```

The response will contain the fulfillments associated with the order, including fulfillment IDs, line items, and shipment details:

        ```json
        {
          "orderWithFulfillments": {
            "orderId": "265c7d98-a7c3-48c4-89cd-bbdc00921eab",
            "fulfillments": [
              {
                "id": "80f939c8-cdc4-44fe-a058-b54d506af170",
                "createdDate": "2021-05-25T13:55:26.458Z",
                "lineItems": [
                  {
                    "id": "00000000-0000-0000-0000-000000000001",
                    "quantity": 2
                  }
                ],
                "trackingInfo": {
                  "trackingNumber": "12345",
                  "shippingProvider": "ups",
                  "trackingLink": "https://wwwapps.ups.com/WebTracking/track?track=yes&trackNums=12345"
                }
              },
              {
                "id": "eb9138ff-1490-4dbc-b053-743240b9ab8f",
                "createdDate": "2021-05-25T13:55:47.605Z",
                "lineItems": [
                  {
                    "id": "00000000-0000-0000-0000-000000000002",
                    "quantity": 3
                  }
                ],
                "trackingInfo": {
                  "trackingNumber": "12345",
                  "shippingProvider": "ups",
                  "trackingLink": "https://wwwapps.ups.com/WebTracking/track?track=yes&trackNums=12345"
                }
              }
            ]
          }
        }
        ```

To retrieve fulfillments for several orders, pass the `orderIds` to [List Fulfillments For Multiple Orders](/docs/LINK):

```sh
curl -X POST 'https://www.wixapis.com/ecom/v1/fulfillments' \
    --data-binary '{
          "orderIds": [
              "265c7d98-a7c3-48c4-89cd-bbdc00921eab",
              "d1748680-7fd5-401e-9f71-cd3b9ea70bdb"
          ]
    }'\
    -H 'Content-Type: application/json' \
    -H 'Authorization: <AUTH>'
```

The response will contain an array of fulfillments coupled with their respective order IDs:

        ```json
        {
          "ordersWithFulfillments": [
            {
              "orderId": "265c7d98-a7c3-48c4-89cd-bbdc00921eab",
              "fulfillments": [
                {
                  "id": "80f939c8-cdc4-44fe-a058-b54d506af170",
                  "createdDate": "2021-05-25T13:55:26.458Z",
                  "lineItems": [
                    {
                      "id": "00000000-0000-0000-0000-000000000001",
                      "quantity": 2
                    }
                  ],
                  "trackingInfo": {
                    "trackingNumber": "12345",
                    "shippingProvider": "ups",
                    "trackingLink": "https://wwwapps.ups.com/WebTracking/track?track=yes&trackNums=12345"
                  }
                },
                {
                  "id": "eb9138ff-1490-4dbc-b053-743240b9ab8f",
                  "createdDate": "2021-05-25T13:55:47.605Z",
                  "lineItems": [
                    {
                      "id": "00000000-0000-0000-0000-000000000002",
                      "quantity": 3
                    }
                  ],
                  "trackingInfo": {
                    "trackingNumber": "12345",
                    "shippingProvider": "ups",
                    "trackingLink": "https://wwwapps.ups.com/WebTracking/track?track=yes&trackNums=12345"
                  }
                }
              ]
            },
            {
              "orderId": "d1748680-7fd5-401e-9f71-cd3b9ea70bdb",
              "fulfillments": [
                {
                  "id": "9f6ff4c4-1fb2-4b0a-b433-32956052316c",
                  "createdDate": "2021-07-04T13:40:15.860Z",
                  "lineItems": [
                    {
                      "id": "00000000-0000-0000-0000-000000000001",
                      "quantity": 1
                    }
                  ],
                  "trackingInfo": {
                    "trackingNumber": "102030",
                    "shippingProvider": "dhl",
                    "trackingLink": "https://www.logistics.dhl/global-en/home/tracking.html?tracking-id=102030"
                  }
                }
              ]
            }
          ]
        }
        ```