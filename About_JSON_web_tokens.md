# JSON Web Tokens

A JSON web token is an important encryption tool used to send and receive user information to a web application. Not only are JSON tokens useful for securing valuable client information, but JSON web tokens also allow a web application to keep knowledge about a user while the application is running. The token is a message sent between a client and a server that consists of two or three parts: header, payload, and a signature. Each token consists of a long string of characters and each part is separated by a period “.”. This type of web token is known as a JWT, pronounced “JOT” in practice.

JWT's typically communicate between two servers, an authorization server and an application server. first, a login request is received by the authorization server (typically via HTTP). The Authorization server comparies the login information with list of authorized users and decides whether a JWT is issued. If everything checks out a JWT is issued, together with a secret key that indicates user authentication and access role. This secret key is sent to the user, who then sends to the app server via a HTTP request. The message is decrypted via a shared secret key to reveal the user name and role. If details check out with the app server, then the app server will share/display requested information. 

## JWT Implementation Process

To implement a JWT, the following steps need to take place:
1. A user logs into a web application.
2. The server authenticates the user and sends a JWT back to the user.
3. The user can then send messages to the application server attached to the generated JWT, and the server will verify the user.

## Deserialized vs. Serialized JWTs

There are two forms in which a JSON token can arrive. The first is a deserialized token with just a header and a payload. The header of a deserialized token tells the web server how the JSON token was created and which decryption techniques to use. Most of the time, the header will include two fields: the message type and the algorithm used. The type is usually set to JWT, and the algorithms used are most commonly HS256 or SH256 encryption. JWT deserialized tokens are useful in practice where encryption is not necessary and speed is the most desirable outcome, as deserialized tokens do not need to be encrypted. However, the header must always be present in a JWT token.

The payload of a JWT deserialized token holds the user data and could consist of many fields, such as user ID, IP address, or system information. However, the payload of a deserialized JWT can be read by anyone, so it is advisable to withhold any sensitive information from your deserialized JWT payload. The data within the JWT payload is known as a claim. Both the deserialized header and payload are objects and appear as such in code. Parts of a deserialized token appear as follows:

Header:
``` 
{

     “typ”:”JWT”,

     “algo”:”SH256”

}
```
Payload:
``` 
{

     “userId”:”1234567-abc”,

     “iss”:”https://myServer.com/”,

     “sub”:”/subDirectory”,

     “Exp”:”20212512”

}
```
JWT serialized tokens have the additional benefit of signatures, allowing the secure transfer of data from client to application. For security purposes, in practice, most JWT will have all three fields and therefore be serialized. A serialized token has the header and payload hashed together just like a deserialized JWT, as talked about above. The header and payload are encoded using Base64URL and separated by a period (Neekhara 2019). The signature is then appended onto the back of the encrypted message to assure the data is delivered uncorrupt. The serialized web token will consist of these three fields:

Header:
```

{

     “typ”:”JWT”,

     “alg”:”SH256”

}
```
Payload:
```
{

     “userId”:”1234567-abc”,

     “name”:”bob”

     “iss”:”https://myServer.com/”,

     “admin”:true,

     “Exp”:”20212512”

}
```
Signature: “myName” encoded

The encrypted token will be three strings separated by periods, looking similar to this:

`jsMCAFNidaT2cSknOSda.HkasXnPksHahYsaNQsdTl.PlWecsfaLhGGWBvAxZPLkNbt`

Note: In practice this token can be hundreds of characters depending on how much information the web application requests.

The following is an example of the structure of the full JSON web application token architecture:
```
SH256(

     base64UrlEncode(header) + "." +

base64UrlEncode(payload)+”.”+

secret)
```
In practice, a JWT is one layer of security on a system with many. Normally, web applications will also utilize SSL or TLS, so JWT authorization can sometimes be repetitive and add application service overhead. Depending on the application and implementation, JSON web tokens should be utilized to assure user data is accurate and secure.

# How to create request token
For this project, Postman is used to create the security token. Postman is an API platform for building and using API's. However, if we wanted to create the security token from scratch using python, it would look something like this: 

``` python
import requests
url = "localhost:400/books"
payload = {}
headers = {
    '': '',
    'Authorization': 'Bearer
    jsMCAFNidaT2cSknOSda.HkasXnPksHahYsaNQsdTl.PlWecsfaLhGGWBvAxZPLkNbt
    jsMCAFNidaT2cSknOSda.HkasXnPksHahYsaNQsdTl.PlWecsfaLhGGWBvAxZPLkNbt'
}

response = requests.request("GET", url, headers=headers, data = payload) #send request to URL defined above
```