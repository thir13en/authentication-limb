# Local Storage

### Pros
* It's **pure JavaScript** and it's convenient. If you don't have a back-end and you're relying on a third-party API, you can't always ask them to set a specific cookie for your site.
* Works with APIs that require you to put your access token with string interpolation: `Authorization Bearer ${access_token}`.

### Cons
* Vulnerable to XSS attacks