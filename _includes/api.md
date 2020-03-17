# Online API

Here some help full Citybreak online API to be user via a CMS site.

## Linking API

Determine the link to a dynamic page irregardless of its language, there is an api endpoint available that either redirects or provides redirect information based on a query.

**Linking to products:**

``
https://{ONLINE-HOST}/en/link/product/{CBIS-PRODUCT-ID}
``

**Valid extra parameters**
* ?format=json
* ?format=xml

**Link to a supplier package**

``
https://{ONLINE3-HOST}/en/link/packagelight/{SUPPLIER-PACKAGE-ID}
``

## Bookable status API

Online bookable status API  can be usefull to find out if a product is bookable or not via a simple call.
This can then be user to build a citybreak online widget in the CMS or similar to have a more dynamic implementation.

Sample: 

``
https://{ONLINE-HOST}/en/api/products/bookablestatus/{CBIS-PRODUCT-ID}
``

> Sample output

```html

<BookableStatusResponse xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.datacontract.org/2004/07/Citybreak.Online3.Web.ApiModels.Products">
<BookingType>Todo</BookingType>
<Status>Online3</Status>
</BookableStatusResponse>
```
