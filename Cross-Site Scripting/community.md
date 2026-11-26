## Title
Stored XSS - Forum Discussions (Reddit Clone)
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://community.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the user registration and profile functionality of the application.

The application accepts user-controlled input in multiple fields, including First Name, Middle Name, Last Name, Username, Organization/Institution and Affiliation/Bio, without properly sanitizing or encoding the submitted data.

By injecting JavaScript payloads into these fields, an attacker may be able to execute arbitrary JavaScript when the stored information is displayed by the application.

Since the malicious input is stored in the application, the vulnerability may affect other users who access the affected content.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://community.pwnedbox.site/.

Navigate to the user registration page.

Locate the registration fields, including First Name, Middle Name, Last Name, Username, Organization/Institution and Affiliation/Bio.

Enter the following test payloads into the respective fields:

First Name:

'"><script>confirm(1)</script>

Middle Name:

'"><script>confirm(2)</script>

Last Name:

'"><script>confirm(3)</script>

Username:

'"><script>confirm(4)</script>

Organization/Institution:

'"><script>confirm(5)</script>

Affiliation/Bio:

'"><script>confirm(6)</script>

Complete the remaining required registration fields.

Submit the registration form.

Navigate to the page where the submitted user information is displayed.

Observe the JavaScript confirmation dialog.

Verify whether the payload executes again when the stored information is accessed or viewed.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1706" height="662" alt="Screenshot 2026-11-23 175852" src="https://github.com/user-attachments/assets/7c681623-9644-466e-b5e0-8ffbeb82a455" />

<img width="661" height="307" alt="Screenshot 2026-11-23 175924" src="https://github.com/user-attachments/assets/9e011c48-67d6-4b3d-835b-c9a3184f41c6" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could potentially exploit this vulnerability to execute malicious JavaScript in the browsers of users viewing affected content.

Potential consequences include:

Stealing sensitive information accessible to JavaScript.

Performing unauthorized actions through an authenticated user's session.

Displaying fake login forms for phishing attacks.

Modifying application content displayed to users.

Targeting multiple users who access the affected profile or discussion content.

The impact depends on which users can access the affected content and where the application renders the stored input.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement server-side input validation for all user-controlled registration fields.

Apply context-aware output encoding before displaying user-supplied data.

Sanitize HTML input using a trusted HTML sanitization library wherever HTML is permitted.

Prevent direct execution of user-controlled JavaScript.

Avoid inserting untrusted data using unsafe DOM methods such as innerHTML.

Implement a restrictive Content Security Policy (CSP).

Configure session cookies with HttpOnly, Secure and appropriate SameSite attributes.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
