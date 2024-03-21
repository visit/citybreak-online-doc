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

## Bookable status API

Online bookable status API  can be useful to find out if a product is bookable or not via a simple call.
This can then be used to build a citybreak online widget in the CMS or similar to have a more dynamic implementation.

``
//[online-host]/[culture]/api/products/bookablestatus?cbisProductId=[CBIS-PRODUCT-ID]
``
