# Tracking

Citybreak online tracking alternatives and technical information.

## Booking tracking ID

_(NOTE: This is a legacy feature and will be removed later on. This feature only works with redirect PSP integrations.)_

The booking tracking feature is a simple way for a client to track whether or not certain bookings were referred to by a tracking key.

A tracking key is a text string that can be any value, and may be provided through a direct link or within a widget.

Once a tracking key is set, it remains valid for 30 days unless the cookie is manually deleted. Every time a request is made with the same tracking key, the 30-day period will refresh and restart.

If a tracking key is already set, it will not be overridden by another key. The first key must expire before a new one can be applied.

Referral statistics can be obtained by creating one of the following reports in <https://reports.citybreak.com>:
* Product report
* Analysis per country

Within these reports, there is a column that represents the tracking key used at the booking level, if one was present.

Parameter:  
**?tid=[your value]**

Direct link sample  
```
//[online-host]/[culture]/[slug]?tid=mytrackingkey
```

## Custom conversion tracking

To make your script work for your organization, you need to configure it. Change the variables in your script using the variable names below. These custom scripts are added to the booking confirmation page.

Parameter | Description
--------- | --------- 
{bookingcode} | Booking number, e.g. ABCD12.
{bookingvalue} | Total sum of the customer's booking.
{customerfirstname} | Customer's first name
{customersurname} | Customer's surname
{randomnumber} | Generates a random number
{date} | Timestamp
{isodate} | Timestamp (yyyy-MM-dd)
{currency} | Currency
{zipcode} | Zip code
{bookingJSONObject} | Booking information serialized as a JSON object. Assign it to a JavaScript variable. If serialization fails, {bookingJSONObject} will be replaced with `undefined`, so ensure you check for it. Empty arrays are not serialized. All numbers are formatted as strings according to the customer’s language culture.

> Example of {bookingJSONObject} usage: 
> 
> var booking = {bookingJSONObject};
> Will generate:
> var booking = { "BookingCode": "ABCD12", "City": "asd", "Country": "SE", "State": "asd", "TotalAmount": "600.0", "TotalTax": "64.29", "Products": [{ "Id": "123456", "Name": "Hotell_name/room_name", "Category": "Accommodation/Hotelroom", "Price": "600.0", "Quantity": "1", "DocumentUrls": ["https://doc.citybreak.com/url-to-ticket"] }] };

```html
<script type="text/javascript" src="//citybreak.com/?value={bookingvalue}&cur={currency}&order={bookingcode}&rand={randomnumber}">
</script>
```

## Google tracking

Citybreak online Google tracking options:
* Google Analytics (gtag.js)
* Google Tag Manager (gtm.js)

```
Example of Google Analytics gtag.js

<!-- Begin - Google tag (gtag.js) and Google Analytics v4 DataLayer-->
<script type="text/javascript">
window.dataLayer = window.dataLayer || [];
function gtag() { dataLayer.push(arguments); }
gtag('js', new Date());
gtag('config', 'G-[ID]');
</script>
```

```
Example of Google Tag Manager gtm.js

<!-- Begin - Google Tag Manager v4 (gtm.js) DataLayer and Events-->
<script type="text/javascript">
(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
                                new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
                                j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
                                '//www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
                                })(window,document,'script','dataLayer','GTM-[ID]');
</script>
```

Events:
* [view_cart](#view_cart)
* [begin_checkout](#begin_checkout)
* [purchase](#purchase)
* [remove_from_cart](#remove_from_cart)
* [add_to_cart](#add_to_cart)
* [select_item](#select_item)

A tracker property is implemented in Citybreak Admin per online.  
To add or remove your tracker properties, contact our support with the [online ID] or [URL to the ecom] and the tracker property you want to add or remove.

_Example: "Please add this tracker property 'G-[ID]' or 'GTM-[ID]' to online ID: [add identifier] OR URL to Citybreak online booking."_

FYI:
* Google tracking is only available in our production environment.
* Avoid adding Google tracking scripts via your template page. (To avoid the risk of double tracking.)
* Questions or feature requests related to the events we provide? Please contact us.

Need help with Google tools or your metric plan?  
Don’t worry! Our tracker partner, BBO, is ready to assist you. Contact them at: kund-visit@bebetteronline.com

### <a id="view_cart"></a> view_cart - This event signifies that a user viewed their cart.  
Event fires on ``.../basket``

```
Example output

    'event': "view_cart",
    'ecommerce': {
        'currency': "SEK",
        'value': 1234.00,
        'items': [{
            'item_name': "My product",
            'item_id': "123456",
            'item_brand': "My supplier",
            'price': 1234.00,
            'item_category': "Accommodation",
            'quantity': 1,
            'affiliation': "1234567890"
        }]
    }
```

| Name       | Type   | Example value | Description                                                                   |
|------------|--------|---------------|-------------------------------------------------------------------------------|
| currency   | String | SEK           | Currency of the items associated with the event, in 3-letter ISO 4217 format. |
| value      | Number | 1234.00       | Value of products in the cart                                                 |
| items      | Array  | See Items     | The items for the event.                                                      |

Items parameters

| Name              | Type   | Example value | Description                                                                   |
|-------------------|--------|---------------|-------------------------------------------------------------------------------|
| item_id           | String | 123456        | Citybreak product ID                                                          |
| item_name         | String | My product    | Citybreak product system name                                                 |
| item_brand        | String | My supplier   | Citybreak supplier name                                                       |
| price             | Number | 1234.00       | Product price                                                                 |
| item_category     | String | Accommodation| System category                                                               |
| item_category2    | String |               |                                                                               |
| item_category3    | String |               |                                                                               |
| item_category4    | String |               |                                                                               |
| item_category5    | String |               |                                                                               |
| quantity          | Number | 1             | Quantity of product                                                           |
| affiliation       | String | 1234567890    | Citybreak online identifier ID                                                |
| item_package_id   | Number | 1234          | Citybreak dynamic package system ID OR iTicket bookingFlow system ID         |
| item_package_name | String | My Package    | Citybreak dynamic package system name OR iTicket bookingFlow system name     |

---

### <a id="begin_checkout"></a> begin_checkout - This event signifies that a user has begun a checkout.  
Event fires on ``.../paymentdetails``

```
Example output

    'event': "begin_checkout",
    'ecommerce': {
        'currency': "SEK",
        'value': 1234.00,
        'items': [{
            'item_name': "My product",
            'item_id': "123456",
            'item_brand': "My supplier",
            'price': 1234.00,
            'item_category': "Accommodation",
            'quantity': 1,
            'affiliation': "1234567890",
            "item_category": "Accommodation",      
            "item_category2": null,      
            "item_category3": null,      
            "item_category4": null,      
            "item_category5": null, 
            'item_package_id': "1234",
            'item_package_name': "My Package"
        }]
    }
```

| Name       | Type   | Example value | Description                                                                   |
|------------|--------|---------------|-------------------------------------------------------------------------------|
| currency   | String | SEK           | Currency of the items associated with the event, in 3-letter ISO 4217 format. |
| value      | Number | 1234.00       | Value of products in the cart                                                 |
| items      | Array  | See Items     | The items for the event.                                                      |

Items parameters

| Name              | Type   | Example value | Description                                                                   |
|-------------------|--------|---------------|-------------------------------------------------------------------------------|
| item_id           | String | 123456        | Citybreak product ID                                                          |
| item_name         | String | My product    | Citybreak product system name                                                 |
| item_brand        | String | My supplier   | Citybreak supplier name                                                       |
| price             | Number | 1234.00       | Product price                                                                 |
| item_category     | String | Accommodation| System category                                                               |
| item_category2    | String |               |                                                                               |
| item_category3    | String |               |                                                                               |
| item_category4    | String |               |                                                                               |
| item_category5    | String |               |                                                                               |
| quantity          | Number | 1             | Quantity of product                                                           |
| affiliation       | String | 1234567890    | Citybreak online identifier ID                                                |
| item_package_id   | Number | 1234          | Citybreak dynamic package system ID OR iTicket bookingFlow system ID         |
| item_package_name | String | My Package    | Citybreak dynamic package system name OR iTicket bookingFlow system name     |

---

### <a id="purchase"></a> purchase - This event signifies when one or more items are purchased by a user.  
Event fires 1 time on ``.../confirmation``

```
Example output

    'event': "purchase",
    'ecommerce': {
        'transaction_id': "ABCD12",
        'value': 1234.00,
        'tax': 123.12,
        'currency': "SEK",
        'items': [{
            'item_name': "My product",
            'item_id': "123456",
            'item_brand': "My supplier",
            'price': 1234.00,
            'item_category': "Accommodation",
            'quantity': 1,
            'affiliation': "1234567890",
            "item_category": "Accommodation",      
            "item_category2": null,      
            "item_category3": null,      
            "item_category4": null,      
            "item_category5": null, 
            'item_package_id': "1234",
            'item_package_name': "My Package"
        }]
    }
```

| Name            | Type   | Example value | Description                                                                   |
|------------------|--------|---------------|-------------------------------------------------------------------------------|
| transaction_id   | String | ABCD12        | Booking number                                                                |
| value            | Number | 1234.00       | Booking value                                                                 |
| tax              | Number | 123.12        | Booking tax value                                                             |
| currency         | String | SEK           | Currency in 3-letter ISO 4217 format                                          |
| items            | Array  | See Items     | The items for the event.                                                      |

Items parameters

| Name              | Type   | Example value | Description                                                                   |
|-------------------|--------|---------------|-------------------------------------------------------------------------------|
| item_id           | String | 123456        | Citybreak product ID                                                          |
| item_name         | String | My product    | Citybreak product system name                                                 |
| item_brand        | String | My supplier   | Citybreak supplier name                                                       |
| price             | Number | 1234.00       | Product price                                                                 |
| item_category     | String | Accommodation| System category                                                               |
| item_category2    | String |               |                                                                               |
| item_category3    | String |               |                                                                               |
| item_category4    | String |               |                                                                               |
| item_category5    | String |               |                                                                               |
| quantity          | Number | 1             | Quantity of product                                                           |
| affiliation       | String | 1234567890    | Citybreak online identifier ID                                                |
| item_package_id   | Number | 1234          | Citybreak dynamic package system ID OR iTicket bookingFlow system ID         |
| item_package_name | String | My Package    | Citybreak dynamic package system name OR iTicket bookingFlow system name     |

---

### <a id="remove_from_cart"></a> remove_from_cart - This event signifies when items are removed from `/basket` by a user.  
Event fires 1 time per user action on `/basket`

```
Example output

    'event': "remove_from_cart",
    'ecommerce': {
        'currency': "SEK",
        'value': 1234.00,
        'items': [{
            'item_name': "My product",
            'item_id': "123456",
            'item_brand': "My supplier",
            'price': 1234.00,
            'item_category': "Accommodation",
            'quantity': 1,
            'affiliation': "1234567890",
            "item_category": "Accommodation",      
            "item_category2": null,      
            "item_category3": null,      
            "item_category4": null,      
            "item_category5": null, 
            'item_package_id': "1234",
            'item_package_name': "My Package"
        }]
    }
```

| Name       | Type   | Example value | Description                                                                   |
|------------|--------|---------------|-------------------------------------------------------------------------------|
| currency   | String | SEK           | Currency in 3-letter ISO 4217 format                                          |
| value      | Number | 1234.00       | Booking value                                                                 |
| items      | Array  | See Items     | The items for the event.                                                      |

Items parameters

| Name              | Type   | Example value | Description                                                                   |
|-------------------|--------|---------------|-------------------------------------------------------------------------------|
| item_id           | String | 123456        | Citybreak product ID                                                          |
| item_name         | String | My product    | Citybreak product system name                                                 |
| item_brand        | String | My supplier   | Citybreak supplier name                                                       |
| price             | Number | 1234.00       | Product price                                                                 |
| item_category     | String | Accommodation| System category                                                               |
| item_category2    | String |               |                                                                               |
| item_category3    | String |               |                                                                               |
| item_category4    | String |               |                                                                               |
| item_category5    | String |               |                                                                               |
| quantity          | Number | 1             | Quantity of product                                                           |
| affiliation       | String | 1234567890    | Citybreak online identifier ID                                                |
| item_package_id   | Number | 1234          | Citybreak dynamic package system ID OR iTicket bookingFlow system ID         |
| item_package_name | String | My Package    | Citybreak dynamic package system name OR iTicket bookingFlow system name     |

---
### <a id="add_to_cart"></a> add_to_cart - This event signifies that a user has added their cart.  
Event fires on users action in the last step for the Dynamic Pakages and iTicket bookingFlow.

(Will soon be added for the Activity booking widget widget)

```
Example output

    'event': "add_to_cart",
    'ecommerce': {
        'currency': "SEK",
        'value': 1234.00,
        'items': [{
            'item_name': "My product",
            'item_id': "123456",
            'item_brand': "My supplier",
            'price': 1234.00,
            'item_category': "Accommodation",
            'quantity': 1,
            'affiliation': "1234567890",
            "item_category": "Accommodation",      
            "item_category2": null,      
            "item_category3": null,      
            "item_category4": null,      
            "item_category5": null, 
            'item_package_id': "1234",
            'item_package_name': "My Package"
        }]
    }
```

| Name       | Type   | Example value | Description                                                                   |
|------------|--------|---------------|-------------------------------------------------------------------------------|
| currency   | String | SEK           | Currency of the items associated with the event, in 3-letter ISO 4217 format. |
| value      | Number | 1234.00       | Value of products in the cart                                                 |
| items      | Array  | See Items     | The items for the event.                                                      |

Items parameters

| Name              | Type   | Example value | Description                                                                   |
|-------------------|--------|---------------|-------------------------------------------------------------------------------|
| item_id           | String | 123456        | Citybreak product ID                                                          |
| item_name         | String | My product    | Citybreak product system name                                                 |
| item_brand        | String | My supplier   | Citybreak supplier name                                                       |
| price             | Number | 1234.00       | Product price                                                                 |
| quantity          | Number | 1             | Quantity of product                                                           |
| affiliation       | String | 1234567890    | Citybreak online identifier ID                                                |
| item_category     | String | Accommodation| System category                                                               |
| item_category2    | String |               |                                                                               |
| item_category3    | String |               |                                                                               |
| item_category4    | String |               |                                                                               |
| item_category5    | String |               |                                                                               |
| item_package_id   | Number | 1234          | Citybreak dynamic package system ID OR iTicket bookingFlow system ID         |
| item_package_name | String | My Package    | Citybreak dynamic package system name OR iTicket bookingFlow system name     |

---

### <a id="select_item"></a> select_item - This event signifies users navigation per step in package bookingflows
Event fires on users action with in the Dynamic Pakages and iTicket bookingFlow.
Every step has 1 or 2 views depending on package/product configurations


```
Example output

  'event': "select_item",
  'ecommerce':{
      "package_step_name': "package step name",
      'package_step_index': "1",
        'items': [{
          'item_package_id': 1234,
          'item_package_name': "My package"
        }]
  }
```

| Name       | Type   | Example value | Description                                                                   |
|------------|--------|---------------|-------------------------------------------------------------------------------|
| package_step_name   | String        | My package step name | Citybreak dynamic package system step name OR iTicket bookingFlow slot name (on IT BF first click we will send "configuration" |
| package_step_index   | Number        | 1                    | Step index order, what step is this in the user booking journey for the package |

Items parameters

| Name              | Type   | Example value | Description                                                                   |
|-------------------|--------|---------------|-------------------------------------------------------------------------------|
| item_package_id   | Number | 1234          | Citybreak dynamic package system ID OR iTicket bookingFlow system ID         |
| item_package_name | String | My Package    | Citybreak dynamic package system name OR iTicket bookingFlow system name     |

---


## Booking confirmation URLs

```
//[online-host]/[culture]/confirmation...
```

Language | URL
--------- | -------------
sv        | /Bekraftelse
da        | /Bekraftelse
de        | /Bestaetigung
es        | /confirmacion
fi        | /vahvistus
fr        | /confirmation
it        | /conferma
nl        | /bevestiging
no        | /bekreftelse
pt        | /confirmacao
en        | /confirmation
Not in list | /confirmation

_Note: After /confirmation we add unique parameters to define the booking_
