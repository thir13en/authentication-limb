# Cookies


### Pros
The cookie is **not** accessible via `JavaScript`; hence, it is **not as vulnerable to XSS attacks** as localStorage.
* If you're using `httpOnly` and `secure cookies`, that means your cookies cannot be accessed using `JavaScript`. This means, even if an attacker can run `JS` on your site, they can't read your access token from the cookie.
* It's **automatically sent** in every HTTP request to your server.