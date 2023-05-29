# Widgets

Citybreak online comes with a set of standard widgets in relation to the implementation.
The widgets are JavaScript widgets that are easy to integrate with a few lines of code.

All widget got a sctipt tag loaded asynchronously
Example script:
```html
<script async type="text/javascript" src="//[online-host]/[culture]/...
</script>
```
And a div tag that that you add where the widget will be inserted into the page.
Example div:
``
<div id="[id needed for widget]"></div>
``
See example for the widget you need below.

FYI:
- Make sure you only run ONE widget script at the time. 
- Don´t load a widget scripts on your tempalte page. This will affect the booking controlles and create possible conflicts.
- Never use CSS overrides on the widget since the CSS are controlled from the impementaion.
_(if you want to use custom CSS this should be loaded via CSS parameter and the url where you host the CSS)_

### Widget types

- [Searchforms widgets](#Searchforms)
- [Combine widgets](#Combine)
- [product & package widgets](#product_package)
- [Basket widget](#Basket)

## <a id="Searchforms"></a> Searchform widgets - Used for a search or filtering for prodcuts per of guide.

Searchform widget are user if you want to have a singel searchform widget loaded on the page. 
(if you need to load 2 widget on 1 page see combine widget (LINK))

### Accommodation searchform
```html
Accommodation searchform example:
<div id="citybreak_accommodation_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationwidget/searchform">
</script>
```
Use for multi property accommodation, search will target

| Parameter       	   |type    | Example value  | Description                                                                             |
|----------------------|--------|----------------|-----------------------------------------------------------------------------------------|
| defaultCategoryId    | int    | 123456   	     | Set default category in the widget. CBIS category id is needed.						   |
| lockCategory		   | Bool   | true   	     | Use this parameter to lock down the category dropdown, when this is set then the dropdown with the categories will be hidden.|
| geoNodeId		       | int    | 123456   	     | Set default geonode in the widget. CBIS geonode id is needed.						   |
| cbispids		       | int    | 123456   	     | Set default products in the widget. CBIS prodcut id is needed.						   |
| defaultArrivalDate   | Date   | 2023-03-12     | A valid date to set the default arrival date in the widget, the format of the date must be the same as the format of the requested widget|
| defaultDepartureDate | Date   | 2023-03-13	 | A valid date to set the default departure date in the widget, the format of the date must be the same as the format of the requested widget|
| promotionCode	       | String | Promo_2023     | Use this parameter if you want to set a promotion code in the promotion code field.	   |
| css 			       | 		| [url]			 | Add absolute url to you custom hosted CSS.											   |


### Parameter for number of rooms and guests
You define the number of adults and children (including the child’s age) that will stay in each room as parameters in the direct search, so called ”Room configuration”. It can for example be a search with two rooms where the first room shall have two adults and the other room shall have one adult and a child with age 5.

| Parameter |type    | Example value  							1					| Description                                                                             |
|-----------|--------|--------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| &pr    	| String | &pr=1 (One room with one adults is entered)| This is the base parameter for the room configuration that shall be searched.|
| a		    | String | &pr=1a10 (One room with one adult and one child (10 yrs) is entered)| The separator between adults and children.|
| r		    | String | &pr=1r1r1 (One room with one adult and two children (10, 12 yrs) is entered)| The separator if the search is made on more rooms than one.|
| c		    | String | &pr=1a10c12(Two rooms with one adult and two children (10, 12 yrs) in the first room and two adults in the second room is entered)| The separator if the search shall be made on more than one child.|

### Activity searchform
```html 
Activity searchform example: 
<div id="citybreak_activity_searchform_widget"></div> 

<script async type="text/javascript" src="//[online-host]/[culture]/activitywidget/searchform">
</script>
```
Use for multi product todos, search/fitler will target

### Ferry searchform
```html
Ferry searchform example:
<div id="citybreak_ferry_searchform_widget"></div> 

<script async type="text/javascript" src="//[online-host]/[culture]/ferrywidget/searchform">
</script>
```
Use for external ferry search

### Flight searchform
```html
Flight searchform example:
<div id="citybreak_flight_searchform_widget"></div> 

<script async type="text/javascript" src="//[online-host]/[culture]/flightwidget/searchform">
</script>
```
Use for external flight search

| Parameter       	   |type    | Example value  | Description                                                                             |
|----------------------|--------|----------------|-----------------------------------------------------------------------------------------|
| defaultArrivalDate   | String | 2023-03-12     | Set default default arrival date.													   |
| defaultDepartureDate | String | 2023-03-13     | Set default default departure date.													   |
| preselectFlexibleDates | Bool | True           | Use to preselect flexible date search.										       	   |
| preselectedEndLocationId | Int| 123456         | Use to preselect a end location id (Travelswitch(agregatror) location id).		   	   |
| lockEndLocation 	   | Bool   | True      	 | Use to locked/disabled changing the end location. 								   	   |
| sgid 	   			   | Int    | 123456      	 | Use to preselect start location using a CBIS geonode id.						   		   |
| css 			       | 		| [url]			 | Add absolute url to you custom hosted CSS.											   |

### Carrental searchform
```html
Carrental searchform example:
<div id="citybreak_carrental_searchform_widget"></div> 

<script async type="text/javascript" src="//[online-host]/[culture]/carrentalwidget/searchform">
</script>
```
Use for external carrental search

### Public transport searchform
```html
Public Transport searchform example:
<div id="citybreak_publictransportwidget_searchform_widget"></div> 

<script async type="text/javascript" src="//[online-host]/[culture]/publictransportwidget/searchform">
</script>
```
Use for external public transport search

## <a id="Combine"></a> Combine widget - Used if you want to load 2 or more widgets on the same page.
```html
Combine Accommodation and ferry searchform example:
<div id="citybreak_accommodation_searchform_widget"></div>
<div id="citybreak_ferry_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/combinewidget/combine?c=accommodationwidget&c=ferrywidget&a=searchform&a=searchform&p=defaultCategoryId=1345;defaultRoomCfg=2&p=alignDirection=2">
</script>
```
You have 3 parameters what has to be included.

| Type 		 |Parameter | Example value 											   | Description                                                                  |
|------------|----------|--------------------------------------------------------------|------------------------------------------------------------------------------|
| Controller | c= 		| c=accommodationwidget&c=ferrywidget 						   | Names of controllers for the desired widgets                                 |
| Action 	 | a= 		| a=searchform&a=searchform 								   | Names of actions for the widget controllers specified in the "c" parameter   |
| Parameter  | p= 		| p=defaultCategoryId=1345;defaultRoomCfg=2&p=alignDirection=2 | Parameters to each widget action specified by the "c" and "a" parameters. To pass multiple parameters to a widget, use a semicolon-separated list of keys and values |

## <a id="product_package"></a> Product & package widgets - Used to load a product or package booking widget

### Activity & merchandise product widget
```html
Activity product example:
<div id="citybreak_activity_booking_widget"></div>
<div id="activity_booking_widget-[ID]"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/activitywidget/booking"></script>
<script type="text/javascript">
    document.addEventListener('cb-activity-widget-loaded', function() {
      console.log('Activity booking widget loaded');
        window.citybreakActivityBooking.initContainer(document.getElementById('activity_booking_widget-[ID]'), {
          cbisProductId: [ID],
          proceedToBasket: true
        });
    }, false);
 </script>
```
Activity & merchandise product booking widget - load one per page. (you can load multipe products in one script if needed.)

| Parameter       |type  | Example value  | Description                                                                             |
|-----------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId  | Int  | 123456   	  | CBIS product id, We reccomend that you keep this ID on all elements See [ID] in example.|
| proceedToBasket | Bool | true (or false)| Use to proceed to basket(checkout) or stay on widget page?  	  					    |
| css 			  |      | [url]		  | Add absolute url to you custom hosted CSS.												|
| defaultDate	  | Date | 2023-06-11     | Use JavaScript "new" date format, default selected date									|
| startDate 	  | Date | 2023-07-01     | Use JavaScript "new" date format, widget start date selectable date						|
| endDate	 	  | Date | 2023-07-01     | Use JavaScript "new" date format, maximum selectable date								|

*cbisProductId is requierd 

### Booking event listner for Activity
You may also customize the booking process with the proceedToBasket option and 'cb-activity-booked' event.
*The cb-activity-booked event receives:*
cbisProductId: a CBIS product id of the booked product, basketProductIds: a list of resulting basket product ids, complementaryUrl: url to complementary page (will redirect to basket if no complementary options are available), success: [bool] whether the product was added successfully to basket

### iTicket Activity Transport widget
```html
iTicket Activity Transport example:
<div id="citybreak_activity_transport_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/activitytransportwidget/searchform?cbisProductId=[ID]">
</script>
```
Use for iticket transport products.

| Parameter       	 |type  | Example value  | Description                                                                             |
|--------------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId     | Int  | 123456   	     | CBIS product id, product to display the widget.										   |
| proceedToBasket 	 | Bool | true (or false)| Use to proceed to basket(checkout) or stay on widget page?    						   |
| css 			  	 |      | [url]		     | Add absolute url to you custom hosted CSS.											   |
| preferredDate	  	 | Date | 2023-06-11     | A valid date to set the default initially selected date in the widget, the format of the date must be the same as the format of the requested widget. If the preferred date is not available it will fall back to default behavior.|
| preferredDeparture | Date | 2023-06-11     | Id of the location that will be initially selected as departure location. If not available it will fallback to default behavior.|
| preferredArrival 	 | Date | 2023-07-01     | Id of the location that will be initially selected as arrival location. If not available it will fallback to default behavior.|
| enablePromocode	 | Bool | true (or false)| Whether field for entering promocode will be visible in the widget. If parameter is not added widget defaults to false.|

*cbisProductId id requierd 

### Booking event listner for iTicket Activity Transport
You may also customize the booking process as the with the proceedToBasket option and 'cb-activitytransport-booked'.

### Accommodation product widget
```html
Accommodation prodcut example:
<div id="citybreak_accommodation_property_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationPropertyWidget/searchform?productid=[ID]">
</script>
```
Use for one accommodation property.

| Parameter       	 |type  | Example value  | Description                                                                             |
|--------------------|------|----------------|-----------------------------------------------------------------------------------------|
| *productId         | Int  | 123456   	     | CBIS product id, product to display the widget. You can only use one product per widget.|
| css 			  	 |      | [url]	    	 | Add absolute url to you custom hosted CSS.											   |


### Dynamic packages widget
Use for dynamic package you have 1 widget per package type.

Parameters for all package types

| Parameter       |type  | Example value  | Description                                                                             |
|-----------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId  | Int  | 123456   	  | CBIS product id for the package															|
| css 			  |      | [url]	      | Add absolute url to you custom hosted CSS.											    |

*cbisProductId is requierd 

### Accommodation Ferry package widget
```html
Accommodation Ferry package example:
<div id="citybreak_accommodation_ferry_package_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationferrypackagewidget/searchform?cbisProductid=[ID]">
</script>
```
Use for package type AccommodationFerry

### Accommodation Todo package widget
```html
Accommodation Todo package example:
<div id="citybreak_accommodation_todo_package_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationtodopackagewidget/searchform?cbisProductid=[ID]">
</script>
```
Use for package type AccommodationTodo

### Accommodation Accommodation package widget
```html
Accommodation Accommodation package example:
<div id="citybreak_accommodation_accommodation_package_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationaccommodationpackagewidget/searchform?cbisProductid=[ID]">
</script>
```
Use for package type AccommodationAccommodation

### Todo Todo package widget
```html
Todo Todo package example:
<div id="citybreak_todo_todo_package_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/todotodopackagewidget/searchform?cbisProductid=[ID]">
</script>
```
Use for package type TodoTodo

### Accommodation Flight package widget
```html
Accommodation Flight package example:
<div id="citybreak_accommodation_flight_package_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationflightpackagewidget/searchform?cbisProductid=[ID]">
</script>
```
Use for package type AccommodationFlight

### <a id="Basket"></a> Basket widget - Used if you want to have a shopping cart in the CMS and in your template page.
```html
Basket example:
<a id="citybreak_basket_widget_display" href="#" tabindex="0"></a>
<div id="citybreak_basket_widget_summary"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/basketwidget/widget">
</script>
```
The basket widget can be used within or outside of the Citybreak online template page.
When the basket widget is used within the template the script tag must be omitted.

Note: citybreak_basket_widget_display is a optional trigger
