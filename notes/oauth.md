# Oauth


OAuth 2.0 is an authorization framework that defines how a third-party application can obtain access to a service securely without requiring security details (username, password, etc.) from the user. A common example of OAuth 2.0 is when you use "Sign in with Google" to log in to other websites.  

Here you are an example authentication flow with Oauth:  
![oauth-flow](img/oauth1.png)  

### `Sign in with Google` as an example

1. Service wants to access User's Google Calendar. Service redirects User to sign in to his Google account where he grants Calendar permission for Service
1. Google returns an `Authorization Grant` and redirects User to Service.
1. Service gives the `Authorization Grant` to Google and
1. receives an `Access Token`
1. Service can now use this `Access Token`
1. Service can access User's Google Calendar, but not his Google Drive or other resources

### Tokens
There are two kinds: `Access Token` and `Refresh Token`. The access tokens tend to be **short lived**, the the refreshed token is used once the access token has expired in order to retrieve a new access token.

#### Access Token
With a `short-lived access token`, we can use a `JWT Token` to make a **self-encoded access token**.

#### Refresh Token
A `refresh token` is a special token that is used to obtain a new `Access Token`. Since this is long-lived, refresh tokens **are generally opaque strings stored in the database**. Storing refresh tokens in the database **allows you to revoke them by deleting it from the database**.  
Because **there is no way to expire an Access Token**, we should make the access token short-lived. Revoking the refresh token prevents malicious parties from refreshing an expired Access Token. This means that **if your Access Token expires in 1 hour, then an attacker who obtained your Access Token can only access your API for 1 hour** before it expires.

### Best way to persists OAuth 2.0 tokens
1. Store your access token in `localStorage`: **prone to XSS**.
1.Store your access token in `httpOnly` cookie: **prone to CSRF but can be mitigated**, a bit **better in terms of exposure to XSS**.
1. Store the refresh token in `httpOnly` cookie: **safe from CSRF, a bit better in terms of exposure to XSS**. We'll go over how **Option 3 works as it is the best out of the 3 options**.

#### Why is this safe from CSRF?
Although a form submit to `/refresh_token` will work and a new `access token` will be returned, the attacker can't read the `response` if they're using an `HTML `form. To prevent the attacker from successfully making a fetch or `AJAX request` and read the response, this **requires the Authorization Server's `CORS` policy to be set up correctly** to prevent requests from unauthorized websites.
