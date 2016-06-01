A simple C# OAuth2 auth-code wrapper library.

## How to Create the Redirect

```csharp
var systemRedirectUri = OAuth2.CreateRedirect(
	new OAuth2.OAuth2Provider {
		ClientId = "my-client-id",
		ClientSecret = "my-client-secret",
		Scope = "email",
		AuthUri = "https://graph.facebook.com/oauth/authorize",
		AccessTokenUri = "https://graph.facebook.com/oauth/access_token",
		UserInfoUri = "https://graph.facebook.com/me"
	},
	"https://awesome-domain.com/my-awesome-oauth-callback");
```

This will give you a URI you can just forward the user too. They will sign in and give the app access, which will redirect back to: `https://awesome-domain.com/my-awesome-oauth-callback?code=XXX`

## How to Authenticate by Code

```csharp
var response = OAuth2.AuthenticateByCode(
	new OAuth2.OAuth2Provider { ... },
	"same redirect uri as before",
	"code from callback from provider");
```

The library will make a web request to the provider with the auth code given and, hopefully, return with a valid access token. You are now authorized with the given provider.