# Widgets

Citybreak Online comes with a set of standard widgets.  
These are JavaScript widgets that are easy to integrate with just a few lines of code.

All widgets use a script tag that is loaded asynchronously.  
Example script:

```html
<script async type="text/javascript" src="//[online-host]/[culture]/..."></script>
```

You also need a `div` tag to indicate where the widget will be inserted on the page.  
Example `div`:

```html
<div id="[id needed for widget]"></div>
```

See the example for the specific widget you need below.

**FYI:**
- **Do not** load widget scripts on your template page—this may affect booking controls and create potential conflicts.
- **Never** override the widget CSS manually, as the styling is controlled by the implementation.
- Need to test widgets in a CMS test environment? Ensure the domain is properly set up in the CMS and test CB Online to avoid potential CORS issues.  
  _(If you want to use custom CSS, it should be loaded using the `css` parameter and a URL pointing to your hosted stylesheet.)_

### Widget Types

- [Search Forms Widgets](#Searchforms)
- [Product Booking & Package Search Widgets](#product_package)
- [Traveller Rating / Guest Reviews Widget](#traveller_rating)
- [Basket Widget](#Basket)

## <a id="Searchforms"></a> Searchform widgets 

Searchform widgets are used if you need a multi-product or a transport searchform in your CMS.

### Accommodation searchform widget
```html
Accommodation searchform example:
<div id="citybreak_accommodation_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationwidget/searchform"></script>
```
Use for multi-property accommodation search.
_(NOTE: will be replaced shortly with a newer token based version)_

| Parameter               | Type   | Example Value | Description                                                                                     |
|-------------------------|--------|----------------|-------------------------------------------------------------------------------------------------|
| defaultCategoryId       | int    | 123456         | Set the default category in the widget. CBIS category ID is needed.                             |
| lockCategory            | Bool   | true           | Lock the category dropdown. When set, the dropdown with categories will be hidden.              |
| geoNodeId               | int    | 123456         | Set default geonode in the widget. CBIS geonode ID is needed.                                   |
| cbispids                | int    | 123456         | Set default products in the widget. CBIS product ID is needed.                                  |
| defaultArrivalDate      | Date   | 2023-03-12     | Set the default arrival date. Format must match the format of the requested widget.             |
| defaultDepartureDate    | Date   | 2023-03-13     | Set the default departure date. Format must match the format of the requested widget.           |
| promotionCode           | String | Promo_2023     | Set a promotion code in the promotion code field.                                               |
| css                     |        | [url]          | Add absolute URL to your custom hosted CSS.                                                     |


### Parameters for number of rooms and guests
You define the number of adults and children (including the child’s age) that will stay in each room using parameters in the direct search—so-called “Room configuration.” For example, a search with two rooms: the first room has two adults, and the second room has one adult and one child aged 5.

| Parameter | Type   | Example Value                                                   | Description                                                                             |
|-----------|--------|------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| &pr       | String | &pr=1 (One room with one adult is entered)                      | The base parameter for the room configuration to be searched.                          |
| a         | String | &pr=1a10 (One room with one adult and one child (10 yrs))       | Separator between adults and children.                                                  |
| r         | String | &pr=1r1r1 (One room with one adult and two children (10, 12 yrs)) | Separator when more than one room is included in the search.                           |
| c         | String | &pr=1a10c12 (Two rooms: one with one adult and children 10,12; second with two adults) | Separator when multiple children are included.        |

--

### Todo searchform widget
```html
Todo searchform example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
Used for filtering products in a Todo product list. Please contact our support team, and we’ll provide the necessary widget.

*What is a Token?* A token provides the necessary parameters to control the widget. Please see the notes below.

**Note:**  
- A token is linked to a single online store.  
- Each token is unique and should only be added once per view.  
- A token is associated with a specific widget type.

---

### Ferry searchform widget
```html
Ferry searchform example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
Used for Ferry search. Please contact our support team, and we’ll provide the necessary widget.

*What is a Token?* A token provides the necessary parameters to control the widget. Please see the notes below.

**Note:**  
- A token is linked to a single online store.  
- Each token is unique and should only be added once per view.  
- A token is associated with a specific widget type.

---

### Flight searchform widget
```html
Flight searchform example:
<div id="citybreak_flight_searchform_widget"></div> 

<script async type="text/javascript" src="//[online-host]/[culture]/flightwidget/searchform"></script>
```
Used for external flight searches.  
(NOTE: will be replaced by a new version)

| Parameter                  | Type   | Example Value | Description                                                                            |
|---------------------------|--------|----------------|----------------------------------------------------------------------------------------|
| defaultArrivalDate        | String | 2023-03-12     | Set the default arrival date.                                                          |
| defaultDepartureDate      | String | 2023-03-13     | Set the default departure date.                                                        |
| preselectFlexibleDates    | Bool   | True           | Use to preselect a flexible date search.                                               |
| preselectedEndLocationId  | Int    | 123456         | Use to preselect an end location ID (Travelswitch aggregator location ID).             |
| lockEndLocation           | Bool   | True           | Locks or disables changing the end location.                                           |
| sgid                      | Int    | 123456         | Use to preselect the start location using a CBIS geonode ID.                           |
| css                       |        | [url]          | Add the absolute URL to your custom hosted CSS.                                        |

---

## <a id="product_package"></a> Product booking & Package widgets

### Todo group booking widget
```html
Todo group booking widget example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
Used for Todo product groups when you want to load the list of child products in a list widget.

For the Todo group booking widget, contact our support team and we’ll provide the widget(s) needed.

*What is a Token?* A token provides the needed parameters to control the widget.

**Note:**  
- A token is linked to a single online store.  
- Each token is unique and should only be added once per view.  
- A token is associated with a specific widget type.

| Parameter         | Type | Example Value | Description                                                                 |
|------------------|------|----------------|-----------------------------------------------------------------------------|
| cbisProductId     | Int  | 123456         | CBIS product ID; must be the parent product of the Todo product group.      |
| allowOverride     | Bool | False          | Toggle external URL parameter override; useful for automating widgets in CMS. |

---

### iTicket Activity Transport booking widget
```html
iTicket Activity Transport example:
<div id="citybreak_activity_transport_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/activitytransportwidget/searchform?cbisProductId=[ID]"></script>
```
Use for iTicket transport products.

| Parameter             | Type   | Example Value | Description                                                                                   |
|----------------------|--------|----------------|-----------------------------------------------------------------------------------------------|
| cbisProductId         | Int    | 123456         | CBIS product ID; specifies the product to display.                                             |
| proceedToBasket       | Bool   | true / false   | Proceed to basket (checkout) or stay on the widget page.                                      |
| css                   |        | [url]          | Add the absolute URL to your custom-hosted CSS.                                               |
| preferredDate         | Date   | 2023-06-11     | Set the initially selected date. If unavailable, fallback behavior applies.                   |
| preferredDeparture    | Date   | 2023-06-11     | ID of the initially selected departure location.                                              |
| preferredArrival      | Date   | 2023-07-01     | ID of the initially selected arrival location.                                                |
| enablePromocode       | Bool   | true / false   | Show promo code field. Defaults to false if parameter is not added.                           |
| tripType              | String | oneway / roundtrip | Set selected trip type on load. Only works if product supports this option.              |

---

### iTicket Bookingflow booking widget
```html
iTicket BookingFlow widgets example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
For iTicket BookingFlow widgets, contact our support team and we’ll provide the widget(s) needed.

*What is a Token?* A token provides the needed parameters to control the widget.

**Note:**  
- A token is linked to a single online store.  
- Each token is unique and should only be added once per view.  
- A token is associated with a specific widget type.

| Parameter             | Type   | Example Value | Description                                                                 |
|----------------------|--------|----------------|-----------------------------------------------------------------------------|
| cbisProductId         | Int    | 123456         | CBIS product ID to display in the widget.                                   |
| startDateISO          | Date   | 2024-12-24     | Default initially selected date in the widget.                              |
| promotionCode         | String | MyPromoCode    | Promo code to load with the widget as active.                               |
| proceedToBasket       | Bool   | true / false   | Proceed to basket (checkout) or stay on the widget page.                    |
| referenceCurrency     | String | USD            | Use ISO format to set reference currency.                                   |
| display               | String | Button         | Display type: Standard, Collapsed, or Button.                               |
| allowOverride         | Bool   | False          | Toggle external URL parameter override. Useful for automating widgets in CMS. |

--

### Accommodation product widget
```html
Accommodation product example:
<div id="citybreak_accommodation_property_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/accommodationPropertyWidget/searchform?productid=[ID]"></script>
```
Use for one accommodation property.  
(NOTE: will be replaced shortly)

| Parameter   | Type | Example Value | Description                                                                 |
|-------------|------|----------------|-----------------------------------------------------------------------------|
| *productId  | Int  | 123456         | CBIS product ID to display the widget. Only one product per widget.        |
| css         |      | [url]          | Add absolute URL to your custom-hosted CSS.                                |

---

### Dynamic packages widget
```html
Dynamic package example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
For Dynamic packages widgets, contact our support team to obtain the necessary widget(s).

*What is a Token?* A token provides the parameters needed to control the widget.

**Note:**  
- A token is linked to a single online store.  
- Each token is unique and should only be added once per view.  
- A token is associated with a specific widget type.

| Parameter       | Type | Example Value | Description                                                                 |
|-----------------|------|----------------|-----------------------------------------------------------------------------|
| cbisProductId   | Int  | 123456         | CBIS product ID for the package to display.                                 |
| allowOverride   | Bool | False          | Toggle external URL parameter override for CMS widget automation.           |

---

## <a id="traveller_rating"></a> Traveller rating / GuestReviews widget

### Traveller rating / GuestReviews widget
```html
Traveller rating / GuestReviews example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
For Traveller rating / GuestReviews widgets, contact our support team to obtain the necessary widget(s).

*What is a Token?* A token provides the parameters needed to control the widget.

**Note:**  
- A token is linked to a single online store.  
- Each token is unique and should only be added once per view.  
- A token is associated with a specific widget type.

| Parameter       | Type   | Example Value | Description                                                            |
|-----------------|--------|----------------|------------------------------------------------------------------------|
| cbisProductId   | Int    | 123456         | CBIS product ID to display in the widget.                              |
| display         | String | Button         | Display type: 'Button' (default) or 'Standard'.                         |
| allowOverride   | Bool   | False          | Toggle external URL parameter override for CMS widget automation.      |

---

## <a id="Basket"></a> Basket widget
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
Used to include a shopping cart in your CMS or template page

The basket widget can be used both within and outside the Citybreak Online template page.  
When used within the template, the `<script>` tag must be omitted.

**FYI:**  
The collapsed widget div `<div id="citybreak_basket_widget_summary"></div>` is **not styled** by the Citybreak system.

_Note: `citybreak_basket_widget_display` is an optional trigger._
