# Cookies


### Pros
The cookie is **not** accessible via `JavaScript`; hence, it is **not as vulnerable to XSS attacks** as localStorage.
* If you're using `httpOnly` and `secure cookies`, that means your cookies cannot be accessed using `JavaScript`. This means, even if an attacker can run `JS` on your site, they can't read your access token from the cookie.
* It's **automatically sent** in every HTTP request to your server.

### Cons
Depending on the use case, you might **not** be able to store your `tokens` in the `cookies`.  
* Cookies have a size **limit** of `4KB`. Therefore, if you're using a big `JWT Token`, storing in the cookie is **not** an option.
* There are scenarios where you can't share `cookies` with your `API server` or the `API` requires you to put the access token in the `Authorization header`. In this case, you won't be able to use cookies to store your tokens.

However, in the case of an `XSS attack`, an attacker can run `JavaScript` in your application, then they can just send an `HTTP` request to your server and that **will automatically include your `cookies`**.  
It's just **less convenient for the attacker because they can't read the content of the token** although they rarely have to. It might also be more advantageous for the attacker to attack using victim's browser (by just sending that HTTP Request) rather than using the attacker's machine.
