# Tracking

Citybreak online support the basic google tracking and has a few custom build options that can be used.

## Booking tracking id

The booking tracking feature is a simple way for a client to track whether or not certain bookings were referred to by a tracking key or not.

A tracking key is a text string which could be any value, it could be provided through a direct link or within a widget.

Once a tracking key is set it will remain alive for 30 days unless the cookie is manually deleted, everytime a request is done with the same tracking key the period of 30 days will refresh and start over.

If an already existing tracking key is set it will never be overridden by another key, meaning that the first key must expire before a new one can be set.

Referral statistics can be obtained by creating one of following reports in <https://reports.citybreak.com>
* Product report
* Analysis per country

Within these reports there's a column which represents which tracking key was used on a booking level, if there was one present.

Paramerter:
**?tid=[your value]**

Direct link sample
``
https://[ONLINE-HOST]/[culture]/[Citybreak guide]?tid=mytrackingkey
``


Widget link sample
``
https://[ONLINE-HOST]/[culture]/[widgettype]/searchform?tid=mytrackingkey
``

## Custom conversion tracking

To make your script work for your organization you need to configure it. To do so you need to change the variables in your script with the variable names below. This custum scripts are added to the booking confirmaiton page.


Parameter | Description
--------- | --------- 
{bookingcode} | Booking number, e.g. ABCD12.
{bookingvalue} | Total sum of customers booking.
{customerfirstname} | Customers first name
{customersurname} | Customers surname
{randomnumber} | Generates a random number
{date} | Time stamp
{isodate} | Time stamp (yyyy-MM-dd)
{currency} | Currency
{zipcode} | Zipcode
{bookingJSONObject} | Booking information serialized as a JSON object, assign it to a javascript variable. If serialization fails {bookingJSONObject} will be replaced by undefined, so guard for it. Empty arrays are not serialized. All numbers are formatted as strings to the customer language culture.


> Example of {bookingJSONObject} usage: 
> 
> var booking = {bookingJSONObject};
> Will generate:
> var booking = { "BookingCode": "STRW85", "City": "asd", "Country": "SE", "State": "asd", "TotalAmount": "600.0", "TotalTax": "64.29", "Products": [{ "Id": "248466", "Name": "Hotell_name/room_name", "Category": "Accommodation/Hotelroom", "Price": "600.0", "Quantity": "1", "DocumentUrls": ["https://doc.citybreak.com/url-to-ticket"] }] };


```html

<script type="text/javascript" src="//citybreak.com/?value={bookingvalue}&cur={currency}&order={bookingcode}&rand={randomnumber}"></script>

```

## Google tracking

Citybreak online has standard support for google tracking.
* Google analytics ga.js (depricated)
* Universal Analytics analytics.js (depricated by google July 1, 2023)
* Google tag manager gtm.js
* Google analytics 4 gtag.js **SOON AVAILABLE**
* Google tag manager (with ga4 datalayer) gtm.js **SOON AVAILABLE**

_**NOTE: adding Google tracker property id via your template page is not allowed. We what to avoid dubble tracking**_

We just need to add the google tracking property id for you when implementing a new Citybreak online.
Need help to add this contact us!

FYI:
* We dont have any google trackers active via our development or tests environments. But we can setup a test online in product if requested.
* Missing something? Please contact us with specified sample of you needs or what your are missing and why you need if. Then we will consider developing support to our default feature set.

## Goolge Purchase output sample (will soon be updated with GA4 format)

> Purchase event output sample

```html
<script>
citybreak0dataLayer = [{
'onlineGuide': '[citybreak_online_id]',
'organizationId': '[citybreak_organization_id]',
'culture': 'en-GB'
}];

if (shouldSendCheckoutTrackingGTMCookie === 'true') {
 citybreak0dataLayer.push({
 'ecommerce': {
  'checkout': {
   'actionField': {
    'step': 1
    },
   'currencyCode': 'SEK',
   'products': [{
    'name': "Hotel_name/room_name",
    'id': '******',                    
    'price': '1234.00',
    'category': "Accommodation/Room",
    'quantity': 2
    }]
   }
  }
 },
 {
 'event': 'checkout',
 'eventCallback': function() {
   console.log('Checkout event has fired');
  }
 });
}
(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
                               new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
                                j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
                               '//www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
                                })(window,document,'script','citybreak0dataLayer','GTM-[tracker_id]');
 </script>
```
## Booking confimation urls

``http(s)://[CB online url]/[Lang/Culture]/confirmation...``

Language | url
--------- | ---------
sv | /Bekraftelse
da | /Bekraftelse
de | /Bestaetigung
es | /confirmacion
fi | /vahvistus
fr | /confirmation
it | /conferma
nl | /bevestiging
no | /bekreftelse
pt | /confirmacao
en | /confirmation
Not in list | /confirmation

_Note: After /confirmation we add unique parameters to define the booking_
