# Widgets

Citybreak online comes with a set of standard widgets these widgets are fully customizable with its own CSS that can be sent in as a parameter, thus making it possible to change the style in different locations.

The widgets are JavaScript widgets that are easy to integrate with a few lines of code.

Make sure you only run ONE widget script at the time. 
If you need to have more then one widget on the same page/view you can load and unload the scripts to handle this.

## Implementation

To implement the widgets you need to add two things to your webpage:

1. A script tag that points to our server. Should be loaded asynchronously by using the below script added just before ``</head>``. Replace WIDGET_URL with a URL constructed according to instructions below.

```html
<script type="text/javascript">
        (function() {
              var widget = document.createElement('script'); widget.type = 'text/javascript'; widget.async = true;
               widget.src = 'https://[WIDGET_URL]';
              var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(widget, s);
        })();
</script>
```

2. A div tag somewhere in the document body with an id parameter for each widget. This is where the widget will be inserted into the document. There is a separate id for each widget, e.g:

``
<div id="citybreak_accommodation_searchform_widget"></div>
``

```html
<div id="citybreak_accommodation_searchform_widget"></div>
```

## Combine widget
The combine widget is located at: 
``
/combinewidget/combine
``

The combine widget requires three parameters:

**c=**

Controller - A list of names of controllers for the desired widgets, e.g. 
``
"c=accommodationwidget&c=basketwidget&c=ferrywidget"
``

**a=**

Action - A list of names of actions for the widget controllers specified in the "c" parameter, e.g. 
``
"a=searchform&a=basket&a=searchform"
``
This would pass "searchform" as an action to "accommodationwidget", "basket" as an action to "basketwidget" and "searchform" as an action to "ferrywidget".

**p=**

Parameters - A list of parameters to each widget action specified by the "c" and "a" parameters. To pass multiple parameters to a widget, use a semicolon-separated list of keys and values, e.g. 
``
"p=defaultCategoryId=1345;defaultRoomCfg=2&p=&p=alignDirection=2"
``
This would send defaultCategoryId=1345 and defaultRoomCfg=2 to /accommodationwidget/searchform, an empty list of parameters to /basketwidget/basket and "alignDirection=2" to /ferrywidget/searchform in the previous examples.

The parameters have to be passed in the correct order, i.e. the value of the first "a" parameter will be passed to the first "c" parameter and so on. The parameters must exactly match, i.e. if you have three controllers ("c" parameters) you have to pass three actions ("a" parameters) and three parameter values ("p" parameters).

> Combine widgets sample

```html
<script type="text/javascript">
        (function() {
              var widget = document.createElement('script'); widget.type = 'text/javascript'; widget.async = true;
               widget.src = 'https://[ONLINE-HOST]/combinewidget/combine?c=accommodationwidget&c=basketwidget&c=ferrywidget&a=searchform&a=minibasket&a=searchform&p=defaultCategoryId=1345;defaultRoomCfg=2&p=&p=alignDirection=2';
              var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(widget, s);
        })();
</script>
```

> Combine widget dive place holder sample

```html
<div id="citybreak_accommodation_searchform_widget"></div>
<div id="citybreak_basket_minibasket_widget"></div>
<div id="citybreak_ferry_searchform_widget"></div>
```

## Accommodation search widget
Script resource: 
``
/accommodationwidget/searchform
``

Div tag Id: 
``
citybreak_accommodation_searchform_widget
``

### Valid parameters
**string css**

URL to where the CSS can found, if not submitted the default CSS will be used.

**int? defaultCategoryId**

To set a default category on the widget, the Id category can be found in the dropdownlist of the widget, the category tree is administered in CBIS

**string defaultRoomCfg**

This is a string that can be set the default number of room/adults/children, the string is build up by using our format.

**PARAMETERS FOR NUMBER OF ROOMS/CABINS AND GUESTS**

You define the number of adults and children (including the child’s age) that will stay in each room as parameters in the direct search, so called ”Room configuration”. It can for example be a search with two rooms where the first room shall have two adults and the other room shall have one adult and a child with age 5.

**``“&pr”``**  is the base parameter for the room configuration that shall be searched.

**``“a“``** is the separator between adults and children.

**``“r“``** is the separator if the search is made on more rooms than one.

**``“c“``** is the separator if the search shall be made on more than one child.

**Example:**

   * One room with one adults is entered ``”&pr=1”``

   * Three  rooms with one adult in each room is entered ``“&pr=1r1r1“``

   * One room with one adult and one child (10 yrs) is entered ``“&pr=1a10“``

   * One room with one adult and two children (10, 12 yrs) is entered ``“&pr=1a10c12``

   * Two rooms with one adult and two children (10, 12 yrs) in the first room and two adults in the second room is entered ``“&pr=1a10c12r2“``

**DateTime? defaultArrivalDate**

A valid date to set the default arrival date in the widget, the format of the date must be the same as the format of the requested widget

**DateTime? defaultDepartureDate**

A valid date to set the default departure date in the widget, the format of the date must be the same as the format of the requested widget

**int? alignDirection**

Use this to position objects in the widget either to the left or to the right.

``0=objects`` will be aligned to the left (default)

``2=objects`` will be aligned to the right.

**int? geoNodeId**

Use this to set a default geo node in the widget, this parameter will render the name of the geonode in textbox “Where do you want to go”.

**int? cbispids**

Use this to set a default product in the widget, this parameter will render the name of the product in textbox “Where do you want to go”.

**bool? lockCategory**

Use this parameter to lock down the category dropdown, when this is set then the dropdown with the categories will be hidden, and the auto complete of the “where do you want to go” will only display objects that are of/has this category.

**String promotionCode**

Use this parameter if you want to set a promotion code in the promotion code field.

## Rental car widget
Script resource: 
``
/carrentalwidget/searchform
``

Div tag Id: 
``
citybreak_carrental_searchform_widget
``

### Valid parameters
**string css**

URL to where the CSS can found, if not submitted the default CSS will be used.

**int? alignDirection**

Use this to position objects in the widget either to the left or to the right.

``0=objects`` will be aligned to the left (default)

``2=objects`` will be aligned to the right.

## Ferry search widget
Script resource: ``/ferrywidget/searchform``

Div tag Id: ``citybreak_ferry_searchform_widget``

### Valid parameters
**string css**

URL to where the CSS can found, if not submitted the default CSS will be used.

**int? alignDirection**

Use this to position objects in the widget either to the left or to the right.

``0=objects`` will be aligned to the left (default)

``2=objects`` will be aligned to the right.

## Flight search widget
Script resource 
``
/flightwidget/searchform
``

Div tag Id: 
``
citybreak_flight_searchform_widget
``

### Valid parameters
**string css**

URL to where the CSS can found, if not submitted the default CSS will be used.

**int? alignDirection**

Use this to position objects in the widget either to the left or to the right.

``0=objects`` will be aligned to the left (default)

``2=objects`` will be aligned to the right.

**string defaultArrivalDate**

Use this to configure a default arrival date.

**string defaultDepartureDate**

Use this to configure a default departure date.

**bool? preselectFlexibleDates**

Use this to preselect flexible date search.

True = flexible date search is preselected

**int? preselectedEndLocationId**

Use this to preselect a end location id (aggregator location id).

**bool? lockEndLocation**

Use this to locked/disabled changing the end location.

True = changing end location is locked/disabled

**int? sgid**

Use this to preselect start location using a CBIS geonode id.

tring defaultArrivalDate

Use this to configure a default arrival date, example 2016-01-20 

## Basket widget
The basket widget can be used within or outside of the Citybreak online template page.

When the basket widget is to be used within the template the script tag must be omitted.

Script resource: ``/basketwidget/widget``

Div tag id: ``citybreak_basket_widget_summary``

optional trigger id: ``citybreak_basket_widget_display``

## Accommodation property / product widget
Script resource ``AccommodationPropertyWidget/searchform``

Div tag Id: ``citybreak_accommodation_property_widget``

```html
 <script type="text/javascript">
  (function() {
	try{
	var widget = document.createElement('script');
	widget.type = 'text/javascript';
	widget.async = true;
	widget.src = 'https://[WIDGET_URL]' + '?productid=123456';
	var s = document.getElementsByTagName('script')[0];
	s.parentNode.insertBefore(widget, s);
	} catch {return;} })();							
</script>

<div id="citybreak_accommodation_property_widget"></div>
```
#### Valid parameters
**int ProductId**

The CBIS id of the property/product to display the search form for.

## Activity transport product widget
Script resource ``activitytransportwidget/searchform``

Div tag Id: ``citybreak_activity_transport_searchform_widget``

```html
<script type="text/javascript">
	(function() { 		
	var widget = document.createElement('script'); widget.type = 'text/javascript'; widget.async = true;
        widget.src = 'https://[WIDGET_URL]' + '?cbisProductId=123456';		
        var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(widget, s);			
	})(); 
</script>

<div id="citybreak_activity_transport_searchform_widget"></div>
```

### Valid parameters
**int cbisProductId**

The id of the product to display the search form for.

**DateTime? preferedDate**

A valid date to set the default initially selected date in the widget, the format of the date must be the same as the format of the requested widget.

If the prefered date is not available it will fallback to default behaviour.

**int? preferredDeparture**

Id of the location that will be initially selected as departure location. If not available it will fallback to default behavior.

**int? preferredArrival**

Id of the location that will be initially selected as arrival location. If not available it will fallback to default behavior.

**bool? enablePromocode**

Whether  field for entering promocode will be available/visible in the widget. If not available, defaults to false.

**bool? proceedToBasket**

Whether to proceed to basket after booking. If not available, defaults to true.

### Booking event
Same as Booking event for Activity booking widget except the event is in this case ``'cb-activitytransport-booked'``.

## Activity product widget
This widget does not take a product id as parameter, instead you initialize it with javascript. This enables you to show multiple booking widgets on the same page.

Script resource 
``
activitywidget/booking
``

Div tag Id: 
``
citybreak_activity_booking_widget
``

### Valid parameters
**string css**

URL to where the CSS can found, if not submitted the default CSS will be used.

**Initialization**
To initialize a widget, create a container for the product and run initContainer with the required cbisProductId option.

```html
<script type="text/javascript">
  (function() {
   document.addEventListener('cb-activity-widget-loaded', function() {
       window.citybreakActivityBooking.initContainer(document.getElementById('activity_booking_widget-12345'), {
            cbisProductId: 12345
        });
       window.citybreakActivityBooking.initContainer(citybreakjq('#activity_booking_widget-67891'), {
            cbisProductId: 67891
        });
    }, false);
  })();
</script>
```

```html
<div id="citybreak_activity_booking_widget">
   <div id="activity_booking_widget-12345"></div>
   <div id="activity_booking_widget-67891"></div>
</div>
```

**Valid options to initContainer are:**

``
{
  cbisProductId: [required, int] a CBIS product id,
  proceedToBasket: [bool] whether to proceed to basket after booking, defaults to true,
  defaultDate: [date] a default selected date (Use JS new date format),
  startDate: [date] minimum selectable date,
  endDate: [date] maximum selectable date
}
``

### Booking event
You may also customize the booking process with the proceedToBasket option and cb-activity-booked event.

```html
<script type="text/javascript">
  (function() {
   document.addEventListener('cb-activity-booked', function(data) {
        console.log("Activity booked?: " + data.detail.success);
    }, false);
   document.addEventListener('cb-activity-widget-loaded', function() {
       window.citybreakActivityBooking.initContainer(document.getElementById('activity_booking_widget-12345'), {
            cbisProductId: 12345,
            proceedToBasket: false
        });
    }, false);
  })();
</script>
```

```html
<div id="citybreak_activity_booking_widget">
   <div id="activity_booking_widget-12345"></div>
</div>
```

**The cb-activity-booked event receives:**
``
detail: {
    cbisProductId: a CBIS product id of the booked product,
    basketProductIds: a list of resulting basket product ids,
    complementaryUrl: url to complementary page (will redirect to basket if no complementary options are available),
    success: [bool] whether the product was added successfully to basket
}
``
## Dynamic package widgets

Script and div resource differ per package type here is some samples

### Accommodation Todo package widget
Script resource differ per package type
``accommodationtodopackagewidget/searchform``

Div tag Id:
 ``citybreak_accommodation_todo_package_searchform_widget``

#### Valid parameters
**int cbisProductId**

The id of the product/package to display the search form for.

### Todo Todo package widget
Script resource differ per package type
``todotodopackagewidget/searchform``

Div tag Id:
 ``citybreak_todo_todo_package_searchform_widget``

#### Valid parameters
**int cbisProductId**

The id of the product/package to display the search form for.

### Accommodation Ferry package widget
Script resource differ per package type
``accommodationferrypackagewidget/searchform``

Div tag Id:
 ``citybreak_accommodation_ferry_package_searchform_widget``

#### Valid parameters
**int cbisProductId**

The id of the product/package to display the search form for.

```html
<script type="text/javascript">
    (function () {
        var widget = document.createElement('script');
        widget.type = 'text/javascript';
        widget.async = true;
        widget.src = '//[ONLINE-HOST]/[CULTURE]/accommodationferrypackagewidget/searchform?cbisProductId=[CBIS_ID]';
        var s = document.getElementsByTagName('script')[0];
        s.parentNode.insertBefore(widget, s);
    })();
</script>
        <div id="citybreak_accommodation_ferry_package_searchform_widget"></div>
```
