# Refresh Token

A refresh token is a special key that enables a clint for an API or service to retrieve new access tokens without requiring the user to perform a complete login.

> **NOTE**
> Do not use refresh token without **Refresh Token Rotation**.

- Refresh token lifespan should be managed by the lifespan of a access token.
- Keep it secret, keep it safe.
- Do not add sensitive data to the payload.
- Give token an expiration.
- Embrace HTTPS
- Store and reuse

 