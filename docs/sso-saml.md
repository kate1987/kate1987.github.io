# Configure SAML SSO using Okta for your Organization

## Overview
Lightrun offers support for Single Sign-On (SSO) using Okta as the identity provider (IdP) by integrating Lightrun with the SAML 2.0 integration in Okta.

Using SAML, Lightrun functions as a service provider, receiving user authentication information from Okta, which serves as the external identity provider. When SSO is enabled, Lightrun is no longer responsible for user authentication, but still manages the redirection of login requests to the identity provider and verifies the integrity of the response from the identity provider.
### Terminology

- Identity Provider (IdP): A service that manages user accounts, providing authentication services to applications. Lightrun supports Okta for this purpose.
- Service Provider: The website that hosts apps. In our case, it is Lightrun.
- Service Provider Entity UID: The URL is used to uniquely identify your service provider and is generated in the SSO page in the Lightrun Management Portal.
- Single Sign on URL: This endpoint URL is generated in the SSO page in the Lightrun Management Portal.
- Single Sign on Service URL: The URL is used for sending authentication requests (`SAMLAuthnRequest`) and is generated in Okta.

The process of setting up SSO involves these main stages:

1. Setting up the Lightrun-SAML integration in Okta. 
2. Configuring and enabling SSO in the Lightrun Management Portal.
   
## Set up Lightrun SAML integration in Okta

Setting up the Lightrun integration in Okta includes these main steps.

###### STEP 1: COPY URLS in lightrun management portal 

1. Log in to your Lightrun account.
2. In the **Identity and Access Management** tab > **Identity Configuration** > **Provisioning**.
3. To enable SSO, click the **SSO** toggle.
4. Click **Okta** as your Identity Provider.
5. From the **Single sign on URL** field, click **Copy**. 
   
   This field will serve as the redirect URL used when configuring the identity provider.

6. From the **Service Provider entity ID** field, click **Copy**. This field will serve as the unique identification of the SAML Service provider.

###### STEP 2: SET UP LIGHTRUN SAML INTEGRATION IN OKTA

1. Sign in to Okta.
2. In the Administration console, click the **Application** tab.
3. Click **Create App Integration**, and select **SAML 2.0**, and click **Next**.
    
    The Create Lightrun-SAML Integration page opens.

4. Click on the **General Settings** tab.
5. In the **App name** field, provide a name for the integration. For example, `<lightrun-app>` and click **Next**.
6. Proceed to the **Configure SAML** tab.
   
    The SAML Setting window opens.

7.  In the **Single sign-on URL** field, paste the URL you copied from the **Single sign on URL** field within the SSO page in the Lightrun Management Portal.
8. In the **Audience URI (SP Entity ID)** field, paste the URL you copied from the **Service provider entity ID** field.
9.  In the **Name ID format** field, select **EmailAddress** from the list.
10. In the **Application username** field, select **Email** from the list.
11. Click **Next**.
12. Fill in the feedback form, and click **Finish**.

## Set up SSO in Lightrun

###### STEP 1: COPY URLS in OKTA 

1. In Okta, access your `<lightrun app>` that you configured in the previous stage. 
2. Access the SSO tab, and copy the **Sign-On URL**. This URL will need to be pasted in the **SSO** page in the Lightrun Management Portal.

###### Step 2: CONFIGURE and Enable SSO IN THE LIGHTRUN

Setting up the SSO in the Lightrun Management Portal includes these main steps.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the **Identity and Access Management** tab > **Identity Configuration** > **Login methods** > **Provisioning** section.

    ![Enable SSO with Okta --70%](/assets/images/sso-enable-with-okta.png)

3. To enable SSO, click the **SSO** toggle.
4. Ensure that your external Identity Provider (IdP) is set to **Okta**. 
5. In the **Single Sign On Service URL** field, paste the **Sign-On URL** you copied in the [Copy URLs in Okta step](#step-1-copy-urls-in-okta), which is used to send authentication requests (`SAMLAuthnRequest`).
6. Click **Save**.

## Further Reading

- [Single Sign-On Overview](sso.md)
- [Log in to the Lightrun Management Portal using SSO](sso-login.md)

