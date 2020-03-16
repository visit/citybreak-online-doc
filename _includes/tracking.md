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
[subdomain].[domain].[topdomain]/[culture]/[Citybreak guide]?tid=mytrackingkey
``

Widget link sample
``
[subdomain].[domain].[topdomain]/[culture]/[widgettype]/searchform?tid=mytrackingkey
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
{bookingJSONObject} | Booking information serialized as a JSON object, assign it to a javascript variable. If serialization fails 
{bookingJSONObject} | will be replaced by undefined, so guard for it.


> Example of {bookingJSONObject} usage: 
> 
> var booking = {bookingJSONObject};
> Will generate:
> var booking = { "BookingCode": "STRW85", "City": "asd", "Country": "SE", "State": "asd", "TotalAmount": 600.0, "TotalTax": 64.29, "Products": [{ "Id": 248466, "Name": "Hotell_name/room_name", "Category": "Accommodation/Hotelroom", "Price": 600.0, "Quantity": 1, "Start": new Date(1355698800000), "End": new Date(1355785200000), "SubProducts": [] }] };


```html

<script type="text/javascript" src="//citybreak.com/?value={bookingvalue}&cur={currency}&order={bookingcode}&rand={randomnumber}"></script>

```

## Google tracking

Citybreak online has build in standard support for google tracking.
* Google analytics ga.js
* Universal Analytics analytics.js
* Google tag manager gtm.js

_**NOTE: adding Google tracker id via your template page is not allowed. We what to avoid dubble tracking**_

We just need to add the google tracking id for you when implementing a new Citybreak online.
Need help to add this contact us!

FYI:
* We dont have anny google trackers active via our development ot tests enviromets. But we can setup a test online in product if requested.
* Missing something? Pleace contact us with specified sample of you needs or what your are missing and why you need if. Then we will consider developming support to our default feature set.

### Enhanced e-commerce

Citybreak has some support for enhance ecommerce and event tracking.

Citybreak online are able to keep track of user behaviour in Citybreak online web pages and send them to Universal Analytics account, by using Google Tag Manager container(s). Citybreak online supports single and multiple GTMs on page.
We keep track of the following GTM events:

1. Page View
2. Checkout Step
3. Checkout Step Option
4. Purchase

**Table1** describes pages where mentioned events are fired:

Page View | Checkout Step | Checkout Step Option |	Purchase
--------- | --------- | --------- | ---------
All pages (on load)	| Group Basket; (on load) | Payment Details* (on successfull form submit)	| Confirmation (on load)
 | Payment Details; (on load) | | 
 | Confirmation; (on load) | | 
 
**Payment details page may have 2 dimensions that are of interest: Payment Type (full payment, down payment ...) and Payment Option (VISA, Master, Paypal ...). We are firing GTM events for each of the present dimensions.**

### Setting up the UA account

If you already have UA account set up, you only need to set up a view so skip to step 5.

1. Sign in to your Google Marketing Platform and select product Analytics.
2. Under the Admin console create account, by giving it a name and saving it.
3. Create a property, by naming it. I suggest to enable user metrics in reporting.
4. Make a note of the **Tracking Id (UA-*******-**)** of your property. You will need it later. 
5. Create a view (or use the default one called All Web Site Data), by:
   * specifing the domain URL
   * Enable Ecommerce
   * Enable Enhanced Ecommerce Reporting
   * Add labels for Checkout process, just in order for you to keep track of steps.
     * /basket
     * /customerinformation
     * /confirmation  

![Sample](//visit.github.io/citybreak-online-doc/images/ga1.png "Sample")

### Setting up Google tag manager 

If you already have account set up, you can continue from step 2.
If you also have a container set up, you can continue from step 4.

![Sample](//visit.github.io/citybreak-online-doc/images/ga2.png "Sample")

1. Open Tag Manager and in Admin console create new account
2. Set up a container name and select Web
3. Switch to Workspace tab
4. Add Variables (name these to your liking or use the suggested ones - you will use them later on so make note):

**checkoutstepvalue:**
  * **Variable type:** Data Layer Variable
  * **Data Layer Variable Name:** ecommerce.checkout.actionField.step
  * **Data Layer Version:** Version 2
  
**checkoutoptionvalue:**
  * **Variable type:** Data Layer Variable
  * **Data Layer Variable Name:** ecommerce.checkout_option.actionField.option
  * **Data Layer Version:** Version 2
5. Add Triggers (name these to your liking or use the suggested ones):

**checkout:**
  * **Trigger type:** Custom Event
  * **Event name:** checkout
  * **Fires on:** Event equals checkout
  
**checkoutoption:**
  * **Trigger type:** Custom Event
  * **Event name:** checkoutOption
  * **Fires on:** Event equals checkoutOption
6. Add Tags (name these to your liking or use the suggested ones):

**cbonlinecheckout:**
  * **Tag Type:** Google Analytics - Universal Analytics
  * **Track Type:** Event
  * **Category:** checkout
  * **Action:** checkout_step_{{checkoutstepvalue}}
  * **Label:** {{checkoutoptionvalue}}
  * **Value:** {{checkoutoptionvalue}}
  * **Google Analytics Settings -> Enable overriding settings in this tag:** true
  * **Tracking ID:** your tracking ID from UA (UA-*******-**)
  * **More Settings -> Ecommerce -> Enable Enhanced Ecommerce Features:** True
  * **Use Data Layer:** Checked
  * **Firing Triggers -> Choose a trigger:** checkout
  * **Firing Triggers -> Choose a trigger:** checkoutoption (2 triggers for one tag)
  
**cbonlinepageview:**
  * **Tag Type:** Google Analytics - Universal Analytics
  * **Track Type:** Page View
  * **Google Analytics Settings -> Enable overriding settings in this tag:** true
  * **Tracking ID:** your tracking ID from UA (UA-*******-**)
  * **Firing Triggers -> Choose a trigger:** All Pages

![Sample](//visit.github.io/citybreak-online-doc/images/ga3.png "Sample")
![Sample](//visit.github.io/citybreak-online-doc/images/ga4.png "Sample")


### Reading the event data

Look at the Real-Time reports. Be aware that every dimension you select under Real-Time, will behave as a filter.
Behaviour -> Events -> Overview

![Sample](//visit.github.io/citybreak-online-doc/images/ga5.png "Sample")

* The Conversions -> Ecommerce -> Checkout Behaviour

![Sample](//visit.github.io/citybreak-online-doc/images/ga6.png "Sample")

**Need to add a tracker id or edit a exsiting one. Contact our support in we will help you**

### Purchase output sample

> Purchase event output sample

```html
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
    'price': '1234,00',
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
```
