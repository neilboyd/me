# [NDC Security](https://ndc-security.com/) - Oslo 8-11 January 2024

## Workshop: [Identity & Access Control for modern Applications and APIs using ASP.NET Core 8](https://ndc-security.com/workshops/identity-and-access-control-for-modern-applications-anders-abel/3cbf535885dc) *Ander Abel*

### Day 1

Apparently the workshop has been going for 10 years, but it's constantly updated and still very much relevant.

Browser talks to webapp, services. Services talk to each other.
Assume zero trust, unlike 10 years ago when we trusted everything inside the firewall.

[`IIdentity`](https://learn.microsoft.com/en-us/dotnet/api/system.security.principal.iidentity?view=netframework-1.1)
and
[`IPrincipal`](https://learn.microsoft.com/en-us/dotnet/api/system.security.principal.iprincipal?view=netframework-1.1)
have been around since the start of .Net and are still the basis of authentication and authorization,
but they're based on a name and roles, which is not very flexible.

Identity name should be:
- immutable (persistent)
- unique
- never re-used

So don't use things like email address, or a social security number that's based on gender (like Norway does/did).
Use a guid.

.Net 4.5 introduced **claims** into .Net framework in 2012.
Claims are a key/value pair, with an optional issuer.

[`ClaimsIdentity`](https://learn.microsoft.com/en-us/dotnet/api/system.security.claims.claimsidentity?view=netframework-4.5)
implements `IIdentity`.
[`ClaimsPrincipal`](https://learn.microsoft.com/en-us/dotnet/api/system.security.claims.claimsprincipal?view=netframework-4.5)
implements `IPrincipal` and contains a collection of `ClaimsIdentity`s.

Claim **key**:
- OpenId defines a set of standard claims
- but it can be anything
- `sub` is kinda like `Name` in original `IIdentity`
  - "human"
  - unique at issuer

Claim **type** - eg to tie name to a well-known name.
Or can specify the type in the constructor.

`IIdentity.IsAuthenticated` is read-only. It's set by defining `authenticationType` in the constructor.

**Tip:** always use the
[4 parameter constructor](https://learn.microsoft.com/en-us/dotnet/api/system.security.claims.claimsidentity.-ctor?view=netframework-4.5#system-security-claims-claimsidentity-ctor(system-collections-generic-ienumerable((system-security-claims-claim))-system-string-system-string-system-string))
(second parameter is `authenticationType`).

ASP.NET middleware can handle request, or just part of it (ie process and continue).
Defined in order, eg first static files, then HSTS, then authentication, then authorization.

[Auth middleware extension methods](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication?view=aspnetcore-8.0)
are badly named:
- [`SignInAsync`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.signinasync?view=aspnetcore-8.0) - creates a session
- [`ChallengeAsync`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.challengeasync?view=aspnetcore-8.0) - initiates sign in
- [`AuthenticateAsync`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authentication.authenticationhttpcontextextensions.authenticateasync?view=aspnetcore-8.0) - queries if authenticated

Always validate `ReturnUrl` when redirecting.
[`LocalRedirect`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.localredirect?view=aspnetcore-8.0)
does that, or manually check with
[`IsLocalUrl`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.iurlhelper.islocalurl?view=aspnetcore-8.0)
and handle if it's not.

[Data protection (DPAPI) in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/security/data-protection/configuration/overview?view=aspnetcore-8.0):
- manages the cookie encryption
- manages the keys
  - rotation
  - sharing across services that need to share, eg multiple webapp instances

In our IdentityServer we skipped key management
["for now"](https://github.com/NIPOSoftwareBV/nfield-identity/blob/master/Nfield.Identity/Startup.cs#L112).
There are
[examples](https://github.com/IdentityServer/IdentityServer4/tree/main/samples/KeyManagement)
in IdentityServer4 source.

`[Authorize("policy")]` attribute (new way).
Or can check in code.
Or in a view.  
`[Authorize(Roles="roles")]` attribute (old way).

`AddPolicy("policy", options => {...})]`
- can just require claims
- or can be more dynamic - `RequireAssertions` - but then can only check in code, not attribute
- if `RequireAssertion` gets too complex, use the authorization handler framework - see the lab

`RemoteAuthenticationHandler` for delegated auth.
`SignInAsync` not implemented - use `ChallengeAsync` instead.  
eg Google doesn't implement `SignOutAsync` because they don't want you to sign out.

Redirect from Google assumes `ReturnUrl` is safe - se we should validate it to prevent open redirection.

Google handler writes directly to the cookie handler that we define first in the pipeline.
- we might not want that
- can add another "temp" scheme in between
- convert Google identity to our identity
- see the lab

**OpenId Connect** "using IdentityServer as an example".

Endpoints:
- discovery - `/.well-known/openid-configuration` - static json
- authorize - html
- token - api

nonce (number used once) is OpenId Connect's way of doing XSS protection,
ie checking that the response is for my request.

Identity token contains header, payload, signature.

Discovery endpoint includes `jwks_uri` - list of keys so that we can validate the signature.

There's a list of validations that we should do on the token - defined in
[OpenId spec](https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation).  
Use
[`JsonWebTokenHandler.ValidateTokenAsync`](https://learn.microsoft.com/en-us/dotnet/api/microsoft.identitymodel.jsonwebtokens.jsonwebtokenhandler.validatetokenasync?view=msal-web-dotnet-latest#microsoft-identitymodel-jsonwebtokens-jsonwebtokenhandler-validatetokenasync(system-string-microsoft-identitymodel-tokens-tokenvalidationparameters))
to do it - using properties from the key.  
But then also validate nonce:
- that's OpenId-specific - not part of JWT
- nonce is usually generated in the authorize request and written to a cookie,
  and then read back from the cookie when validating

AAD can also be used as identity provider, but it's not very customizable.
IdentityServer lets you fully customize.

IdentityServer is just a place to put all the code we've been writing up to now
so that it can be shared across multiple clients.
The client code to use it is very simple - just configuration in `Startup`.  
One IdentityServer that multiple clients use - SSO.

**Tip:** always use https, even locally, because it's handled differently to http.
