## Title
Stored XSS - Product Reviews (Flipkart Clone)
<!-- Write a short, clear title describing the vulnerability and where it was found. Example: Stored XSS in User Profile -->

## Description
**Affected URL:** https://members.pwnedbox.site/
A Stored Cross-Site Scripting (XSS) vulnerability was identified in the product review functionality of the application.

The application allows users to submit product reviews containing potentially malicious JavaScript without properly sanitizing or encoding the input.

The vulnerability exists in the Headline / Short Title and Detailed Review Comments fields. An attacker can inject JavaScript payloads into these fields, which may execute when the stored review is rendered by the application.

Since the submitted content is stored in the application, other users viewing the affected product review may also be exposed to the malicious script.
<!-- Explain what the vulnerability is, where it exists, and why it is a security issue. Include the affected URL or endpoint. -->

## Steps to Reproduce
Visit https://members.pwnedbox.site/.

Open the product page with the following URL:

https://members.pwnedbox.site/index.php?product_id=1

Navigate to the Write a Customer Review section.

Select a star rating.

Enter the following payload in the Headline / Short Title field:

"><shri<script>confirm(1)</script>

Enter the following payload in the Detailed Review Comments field:

"><shri<script>confirm(2)</script>

Submit the product review.

Observe the application response.

A JavaScript confirmation dialog displaying 2 appears on members.pwnedbox.site.
<!-- Provide clear, numbered steps so another person can reproduce the issue. Include required requests, parameters, and actions. -->

## POC (Proof of Concept)
<img width="1592" height="840" alt="Screenshot 2026-11-23 180219" src="https://github.com/user-attachments/assets/8499a972-de27-4db2-99ec-640dc0688b4f" />

<img width="962" height="227" alt="Screenshot 2026-11-23 180230" src="https://github.com/user-attachments/assets/8e094ae4-ff58-4d63-bf81-49dbffc61e6c" />
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->
<!-- Add screenshots, HTTP requests/responses, payloads, or videos that demonstrate the vulnerability. -->

## Impact
An attacker could potentially exploit this vulnerability to execute malicious JavaScript in the browsers of users viewing the affected product reviews.

Potential consequences include:

Stealing sensitive information accessible to JavaScript.

Performing unauthorized actions through an authenticated user's session.

Displaying fake login forms for phishing attacks.

Modifying product review content or page elements.

Targeting multiple users who visit the affected product page.
<!-- Explain what an attacker could achieve, who could be affected, and the realistic security consequences. -->

## Remediation
Implement server-side input validation for all product review fields.

Apply context-aware output encoding before displaying user-submitted content.

Sanitize user-generated HTML using a trusted HTML sanitization library if HTML formatting is required.

Prevent execution of user-controlled JavaScript and event handlers.

Avoid inserting untrusted content directly into the DOM using unsafe methods such as innerHTML.

Implement a restrictive Content Security Policy (CSP).

Configure session cookies with HttpOnly, Secure, and appropriate SameSite attributes.
<!-- Suggest specific steps to fix the vulnerability. Include secure coding practices or configuration changes where appropriate. -->
