## Title
Reflected XSS - Imgur Mobile
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://media.pwnedbox.site/
The application is vulnerable to Reflected XSS through the account profile URL. During testing, specially crafted HTML and JavaScript payloads were injected into the account-related URL.

The application failed to properly encode the injected input, allowing the browser to interpret the payload as executable JavaScript. A JavaScript prompt displaying media.pwnedbox.site appeared, confirming successful script execution.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Open https://media.pwnedbox.site/

Navigate to the account profile or Messages section.

Inject the following payload into the profile URL:

"><img src=x onerror=prompt(document.domain)>

Load the modified URL.

Observe the JavaScript prompt displaying media.pwnedbox.site.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1361" height="967" alt="Screenshot 2026-11-18 065243" src="https://github.com/user-attachments/assets/72a01623-9999-4495-97c9-651a9604c1d9" />

<img width="811" height="1001" alt="Screenshot 2026-11-18 065254" src="https://github.com/user-attachments/assets/303f787d-47ca-4e81-93ac-15cac9fb7170" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
JavaScript Execution: Attackers can execute scripts in the browser of users visiting the crafted URL.

Phishing Attacks: Fake login forms can be displayed to steal user credentials.

Session Information Exposure: Information accessible to JavaScript may be exposed.

Website Manipulation: Attackers could modify page content or display misleading messages.

Unauthorized Actions: Scripts may perform actions using an authenticated user's session, depending on application protections.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Input Validation: Validate user-controlled URL parameters and profile-related input.

Output Encoding: Apply context-specific HTML encoding before rendering user input.

Safe DOM Handling: Avoid unsafe HTML insertion methods such as innerHTML.

Content Security Policy: Implement a restrictive CSP to reduce unauthorized script execution.

Secure Cookie Configuration: Use HttpOnly, Secure, and appropriate SameSite cookie attributes.

Regular Security Testing: Perform periodic security assessments to identify and fix XSS vulnerabilities.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
