# Citybreak online documentaiton

Welcome to Citybreak online documentation.
Here you will find information related to Citybreak online widgets, template pages and tracking.

If you can find the information you are looking, or if the informatio in incorrect. Please contact us at help@citybreak.com and we'll get back to you as soon as possible.

## Example

```html
curl -X GET 
  --header 'ApiKey: APIKEY132456789EWOK'
  --header 'Accept: application/json' 
  --header 'Accept-Language: en-US'
  'https://example.citybreak.com/v1/example'
```

```javascript
var r = fetch("https://example.citybreak.com/v1/example",
{
  headers: {
    "ApiKey:" "APIKEY132456789EWOK",
    "Accept": "application/json",
	"Accept-Language": "en-US"
  }  
});
```

> Example of response:

```json
{
  "Examples": [
	"Hello World test",
	"Ewoks are the best"
  ]
}
```

An example.

### HTTP Request

`POST https://example.citybreak.com/v1/example`

### Query Parameters

Parameter | Type |Description
--------- | ------ | -----------
Accept-Language | Header | The language.

