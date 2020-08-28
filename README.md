# Authentise Engineering

# Introduction to oAuth2

# What is oAuth2?

OAuth2 is a standard protocol for Authorization. OAuth2 is a continuation of the OAuth standard protocol that was built since 2006. OAuth2 focuses on the simplicity of client-side development while the process of implementing authorization. 

# OAuth2 requires 4 Roles:

1. Resource Owner - User who needs access to the API resource.
2. Resource Server - API resource store, which we need to secure.
3. Client - This is an API resource based application.
4. Authorization Server - Service allows access to the resource API.

# OAuth2 Token

1. Access Token is a Token to send and request information.This Token has a minimum life time of about 1 hour.
2. Refresh Token is used for new access token. This token is not a token sent to request information and life time will be longer.

# OAuth2 procedures
1. Client requests to the Resource Owner that it wants access to the Resource Server.
2. When the Resource Owner grants permission, the Client receives the authorization grant of the Resource Owner.
3. Client sends the authorization grant of the Resource Owner and client credentials to the Autorization Server.
4. If authentication is successful, the Authorization Server will return an access token.
5. Client calls to the Resource Server with an access token for authentication.
6. If authentication is successful, the Resource Server will respond to the information required by the Client.

# Endpoints and their purpose

Request a new Access Token using Refresh Token using HTTP POST in the Authorization Header with (Query Param).

# Details in this project !!!

# oAuth2 authorization server using Resource Owner Password Credentials Grant and a JWT bearer token

This grant type is used where the client is trusted by the resource owner (the user) and has a client id and client secret known by this server. Trust implies the user is willing to enter their username and password into the client, which usually means the client is issued or approved by the some organization that owns the authorization server.

eg. the Twitter IOS app issued by Twitter, but not a third-party app what authenticates against Twitter's API.

An IOS client use-case is:

1. The user would enter their username and password into the client. These do not need to be stored by the client (but it can use the IOS keystore).
2. The client authenticates (grant_type=password) against this server and receives an access token and refresh token. The client Id and client secret are also validated by this server.
3. The client uses the access token for all subsequent requests (http header Authorization: bearer )
4. If the access token expires, the client requests a new one from this server (grant_type=refresh_token) and receives a new access token
5. The refresh token is retained by the client so the user doesn't have to login again. Once the refresh token has expired the user will need to login again (or start again using credentials in the keystore).

The access token is generated using JWT. The benefits of this token are:

1. this server does not need to retain the tokens issued. It just needs to verify them.
2. the token can be passed straight through to other servers (eg. microservers) that only need to verify it (ie. they trust the signed JWT)
3. the token carries private claims that can be passed straight through to other servers (eg. user role/permission claims)
