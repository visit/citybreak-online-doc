# Template Page

Citybreak Online enables customization by offering the possibility to include a template page for header and footer. The template page is provided by setting an absolute URL to an HTML page containing a placeholder element where the Citybreak online booking engine will be injected. This gives the user ability to use their own header and footer as well as other static resources such as style sheets and JavaScripts. 

_A responsive template page is strongly recommended._

![Citybreak online template page solution](//visit.github.io/citybreak-online-doc/images/cb_online_temp.png "Citybreak online template page solution")

## Brief description

### Restrictions

* **Valid HTML5 markup** 
Citybreak online will parse the template page as HTML5 markup and it will therefore need to consist of valid HTML5 markup. The validity of the markup is determined by the tool we use for parsing, which is currently HtmlAgilityPack, but the markup can be validated with a tool such as the W3C validator using the HTML 5 doctype setting. The DOCTYPE is replaced or set by Citybreak online to ``<!DOCTYPE html>``

* **No Citybreak online widgets included in the header/footer template page** 
Loading an Citybreak online widget (via script) in the header/footer template page will cause serious conflicts and JavaScript errors. It is therefore not supported at this moment.

* **No Google Analytics tracking scripts** 
(calls to _trackPageview, _trackEvent etc) are allowed in the template page. This would cause double page views.

* **Must Contain a div element with id attribute set to ``cb_init_bookingengine``**
This will be the placeholder where the Citybreak online booking engine will be injected.

* **All meta tags except 'viewport' will be removed**

_NOTE: Consultning or troubleshooting a tempate will be debited with standard hour rate._

## Optional functionality

### Cookie consent

```html
> Usually tracking script tags look like this:

<script data-cb-template-trackerscript>    
</script>

<script type="text/javascript">
code
</script>

> In our example we have a cookie consent solution which has categorized tracking scripts using a CSS class 'optanon-category-C0002'.
> We modify our template accordingly

<script data-cb-template-trackerscript class="optanon-category-C0002">    
</script>

> This will cause tracking scripts execution to be handed over to the control of your cookie consent solution, using script-tag rewriting:

<script type="text/plain" class="optanon-category-C0002">
code
</script>
```

Scripts rendered by the Online that perform tracking are categorized into one category, decorate the <script data-cb-template-trackerscript> tag with the attributes used by your cookie consent solution to categorize scripts that perform tracking. 
     
The online will use the attributes of the script tag as a template when producing script tags containing trackers.

Your cookie consent solution needs to support script-tag rewriting which is one of the most efficient methods of preventing cookies controlled by script tags being set without consent. This method requires the least amount of change to your site.

Most cookie consent solutions work by categorizing scripts by HTML attributes.

When the above code loads, JavaScript inside the tags will not run, and no cookies will be set. Then, when the Cookie Compliance code loads, if cookies for the associated group have consent, it will dynamically change the tag to: script type=text/JavaScript – the code inside the tags will then be recognized and run as normal.












### Language select feature
Language select feature (if multiple languages are configured for the specific guide and a span with id attribute ``cb_replace_languages_select`` is encountered).

_Note: not supported in one domain implementations_

### Reference currency
Reference currency select feature (if multiple refence currency’s are configured for the specific guide and a span with id attribute ``cb_replace_referencecurrency_select`` is encountered).

This can also be implemented by adding a parameter to the CB online URLs.

Parameter
- refcur

Values sample:
- EUR
- SEK
- NOK
- USD
etc.

``https://[CBONLINE_URL]?refcur=EUR``

_Note: not supported in one domain implementations_

### Features
* Relative href/src rewriting.
* Title inject from Citybreak.
* Meta keyword inject
* Meta description inject
* Preserves CSS links and script references in original document.
* Injects CSS links and scripts from Citybreak online.
* Possibly remove form tags if interfering with Citybreak online.
* Possibly remove VIEWSTATE hidden input field.

## Detailed description
This section will go into the details of how to create your external header footer.

### Error reporting
If something goes wrong during the creation of the header/footer include from Citybreak, the error will be reported as a .NET stack trace in a comment at the bottom of the HTML generated. The standard header footer of Citybreak online will be used meanwhile.

### Features
Form tags
If a form tag is encountered in the header/footer include document that has a child element that defines special functionality for Citybreak online (such as the content div or language span, described below), the form will simply be removed and replaced by an HTML comment that states that the tag was removed. Form tags that do not interfere with Citybreak functionality will be preserved.

### .NET Viewstate
If a hidden input field with the name attribute set to ‘__VIEWSTATE’ is encountered, it will be replaced with a comment stating the field was removed. If you are using .NET WebForms a form tag will most likely wrap the entire page. That form element will be removed (since it wraps all elements of the page, and we want to make sure that we don’t pass too much unnecessary data back and forth from the client to the server).

### Citybreak Online content div
```html
<div id="cb_init_bookingengine">
     <h1>Booking engine goes here.</h1>
</div>
```
The Citybreak online will download the file, parse it, modify it as necessary and split the content in two parts: one header and one footer. You should define a div tag with the id attribute set to ‘cb_init_bookingengine’  where you would like the Citybreak online content to be injected.

Everything within this div element will be ignored and replaced by the Citybreak online content. In this case will the h1 tag be ignored and the specific requested Citybreak online page will be inserted there instead. If this tag is omitted the header/footer has no meaning in the context of Citybreak online and will be dealt with according to section Error reporting.

### Change language
```html
<span id="cb_replace_languages_select"></span> 
```
If the online guide implements more than one language, a change language control can be included into the header/footer document. Just include a span tag where you wish to insert the language change controls.

The id attribute must be the specific ‘cb_replace_languages_select’. Everything in the span will be ignored and replaced with a form element which has some hidden fields as well as select box with available languages and an input type submit control. This will enable the user to change language and still end up at the same page as currently is viewed.

### Title tag
The contents of the title tag will be replaced with a title appropriate for the Citybreak online page that is displayed. This title is generated from Citybreak online and can not be changed from the include file.

### Relative href/src URL rewriting
All elements that have attributes named href or src will be tried to be rewritten in the context of the URL where the page was downloaded from. That is, Citybreak online will try to rewrite relative paths to absolute paths.

If the include file was found at ``https://somesite.com/templ/cb.htm`` and a tag in that document is defined as ``/css/base.css`` the tag will be rewritten to the definition ``https://somesite.com/css/base.css`` It applies to all elements with the attribute href or src, meaning it applies to link tags, script tags, img tags etc, etc.

### Meta keyword inject
If a specific page in Citybreak online defines specific keywords to be used, it will create a new meta tag with them. If a meta keywords tag already exists in the header/footer document, Citybreak online will append the specific keywords to it.

### Meta description inject
If no meta description tag is defined on the page, Citybreak online will create one and append it to the document. If one exists in the include document, Citybreak online will append its own description to the tag.

### Meta refresh
If meta refresh is defined on the include page, it will be removed. In rare cases Citybreak Citybreak online will define a refresh tag.

### Meta content charset
Citybreak online will remove all elements that define meta http-equiv and replace it with the following: 

```html
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
```

### Robots
If meta tags to hint robots are encountered they are preserved, except for pages that Citybreak online defines as local. Those pages will be tagged as noindex, nofollow. If requested we can set the Citybreak online entirely as noindex

### Head re-ordering
Citybreak online will reorder the tags in the head. The elements will be rearranged according to
this order:

1. Title element.
2. Meta tags.
3. Link definitions from header.
4. Citybreak online link definitions.
5. Explicit style definition from header.
6. Script definitions from header.
7. Script definitions from Citybreak online.
8. Content Script definitions.

### Injected CSS classes
The Citybreak online will inject class names on specific tags in the include file where applicable for styling purposes.

### Conventions used
CSS class names
To make it harder for CSS class names to interfere, the Citybreak online team preambles all its internal CSS classes with either ``Citybreak`` or ``cb_``.

### CSS web fonts
When using custom fonts in the header/footer template, access must be granted for your Citybreak online sub-domain. This applies to both 3rd party services such as Typekit, as well as hosted fonts declared via @font-face CSS rules.

### BodyCssClasses
Citybreak online inserts some CSS classes into the class attribute of the Body element based on what section of Citybreak online is active. This enables you to do special styling based on the currently active section, and these values are also accessible from javascript. It also inserts the currently active language. The body tag always has a class of cb_citybreak_body when Citybreak online is active.

**Language**
The currenly active language is inserted prepended by cb_lang_ , e.g cb_lang_sv or cb_lang_en

**Section**
The currently active section is indicate with a cb_ prefix followed by the name of the section. The following values are used:

Section | Class 
--------- | ---------
Accommodation | cb_accommodation
Basket | cb_checkout
Basket & Payment pages | cb_basket
Payment page | cb_basket cb_progress
Events | cb_event
Todo | cb_activity
Ferry | cb_ferry
Add-ons / Complementary information | cb_complementary
Packages | cb_package


### jQuery
Citybreak online uses the jQuery JavaScript library. The specific jQuery handle is called ''‘citybreakjq’'' and should **never be interfered with**.

### Extra url parameters

If you want to compare your CB online url with and with out the template page loaded you can user this URL parameter:  
``NoHeaderFooter=true``

```html
//[ONLINE-HOST]/[CULTURE]/[CB ONLINE URL...]?NoHeaderFooter=true
```

If you want to load all System translation strings on a url you can user this parameter:  
``showTranslationKeys=true``

```html
//[ONLINE-HOST]/[CULTURE]/[CB ONLINE URL...]?showTranslationKeys=true
```
