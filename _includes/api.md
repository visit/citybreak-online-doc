# Online API

Some help full Citybreak online APIs you can use via a CMS site etc...

## Linking API

Determine the link to a dynamic page irregardless of its language, there is an api endpoint available that either redirects or provides redirect information based on a query.

**Linking to products:**

``
//[online-host]/[culture]/link/product/[CBIS-PRODUCT-ID]
``

**Link to a supplier package**

``
//[online-host]/[culture]/link/packagelight/[SUPPLIER-PACKAGE-ID]
``

**Link to the My Page login**

``
//[online-host]/[culture]/link/mypage?code=[CODE]&userName=[USERNAME]&redirectUrl=[RELATIVE-URL]
``

Logs a person in with the credentials from the magic link and redirects to `redirectUrl`. Used when integrating an external login (SSO).

[See information under login or click here](https://visit.github.io/citybreak-online-doc/#mypage_login_link)

## Session API

Returns the session key of the current visitor as a JSON string. The session key is the channel name used by the [booking events](https://visit.github.io/citybreak-online-doc/#booking_events).

``
//[online-host]/[culture]/session
``

## Basket API

Lets a CMS page work with the visitor's Citybreak Online basket. Both paths are the same in every language. Call them on the same online host and culture as your booking widgets, since the visitor's session is per culture.

**Basket id of the current visitor**

``
//[online-host]/[culture]/basket/id
``

Returns the basket id of the visitor's session as JSON, or an empty response when the visitor has no basket. Call it from the browser with `credentials: 'include'` so the session cookie is sent.

**Connect a Galaxy basket to the visitor**

``
//[online-host]/[culture]/basket/connect?basketId=[BASKET-ID]&sourceSessionId=[SESSION-ID]&returnUrl=[RELATIVE-URL]
``

Hands a basket created through the Galaxy API over to the visitor's session, so the booking widgets add to it and the checkout continues in Citybreak Online. Then redirects to `returnUrl`, a URL-encoded path on the same site, or to the basket page when it is left out. Works with GET or POST.

`basketId` and `sourceSessionId` are the `BasketId` and `SessionId` from Galaxy's Get Basket, and its `HybridCheckoutUrl` is this link ready-made. The session changes once the basket is connected, so build the link from a fresh Get Basket every time. [See the Galaxy hybrid checkout](https://visit.github.io/galaxy-docs/#create-basket-for-hybrid-checkout-in-citybreak-online3)

## Bookable status API

Online bookable status API  can be useful to find out if a product is bookable or not via a simple call.
This can then be used to build a citybreak online widget in the CMS or similar to have a more dynamic implementation.

_(NOTE: This is a legacy feature and will be removed later on.)_


``
//[online-host]/[culture]/api/products/bookablestatus?cbisProductId=[CBIS-PRODUCT-ID]
``
