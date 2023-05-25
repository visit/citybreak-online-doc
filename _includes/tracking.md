# Tracking

Citybreak online tracing alternativs and technical information

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
> var booking = { "BookingCode": "ABCD12", "City": "asd", "Country": "SE", "State": "asd", "TotalAmount": "600.0", "TotalTax": "64.29", "Products": [{ "Id": "123456", "Name": "Hotell_name/room_name", "Category": "Accommodation/Hotelroom", "Price": "600.0", "Quantity": "1", "DocumentUrls": ["https://doc.citybreak.com/url-to-ticket"] }] };


```html

<script type="text/javascript" src="//citybreak.com/?value={bookingvalue}&cur={currency}&order={bookingcode}&rand={randomnumber}">
</script>

```

## Google tracking (GA4)

Citybreak online has support for google tracking.
* Google tag manager gtm.js (Not recomended)
* Google analytics 4 gtag.js
* Google tag manager (with ga4 datalayer) gtm.js

Events:
* [view_cart](#view_cart)
* [begin_checkout](#begin_checkout)
* [purchase](#purchase)
* remove_from_cart (soon avaliable - stay tuned)
* add_payment_info (soon avaliable - stay tuned)

A tracker property is implemented in Citybreak admin per online.
To add or remove your tracker propertys, contact our support with the [online id] or [url to the ecom] and the tracker property you want to add or remove.
_Example: "Please add this tracker property "G-[ID]" or GTM-[ID]" to onlineid: [add intentifier] OR url to citybreak online booking_

FYI:
* Google tracking is only avaliable in our production environment
* Avoid to add Google tracking scripts via your template page. To avoid risk of double tracking
* Questions related to the events we provied please contact our support.

### <a id="view_cart"></a> 'view_cart' - This event signifies that a user viewed their cart. 
Fires on .../basket

| Name     | Type   | Example value | Description                                                                   |
|----------|--------|---------------|-------------------------------------------------------------------------------|
| Currency | String | SEK           | Currency of the items associated with the event, in 3-letter ISO 4217 format. |
| value | Number | 1234.00           | Value of products in the cart |
| items    | Array - see Items below | 	    | 	The items for the event.                                                     |

Items parameters

| Name     | Type   | Example value | Description                                                                   |
|----------|--------|---------------|-------------------------------------------------------------------------------|
| item_id  | String | 123456           | Citybreak prodcut id |
| item_name    	| String | My product | 	Citybreak product system name                                               |
| price    	| Number | 1234.00 | 	Product price                                                                      |
| item_category     | String | Acommodation | 	Citybreak system category                                |
| item_category2    | String |  | 	                           |
| item_category3    | String |  | 	                               |
| item_category4    | String |  | 	                                |
| item_category5    | String |  | 	 |
| quantity    | Number | 1 	| 	Quantity of product                                           |
| affiliation    | String | 1234567890 | 	Citybreak online identifier id                                           |

Example output

			'event':"view_cart",
			'ecommerce': {
                            'currency': "SEK",
                            'items': [{
                    'item_name': "My product",
                    'item_id': "123456",                    
                    'price': 1234.00,
                    'item_category': "Acommodation",
                    'quantity': 1,
                    'affiliation': "1234567890"
                }

### <a id="begin_checkout"></a> 'begin_checkout' - This event signifies that a user has begun a checkout.
Event fires on .../paymentdetails

| Name     | Type   | Example value | Description                                                                   |
|----------|--------|---------------|-------------------------------------------------------------------------------|
| Currency | String | SEK           | Currency of the items associated with the event, in 3-letter ISO 4217 format. |
| value | Number | 1234.00           | Value of products in the cart |
| items    | Array - see Items below | 	    | 	The items for the event.                                                     |

Items parameters

| Name     | Type   | Example value | Description                                                                   |
|----------|--------|---------------|-------------------------------------------------------------------------------|
| item_id  | String | 123456           | Citybreak prodcut id |
| item_name    | String | My product | 	Citybreak product system name                                               |
| price    | Number | 1234.00 | 	Product price                                                                      |
| item_category     | String | Acommodation | 	Citybreak system category      |
| item_category2    | String |  | 	 |
| item_category3    | String |  | 	 |
| item_category4    | String |  | 	 |
| item_category5    | String |  | 	 |
| quantity    | Number | 1 | 	Quantity of product                            |
| affiliation    | String | 1234567890 | 	Citybreak online identifier id     |


Example output

			'event':"begin_checkout",
                        'ecommerce': {
                            'currency': "SEK",
                            'items': [{
                    'item_name': "My product",
                    'item_id': "123456",                    
                    'price': 1234.00,
                    'item_category': "Acommodation",
                    'quantity': 1,
                    'affiliation': "1234567890"
                }

### <a id="purchase"></a> 'purchase' - This event signifies when one or more items is purchased by a user.
Event fires 1 time on .../confirmation

| Name     | Type   | Example value | Description                                                                   |
|----------|--------|---------------|-------------------------------------------------------------------------------|
| transaction_id | string | ABCD12  | Booking number |
| value    | Number | 1234.00	    | 	Booking value                                                   |
| tax    | Number | 123.12	    | 	Booking tax value                                                   |
| Currency | String | SEK           | Currency of the items associated with the event, in 3-letter ISO 4217 format. |
| items    | Array - see Items below | 	    | 	The items for the event.                                        |

Items parameters

| Name     | Type   | Example value | Description                                                                   |
|----------|--------|---------------|-------------------------------------------------------------------------------|
| item_id  | String | 123456           | Citybreak prodcut id |
| item_name    | String | My product | 	Citybreak product system name                                               |
| price    | Number | 1234.00 | 	Product price                                                                   |
| item_category     | String | Acommodation | 	Citybreak system category                                 |
| item_category2    | String |  | 	|
| item_category3    | String |  | 	|
| item_category4    | String |  | 	|
| item_category5    | String |  | 	|
| quantity    | Number | 1 | 	Quantity of product                                           |
| affiliation    | String | 1234567890 | 	Citybreak online identifier id                                          |


Example output

			    'event': "purchase",
                            'ecommerce': {
                                'transaction_id': "ABCD12",
                                'value': 1234.00,
                                'tax': 123.12,
                                'currency': "SEK",
                                'items': [{
                    'item_id': "123456",
                    'item_name': "My product",
                    'item_category': "Acommodation",
                    'price': 1234.00,
                    'quantity': 1,
                    'affiliation': "1234567890"
                }


## Booking confimation urls

``https://[CB online url]/[Lang/Culture]/confirmation...``

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
