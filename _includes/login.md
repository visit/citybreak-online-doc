# Login

Citybreak Online can be integrated with an external login (SSO) so that a person who signs in on your site is also signed in to the booking engine.

Your site logs a person in with one of their bookings: its booking code and the customer's e-mail address. My Page must be activated on your online.

## Login flow

The flow is based on two request parameters, `code` and `userName`: the booking code and the hashed e-mail address of a booking the person has made. Both are in the booking's My Page link, which is in the booking confirmation e-mail and in the BI API as `MyPageBookingUrl`.

1. **The credentials are stored.**
Any request carrying `code` & `userName` stores those details in a booking credentials cookie, `bookcred_online3_{guideIdentifier}`. The credentials are **not** verified at this point, only stored.

2. **The credentials are used.**
When the visitor opens My Page, or a checkout page where guest or customer details are entered, Citybreak Online tries to log the person in with the stored credentials. No other page does this.

3. **The person is logged in.**
On success the `pgid_online3_{guideIdentifier}` cookie is set. The `bookcred` cookie remains, but is no longer used once a `pgid` cookie exists.

This means a visitor who has only passed `code` & `userName` to an arbitrary page is not logged in yet. Use the login link below if you need the login to happen at a specific point in your own flow.

The login lasts until the browser is closed. There is no logout link; the person logs out on My Page.

## Logging in from your own site

1. The person signs in on your site.
2. Your backend finds a booking the person has made, see [linking bookings to your accounts](#linking-bookings-to-your-accounts), and takes `code` and `userName` from the booking's `MyPageBookingUrl` in the BI API.
3. Your site sends the browser to the [My Page login link](#mypage_login_link) with `code`, `userName` and a `redirectUrl` to the page the person should land on.
4. Citybreak Online logs the person in and redirects to `redirectUrl`. The `cb-logged-in` class is set on that page.

The login link needs a booking, so a person who hasn't booked yet can't be logged in from your site. They fill in the customer details form at checkout as usual.

Your own sign-in button can go in your online's page template. Hide it once the person is logged in, as shown under [detecting login state](#detecting-login-state).

## <a id="mypage_login_link"></a> My Page login link

The login link validates the credentials and logs the person in, instead of waiting for the visitor to reach a page that triggers the automatic login. Add `redirectUrl` and the visitor is sent there on success.

```html
My Page login link example:

//[online-host]/[culture]/link/mypage?code=[CODE]&userName=[USERNAME]&redirectUrl=[RELATIVE-URL]
```

| Parameter    | Type   | Example value              | Description                                                             |
|--------------|--------|----------------------------|-------------------------------------------------------------------------|
| code         | String | ABCD12                     | Booking code, from the booking's My Page link.                           |
| userName     | String | 8f3b...e21a                | Hashed e-mail address, from the booking's My Page link.                  |
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

## Linking bookings to your accounts

To connect a booking with the person's account on your site:

- **On the confirmation page**, a tracker script can hand the booking to your own script, see [handing the booking over to your own script](#handing-the-booking-over-to-your-own-script). Your script then tells your site which booking the signed-in person just made.
- **On your backend**, fetch the full booking from the [BI API](https://visit.github.io/bi-api-doc/) with the booking code. It includes the customer, and the booking's `MyPageBookingUrl`, which logs the person in to My Page for that booking.
- **To get every booking**, including bookings made outside your site, poll the BI API's GetMany from your backend.
