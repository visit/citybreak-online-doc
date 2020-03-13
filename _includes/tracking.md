# Tracking

## Booking tracking id

The reservation tracking feature is a simple way for a client to track whether or not certain reservations were referred to by a tracking key.

A tracking key is a text string which could be any value, it could be provided through a direct link or within a widget.

Direct link sample
online3.test.citybreak.com/501372096/en/en/accommodation?**tid=mytrackingkey**

Widget link sample
online3-next.citybreak.com/1795316478/sv/sv-se/eventwidget/searchform?tid=mytrackingkey
[subdomain].[domain].[topdomain]/[culture]/eventwidget/searchform?**tid=mytrackingkey**

Once a tracking key is set it will remain alive for 30 days unless the cookie is manually deleted, everytime a request is done with the same tracking key the period of 30 days will refresh and start over.

If an already existing tracking key is set it will never be overridden by another key, meaning that the first key must expire before a new one can be set.

Referral statistics can be obtained by creating one of following reports in <https://reports.citybreak.com>
* Product report
* Analysis per country

Within these reports there's a column which represents which tracking key was used on a booking level, if there was one present.

## Custom Conversion Tracking

To make your script work for your organization you need to configure it. To do so you need to change the variables in your script with the variable names below.

``{bookingcode} = Booking number, e.g. ABCD12
{bookingvalue} = Total sum of customers booking
{customerfirstname} = Customers first name
{customersurname} = Customers surname
{randomnumber} = Generates a random number
{date} = Time stamp
{isodate} = Time stamp (yyyy-MM-dd)
{currency} = Currency
{zipcode} = Zipcode
{bookingJSONObject} = Booking information serialized as a JSON object, assign it to a javascript variable. If serialization fails {bookingJSONObject} will be replaced by undefined, so guard for it.
Example of {bookingJSONObject} usage: 
var booking = {bookingJSONObject};
Will generate:
var booking = { "BookingCode": "STRW85", "City": "asd", "Country": "SE", "State": "asd", "TotalAmount": 600.0, "TotalTax": 64.29, "Products": [{ "Id": 248466, "Name": "Testhotell/Enkelrum test", "Category": "Accommodation/Hotelroom", "Price": 600.0, "Quantity": 1, "Start": new Date(1355698800000), "End": new Date(1355785200000), "SubProducts": [] }] };``


```html
<script type="text/javascript" src="//citybreak.com/?value={bookingvalue}&cur={currency}&order={bookingcode}&rand={randomnumber}"></script>
```

## Google tracking

General description

### Universal Analytics

### GTM
