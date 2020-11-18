# JWT

`JSON Web Tokens (JWT)` is a signed `JSON` object. This means you can trust the data contained in the JSON object by verifying the signature. For authorizing a user, you can include the user's ID and email in the JWT.

When you give the `JWT Access Token` to the `Resource Server` (your backend API server), your server can validate the `JWT Token` **without needing to access the database** to check if it's valid.

All your server needs to do is to validate that the `JWT Token` is valid using a library, see the user ID of the user making the request from the token, and trust that this user ID is already authenticated.
