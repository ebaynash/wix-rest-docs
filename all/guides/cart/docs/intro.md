SortOrder: 0
# About Cart API

The Cart services API is a part of the Wix eCommerce platform.
The API consists mainly of CRUD operations on cart line items and discounts.

- Create Cart - Create a new cart, with line items and optional discounts.
- Get Cart - Get a Cart by ID (returned by Create / Update Cart)
- Update Cart - Update cart fields.
    - Notice that line items and custom line items can only be overridden.
- Delete Cart - Delete a Cart by its ID.
- Add Line Items To Cart - Add catalog line items and custom line items to the Cart.
- Update Line Items Quantity - Update line items quantity by item IDs.
- Remove Coupon - Remove the Coupon that is applied on the Cart.
- Remove Line Items - Remove specific line items from the cart, by item IDs.
- Estimate Totals - Calculates the Cart's totals based on cartId, shipping option and buyer addresses.
    - Clarification: Cart does not calculate its totals automatically when each action made.
      Therefore, there need to call this endpoint in order to get calculated totals with discounts, shipping, tax etc.
- Create Checkout - Create a Checkout entity, based on the Cart's content.
    - If Checkout does not exist for this Cart, a new Checkout will be created.
    - If Checkout exists, this Checkout will be updated.