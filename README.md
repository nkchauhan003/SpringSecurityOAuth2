SpringSecurityOAuth2
====================

Securing Restful Web Services with Spring Security and OAuth2 
<br/><br/><br/>
The flow of application will go something like this:<br/><br/>
1) User sends a GET request to server with five parameters: grant_type,  username, password, client_id, client_secret;  something like this
<br/>
<a href="http://localhost:8080/SpringRestSecurityOauth/oauth/token?grant_type=password&client_id=restapp&client_secret=restapp&username=beingjavaguys&password=spring@java">http://localhost:8080/SpringRestSecurityOauth/oauth/token?grant_type=password&client_id=restapp&client_secret=restapp&username=beingjavaguys&password=spring@java</a>  <br/><br/>

2) Server validates the user with help of spring security, and if the user is authenticated, OAuth generates a access token and send sends back to user in following format.<br/>
{<br/>
"access_token": "22cb0d50-5bb9-463d-8c4a-8ddd680f553f",<br/>
"token_type": "bearer",<br/>
"refresh_token": "7ac7940a-d29d-4a4c-9a47-25a2167c8c49",<br/>
"expires_in": 119<br/>
}<br/><br/>

Here we got access_token for further communication with server or to get some protected resourses(API’s), it mentioned a expires_in time that indicates the validation time of the token and a refresh_token that is being used to get a new token when token is expired.<br/><br/>
3) We access protected resources by passing this access token as a parameter, the request goes something like this:<br/><br/>
<a href="http://localhost:8080/SpringRestSecurityOauth/api/users/?access_token=8c191a0f-ebe8-42cb-bc18-8e80f2c4238e">http://localhost:8080/SpringRestSecurityOauth/api/users/?access_token=8c191a0f-ebe8-42cb-bc18-8e80f2c4238e</a><br />
Here http://localhost:8080/SpringRestSecurityOauth is the server path, and  /api/users/
Is an API  URL that returns a list of users and is being protected to be accessed.
<br/><br/>
4) If the token is not expired and is a valid token, the requested resources will be returned.<br/><br/>
5) In case the token is expired, user needs to get a new token using its refreshing token that was accepted in step(2). A new access token request after expiration looks something like this:<br/>
<a href="http://localhost:8080/SpringRestSecurityOauth/oauth/token?grant_type=refresh_token&client_id=restapp&client_secret=restapp&refresh_token=7ac7940a-d29d-4a4c-9a47-25a2167c8c49">http://localhost:8080/SpringRestSecurityOauth/oauth/token?grant_type=refresh_token&client_id=restapp&client_secret=restapp&refresh_token=7ac7940a-d29d-4a4c-9a47-25a2167c8c49</a><br/><br/>
And you will get a new access token along with a new refresh token.
