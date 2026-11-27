## Title
Stored XSS - Video Streaming Service (Netflix Clone)
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://netflix.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the Sign Up functionality of the Video Streaming Service.

The application accepts user-controlled input in registration fields such as Full Name and Username without properly sanitizing or encoding the submitted data.

An attacker can inject JavaScript into these fields during account registration. The injected payload is subsequently executed when the application processes or renders the submitted user information.

This vulnerability allows JavaScript execution within the application's origin and may affect other users who view the affected stored information.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://netflix.pwnedbox.site/.

Open the Sign Up form.

Enter the following payload in the Full Name field:

'">shri<script>confirm("hari")</script>

Enter the following payload in the Username field:

'">shri<script>confirm("hari1")</script>

Enter a valid email address.

Enter a password.

Click the Create Account & Sign Up button.

Observe the browser confirmation dialog displaying hari1.

This confirms that the injected JavaScript executes during the registration process.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="723" height="308" alt="Screenshot 2026-11-23 184020" src="https://github.com/user-attachments/assets/2123a668-84d1-4f20-8013-d0001ae251f9" />

<img width="1057" height="922" alt="Screenshot 2026-11-23 184116" src="https://github.com/user-attachments/assets/ac9942f0-c1ae-4a52-9dd2-ebf9cb5a6c4e" />

<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could exploit this vulnerability to execute arbitrary JavaScript in the browsers of users interacting with affected application content.

Potential consequences include:

Stealing sensitive information accessible to the application.

Performing unauthorized actions using an authenticated user's session.

Manipulating user account information and displayed content.

Redirecting users to malicious websites.

Conducting phishing attacks against registered users.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement server-side input validation for all registration fields, including Full Name and Username.

Apply context-aware output encoding before displaying stored user information.

Sanitize user input wherever HTML content is permitted.

Avoid using unsafe DOM methods such as innerHTML to render user-controlled data.

Use textContent when displaying plain-text user information.

Implement a restrictive Content Security Policy (CSP) to reduce the impact of XSS attacks.

Ensure that user-controlled data is safely handled throughout the registration and account display functionality.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
