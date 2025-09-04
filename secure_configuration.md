# Secure Configuration Guidance for A-SCEND

This guide outlines best practices for federal agencies to securely configure A-SCEND, ensuring compliance with federal security requirements.

## Federated Identity
A-SCEND offers username, password, and TOTP MFA authentication by default. Agencies must configure the Single Sign-On (SSO) authentication offered within A-SCEND to meet federal phishing-resistant authentication requirements (KSI-IAM-01)

Configure SSO:

1. Navigate to the SSO settings within the A-SCEND platform.

2. Select your IdP. A-SCEND offers connections to Okta, Microsoft Active Directory (Entra ID), Google Workspace, and custom SAML and OIDC.

3. Follow the on-screen instructions from Auth0 to configure the connection for your selected IdP.

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
