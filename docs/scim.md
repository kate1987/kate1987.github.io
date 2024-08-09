# SCIM provisioning overview

Lightrun user provisioning using the System for Cross-Domain Identity Management (SCIM) protocol allows you to automatically manage and communicate user data and permissions between identity providers (IdP) like Okta or Azure AD and a service provider like Lightrun. Lightrun supports Cross-domain Identity Management (SCIM 2.0) SCIM provisioning allows Admins to manage users directly from an IdP, removing the need to manage users in both locations in parallel.

## Guidelines for managing users using SCIM provisioning

The following rules and guidelines apply for managing users using SCIM:

- Only one IdM should be integrated with our SCIM.
- When you create users in SCIM, the users are displayed as read-only in the User Management tab in the Lightrun Portal.
- You cannot remove SCIM managed users from the Management Portal.
- By default, the SCIM users are added to the default Agent Pool and receive user-role permissions. 
- You can assign users to different agent pools and they will inherit the roles assigned to the assigned agent pool.
- Existing Lightrun users can be migrated to SCIM by selecting the  **Provision existing users with SCIM** toggle in the SCIM page.

## Provisioning existing Lightrun users with SCIM

Lightrun supports provisioning existing users through SCIM. This means you can shift the responsibility of managing your current Lightrun users to a chosen identity provider. However, it's important to ensure that these Lightrun users have been premanaged through SCIM before initiating the migration process.

1. Log in to your Lightrun account.
2. Click **Settings** on the top right-hand side of your screen to navigate to the **Identity and Access Management** tab > **Identity Configuration**.
3. The **Login methods** page opens.
4. To enable, click **SSO** toggle and configure SSO as described in [SSO](/sso). 
5. To enable, click **SCIM** toggle.
6. Click **Provision existing users with SCIM** toggle.
7. Click **Save**.
   The Lightrun users are now managed from your SCIM and disabled in the Lightrun Management Portal.


## Set up provisioning

Your SCIM provisioning setup will vary depending on the identity provider you use.

### Prerequisite

Enable SSO in the **Identity Configuration** page located under the **Identity and Access Management** tab. For more information, see [SSO](/sso).

We support setting up SCIM with the following IdPs:

- [SCIM Provisiong using Okta](scim-provisioning-okta.md)
- [SCIM Provisioning using Azure AD](scim-provisioning-azure-ad.md)




