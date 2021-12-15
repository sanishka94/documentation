# Facebook Developers

## Graph API
Click this link to go to FB Graph API Console https://developers.facebook.com/tools/explorer.
Use this to make api calls and get access tokens.

### Get Short Lived User Access Token
This can be generated from the side console in the graph api explorer console.

### Get Long Lived User Access Token
Send get request to this endpoint: https://graph.facebook.com/{graph-api-version}/oauth/access_token?grant_type=fb_exchange_token&client_id={app-id}&client_secret={app-secret}&fb_exchange_token={user-access-token}
                                   
- An example for graph API version: "v12.0". Make sure you put the current version here.
- App ID and the App secret can be obtained from: App page -> Settings -> Basic 
- or from the url: https://developers.facebook.com/apps/{app-id}/dashboard)
- For the access token, use your (short lived) access token generated from the graph api console.

### Get User ID
Send get request to this endpoint: https://graph.facebook.com/me?access_token={user-access-token}


### Get Long Lived Page Access Token
Send get request to this endpoint: https://graph.facebook.com/{graph-api-version}/{user-id}/accounts?access_token={long-lived-user-access-token}
or : https://graph.facebook.com/{graph-api-version}/{page-id}/?fields=access_token&access_token={long-lived-user-access-token}

- An example for graph API version: "v12.0". Make sure you put the current version here.
- The Long lived pags access token will come in the "access token" attribute.
- The page Id can be obtained in the same way the user id is obtained, but with a short lived page token taken from the graph api explorer

### Debug
To debug and in some cases extend access tokens, use this link: https://developers.facebook.com/tools/debug/accesstoken


## Facebook Login
- Reference: 
  - https://developers.facebook.com/docs/reference/javascript/FB.getLoginStatus
  - https://developers.facebook.com/docs/reference/javascript/FB.login/v12.0
