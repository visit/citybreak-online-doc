# Login

Citybreak Online can be integrated with an external login (SSO) so that a person who signs in on your site is also signed in to the booking engine.

## Login flow

The flow is based on two request parameters, `code` and `userName`, which are the credentials from the magic link sent to the customer.

1. **The credentials are stored.**
Any request carrying `code` & `userName` stores those details in a booking credentials cookie, `bookcred_online3_{guideIdentifier}`. The credentials are **not** verified at this point, only stored.

2. **The credentials are used.**
Whenever the visitor enters a page where a login normally happens - the My Page section, or the customer details form - Citybreak Online tries to log the person in automatically using the stored credentials.

3. **The person is logged in.**
On success the `pgid_online3_{guideIdentifier}` cookie is set. The `bookcred` cookie remains, but is no longer used once a `pgid` cookie exists.

This means a visitor who has only passed `code` & `userName` to an arbitrary page is not logged in yet. Use the login link below if you need the login to happen at a specific point in your own flow.

## <a id="mypage_login_link"></a> My Page login link

The login link validates the credentials and logs the person in, instead of waiting for the visitor to reach a page that triggers the automatic login. Add `redirectUrl` and the visitor is sent there on success.

```html
My Page login link example:

//[online-host]/[culture]/link/mypage?code=[CODE]&userName=[USERNAME]&redirectUrl=[RELATIVE-URL]
```

| Parameter    | Type   | Example value              | Description                                                             |
|--------------|--------|----------------------------|-------------------------------------------------------------------------|
| code         | String | abc123                     | Login code from the magic link.                                          |
| userName     | String | name@example.com           | User name from the magic link.                                           |
| redirectUrl  | String | /1234567890/en/en-gb/todo  | Page to redirect to after a successful login. **Relative URLs only.**   |

If the login fails, the login form is shown instead. If `redirectUrl` is omitted, or is not a relative URL, a successful login lands on the My Page booking view.

_Note: the redirect is sent with no-cache headers, so the same login link can be used more than once (for example log in, log out and log in again on the same page)._

## Detecting login state

**Do not read the login cookies from JavaScript.** Both `bookcred_online3_{guideIdentifier}` and `pgid_online3_{guideIdentifier}` are flagged `HttpOnly` and can therefore not be read by scripts. This is a security requirement and can not be turned off.

Use the `cb-logged-in` CSS class instead. Citybreak Online sets it on the `body` element, and it is only present when the visitor is actually logged in - not when there is only an unverified credential cookie.

```html
<body class="cb_lang_en cb-body cb-section-checkout cb-basket cb-logged-in">

<style>
     body.cb-logged-in #login-button { display: none; }
</style>
```

Since the class follows the login state, it is present on the page you send the visitor to with `redirectUrl`. If you only set the credential cookie, the class does not appear until the visitor reaches a page that triggers the automatic login.

[See the full list of body CSS classes under template page or click here](https://visit.github.io/citybreak-online-doc/#bodycssclasses)
