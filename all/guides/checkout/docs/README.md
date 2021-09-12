SortOrder: 0
# Introduction

This is Loom-Auto CheckoutService.

## Permissions
Checkout can be created by
### Site member
`checkout.buyerInfo.memberId` will be set automatically.
- Same logged in site member can access it without permissions check.
- Anonymous visitors and different members will receive NOT_FOUND
- For other identities permissions will be checked (specific permissions depends on endpoint)

### Anonymous visitor
`checkout.buyerInfo.visitorId` will be set automatically.
- Any anonymous visitor can access it
- Any member can access it which means that after login buyer still can access his checkout.
After checkout first time accessed by member `checkout.buyerInfo.memberId` will be set and "Site member" rules will be applied.
- For other identities permissions will be checked (specific permissions depends on endpoint)

### User/Service/TPA with ECOM.MODIFY_CHECKOUTS permission
During creation `checkout.buyerInfo.id` can be provided. Access to checkout will be defined by it
- If `checkout.buyerInfo.memberId` set see "Site member" rules
- If `checkout.buyerInfo.anonymous: false` set then checkout can be access only after permissions check (means visitors/members cannot access it)
- If `checkout.buyerInfo.anonymous: true` set then checkout can be accessed by everyone. After it is first accessed by visitor or member `checkout.buyerInfo` will be updated and permissions will be applied according to "Site member" or "Anonymous visitor" rules


## Validations
### Create checkout
- ECOM.ADMIN_MODIFY_CHECKOUTS permission required to create checkout with `customLineItems` or/and `merchantDiscounts` 
- Checkout cannot be created without items: at least one item in `lineItems` or `customLineItems` must be provided
- `channelType` is required, UNSPECIFIED value not allowed
- `checkoutInfo.customFields.value` is required, null value not allowed
- It is allowed to provide `id` for `lineItems`/`customLineItems` but if you do so make sure that unique id provided for each item. If ids not provided they will be generated automatically

### Update checkout
-  ECOM.ADMIN_MODIFY_CHECKOUTS permission required to
    - Set `merchantDiscounts`
    - Update anything in `checkout.buyerInfo` other than `email`
- Update request should update something: either some fields in `checkout` or `giftCardCode`/`couponCode`/`merchantDiscounts`. It is possible to update all of them in same request but if nothing updated request will fail
- `checkoutInfo.customFields.value` is required, null value not allowed
- It is not allowed to remove `checkout.buyerInfo.email` once it is set
 

### Addresses
Related to `billingInfo` and `shippingInfo.shippingDestination`
- Either `address.addressLine` or `address.streetAddress` can be provided but not both
- `contactDetails.vatId` is optional but if you provide it make sure to provide `type`, UNSPECIFIED value not allowed
- In order to be compliant with GDPR we don't save PII data if we don't have clear way to identify owner of it.
It means that addresses can be saved only if:
    - checkout created/update by member (then we will save `buyerInfo.memberId`)
    OR
    - `buyerInfo.email` provided 
    OR
    - `buyerInfo.contactId` provided
    
### Create order
- Order will not be created if checkout changed after it was last time accessed (for example price of item changed, coupon expired and so on). We validate only total price at the moment 
- Order cannot be created if some of `checkout.lineItems` have `availability.status` NOT_FOUND or NOT_AVAILABLE. Please remove such items first using `RemoveLineItems` endpoint
- Order cannot be created if `checkout.calculationErrors` not empty
- If checkout has any shippable line item (see `checkout.lineItems.physicalProperties.shippable` property) then it also should have `checkout.shippingInfo.selectedCarrierServiceOption`.
Exemption: `channelType: POS`
- `checkout.billingInfo.contactDetails` required for channel type WIX_APP_STORE and WEB
- `paymentToken` required if `checkout.priceSummary.total.amount` greater than `checkout.giftCard.amount.amount` (or greater than 0 if `checkout.giftCard` not defined)

#### Subscription validations
If `checkout.lineItems.subscriptionOptionInfo` defined for any of items then next validations applied:
- Checkout should have only one line item
- Gift card cannot be applied
- Total price must be greater than 0 (see `checkout.priceSummary.total.amount` property)