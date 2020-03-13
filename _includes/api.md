# Online API

DOCS IN PROGRESS

## Linking API

To be able to determine the link to a dynamic page irregardless of its language, there is an api endpoint available that either redirects or provides redirect information based on a query.

Linking to products:
´´
https://{ONLINE-HOST}/en/link/product/{CBIS-PRODUCT-ID}
´´

This will give a redirect to the correct url.
 
If the querystring ?format=json or format=html is appended, the correct link will be returned in json or xml respectively.

e.g

 https://www2.visittheuniverse.com/en/link/product/55221?format=json

result:
{
Url: "https://www2.visittheuniverse.com/en/accommodation/a55221/planet-earth-hotel/details",
Name: "Planet Earth Hotel",
Id: 55221
}
{
Url: "https://www2.visittheuniverse.com/en/accommodation/a55221/planet-earth-hotel/details",
Name: "Planet Earth Hotel",
Id: 55221
}
Link to a supplier package
 https://{ONLINE3-HOST}/en/link/packagelight/{SUPPLIER-PACKAGE-ID}

e.g

 https://www2.visittheuniverse.com/en/link/packagelight/22233?format=json

result:
{
Url: "https://www2.visittheuniverse.com/sv/boende/a1234/br%c3%b6sarps-g%c3%a4stgifveri-%26-spa/pl22233/supplierpackagedetails/my-weekend?propertyId=ptg-1111",
Name: "My Weekend package",
Id: 22233
}

## Bookable status API

Online bookable status API - with type - sample: https://www.kvitfjell.no/bestill/api/products/bookablestatus/1538217
