# Facebook Developers

## Graph API
Click this link to go to FB Graph API Console https://developers.facebook.com/tools/explorer.
Use this to make api calls and get access tokens.

### Get Short Lived User Access Token
This can be generated from the side console in the graph api explorer console.

### Get Long Lived User Access Token
Send get request to this endpoint: https://graph.facebook.com/{graph-api-version}/oauth/access_token?
                                   grant_type=fb_exchange_token&
                                   client_id={app-id}&
                                   client_secret={app-secret}&
                                   fb_exchange_token={your-access-token}
                                   
- App ID and the App secret can be obtained from: App page -> Settings -> Basic

### Get User ID
Send get request to this endpoint: https://graph.facebook.com/me?access_token={your-access-token}


### Get Long Lived Page Access Token
