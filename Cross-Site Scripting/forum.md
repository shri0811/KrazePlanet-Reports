## Title
Stored XSS - Acronis
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://forum.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the user profile functionality.

The application appears to accept user-supplied HTML and JavaScript in profile fields such as profile information and signature without properly sanitizing the input.

An attacker can inject malicious HTML containing JavaScript event handlers. When the affected content is rendered by the application, the injected JavaScript executes in the victim's browser.

Since the malicious payload is stored in the profile, it may execute whenever another user visits or views the affected profile or content containing the injected information.

<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://forum.pwnedbox.site/.

Log in to the application.

Navigate to the user profile or profile settings section.

Locate the editable profile information and signature fields.

Insert the following test payload into a supported field:

<img src=x onerror=confirm(1)>

Save the profile changes.

Navigate to the page where the updated profile information or signature is displayed.

Observe that a JavaScript confirmation dialog appears.

This confirms that the injected JavaScript is being executed when the stored content is rendered.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="700" height="980" alt="Screenshot 2026-11-23 061342" src="https://github.com/user-attachments/assets/a9e40a0f-bdab-4cc6-87d1-d715c7b1ef47" />

<img width="1075" height="351" alt="Screenshot 2026-11-23 175758" src="https://github.com/user-attachments/assets/d5589d9c-f87a-4cbd-9f2e-7e0fd8ccca8e" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could exploit this vulnerability to execute arbitrary JavaScript in the browser of users viewing the affected content.

Potential consequences include:

Stealing sensitive information accessible to JavaScript.

Performing unauthorized actions through an authenticated user's session.

Displaying fake login forms for phishing attacks.

Modifying the content displayed on the forum.

Targeting multiple users who view the affected profile or forum posts.An attacker could exploit this vulnerability to execute arbitrary JavaScript in the browser of users viewing the affected content.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement proper server-side input validation and HTML sanitization.

Encode user-generated content before displaying it in HTML.

Remove or safely handle dangerous HTML elements and JavaScript event attributes.

Avoid rendering untrusted user input directly as HTML.

Implement a restrictive Content Security Policy (CSP).

Configure session cookies with appropriate HttpOnly, Secure, and SameSite attributes.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
