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

## Bookable status API

Online bookable status API  can be useful to find out if a product is bookable or not via a simple call.
This can then be used to build a citybreak online widget in the CMS or similar to have a more dynamic implementation.

_(NOTE: This is a legacy feature and will be removed later on.)_


``
//[online-host]/[culture]/api/products/bookablestatus?cbisProductId=[CBIS-PRODUCT-ID]
``
