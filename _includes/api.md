# Online API

Here some help full Citybreak online API to be user via a CMS site.

## Linking API

Determine the link to a dynamic page irregardless of its language, there is an api endpoint available that either redirects or provides redirect information based on a query.

**Linking to products:**

``
https://[ONLINE-HOST]/[CULTURE]/link/product/[CBIS-PRODUCT-ID]
``

**Link to a supplier package**

``
https://[ONLINE-HOST]/[CULTURE]/link/packagelight/[SUPPLIER-PACKAGE-ID]
``

## Bookable status API

Online bookable status API  can be usefull to find out if a product is bookable or not via a simple call.
This can then be user to build a citybreak online widget in the CMS or similar to have a more dynamic implementation.

``
https://[ONLINE-HOST]/[CULTURE]/api/products/bookablestatus?cbisProductId=[CBIS-PRODUCT-ID]
``
