SpringSecurityOAuth2
====================

Securing Restful Web Services with Spring Security and OAuth2 

The flow of application will go something like this:
1)	User sends a GET request to server with five parameters: grant_type,  username, password, client_id, client_secret;  something like this

http://localhost:8080/SpringRestSecurityOauth/oauth/token?grant_type=password&client_id=restapp&client_secret=restapp&username=beingjavaguys&password=spring@java  

2)	Server validates the user with help of spring security, and if the user is authenticated, OAuth generates a access token and send sends back to user in following format.
{
•	"access_token": "22cb0d50-5bb9-463d-8c4a-8ddd680f553f",
•	"token_type": "bearer",
•	"refresh_token": "7ac7940a-d29d-4a4c-9a47-25a2167c8c49",
•	"expires_in": 119
}
Here we got access_token for further communication with server or to get some protected resourses(API’s), it mentioned a expires_in time that indicates the validation time of the token and a refresh_token that is being used to get a new token when token is expired.
3)	 We access protected resources by passing this access token as a parameter, the request goes something like this:
              http://localhost:8080/SpringRestSecurityOauth/api/users/?access_token=8c191a0f-ebe8-42cb-bc18-8e80f2c4238e
Here http://localhost:8080/SpringRestSecurityOauth is the server path, and  /api/users/
Is an API  URL that returns a list of users and is being protected to be accessed.
4)	If the token is not expired and is a valid token, the requested resources will be returned.
5)	In case the token is expired, user needs to get a new token using its refreshing token that was accepted in step(2). A new access token request after expiration looks something like this:
http://localhost:8080/SpringRestSecurityOauth/oauth/token?grant_type=refresh_token&client_id=restapp&client_secret=restapp&refresh_token=7ac7940a-d29d-4a4c-9a47-25a2167c8c49
And you will get a new access token along with a new refresh token.
