# Widgets

Citybreak Online comes with a set of standard widgets.
The widgets are JavaScript widgets that are easy to integrate with a few lines of code.

All widgets got a script tag loaded asynchronously
Example script:
```html
<script async type="text/javascript" src="//[online-host]/[culture]/...</script>
```
And a div tag that you add where the widget will be inserted into the page.
Example div:
``<div id="[id needed for widget]"></div>``

See the example for the widget you need below.

FYI:
- Make sure you only run ONE widget script at a time.
- Don’t load widget scripts on your template page. This will affect the booking controls and create potential conflicts.
- Never use CSS overrides on the widget, as the CSS is controlled by the implementation.
- Need to test widgets in a CMS test environment? Make sure you have a proper domain setup in the CMS and test CB online to avoid potential CORS issues.
_(If you want to use custom CSS, it should be loaded via the CSS parameter and the URL where you host the CSS.)_


### Widget types

- [Searchforms widgets](#Searchforms)
- [Product & package widgets](#product_package)
- [Basket widget](#Basket)

## <a id="Searchforms"></a> Searchform widgets - Used for a search or filtering for products per guide.

Searchform widgets are used if you need a multi-product or a transport searchform in your CMS.

### Accommodation searchform
```html
Accommodation searchform example:
<div id="citybreak_accommodation_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationwidget/searchform"></script>
```
Use for multi property accommodation, search will target 
(NOTE: will be replaced shortly)

| Parameter       	   |type    | Example value  | Description                                                                             |
|----------------------|--------|----------------|-----------------------------------------------------------------------------------------|
| defaultCategoryId    | int    | 123456   	     | Set the default category in the widget. CBIS category ID is needed.						   |
| lockCategory		   | Bool   | true   	     | Use this parameter to lock down the category dropdown, when this is set then the dropdown with the categories will be hidden.|
| geoNodeId		       | int    | 123456   	     | Set default geonode in the widget. CBIS geonode ID is needed.						   |
| cbispids		       | int    | 123456   	     | Set default products in the widget. CBIS product ID is needed.						   |
| defaultArrivalDate   | Date   | 2023-03-12     | A valid date to set the default arrival date in the widget, the format of the date must be the same as the format of the requested widget|
| defaultDepartureDate | Date   | 2023-03-13	 | A valid date to set the default departure date in the widget, the format of the date must be the same as the format of the requested widget|
| promotionCode	       | String | Promo_2023     | Use this parameter if you want to set a promotion code in the promotion code field.	   |
| css 			       | 		| [url]			 | Add absolute URL to your custom hosted CSS.											   |


### Parameter for number of rooms and guests
You define the number of adults and children (including the child’s age) that will stay in each room as parameters in the direct search, so-called ”Room configuration”. It can for example be a search with two rooms where the first room shall have two adults and the other room shall have one adult and a child with age 5.

| Parameter |type    | Example value  												| Description                                                                             |
|-----------|--------|--------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| &pr    	| String | &pr=1 (One room with one adult is entered)| This is the base parameter for the room configuration that shall be searched.|
| a		    | String | &pr=1a10 (One room with one adult and one child (10 yrs) is entered)| The separator between adults and children.|
| r		    | String | &pr=1r1r1 (One room with one adult and two children (10, 12 yrs) is entered)| The separator if the search is made on more rooms than one.|
| c		    | String | &pr=1a10c12(Two rooms with one adult and two children (10, 12 yrs) in the first room and two adults in the second room is entered)| The separator if the search shall be made on more than one child.|

### Activity/Todo searchform
```html
Todo searchform example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
Used for filtering products in a Todo product list. Please contact our support team, and we’ll provide the necessary widget.

*What is a Token?* A token will provide the needed parameters to control the widget. Please take a look at the parameter below.
Note: 
- A token is linked to a single online store.
- Each token is unique and should only be added once per view.
- A token is associated with a specific widget type.


### Ferry searchform
```html
Ferry searchform example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
Used for Ferry search. Please contact our support team, and we’ll provide the necessary widget.

*What is a Token?* A token will provide the needed parameters to control the widget. Please take a look at the parameter below.
Note: 
- A token is linked to a single online store.
- Each token is unique and should only be added once per view.
- A token is associated with a specific widget type.

### Flight searchform
```html
Flight searchform example:
<div id="citybreak_flight_searchform_widget"></div> 

<script async type="text/javascript" src="//[online-host]/[culture]/flightwidget/searchform"></script>
```
Use for external flight search
(NOTE: will be replaced shortly)

| Parameter       	   |type    | Example value  | Description                                                                             |
|----------------------|--------|----------------|-----------------------------------------------------------------------------------------|
| defaultArrivalDate   | String | 2023-03-12     | Set default default arrival date.													   |
| defaultDepartureDate | String | 2023-03-13     | Set default default departure date.													   |
| preselectFlexibleDates | Bool | True           | Use to preselect flexible date search.										       	   |
| preselectedEndLocationId | Int| 123456         | Use to preselect a end location id (Travelswitch(agregatror) location ID).		   	   |
| lockEndLocation 	   | Bool   | True      	 | Use to locked/disabled changing the end location. 								   	   |
| sgid 	   			   | Int    | 123456      	 | Use to preselect start location using a CBIS geonode ID.						   		   |
| css 			       | 		| [url]			 | Add absolute url to you custom hosted CSS.											   |

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
Activity & merchandise product booking widget - load one per page. (you can load multiple products in one script if needed.) 
(NOTE: will be replaced shortly)

| Parameter       |type  | Example value  | Description                                                                             |
|-----------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId  | Int  | 123456   	  | CBIS product id, We recommend that you keep this ID on all elements See [ID] in the example.|
| proceedToBasket | Bool | true (or false)| Use to proceed to basket(checkout) or stay on widget page?  	  					    |
| css 			  |      | [url]		  | Add absolute URL to your custom-hosted CSS.												|
| defaultDate	  | Date | 2023-06-11     | Use JavaScript "new" date format, default selected date									|
| startDate 	  | Date | 2023-07-01     | Use JavaScript "new" date format, widget start date selectable date						|
| endDate	 	  | Date | 2023-07-01     | Use JavaScript "new" date format, maximum selectable date								|
| enablePromocode	 | Bool | true (or false)| Whether the field for entering promo code will be visible in the widget. If the  parameter is not added widget defaults to false.|

*cbisProductId is requierd 


### iTicket Activity Transport widget
```html
iTicket Activity Transport example:
<div id="citybreak_activity_transport_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/activitytransportwidget/searchform?cbisProductId=[ID]"></script>
```
Use for iticket transport products.

| Parameter       	 |type  | Example value  | Description                                                                             |
|--------------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId      | Int  | 123456   	     | CBIS product id, product to display the widget.										   |
| proceedToBasket 	 | Bool | true (or false)| Use to proceed to basket(checkout) or stay on widget page?    						   |
| css 			  	 |      | [url]		     | Add absolute URL to your custom-hosted CSS.											   |
| preferredDate	  	 | Date | 2023-06-11     | A valid date to set the default initially selected date in the widget, the format of the date must be the same as the format of the requested widget. If the preferred date is not available it will fall back to default behavior.|
| preferredDeparture | Date | 2023-06-11     | Id of the location that will be initially selected as departure location. If not available it will fall back to default behavior.|
| preferredArrival 	 | Date | 2023-07-01     | Id of the location that will be initially selected as arrival location. If not available it will fall back to default behavior.|
| enablePromocode	 | Bool | true (or false)| Whether the field for entering promo code will be visible in the widget. If the  parameter is not added widget defaults to false.|
| tripType	 | String | oneway (or roundtrip) |Set selected trip type onload roundtrip OR oneway, only work for iTicket products with a trip type as the option of course.  |

*cbisProductId id required 

### iTicket Bookingflow widgets
```html
iTicket BookingFlow widgets example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
For iTicket BookingFlow widgets contact our support, then we'll give you the widget(s) needed.

*What is a Token?* A token will provide the needed parameters to control the widget. Please take a look at the parameter below.
Note: 
- A token is linked to a single online store.
- Each token is unique and should only be added once per view.
- A token is associated with a specific widget type.

| Parameter       	 |type  | Example value  | Description                                                                             |
|--------------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId      | Int  | 123456   	     | CBIS product id, product to display the widget.										   |
| startDateISO     	 | Date | 2024-12-24     | A valid date to set the default initially selected date in the widget. |
| promotionCode 	 | String | MyPromoCode  | Add the promo code you want to load with the widget as active. |
| proceedToBasket 	 | true (or false) | Use to proceed to basket(checkout) or stay on widget page? |
| referenceCurrency	 | String | USD	         | Use ISO format to set reference currency.  |
| display        	 | String | Button       | Selected Display type: Standard, Collapsed or Button. |
| allowOverride    	 | Bool   | False        | Used to toggle  external URL parameter override, can be useful if you want to automate widgets in your CMS. |

### Accommodation product widget
```html
Accommodation product example:
<div id="citybreak_accommodation_property_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationPropertyWidget/searchform?productid=[ID]"></script>
```
Use for one accommodation property. (NOTE: will be replaced shortly)

| Parameter       	 |type  | Example value  | Description                                                                             |
|--------------------|------|----------------|-----------------------------------------------------------------------------------------|
| *productId         | Int  | 123456   	     | CBIS product id, product to display the widget. You can only use one product per widget.|
| css 			  	 |      | [url]	    	 | Add absolute URL to your custom hosted CSS.											   |


### Dynamic packages widgets
```html
Dynamic package example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
For Dynamic packages widgets contact our support, then we'll provide you with the widget(s).

*What is a Token?* A token will provide the needed parameters to control the widget. Please take a look at the parameter below.
Note: 
- A token is linked to a single online store.
- Each token is unique and should only be added once per view.
- A token is associated with a specific widget type.

| Parameter       	 |type  | Example value  | Description                                                                             |
|--------------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId      | Int  | 123456   	     | CBIS product id, package to display the widget.										   |
| allowOverride    	 | Bool   | False        | Used to toggle  external URL parameter override, can be useful if you want to automate widgets in your CMS. |

### Traveller rating / GuestReviews widget
```html
Traveller rating / GuestReviews example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
For Traveller rating / GuestReviews widgets contact our support, then we'll provide you with the widget(s).

*What is a Token?* A token will provide the needed parameters to control the widget. Please take a look at the parameter below.
Note: 
- A token is linked to a single online store.
- Each token is unique and should only be added once per view.
- A token is associated with a specific widget type.

| Parameter       	 |type  | Example value  | Description                                                                             |
|--------------------|------|----------------|-----------------------------------------------------------------------------------------|
| cbisProductId      | Int  | 123456   	     | CBIS product id, package to display the widget.										   |
| display        	 | String | Button       | Display type options: (default) Button or standard |
| allowOverride    	 | Bool   | False        | Used to toggle  external URL parameter override, can be useful if you want to automate widgets in your CMS. |

## <a id="Basket"></a> Basket widget - Used if you want to have a shopping cart in the CMS and in your template page.
```html

Basket example if anchor:
<a id="citybreak_basket_widget_display" href="javascript:void(0);"></a>
<div id="citybreak_basket_widget_summary"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/basketwidget/widget"></script>
```
```html
Basket example if span:
<span id="citybreak_basket_widget_display" tabindex="0"></span>
<div id="citybreak_basket_widget_summary"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/basketwidget/widget"></script>
```
The basket widget can be used within or outside of the Citybreak online template page.
When the basket widget is used within the template the script tag must be omitted.

FYI: The collapsed widget div ``<div id="citybreak_basket_widget_summary"></div>`` is not Styled from the Citybreak system.

Note: citybreak_basket_widget_display is an optional trigger





