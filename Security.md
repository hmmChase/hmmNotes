# _Security_

---

# _Client-Side Security_

## Vulnerabilities

- Theft of Proprietary Code
- Theft of Data
- Falsifying Information

## The Data Validation Waterfall

### Client-Side Validation

- Should be visual, simple validations to give user quick feedback
- Use things like [HTML5 input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) and [pattern attributes](https://webdesign.tutsplus.com/tutorials/html5-form-validation-with-the-pattern-attribute--cms-25145).
- Never depend on a client-side validation working
- UI can be abused, and sometimes the user is not even using the browser (think curl or using postman)
- The mission critical validation should happen on a server
- Avoid having heavy validation on the client-side when you don’t need it to prevent mismatch in validation rules across your server and client
- The less rules you have on the client, the less places you have to change code when you change your validations
- Keep all your validations in one place
- Do not sprinkle them throughout your components/JS view related files

### Server-Side Validation

- Everything is Suspect
- Assume all data coming in from the UI is suspect and have server level validations cross check this information
- This is also helps you protect your business logic. Since all client-side code can be viewed, if you hide the business logic in the server, you can protect it from theft
- Use Environment Variables
- Store your credentials and secrets in a file separate from the code that gets committed to GitHub or equivalent. Use environment variables: [the logic](https://12factor.net/config)
- On Heroku: [Use the CLI](https://devcenter.heroku.com/articles/config-vars#setting-up-config-vars-for-a-deployed-application) or [the interface](https://devcenter.heroku.com/articles/config-vars) [On Amazon EC2](http://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html).
- But wait, you might be asking, I just pushed my Firebase credentials up to GitHub? Am I good? Well, check out the ‘web’ portion of the [Firebase Launch Checklist](https://firebase.google.com/support/guides/launch-checklist).
- HTTP vs HTTPS
- HTTP is HyperText Transfer Protocol while HTTPS is HyperText Transfer Protocol Secure.
- All communications sent over HTTP connections are in ‘plain text’ and can be read by anyone who can interrupt the communication.
- HTTPS, however, uses Secure Sockets Layer (SSL) to transmit information. In order to make an HTTPS connection to a webpage, your website needs an ‘SSL certificate’. When this is received, the browser and your website begin a ‘SSL handshake’, generate secrets and establish a secure connection
- If you use services like Firebase and Heroku, these things are handled for you. But it gets tricker when you want to use a custom domain
- [Let’s Encrypt](https://letsencrypt.org/how-it-works/) is your friend
- Authentication & Web Tokens
- You will get to use JWTs this module, but here is a [quick intro to JWTs](https://jwt.io/introduction/) if you can’t wait.
- Basically, modern authentication of users depends on handshakes and encryption. Consider this a hand wave.
- Same-Origin Policy & Cross-Origin Resource Sharing
- The [same-origin policy](https://en.wikipedia.org/wiki/Same-origin_policy) permits `permits scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin.`
- This worked great at preventing malicious scripts for a while - but now many of use server REST APIs from different origins and this became a problem that we started solving with hacks. Many of said hacks were insecure.
- [CORS](https://enable-cors.org/) enables you to safely overwrite and relax these rules for specific whitelisted domains.

### Database Validations

- Best Practice
- Never fully trust your users. Before data can be stored in the database, do some base-level data validation. And never store plain text passwords in your database. If you absolutely need to store passwords, then use a proven, maintained library like [bcrypt](https://www.npmjs.com/package/bcrypt)
- Tech Recommendations:
  - Any major database will include methods and constraints to validate data quickly prior to storage.
  - It’s beyond the scope of this lesson to get into them specifically - but know that there are simple ways to do things like ‘hey database, refuse to accept `null` values in this column of the table’.
- [Postgresql](http://nathanmlong.com/2016/01/protect-your-data-with-postgresql-constraints/)
- [Firebase](https://firebase.google.com/docs/reference/security/database/)
- Dangers
- Never store plain text data in your database
- Don’t Ever Roll Your Own Authentication

---

# _Server-side Security_

- https://zapier.com/engineering/apikey-oauth-jwt/

---

# _Authentication_

- Are you who you say you are?

---

# _Authorization_

- Should you be allowed to do what you're asking to do?

---

# _Hashing function_

- Takes in an input
- Outputs a stings
- Given the same input, you get the same output
- One-way

---

# _Public Key Infrastructure_

- Asymmetric encryption
- Public key
  - used to encrypt
- Private key
  - used to decrypt
- To send an encrypted message to someone, you must encrypt the message with that persons public key, so they can use their private key to decrypt the message

---

# _HTTPS_

- Sensitive information can be included in a network request/response header/body
- Someone can listen in on the network

## SSL

- Includes a public key
- When you visit a secured website, your client asks for the servers certificate
- The client then encrypts the network request using the servers private key

---

# _CORS_

- Cross-Origin Resource Sharing
- Attempts to reduce bandwidth theft

* By default, the JavaScript running on `www.a.com` is forbidden access to the response from `www.b.com`
* CORS allows `www.b.com` to give permission to the JavaScript from `www.a.com` to access the response

- When you make an HTTP request, the browser adds an `Origin` property to the header with the current domain value
  - `Origin: http://`my-site`.com`
- The server, where the script makes its HTTP request, checks if this domain is allowed
- If so, it sends the response with a property of `Access-Control-Allow-Origin` in the response header
  - `Access-Control-Allow-Origin: http://`my-site`.com`
- If not, it sends the response header using its own domain:
  - `Access-Control-Allow-Origin: http://`third-party-site`.com`
- Upon receiving, the browser checks if the header is present and has the current domain value
- If the domains match, the browser carries on with request
- If not, it throws a CORS error

* A third-party server can allow all domains access to its response by sending this header:
  - `Access-Control-Allow-Origin: *`

- To work around CORS you can run a proxy
  - The Proxy goes between your browser and the actual server, and adds the headers on the fly
  - For development, this is a perfectly fine solution
  - Proxies:
    - https://github.com/Rob--W/cors-anywhere
    - https://github.com/gr2m/CORS-Proxy

---

# _JWTs_

- https://jwt.io/
- JSON Web Tokens
- A compact and self-contained way for securely transmitting information between parties as a JSON object
- For Authentication and Authorization

* Consists of three parts separated by dots (`.`)
  - `xxxxx.yyyyy.zzzzz`
  - Header
    - Information about the hashing algorithm and type
    - Typically consists of two parts:
      - the type of the token, which is JWT
      - the hashing algorithm being used, such as HMAC SHA256 or RSA
  - Payload
    - Contains the claims
      - Claims are statements about an entity (typically, the user) and additional data
      - There are three types of claims
        - registered, public, and private
    - Contains Expiration date
  - Signature
    - To create the signature
      - Take the
        - encoded header
          - base64 encoded
        - encoded payload
          - base64 encoded
        - secret key
        - algorithm specified in the header
      - and sign that by sending it through a hashing function
    - used to verify the message wasn't changed along the way
    - in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is

- The application or client requests authorization to the authorization server
  - This is performed through one of the different authorization flows
  - For example, a typical [OpenID Connect](http://openid.net/connect/) compliant web application will go through the `/oauth/authorize` endpoint using the [authorization code flow](http://openid.net/specs/openid-connect-core-1_0.html#CodeFlowAuth)
- When the authorization is granted (the user successfully logs in using their credentials ), the authorization server returns an access token to the application/client
- The server's protected routes will check for a valid JWT in the `Authorization` header, and if it's present, the user will be allowed to access protected resources (like an API)
  - The user agent should send the JWT, typically in the Authorization header using the Bearer schema
    - `Authorization: Bearer <token>`

## _Issuing_

- Someone wants to use our API, but they need a JWT to make API requests

1. Client asks for a JWT from the server
   1. POST request to '/authenticate'
      1. body
         1. username
         2. email
2. Server gets data
   1. Header
      1. alg: HS256
      2. type: JWT
   2. Payload
      1. comes from body
         1. username
         2. email
   3. Signature
      1. header + payload + secret
         1. sends through hashing function
            1. generates an output
               1. this is the signature
3. Server assembles JWT and sends back to client
   1. headers.payload.signature
   2. issues JWT

## _Authenticating_

- Client has a JWT
- Client wants to make an API request
  - DELETE 'api/v1/cats/13'
  - body: {token: JWT}
- Severs needs to almost remake the JWT to compare it to the JWT received
  - takes header and payload from body
  - adds secretKey
    - send to hashing function
      - signature should be the same as the signature received
        - if matches
          - make the request
        - if does not match
          - send 400-level response

---

# _OAuth_

- Open Authorization
- Token based authorization

* Authentication answers the question "Who are you?"
* Authorization answers the question: "What are you allowed to do?".

- Allow user to "log in" to a third-party without giving away their credentials
- Allows scoping of permissions

---

# _Auth0_

- Provides authentication and authorization as a service

## Tenant

- logical isolation unit
- No tenant can access the instance of another tenant

## Domains

- The base URL you will be using to access our API and the URL where users are redirected in order to authenticate
- tenentName + `auth0.com`

---
