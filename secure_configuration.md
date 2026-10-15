# Secure Configuration Guidance for A-SCEND

This guide outlines best practices for federal agencies to securely configure A-SCEND, ensuring compliance with federal security requirements.

## Federated Identity
Federal accounts in A-SCEND must sign in through the agency's own identity provider (IdP) using Single Sign-On (SSO). Federal SSO is provided by the A-SCEND identity broker (Verity), which runs inside the A-SCEND FedRAMP authorization boundary and connects to your agency IdP using SAML 2.0 or OpenID Connect (OIDC).

**Supported IdPs:** Any IdP that supports SAML 2.0 or OIDC, including Microsoft Entra ID, Okta, and Google Workspace.

**Phishing-Resistant MFA (KSI-IAM-01):** A-SCEND relies on your agency IdP to authenticate each user, including multi-factor authentication. Configure the IdP sign-in policy that applies to A-SCEND to require phishing-resistant MFA, such as PIV/CAC or FIDO2/WebAuthn security keys, for every user.

**SSO Is Required for Federal Accounts:** A-SCEND's standard sign-in (username, password, and TOTP) cannot be used to access a federal account. A-SCEND refuses requests to a federal account from any session that did not sign in through federal SSO, including sessions held by A-LIGN personnel.

### Configure Federal SSO
Do not use the SSO settings page within A-SCEND for a federal account. That page configures standard sign-in, and it cannot create connections from a federal session. Configure federal SSO with an SSO setup link instead:

1. **Request a setup link.** Contact A-LIGN to confirm that your A-SCEND account is designated as a federal account and to request an SSO setup link. A-LIGN sends the link to your agency's IdP administrator.

2. **Open the link within 3 days.** The link is specific to your A-SCEND account and expires after 3 days. If it expires, ask A-LIGN for a new one. Do not forward the link: anyone who has it can configure SSO for your account.

3. **Create the connection.** On the setup page, choose SAML 2.0 or OIDC. Register A-SCEND in your IdP using the service provider details shown on the setup page, then enter your IdP's metadata (SAML) or its discovery URL, client ID, and client secret (OIDC).

4. **Send each user's email address.** Configure your IdP to send the user's email address when they sign in. A-SCEND matches this address, ignoring case, to an existing A-SCEND user. SSO does not create users: add each user to your A-SCEND account and assign them a role before they sign in, using the same email address your IdP sends.

5. **Limit who can use the connection.** In your IdP, assign the A-SCEND application only to personnel who are authorized to access your federal data in A-SCEND, and remove the assignment when that access is no longer needed.

6. **Test sign-in** using the steps below.

### Sign In with Federal SSO
1. On the A-SCEND sign-in page, select **Sign into Federal A-SCEND**.

2. Enter the account ID that A-LIGN provided for your account and select **Continue**.

3. Review the System Use Notification, select **Sign into your organization**, and then select **I Accept** to continue to your agency IdP.

4. Authenticate with your agency IdP. A-SCEND signs you in when your IdP returns you.

Start sign-in from A-SCEND. Sign-in started from your IdP's application portal (IdP-initiated SSO) is not supported.

### Sign Out
Sign out at the end of each session. Signing out revokes your A-SCEND session on the server. It does not end your session with your agency IdP, which your IdP's session settings control.

## Role/Attribute-based Access Control
Access to federal data within A-SCEND should be restricted to authorized personnel only. The following roles can be assigned within A-SCEND to limit access to users with access to federal data:

**Company Administrator and Engagement Administrator:** These roles have broad access to all projects and federal data within your A-SCEND client account. Only users who are allowed access to federal data should be assigned to these roles.

**Security Coordinator, Security Analyst 1, and Security Analyst 2:** These roles only have access to projects they are specifically assigned to. Utilize these roles to grant granular access and restrict users from accessing projects with federal data.

## API Integration
The A-SCEND API allows for the transfer of federal data and must be managed with extreme care. API integration follows the OAuth standards for authenticating and authorization. https://oauth.net/2/ Each OAuth application is scoped to a role at an Account level.

**API Documentation:**
https://docs.a-scend2.com/
 
**Limit API Access:** The ability to manage the API is restricted to Company and Engagement Administrators. Ensure these roles are assigned only to trusted personnel who can access federal data.

**Assess Third-Party Systems:** Before integrating the A-SCEND API with any external system, conduct a thorough security assessment. Verify that the third-party system has appropriate security controls in place to protect federal data.

**Use Dedicated API Keys:** Generate unique API keys for each integration and avoid sharing them. The API keys should be stored securely, ideally in a secret management system, and never hardcoded in applications.
