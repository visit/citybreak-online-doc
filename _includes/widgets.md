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

Use for multi-property accommodation search. 

Documentation will be updated with a new widget version in the near future.


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

--

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

--

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

--

### Activity booking widget

Used for activity & merchandise products
_Note: Not for iTicket Bookingflow products Or iTicket Activity Transport products._

```html
Activity booking widget example:
<script async type="text/javascript" src="//[online-host]/[culture]//widget?token=[Unique Token ID]"></script>

<div id="[Unique Token ID]"></div>
```
Used for activity & merchandise products
_Note: Not for iTicket Bookingflow products Or iTicket Activity Transport products._

For the Todo group booking widget, contact our support team and we’ll provide the widget(s) needed.

*What is a Token?* A token provides the needed parameters to control the widget.

**Note:**  
- A token is linked to a single online store.  
- Each token is unique and should only be added once per view.  
- A token is associated with a specific widget type.

| Parameter         | Type | Example Value | Description                                                                 |
|------------------|------|----------------|-----------------------------------------------------------------------------|
| cbisProductId     | Int  | 123456         | CBIS product ID; must be the parent product of the Todo product group.      |
| promotionCode         | String | MyPromoCode    | Promo code to load with the widget as active.                               |
| enablePromocode       | Bool   | true / false   | Show promo code field. Defaults to false if parameter is not added.  |  
| proceedToBasket       | Bool   | true / false   | Proceed to basket (checkout) or stay on the widget page.   | 
| allowOverride     | Bool | False          | Toggle external URL parameter override; useful for automating widgets in CMS. |


--

### iTicket Activity Transport booking widget
```html
iTicket Activity Transport example:
<div id="citybreak_activity_transport_searchform_widget"></div>

<script async type="text/javascript" src="//[online-host]/[culture]/activitytransportwidget/searchform?cbisProductId=[ID]"></script>
```
Use for iTicket transport products that is not migrated to iTicket Bookingflow.

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

--

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
| startTimeISO          | String   | 12:30     | Filter tour start time on the selected date: Only display tours after added time                           |
| promotionCode         | String | MyPromoCode    | Promo code to load with the widget as active.                               |
| proceedToBasket       | Bool   | true / false   | Proceed to basket (checkout) or stay on the widget page.                    |
| referenceCurrency     | String | USD            | Use ISO format to set reference currency.                                   |
| display               | String | Button         | Display type: Standard, Collapsed, or Button.                               |
| allowOverride         | Bool   | False          | Toggle external URL parameter override. Useful for automating widgets in CMS. |

--

### Accommodation product widget

Use for Single propertys, singls rooms or accommodation supplier packages search and book.

Documentation will be updated with a new widget version in the near future.

--

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

--

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

--

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
