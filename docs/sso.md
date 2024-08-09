# Lightrun Single Sign-On (SSO)

--8<-- "ux-reference/manager-role-only.md"

Lightrun supports Single Sign-On (SSO) with SAML, enabling members of your organization to log in to Lightrun using their credentials stored in your organization’s Okta or Azure AD Identity Providers (IdPs).

Enabling Single Sign-On (SSO) in Lightrun streamlines the login process and minimizes the administrative burden of handling numerous user accounts and passwords across various applications. SSO enhances security by consolidating access through a unified interface with a single set of credentials.

## How does SSO work in Lightrun?

The authentication between Lightrun (the Service Provider) and Okta or Azure AD (the Identity Providers) is as follows:

1. The user browses to the Lightrun Management Portal URL.
2. Lightrun transmits a token that includes specific user information, such as their email address, to Okta or Azure AD, the IdPs, as part of a request to authenticate the user.
3. The IdP parses the SAML request and authenticates the user.
4. The IdP then generates a SAML response, which it sends back to Lightrun.
5. Lightrun, in turn, parses the SAML response, extracting the details to establish the user’s access appropriately.

## Lightrun SSO supported deployments

Lightrun supports the following SSO deployment types:

- SSO using Okta: This option is solely for authentication purposes. It allows users within the organization to securely access Lightrun using a single set of credentials.

- SSO with SCIM Provisioning: This option allows administrators to efficiently manage users from within Okta or Azure AD, eliminating the need to handle user management in both locations simultaneously.

## Get Started with SSO

To begin working with SSO in Lightrun, read the following:

- [Set up SSO with SAML in Okta](sso-saml.md)
- [Log in to the Lightrun Management Portal using SSO](sso-login.md)
